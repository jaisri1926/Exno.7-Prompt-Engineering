# Exno.7-Prompt-Engineering

## Register no.212222060086
## Aim:
   To Develop a prompt-based application tailored to their personal needs, fostering creativity and practical problem-solving skills while leveraging the capabilities of large language models.

## Algorithm:
    Develop a prompt-based application using ChatGPT - To demonstrate how to create a prompt-based application to organize daily tasks, showing the progression from simple to more advanced prompt designs and their corresponding outputs.
# **Prompt-Based Task Organizer: From Simple to Advanced Designs**

This application demonstrates how to build a progressively sophisticated task management system using ChatGPT prompts, evolving from basic to-do lists to AI-powered productivity assistants.

## **Algorithm Implementation**

```python
import openai
from typing import List, Dict
import json
from datetime import datetime

class TaskOrganizer:
    def __init__(self, api_key: str):
        self.client = openai.OpenAI(api_key=api_key)
        self.tasks = []
        self.task_history = []
    
    def run_prompt(self, prompt: str, model: str = "gpt-3.5-turbo") -> str:
        """Execute a ChatGPT prompt and return the response"""
        response = self.client.chat.completions.create(
            model=model,
            messages=[{"role": "user", "content": prompt}]
        )
        return response.choices[0].message.content

    # --- Prompt Evolution Stages ---
    
    def stage1_basic_list(self, tasks: List[str]) -> str:
        """Stage 1: Simple task listing"""
        prompt = f"Organize these tasks in a numbered list:\n{tasks}"
        return self.run_prompt(prompt)
    
    def stage2_prioritized(self, tasks: List[str]) -> str:
        """Stage 2: Priority-based organization"""
        prompt = f"""Prioritize these tasks by urgency and importance (1-4 scale):
        Tasks: {tasks}
        Format as: [priority] task"""
        return self.run_prompt(prompt)
    
    def stage3_time_estimated(self, tasks: List[str]) -> Dict:
        """Stage 3: Time estimation and categorization"""
        prompt = f"""Analyze these tasks and return JSON with:
        1. Time estimate (minutes)
        2. Category (work/personal/errands)
        3. Energy level required (low/medium/high)
        Tasks: {tasks}"""
        return json.loads(self.run_prompt(prompt))
    
    def stage4_smart_scheduler(self, tasks: List[str]) -> Dict:
        """Stage 4: Context-aware scheduling"""
        prompt = f"""Given my current time is {datetime.now().strftime('%H:%M')}, 
        schedule these tasks optimally considering:
        - Typical work hours (9AM-5PM)
        - 60min lunch break at 12-1PM
        - Evening personal time after 7PM
        Tasks: {tasks}
        Return as {{"schedule": [{"task": "...", "time": "HH:MM"}]}}"""
        return json.loads(self.run_prompt(prompt))
    
    def stage5_ai_assistant(self, query: str) -> str:
        """Stage 5: Natural language interaction"""
        prompt = f"""You're a productivity assistant. Help me with:
        {query}
        My current tasks: {self.tasks[-5:] if self.tasks else 'None'}
        Provide actionable advice in bullet points."""
        return self.run_prompt(prompt, model="gpt-4")

    # --- Application Interface ---
    
    def process_tasks(self, tasks: List[str], stage: int = 1):
        """Execute the appropriate prompt stage"""
        self.tasks.extend(tasks)
        
        if stage == 1:
            return self.stage1_basic_list(tasks)
        elif stage == 2:
            return self.stage2_prioritized(tasks)
        elif stage == 3:
            return self.stage3_time_estimated(tasks)
        elif stage == 4:
            return self.stage4_smart_scheduler(tasks)
        elif stage == 5:
            return self.stage5_ai_assistant(tasks[0])  # Single query for stage 5

# Example Usage
if __name__ == "__main__":
    import os
    from dotenv import load_dotenv
    
    load_dotenv()
    organizer = TaskOrganizer(api_key=os.getenv("OPENAI_API_KEY"))
    
    sample_tasks = [
        "Finish quarterly report",
        "Buy groceries",
        "Call mom",
        "Prepare presentation slides",
        "Exercise for 30 minutes"
    ]
    
    print("=== Stage 1: Basic List ===")
    print(organizer.process_tasks(sample_tasks[:3], stage=1))
    
    print("\n=== Stage 2: Prioritization ===")
    print(organizer.process_tasks(sample_tasks, stage=2))
    
    print("\n=== Stage 3: Time Estimation ===")
    print(organizer.process_tasks(sample_tasks[1:4], stage=3))
    
    print("\n=== Stage 4: Smart Scheduling ===")
    print(organizer.process_tasks(sample_tasks, stage=4))
    
    print("\n=== Stage 5: AI Assistant ===")
    print(organizer.process_tasks(["I'm feeling overwhelmed with work"], stage=5))
```

## **Prompt Evolution Roadmap**

### **Stage 1: Basic Task Listing**
- **Prompt Design**: Simple instruction to organize items
- **Output Example**:
  ```
  1. Finish quarterly report
  2. Buy groceries
  3. Call mom
  ```

### **Stage 2: Priority-Based Organization**
- **Prompt Design**: Added prioritization criteria
- **Output Example**:
  ```
  [1] Finish quarterly report (urgent & important)
  [2] Prepare presentation slides (important)
  [3] Buy groceries (urgent)
  [4] Call mom (important)
  [4] Exercise (not urgent)
  ```

### **Stage 3: Time & Energy Analysis**
- **Prompt Design**: Structured JSON output request
- **Output Example**:
  ```json
  [
    {"task": "Buy groceries", "time": 45, "category": "errands", "energy": "medium"},
    {"task": "Call mom", "time": 30, "category": "personal", "energy": "low"}
  ]
  ```

### **Stage 4: Context-Aware Scheduling**
- **Prompt Design**: Incorporates temporal context
- **Output Example**:
  ```json
  {
    "schedule": [
      {"task": "Finish quarterly report", "time": "09:00"},
      {"task": "Prepare presentation slides", "time": "11:00"},
      {"task": "Lunch break", "time": "12:00"},
      {"task": "Buy groceries", "time": "17:30"},
      {"task": "Exercise", "time": "18:30"},
      {"task": "Call mom", "time": "20:00"}
    ]
  }
  ```

### **Stage 5: Natural Language Assistant**
- **Prompt Design**: Conversational interaction
- **Output Example**:
  ```
  • Prioritize your quarterly report first (2h focused work)
  • Batch errands like groceries together 
  • Schedule call with mom during low-energy time
  • Use Pomodoro technique for presentation slides
  ```

## **Key Features**

1. **Progressive Complexity**:
   - Demonstrates prompt engineering evolution
   - Each stage adds new dimensions (priority, time, context)

2. **Practical Implementation**:
   - Ready-to-run Python class
   - Handles both structured and conversational outputs

3. **Customization Hooks**:
   - Easy to modify prompts for specific needs
   - Extendable to integrate with calendar APIs

4. **Learning Scaffolding**:
   - Clear progression from basic to advanced concepts
   - Demonstrates real-world AI application development



# Result:
The Prompt is executed successfully


