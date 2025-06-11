import java.io.*;
import java.time.LocalDate;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

// Task Class
class Task implements Serializable {
    private String title;
    private String category;
    private LocalDate dueDate;
    private boolean isComplete;

    public Task(String title, String category, LocalDate dueDate) {
        this.title = title;
        this.category = category;
        this.dueDate = dueDate;
        this.isComplete = false;
    }

    public String getTitle() {
        return title;
    }

    public String getCategory() {
        return category;
    }

    public LocalDate getDueDate() {
        return dueDate;
    }

    public boolean isComplete() {
        return isComplete;
    }

    public void markComplete() {
        this.isComplete = true;
    }

    @Override
    public String toString() {
        return "Task: " + title + " | Category: " + category + " | Due: " + dueDate + " | Completed: " + (isComplete ? "Yes" : "No");
    }
}

// TaskManager Class
class TaskManager {
    private List<Task> tasks;
    private static final String FILE_NAME = "tasks.ser";

    public TaskManager() {
        tasks = loadTasks();
    }

    public void addTask(Task task) {
        tasks.add(task);
        saveTasks();
    }

    public void removeTask(String title) {
        tasks.removeIf(task -> task.getTitle().equalsIgnoreCase(title));
        saveTasks();
    }

    public void markTaskComplete(String title) {
        for (Task task : tasks) {
            if (task.getTitle().equalsIgnoreCase(title)) {
                task.markComplete();
                break;
            }
        }
        saveTasks();
    }

    public List<Task> getTasks() {
        return tasks;
    }

    private void saveTasks() {
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(FILE_NAME))) {
            oos.writeObject(tasks);
        } catch (IOException e) {
            System.out.println("Error saving tasks: " + e.getMessage());
        }
    }

    @SuppressWarnings("unchecked")
    private List<Task> loadTasks() {
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream(FILE_NAME))) {
            return (List<Task>) ois.readObject();
        } catch (IOException | ClassNotFoundException e) {
            return new ArrayList<>();
        }
    }
}

// Main Class
public class ToDoListApp {
    public static void main(String[] args) {
        TaskManager manager = new TaskManager();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nTo-Do List Application");
            System.out.println("1. Add Task");
            System.out.println("2. Remove Task");
            System.out.println("3. Mark Task as Complete");
            System.out.println("4. View Tasks");
            System.out.println("5. Exit");

            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    System.out.print("Enter task title: ");
                    String title = scanner.nextLine();
                    System.out.print("Enter category: ");
                    String category = scanner.nextLine();
                    System.out.print("Enter due date (YYYY-MM-DD): ");
                    LocalDate dueDate = LocalDate.parse(scanner.nextLine());
                    manager.addTask(new Task(title, category, dueDate));
                    System.out.println("Task added successfully!");
                    break;
                case 2:
                    System.out.print("Enter task title to remove: ");
                    String removeTitle = scanner.nextLine();
                    manager.removeTask(removeTitle);
                    System.out.println("Task removed successfully!");
                    break;
                case 3:
                    System.out.print("Enter task title to mark as complete: ");
                    String completeTitle = scanner.nextLine();
                    manager.markTaskComplete(completeTitle);
                    System.out.println("Task marked as complete!");
                    break;
                case 4:
                    System.out.println("\nCurrent Tasks:");
                    for (Task task : manager.getTasks()) {
                        System.out.println(task);
                    }
                    break;
                case 5:
                    System.out.println("Exiting application. Goodbye!");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }
}
