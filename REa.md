# Звіт до роботи
## Тема: Знайомство з ООП згідно теми_
### Мета роботи: Навчитись використовувати основні принципи ООП, розглянути кострукції побудови класу та створення обєктів та навчитись працювати з ними згідно теми_

---
### Виконання роботи
* Результати виконання завдання *1...N*;
    1. Розробили/Створили перший клас
    1. Програма вивела значення <img width="1053" height="256" alt="image" src="https://github.com/user-attachments/assets/adce8fb4-895b-4bb3-8da9-b0e37da1f399" />
    1. Отримано наступні результати <img width="854" height="256" alt="image" src="https://github.com/user-attachments/assets/0250d9be-042e-4e99-a651-5dbd5047a0b7" />
    1. Навчились бути програмістом
 
1. Чому None створює об'єкт Anonymous?
Відповідь: Об'єкт не отримує імені Anonymous автоматично від Python. Це відбувається через умову, яку ви самі прописали в конструкторі __init__:
self.name = name if name is not None else "Anonymous"
Коли ви передаєте name=None, ця умова стає хибною (name is not None $\to$ False), і замість None змінній self.name присвоюється рядок "Anonymous".
2. Як змінити текст привітання?
Щоб змінити текст, просто відредагуйте рядок у методі say_hello():
def say_hello(self):
        # Змінений текст привітання
        return f"Greetings! I am {self.name}, pleased to meet you."
3. Функція для підрахунку букв імені
Використайте вбудовану функцію len():def count_name_letters(self):
        # Повертаємо довжину рядка self.name
        return len(self.name)
4. Різниця у підрахунку імен у списку names
Якщо ви підрахуєте кількість елементів у списку names, ви отримаєте 6. Якщо ви створите об'єкти, то імена будуть: "Alice", "Bob", "Anonymous", "Charlie", "Dave", "Anonymous".

Відповідь: Різна кількість імен тому, що None — це не ім'я, а відсутність значення. Ваш код в конструкторі __init__ замінює два значення None на рядок "Anonymous". Отже, ви маєте 4 унікальні введені імена та 2 замінені імені "Anonymous".

len(names) = 6 (всі елементи)

Кількість різних імен об'єктів (після заміни) = 5 (Alice, Bob, Charlie, Dave, Anonymous)
5. Модифікація конструктора (__init__) для великої літери
Використовуйте метод capitalize() для рядків:def __init__(self, name=None):
        # 1. Замінюємо None на "Anonymous"
        temp_name = name if name is not None else "Anonymous"
        # 2. Перетворюємо першу літеру на велику
        self.name = temp_name.capitalize()
  6. Модифікація методу create_email
Додайте аргумент за замовчуванням до методу:def create_email(self, domain="company.com"):
        # Використовуємо переданий або стандартний домен
        return f"{self.name.lower()}@{domain}"
7. Перевірка імені на цифри/символи
Додайте перевірку до конструктора, використовуючи метод isalpha() та виклик ValueError:def __init__(self, name=None):
        temp_name = name if name is not None else "Anonymous"
        
        # Перевірка на наявність лише букв
        if not temp_name.isalpha():
            # Дозволяємо "Anonymous", оскільки це внутрішнє значення
            if temp_name != "Anonymous":
                raise ValueError("Ім'я не повинно містити цифр або символів!")
        
        self.name = temp_name.capitalize()

Фінальний Модифікований Клас
class Person:
    def __init__(self, name=None):
        temp_name = name if name is not None else "Anonymous"
        
        # 7. Перевірка на цифри/символи
        if not temp_name.isalpha():
            if temp_name != "Anonymous":
                raise ValueError("Ім'я не повинно містити цифр або символів!")
                
        # 5. Завжди починається з великої літери
        self.name = temp_name.capitalize()

    # 2. Змінений текст привітання
    def say_hello(self):
        return f"Greetings! I am {self.name}, pleased to meet you."

    # 3. Функція для підрахунку букв імені
    def count_name_letters(self):
        return len(self.name)

    # 6. Модифікований метод для зміни домену
    def create_email(self, domain="company.com"):
        return f"{self.name.lower()}@{domain}"
