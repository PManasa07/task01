# task01
import tkinter as tk
from tkinter import simpledialog, messagebox

class TodoListApp:
    def __init__(self, master):
        # Initialize the main application window
        self.master = master
        self.master.title("To-Do List")

        # Create an empty list to store tasks
        self.todo_list = []

        # Create a Listbox widget to display tasks
        self.listbox = tk.Listbox(self.master, selectmode=tk.SINGLE)
        self.listbox.pack(pady=10)

        # Create buttons for adding, editing, and displaying tasks
        add_button = tk.Button(self.master, text="Add Task", command=self.add_task)
        add_button.pack(pady=5)

        edit_button = tk.Button(self.master, text="Edit Task", command=self.edit_task)
        edit_button.pack(pady=5)

        display_button = tk.Button(self.master, text="Display List", command=self.display_list)
        display_button.pack(pady=5)

    def display_list(self):
        # Display the tasks in the Listbox
        self.listbox.delete(0, tk.END)
        for task in self.todo_list:
            self.listbox.insert(tk.END, task)

    def add_task(self):
        # Ask the user to enter a new task
        task = simpledialog.askstring("Add Task", "Enter the task:")
        if task:
            # Add the task to the list and show a success message
            self.todo_list.append(task)
            messagebox.showinfo("Task Added", "Task added successfully!")
            self.display_list()

    def edit_task(self):
        # Get the index of the selected task in the Listbox
        selected_index = self.listbox.curselection()
        if not selected_index:
            # If no task is selected, show a warning message
            messagebox.showwarning("No Task Selected", "Please select a task to edit.")
            return

        task_index = selected_index[0]
        current_task = self.todo_list[task_index]

        # Ask the user to edit the selected task
        new_task = simpledialog.askstring("Edit Task", "Edit the task:", initialvalue=current_task)
        if new_task:
            # Update the task in the list and show a success message
            self.todo_list[task_index] = new_task
            messagebox.showinfo("Task Edited", "Task edited successfully!")
            self.display_list()

def main():
    # Create the main Tkinter window and start the application
    root = tk.Tk()
    app = TodoListApp(root)
    root.mainloop()

if __name__ == "__main__":
    main()
