# Пошаговая инструкция по созданию GUI-приложения «Random Task Generator»

Ниже представлена подробная инструкция для реализации приложения «Генератор случайных задач» на Python с использованием библиотеки `tkinter` для GUI, `random` для случайного выбора, `json` для сохранения истории и Git для контроля версий.

---

## 1. Подготовка окружения

1. Установите Python (если не установлен).
2. Создайте папку проекта, например, `random_task_generator`.
3. Откройте терминал в этой папке и инициализируйте Git-репозиторий:
   ```bash
   git init
   ```

---

## 2. Структура проекта

```
random_task_generator/
│
├── tasks.json        # Файл для хранения истории
├── main.py           # Основной код приложения
├── README.md         # Описание проекта
└── .gitignore        # Игнорируемые файлы (например, __pycache__)
```

---

## 3. Создание списка задач

В начале `main.py` определите словарь задач с типами:

```python
import tkinter as tk
import random
import json

TASKS = {
    "учёба": ["Прочитать статью", "Решить задачу", "Посмотреть лекцию"],
    "спорт": ["Сделать зарядку", "Пробежаться", "Отжаться 20 раз"],
    "работа": ["Написать отчёт", "Провести созвон", "Подготовить презентацию"]
}
```

---

## 4. Реализация GUI и логики

### Основной класс приложения

```python
class TaskGeneratorApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Random Task Generator")
        self.history = self.load_history()

        # Виджеты
        self.task_label = tk.Label(root, text="Ваша задача:", font=("Arial", 14))
        self.task_label.pack(pady=10)

        self.task_display = tk.Label(root, text="", font=("Arial", 16), wraplength=300)
        self.task_display.pack(pady=10)

        self.generate_btn = tk.Button(root, text="Сгенерировать задачу", command=self.generate_task)
        self.generate_btn.pack(pady=5)

        self.filter_var = tk.StringVar(value="все")
        filter_frame = tk.Frame(root)
        filter_frame.pack(pady=5)
        for t in ["все"] + list(TASKS.keys()):
            tk.Radiobutton(filter_frame, text=t, variable=self.filter_var, value=t).pack(side=tk.LEFT)

        self.history_listbox = tk.Listbox(root, width=50, height=10)
        self.history_listbox.pack(pady=10)

        self.update_history_display()

    def generate_task(self):
        task_type = self.filter_var.get()
        if task_type == "все":
            all_tasks = [t for sublist in TASKS.values() for t in sublist]
            task = random.# Пошаговая инструкция по созданию GUI-приложения «Random Task Generator»

Ниже представлена подробная инструкция для реализации приложения «Генератор случайных задач» на Python с использованием библиотеки `tkinter` для GUI, `random` для случайного выбора, `json` для сохранения истории и Git для контроля версий.

---

## 1. Подготовка окружения

1. Установите Python (если не установлен).
2. Создайте папку проекта, например, `random_task_generator`.
3. Откройте терминал в этой папке и инициализируйте Git-репозиторий:
   ```bash
   git init
   ```

---

## 2. Структура проекта

```
random_task_generator/
│
├── tasks.json        # Файл для хранения истории
├── main.py           # Основной код приложения
├── README.md         # Описание проекта
└── .gitignore        # Игнорируемые файлы (например, __pycache__)
```

---

## 3. Создание списка задач

В начале `main.py` определите словарь задач с типами:

```python
import tkinter as tk
import random
import json

TASKS = {
    "учёба": ["Прочитать статью", "Решить задачу", "Посмотреть лекцию"],
    "спорт": ["Сделать зарядку", "Пробежаться", "Отжаться 20 раз"],
    "работа": ["Написать отчёт", "Провести созвон", "Подготовить презентацию"]
}
```

---

## 4. Реализация GUI и логики

### Основной класс приложения

```python
class TaskGeneratorApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Random Task Generator")
        self.history = self.load_history()

        # Виджеты
        self.task_label = tk.Label(root, text="Ваша задача:", font=("Arial", 14))
        self.task_label.pack(pady=10)

        self.task_display = tk.Label(root, text="", font=("Arial", 16), wraplength=300)
        self.task_display.pack(pady=10)

        self.generate_btn = tk.Button(root, text="Сгенерировать задачу", command=self.generate_task)
        self.generate_btn.pack(pady=5)

        self.filter_var = tk.StringVar(value="все")
        filter_frame = tk.Frame(root)
        filter_frame.pack(pady=5)
        for t in ["все"] + list(TASKS.keys()):
            tk.Radiobutton(filter_frame, text=t, variable=self.filter_var, value=t).pack(side=tk.LEFT)

        self.history_listbox = tk.Listbox(root, width=50, height=10)
        self.history_listbox.pack(pady=10)

        self.update_history_display()

    def generate_task(self):
        task_type = self.filter_var.get()
        if task_type == "все":
            all_tasks = [t for sublist in TASKS.values() for t in sublist]
            task = random.choice(all_tasks)
        else:
            task = random.choice(TASKS[task_type])
        
        self.task_display.config(text=task)
        self.history.append(task)
        self.save_history()
        self.update_history_display()

    def update_history_display(self):
        self.history_listbox.delete(0, tk.END)
        for task in self.history:
            self.history_listbox.insert(tk.END, task)

    def save_history(self):
        with open("tasks.json", "w", encoding="utf-8") as f:
            json.dump(self.history, f, ensure_ascii=False, indent=2)

    def load_history(self):
        try:
            with open("tasks.json", "r", encoding="utf-8") as f:
                return json.load(f)
        except FileNotFoundError:
            return []
```

### Запуск приложения

```python
if __name__ == "__main__":
    root = tk.Tk()
    app = TaskGeneratorApp(root)
    root.mainloop()
```

---

## 5. Проверка корректности ввода

Если вы добавите возможность вводить свои задачи (например, через Entry и кнопку «Добавить»), реализуйте проверку:
```python
def add_custom_task(self):
    task = self.entry.get().strip()
    if not task:
        messagebox.showwarning("Ошибка", "Задача не может быть пустой!")
        return
    # Добавление в список и историю...
```

---

## 6. Использование Git

1. Добавьте файлы в репозиторий:
   ```bash
   git add .
   git commit -m "Initial commit: Random Task Generator"
   ```
2. Создайте репозиторий на GitHub/GitLab и залейте проект:
   ```bash
   git remote add origin <ваш_репозиторий>
   git push -u origin master
   ```

---

## 7. Пример README.md

```
# Random Task Generator

**Автор:** Иванов Иван

**Описание:**
Простое GUI-приложение для генерации случайных задач по категориям (учёба, спорт, работа). История сохраняется в JSON, есть фильтрация по типу задач.

**Использование:**
1. Запустите main.py.
2. Нажмите «Сгенерировать задачу».
3. Используйте радиокнопки для фильтрации.
4. История сохраняется автоматически.
```

---

## 8. Возможные тесты

- Генерация задачи при разных фильтрах.
- Проверка сохранения и загрузки истории.
- Попытка добавить пустую задачу (если реализовано).
- Проверка корректности отображения истории.

---

🚀 **Проект готов!** Теперь у вас есть рабочее приложение с историей, фильтрацией, сохранением данных и контролем версий.
