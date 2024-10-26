# codsoftprojects1#TOdolist
import tkinter as tk
from tkinter import ttk, messagebox

# Function to add a new task
def add_task():
    task = task_entry.get()
    if task != "":
        tasks_listbox.insert(tk.END, task)
        task_entry.delete(0, tk.END)
    else:
        messagebox.showwarning("Warning", "You must enter a task.")

# Function to delete a selected task
def delete_task():
    try:
        selected_task = tasks_listbox.curselection()[0]
        tasks_listbox.delete(selected_task)
    except:
        messagebox.showwarning("Warning", "You must select a task to delete.")

# Function to update a selected task
def update_task():
    try:
        selected_task = tasks_listbox.curselection()[0]
        updated_task = task_entry.get()
        if updated_task != "":
            tasks_listbox.delete(selected_task)
            tasks_listbox.insert(selected_task, updated_task)
            task_entry.delete(0, tk.END)
        else:
            messagebox.showwarning("Warning", "You must enter a task.")
    except:
        messagebox.showwarning("Warning", "You must select a task to update.")

# Function to clear the task entry
def clear_entry():
    task_entry.delete(0, tk.END)

# Main window setup
window = tk.Tk()
window.title("To-Do List Application")
window.geometry("400x450")
window.config(bg="#e0f7fa")

# Title Label
title_label = ttk.Label(window, text="To-Do List", font=("Arial", 18, "bold"))
title_label.pack(pady=10)

# Entry and Buttons Frame
frame = ttk.Frame(window)
frame.pack(pady=10)

task_entry = ttk.Entry(frame, width=30, font=("Arial", 14))
task_entry.grid(row=0, column=0, padx=5, pady=5)

add_button = ttk.Button(frame, text="Add Task", command=add_task)
add_button.grid(row=0, column=1, padx=5, pady=5)

update_button = ttk.Button(frame, text="Update Task", command=update_task)
update_button.grid(row=1, column=0, padx=5, pady=5)

clear_button = ttk.Button(frame, text="Clear Entry", command=clear_entry)
clear_button.grid(row=1, column=1, padx=5, pady=5)

delete_button = ttk.Button(frame, text="Delete Task", command=delete_task)
delete_button.grid(row=2, column=0, padx=5, pady=5, columnspan=2)

# Tasks Listbox
tasks_listbox = tk.Listbox(window, width=40, height=10, font=("Arial", 14), selectbackground="#64b5f6")
tasks_listbox.pack(pady=20)

# Scrollbar for the Listbox
scrollbar = ttk.Scrollbar(window, orient="vertical", command=tasks_listbox.yview)
scrollbar.pack(side="right", fill="y")
tasks_listbox.config(yscrollcommand=scrollbar.set)

# Main Loop
window.mainloop()
