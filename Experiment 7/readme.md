

# Exno.7 - Develop a Prompt-Based Application Using ChatGPT

## Date: [22-10-2025]

## Register No.: [212223060182]

## Aim: 
To develop a prompt-based application using ChatGPT to demonstrate how to create a prompt-based application to organize daily tasks, showing the progression from simple to more advanced prompt designs and their corresponding outputs.

## AI Tools Required:
- ChatGPT (OpenAI's Large Language Model)
- Python 3.x
- Tkinter (GUI Framework - built-in with Python)
- JSON (for data persistence)

## Explanation:

### Problem Statement:
In today's fast-paced world, managing daily tasks effectively is crucial for productivity. This experiment demonstrates how to leverage Large Language Models (LLMs) like ChatGPT to generate a complete task management application through progressive prompt engineering.

### Prompt Engineering Approach:
The development follows a structured prompt evolution from basic to advanced:

**Initial Simple Prompt:**
```
"Create a to-do list application"
```

**Intermediate Prompt:**
```
"Create a to-do list application with GUI using Python"
```

**Advanced Prompt (Final):**
```
"To develop a prompt-based application using ChatGPT:
Aim: To demonstrate how to create a prompt-based application to organize 
daily tasks, showing the progression from simple prompt to more advanced 
prompt designs and their corresponding outputs.

gimme code to make a to do list using python with GUI"
```

### Application Features:
1. **Task Management System**
   - Add, delete, and edit tasks
   - Mark tasks as complete/incomplete
   - Priority-based organization (High, Medium, Low)

2. **Visual Interface**
   - Color-coded priority indicators
   - Clean and intuitive GUI design
   - Real-time task statistics

3. **Filtering Capabilities**
   - Filter by priority levels
   - Filter by completion status
   - Dynamic task sorting

4. **Data Persistence**
   - Automatic saving to JSON file
   - Task data retention across sessions
   - Timestamp tracking for task creation

## Procedure:

### Step 1: Define Core Requirements
Identify the essential features needed for a daily task organizer:
- User-friendly graphical interface
- Task input with priority levels
- Task completion tracking
- Data persistence
- Filtering and sorting capabilities
- Visual feedback and statistics

### Step 2: Construct Prompts for LLM
Design progressive prompts to guide the LLM:

**Prompt Evolution:**

**Level 1 - Basic Prompt:**
```
"Create a to-do list"
```
*Output: Simple text-based list concept*

**Level 2 - Specific Prompt:**
```
"Create a to-do list application with Python"
```
*Output: Basic console application*

**Level 3 - Detailed Prompt:**
```
"Create a to-do list using Python with GUI"
```
*Output: Simple Tkinter application*

**Level 4 - Advanced Prompt (Used):**
```
"To develop a prompt-based application using ChatGPT:
Aim: To demonstrate how to create a prompt-based application to 
organize daily tasks, showing the progression from simple prompt 
to more advanced prompt designs and their corresponding outputs.
gimme code to make a to do list using python with GUI"
```
*Output: Comprehensive application with all features*

### Step 3: Implement the Generated Code
1. Save the generated Python code to a file (e.g., `todo_app.py`)
2. Ensure Python 3.x is installed
3. Verify Tkinter availability (comes pre-installed with Python)
4. No additional package installation required

### Step 4: Execute and Test the Application
```bash
python todo_app.py
```

### Step 5: Validate Features
Test each functionality:
- ✓ Adding tasks with different priorities
- ✓ Marking tasks as complete
- ✓ Deleting tasks
- ✓ Filtering by priority and status
- ✓ Data persistence (close and reopen app)
- ✓ Statistics accuracy

### Step 6: Document Observations
- Note the prompt engineering progression
- Record feature implementations
- Document user interface design
- Evaluate code quality and organization

## appication code
```
import tkinter as tk
from tkinter import ttk, messagebox
from datetime import datetime
import json
import os

class TodoApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Daily Task Manager")
        self.root.geometry("800x600")
        self.root.resizable(True, True)
        
        # Data storage
        self.tasks = []
        self.data_file = "tasks.json"
        self.load_tasks()
        
        # Color scheme
        self.colors = {
            'high': '#ff6b6b',
            'medium': '#ffd93d',
            'low': '#6bcf7f',
            'bg': '#f8f9fa',
            'frame': '#ffffff'
        }
        
        self.root.configure(bg=self.colors['bg'])
        self.setup_ui()
        self.refresh_task_list()
    
    def setup_ui(self):
        # Title
        title_frame = tk.Frame(self.root, bg=self.colors['bg'])
        title_frame.pack(pady=10)
        
        title_label = tk.Label(
            title_frame,
            text="📝 Daily Task Manager",
            font=("Arial", 20, "bold"),
            bg=self.colors['bg'],
            fg="#2c3e50"
        )
        title_label.pack()
        
        # Input Frame
        input_frame = tk.Frame(self.root, bg=self.colors['frame'], relief=tk.RAISED, bd=2)
        input_frame.pack(pady=10, padx=20, fill=tk.X)
        
        # Task Entry
        tk.Label(input_frame, text="Task:", font=("Arial", 10), bg=self.colors['frame']).grid(
            row=0, column=0, padx=5, pady=10, sticky=tk.W
        )
        self.task_entry = tk.Entry(input_frame, width=40, font=("Arial", 10))
        self.task_entry.grid(row=0, column=1, padx=5, pady=10)
        self.task_entry.bind('<Return>', lambda e: self.add_task())
        
        # Priority Dropdown
        tk.Label(input_frame, text="Priority:", font=("Arial", 10), bg=self.colors['frame']).grid(
            row=0, column=2, padx=5, pady=10
        )
        self.priority_var = tk.StringVar(value="Medium")
        priority_dropdown = ttk.Combobox(
            input_frame,
            textvariable=self.priority_var,
            values=["High", "Medium", "Low"],
            state="readonly",
            width=10
        )
        priority_dropdown.grid(row=0, column=3, padx=5, pady=10)
        
        # Add Button
        add_btn = tk.Button(
            input_frame,
            text="Add Task",
            command=self.add_task,
            bg="#4CAF50",
            fg="white",
            font=("Arial", 10, "bold"),
            cursor="hand2",
            padx=15
        )
        add_btn.grid(row=0, column=4, padx=10, pady=10)
        
        # Filter Frame
        filter_frame = tk.Frame(self.root, bg=self.colors['bg'])
        filter_frame.pack(pady=5)
        
        tk.Label(filter_frame, text="Filter:", font=("Arial", 9), bg=self.colors['bg']).pack(side=tk.LEFT, padx=5)
        
        self.filter_var = tk.StringVar(value="All")
        for filter_option in ["All", "High", "Medium", "Low", "Completed"]:
            rb = tk.Radiobutton(
                filter_frame,
                text=filter_option,
                variable=self.filter_var,
                value=filter_option,
                command=self.refresh_task_list,
                bg=self.colors['bg'],
                font=("Arial", 9)
            )
            rb.pack(side=tk.LEFT, padx=5)
        
        # Task List Frame
        list_frame = tk.Frame(self.root, bg=self.colors['bg'])
        list_frame.pack(pady=10, padx=20, fill=tk.BOTH, expand=True)
        
        # Scrollbar
        scrollbar = tk.Scrollbar(list_frame)
        scrollbar.pack(side=tk.RIGHT, fill=tk.Y)
        
        # Canvas for tasks
        self.canvas = tk.Canvas(list_frame, bg=self.colors['bg'], yscrollcommand=scrollbar.set)
        self.canvas.pack(side=tk.LEFT, fill=tk.BOTH, expand=True)
        scrollbar.config(command=self.canvas.yview)
        
        # Frame inside canvas
        self.tasks_container = tk.Frame(self.canvas, bg=self.colors['bg'])
        self.canvas.create_window((0, 0), window=self.tasks_container, anchor=tk.NW)
        
        self.tasks_container.bind('<Configure>', lambda e: self.canvas.configure(scrollregion=self.canvas.bbox("all")))
        
        # Stats Frame
        self.stats_frame = tk.Frame(self.root, bg=self.colors['frame'], relief=tk.RAISED, bd=2)
        self.stats_frame.pack(pady=10, padx=20, fill=tk.X)
        
        self.stats_label = tk.Label(
            self.stats_frame,
            text="",
            font=("Arial", 9),
            bg=self.colors['frame'],
            fg="#34495e"
        )
        self.stats_label.pack(pady=5)
        
        self.update_stats()
    
    def add_task(self):
        task_text = self.task_entry.get().strip()
        if not task_text:
            messagebox.showwarning("Empty Task", "Please enter a task!")
            return
        
        task = {
            'id': len(self.tasks),
            'text': task_text,
            'priority': self.priority_var.get(),
            'completed': False,
            'created': datetime.now().strftime("%Y-%m-%d %H:%M")
        }
        
        self.tasks.append(task)
        self.task_entry.delete(0, tk.END)
        self.save_tasks()
        self.refresh_task_list()
        self.update_stats()
    
    def toggle_complete(self, task_id):
        for task in self.tasks:
            if task['id'] == task_id:
                task['completed'] = not task['completed']
                break
        self.save_tasks()
        self.refresh_task_list()
        self.update_stats()
    
    def delete_task(self, task_id):
        self.tasks = [t for t in self.tasks if t['id'] != task_id]
        self.save_tasks()
        self.refresh_task_list()
        self.update_stats()
    
    def refresh_task_list(self):
        # Clear existing widgets
        for widget in self.tasks_container.winfo_children():
            widget.destroy()
        
        # Filter tasks
        filter_value = self.filter_var.get()
        filtered_tasks = self.tasks
        
        if filter_value == "Completed":
            filtered_tasks = [t for t in self.tasks if t['completed']]
        elif filter_value in ["High", "Medium", "Low"]:
            filtered_tasks = [t for t in self.tasks if t['priority'] == filter_value and not t['completed']]
        
        # Sort: incomplete first, then by priority
        priority_order = {'High': 0, 'Medium': 1, 'Low': 2}
        filtered_tasks.sort(key=lambda x: (x['completed'], priority_order.get(x['priority'], 3)))
        
        # Display tasks
        for i, task in enumerate(filtered_tasks):
            self.create_task_widget(task, i)
    
    def create_task_widget(self, task, index):
        task_frame = tk.Frame(
            self.tasks_container,
            bg=self.colors['frame'],
            relief=tk.RAISED,
            bd=1
        )
        task_frame.pack(fill=tk.X, pady=5, padx=5)
        
        # Priority indicator
        priority_color = self.colors[task['priority'].lower()]
        priority_label = tk.Label(
            task_frame,
            text="●",
            font=("Arial", 16),
            fg=priority_color,
            bg=self.colors['frame']
        )
        priority_label.pack(side=tk.LEFT, padx=5)
        
        # Checkbox
        check_var = tk.BooleanVar(value=task['completed'])
        checkbox = tk.Checkbutton(
            task_frame,
            variable=check_var,
            command=lambda: self.toggle_complete(task['id']),
            bg=self.colors['frame']
        )
        checkbox.pack(side=tk.LEFT, padx=5)
        
        # Task text
        text_style = ("Arial", 11, "overstrike") if task['completed'] else ("Arial", 11)
        text_color = "#95a5a6" if task['completed'] else "#2c3e50"
        
        task_label = tk.Label(
            task_frame,
            text=task['text'],
            font=text_style,
            fg=text_color,
            bg=self.colors['frame'],
            anchor=tk.W,
            wraplength=400
        )
        task_label.pack(side=tk.LEFT, fill=tk.X, expand=True, padx=5)
        
        # Priority badge
        priority_badge = tk.Label(
            task_frame,
            text=task['priority'],
            font=("Arial", 8),
            bg=priority_color,
            fg="white",
            padx=5,
            pady=2
        )
        priority_badge.pack(side=tk.LEFT, padx=5)
        
        # Created time
        time_label = tk.Label(
            task_frame,
            text=task['created'],
            font=("Arial", 8),
            fg="#7f8c8d",
            bg=self.colors['frame']
        )
        time_label.pack(side=tk.LEFT, padx=5)
        
        # Delete button
        delete_btn = tk.Button(
            task_frame,
            text="🗑",
            command=lambda: self.delete_task(task['id']),
            bg="#e74c3c",
            fg="white",
            font=("Arial", 10),
            cursor="hand2",
            padx=5
        )
        delete_btn.pack(side=tk.RIGHT, padx=5)
    
    def update_stats(self):
        total = len(self.tasks)
        completed = sum(1 for t in self.tasks if t['completed'])
        pending = total - completed
        
        high = sum(1 for t in self.tasks if t['priority'] == 'High' and not t['completed'])
        medium = sum(1 for t in self.tasks if t['priority'] == 'Medium' and not t['completed'])
        low = sum(1 for t in self.tasks if t['priority'] == 'Low' and not t['completed'])
        
        stats_text = f"Total: {total} | Completed: {completed} | Pending: {pending} | High: {high} | Medium: {medium} | Low: {low}"
        self.stats_label.config(text=stats_text)
    
    def save_tasks(self):
        try:
            with open(self.data_file, 'w') as f:
                json.dump(self.tasks, f, indent=2)
        except Exception as e:
            messagebox.showerror("Error", f"Failed to save tasks: {e}")
    
    def load_tasks(self):
        if os.path.exists(self.data_file):
            try:
                with open(self.data_file, 'r') as f:
                    self.tasks = json.load(f)
            except Exception as e:
                messagebox.showerror("Error", f"Failed to load tasks: {e}")
                self.tasks = []

if __name__ == "__main__":
    root = tk.Tk()
    app = TodoApp(root)
    root.mainloop()
```

## Expected Output:

### Application Interface Components:

1. **Title Bar**
   - "📝 Daily Task Manager" heading
   - Clean, professional design

2. **Input Section**
   - Task text entry field
   - Priority dropdown (High, Medium, Low)
   - "Add Task" button
   - Keyboard shortcut support (Enter key)

3. **Filter Options**
   - Radio buttons: All, High, Medium, Low, Completed
   - Real-time filtering

4. **Task Display Area**
   - Scrollable task list
   - Color-coded priority indicators:
     * Red (●) for High priority
     * Yellow (●) for Medium priority
     * Green (●) for Low priority
   - Checkboxes for completion status
   - Task text with strike-through when completed
   - Priority badges
   - Creation timestamp
   - Delete buttons (🗑)

5. **Statistics Dashboard**
   - Total tasks count
   - Completed tasks count
   - Pending tasks count
   - Priority-wise breakdown

### Sample Usage Scenario:

**Input:**
```
Task: "Complete lab assignment"
Priority: High
```

**Visual Output:**
```
● [☐] Complete lab assignment  [High]  2025-10-22 10:30  [🗑]
```

**After Completion:**
```
● [☑] Complete lab assignment  [High]  2025-10-22 10:30  [🗑]
     (text appears with strikethrough)
```

### Data Persistence (tasks.json):
```json
[
  {
    "id": 0,
    "text": "Complete lab assignment",
    "priority": "High",
    "completed": false,
    "created": "2025-10-22 10:30"
  },
  {
    "id": 1,
    "text": "Study for exam",
    "priority": "Medium",
    "completed": false,
    "created": "2025-10-22 11:15"
  }
]
```

## Code Structure Analysis:

### Key Components:

1. **TodoApp Class**
   - Main application controller
   - Handles all task operations

2. **UI Setup Methods**
   - `setup_ui()`: Creates all interface elements
   - `create_task_widget()`: Generates individual task displays

3. **Task Operations**
   - `add_task()`: Adds new tasks
   - `toggle_complete()`: Marks tasks complete/incomplete
   - `delete_task()`: Removes tasks
   - `refresh_task_list()`: Updates display

4. **Data Management**
   - `save_tasks()`: Saves to JSON
   - `load_tasks()`: Loads from JSON
   - `update_stats()`: Calculates statistics

## Prompt Engineering Insights:

### Effective Prompting Strategies Used:

1. **Context Setting**
   - Provided clear aim and purpose
   - Specified it's for a prompt engineering assignment

2. **Specificity**
   - Mentioned "Python" for language
   - Specified "GUI" for interface type

3. **Implicit Requirements**
   - Professional application expected
   - Feature-rich implementation
   - Best practices adherence

4. **Natural Language**
   - Used casual phrasing ("gimme code")
   - Clear, direct request

## Observations:

### Advantages of LLM-Generated Code:
1. ✓ Rapid prototyping and development
2. ✓ Comprehensive feature implementation
3. ✓ Best practices and design patterns included
4. ✓ Well-commented and organized code
5. ✓ Production-ready functionality

### Learning Outcomes:
1. Understanding prompt engineering principles
2. Importance of prompt specificity
3. Progressive refinement technique
4. LLM capabilities in software development
5. Practical application development skills

## Result:

The lab exercise successfully demonstrated the development of a prompt-based To-Do List application using ChatGPT. The experiment achieved the following outcomes:

### Technical Achievements:
1. ✓ Successfully generated a fully functional GUI application through prompt engineering
2. ✓ Implemented comprehensive task management features (add, delete, complete, filter)
3. ✓ Created an intuitive user interface with visual priority indicators
4. ✓ Achieved data persistence using JSON file storage
5. ✓ Developed real-time statistics and filtering capabilities

### Prompt Engineering Learnings:
1. **Progressive Refinement**: Demonstrated how prompt complexity directly correlates with output sophistication
2. **Contextual Clarity**: Providing assignment context resulted in educational, well-documented code
3. **Specificity Matters**: Specifying "GUI" and "Python" yielded targeted, relevant solutions
4. **Natural Language Effectiveness**: Simple, conversational prompts can generate professional-grade applications

### Practical Problem-Solving:
- Students learned to leverage LLMs for real-world application development
- Understood the importance of clear requirements in prompt design
- Experienced the rapid prototyping capabilities of AI-assisted development
- Gained insights into software architecture through generated code analysis

### Creativity and Adaptability:
- The generated application included features beyond basic requirements (color coding, statistics, timestamps)
- Demonstrated LLM's ability to infer implicit requirements from context
- Showed how AI can enhance creativity by suggesting innovative feature implementations

### Personal Productivity Benefits:
- Created a practical tool for daily task management
- Application can be customized and extended for individual needs
- Serves as a foundation for future prompt-based projects

## Screenshots/Outputs:
<img width="1001" height="787" alt="image" src="https://github.com/user-attachments/assets/88abc954-d1f1-4a20-be25-149bccf6efdf" />


**Conclusion:** This experiment successfully illustrated how Large Language Models can be effectively utilized through strategic prompt engineering to develop sophisticated, user-centric applications. Students gained valuable experience in both prompt design and practical software development, demonstrating the versatility and power of AI-assisted programming in solving everyday productivity challenges.

---
