# ToDo--List--project
imp
import os
from datetime import datetime

FILE_NAME = "tasks.json"

# JSON file లో నుంచి tasks load చేయడం
def load_tasks():
    if os.path.exists(FILE_NAME):
        with open(FILE_NAME, "r") as file:
            return json.load(file)
    return []  # file లేకపోతే empty list

# JSON file లో tasks save చేయడం
def save_tasks(tasks):
    with open(FILE_NAME, "w") as file:
        json.dump(tasks, file, indent=4)

# నయా టాస్క్ add చేయడం
def add_task(tasks):
    task_name = input("\nEnter task name: ")
    task = {
        "id": len(tasks) + 1,
        "name": task_name,
        "completed": False,
        "created_at": datetime.now().strftime("%Y-%m-%d %H:%M")
    }
    tasks.append(task)
    save_tasks(tasks)
    print("✅ Task added successfully!")

# అన్ని tasks చూపించడం
def view_tasks(tasks):
    if not tasks:
        print("\nNo tasks yet! Add some 😊")
        return
    
    print("\n" + "="*60)
    print("ID | Status     | Task Name                  | Created")
    print("="*60)
    for t in tasks:
        status = "✅ Done" if t["completed"] else "❌ Pending"
        print(f"{t['id']:<3}| {status:<10} | {t['name']:<25} | {t['created_at']}")
    print("="*60)

# Task complete mark చేయడం
def complete_task(tasks):
    view_tasks(tasks)
    try:
        task_id = int(input("\nEnter task ID to mark as complete: "))
        for t in tasks:
            if t["id"] == task_id:
                t["completed"] = True
                save_tasks(tasks)
                print("🎉 Task marked as completed!")
                return
        print("❌ Task ID not found!")
    except:
        print("❌ Invalid input!")

# Task delete చేయడం
def delete_task(tasks):
    view_tasks(tasks)
    try:
        task_id = int(input("\nEnter task ID to delete: "))
        for i, t in enumerate(tasks):
            if t["id"] == task_id:
                tasks.pop(i)
                save_tasks(tasks)
                print("🗑️ Task deleted!")
                return
        print("❌ Task not found!")
    except:
        print("❌ Invalid input!")

# Main menu
def main():
    tasks = load_tasks()
    
    while True:
        print("\n🚀 MY TO-DO LIST APP 🚀")
        print("1. Add Task")
        print("2. View Tasks")
        print("3. Complete Task")
        print("4. Delete Task")
        print("5. Exit")
        
        choice = input("\nChoose option (1-5): ")
        
        if choice == "1":
            add_task(tasks)
        elif choice == "2":
            view_tasks(tasks)
        elif choice == "3":
            complete_task(tasks)
        elif choice == "4":
            delete_task(tasks)
        elif choice == "5":
            print("👋 Bye Bye! Have a great day!")
            break
        else:
            print("❌ Wrong choice! Try again")

# Program start
if __name__ == "__main__":
    main()
















    
