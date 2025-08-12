# todolist
List Using Java Swing

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class ToDoListApp extends JFrame {
    private DefaultListModel<String> taskListModel;
    private JList<String> taskList;
    private JTextField taskInput;

    public ToDoListApp() {
        setTitle("To-Do List");
        setSize(400, 500);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null); // Center window

        // Task input field
        taskInput = new JTextField();
        JButton addButton = new JButton("Add Task");
        JButton removeButton = new JButton("Remove Selected");

        // Task list
        taskListModel = new DefaultListModel<>();
        taskList = new JList<>(taskListModel);
        JScrollPane scrollPane = new JScrollPane(taskList);

        // Layout for input panel
        JPanel inputPanel = new JPanel(new BorderLayout());
        inputPanel.add(taskInput, BorderLayout.CENTER);
        inputPanel.add(addButton, BorderLayout.EAST);

        // Add components to frame
        setLayout(new BorderLayout());
        add(inputPanel, BorderLayout.NORTH);
        add(scrollPane, BorderLayout.CENTER);
        add(removeButton, BorderLayout.SOUTH);

        // Add task action
        addButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                String task = taskInput.getText().trim();
                if (!task.isEmpty()) {
                    taskListModel.addElement(task);
                    taskInput.setText("");
                } else {
                    JOptionPane.showMessageDialog(ToDoListApp.this, "Task cannot be empty!");
                }
            }
        });

        // Remove task action
        removeButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                int selectedIndex = taskList.getSelectedIndex();
                if (selectedIndex != -1) {
                    taskListModel.remove(selectedIndex);
                } else {
                    JOptionPane.showMessageDialog(ToDoListApp.this, "Please select a task to remove!");
                }
            }
        });

        // Press Enter to add task
        taskInput.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                addButton.doClick();
            }
        });
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            new ToDoListApp().setVisible(true);
        });
    }
}
