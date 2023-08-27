# to-do-list-using-tikinter
import tkinter as tk
from tkinter import messagebox

def add_task():
    task = task_entry.get()
    if task:
        task_list.insert(tk.END, task)
        task_entry.delete(0, tk.END)
    else:
        messagebox.showwarning("Warning", "Please enter a task.")

def remove_task():
    try:
        selected_task = task_list.curselection()[0]
        task_list.delete(selected_task)
    except IndexError:
        messagebox.showwarning("Warning", "Please select a task to remove.")

def mark_complete():
    try:
        selected_task = task_list.curselection()[0]
        task = task_list.get(selected_task)
        if not task.startswith("[X] "):
            task_list.delete(selected_task)
            task = "[X] " + task
            task_list.insert(tk.END, task)
    except IndexError:
        messagebox.showwarning("Warning", "Please select a task to mark as complete.")

def edit_task():
    try:
        selected_task_index = task_list.curselection()[0]
        selected_task = task_list.get(selected_task_index)
        
        task_entry.delete(0, tk.END)
        task_entry.insert(0, selected_task)
        
        task_list.delete(selected_task_index)
    except IndexError:
        messagebox.showwarning("Warning", "Please select a task to edit.")

root = tk.Tk()
root.title("To-Do List")

task_entry = tk.Entry(root, width=40)
task_entry.pack(pady=10)

add_button = tk.Button(root, text="Add Task", command=add_task)
add_button.pack()

task_list = tk.Listbox(root, selectmode=tk.SINGLE, width=40, height=10)
task_list.pack()

remove_button = tk.Button(root, text="Remove Task", command=remove_task)
remove_button.pack()

complete_button = tk.Button(root, text="Mark Complete", command=mark_complete)
complete_button.pack()

edit_button = tk.Button(root, text="Edit Task", command=edit_task)
edit_button.pack()

root.mainloop()
