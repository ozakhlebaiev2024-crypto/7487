# Звіт до роботи
## Тема: Програмування з використанням ООП
### Мета роботи: Навчитись працювати з Класами та його основними конструкціями;
1) Створюємо базовий клас
class MyAnimals:
    pass

a = MyAnimals()
print(type(a))



2) Порівняння простих даних з об’єктами

animals = ["Рибки", "Кіт", "Собака"]
name = ["Неони", "Мурка", "Рекс"]
age = [1, 5, 2]

print(f"В мене є тваринка {animals[1]} яку звати {name[1]} які {age[1]} років")


class MyAnimals:
    def __init__(self, animals, name, age, mass=None) -> None:
        print(f"В мене є тваринка {animals} яку звати {name} які {age} років")
        self.animals = animals
        self.name = name
        self.age = age
        self.mass = 0 if mass is None else mass


a1 = MyAnimals("Рибки", "Неони", 1)
a2 = MyAnimals("Кіт", "Мурка", 5, 10)
a3 = MyAnimals(animals="Собака", name="Рекс", age=2)

print(a2.name)
a2.name = "Машка"
print(f"Я переіменував свою тваринку на {a2.name}, вона важить {a2.mass} кг")
print(f"Моя тваринка {a1.name}, вона важить {a1.mass} кг")



3) Методи класу

class MyAnimals:
    def __init__(self, animals, name, age, mass=None) -> None:
        self.animals = animals
        self.name = name
        self.age = age
        self.mass = 0 if mass is None else mass

    def speak(self):
        if self.animals == "Кіт":
            return "Мяууу"
        elif self.animals == "Собака":
            return "Гавв"
        return "..."

    def add_one_year(self):
        self.age += 1
        return self.age


a1 = MyAnimals("Рибки", "Неони", 1)
a2 = MyAnimals("Кіт", "Мурка", 5, 10)
a3 = MyAnimals("Собака", "Рекс", 2)

print(a1.speak())
print(a3.speak())
print(a1.age)
print(a1.add_one_year())
print(a1.age)



4) Змінні класу

class MyAnimals:
    total_animals = 0
    total_animal_types = set()

    def __init__(self, animals, name, age) -> None:
        self.animals = animals
        self.name = name
        self.age = age
        MyAnimals.total_animals += 1
        MyAnimals.total_animal_types.add(animals)


print(MyAnimals.total_animals, MyAnimals.total_animal_types)
a1 = MyAnimals("Рибки", "Неони", 1)
MyAnimals("Рибки", "Гупії", 1)
MyAnimals("Кіт", "Мурка", 5)
print(MyAnimals.total_animals, MyAnimals.total_animal_types)

print(a1.total_animal_types)
a1.total_animal_types = {"Собака"}
print(a1.total_animal_types, MyAnimals.total_animal_types)



5) Статичні методи

class MyAnimals:
    def __init__(self, animals, name, age) -> None:
        self.animals = animals
        self.name = name
        self.age = age

    def add_one_year(self):
        self.age += 1
        return self.age

    @staticmethod
    def call_pet():
        return "Тваринка біжить до нас"


a1 = MyAnimals("Рибки", "Гупії", 1)
a2 = MyAnimals("Кіт", "Мурка", 5)

print(a1.call_pet(), MyAnimals.call_pet())
print(a1.add_one_year(), MyAnimals.add_one_year(a1))



6) Properties
from datetime import datetime

class MyAnimals:
    max_age = 20

    def __init__(self, animals, name, age) -> None:
        self.animals = animals
        self.name = name
        self.age = age

    @property
    def live_untill(self):
        return datetime.today().year - self.age + self.max_age


a1 = MyAnimals("Кіт", "Мурка", 5)
print(a1.live_untill)
a1.age += 1
print(a1.live_untill)



7) Методи класу

class MyAnimals:
    total_csv = 0
    total_objects = 0

    def __init__(self, animals, name, age) -> None:
        self.animals = animals
        self.name = name
        self.age = age
        MyAnimals.total_objects += 1

    @classmethod
    def from_csv(cls, csv_data: str):
        cls.total_csv += 1
        animal, name, age = csv_data.split(",")
        return cls(animal, name, int(age))


a1 = MyAnimals.from_csv("Кіт,Мурка,5")
a2 = MyAnimals("Собака", "Рекс", 2)
print(MyAnimals.total_objects, MyAnimals.total_csv)



8) Приватні атрибути

class MyAnimals:
    def __init__(self, animals, name, age) -> None:
        self.animals = animals
        self.name = name
        self.age = age
        self._secret = "private"
        self.__very_secret = "very private"

    @property
    def secret(self):
        return self._secret

    @property
    def very_secret(self):
        return self.__very_secret


a1 = MyAnimals("Собака", "Рекс", 2)
print(a1._secret)
print(a1._MyAnimals__very_secret)
print(a1.secret)
print(a1.very_secret)



9) Магічні методи
class MyAnimals:
    def __init__(self, animals, name, age) -> None:
        self.animals = animals
        self.name = name
        self.age = age

    def __repr__(self):
        return f'MyAnimals("{self.animals}", "{self.name}", {self.age})'

    def __str__(self):
        return f"Обʼєкт: {self.name}"


a1 = MyAnimals("Собака", "Рекс", 2)
print(a1)
print(repr(a1))



10) Арифметичні методи

class MyAnimals:
    def __init__(self, animals, name, age) -> None:
        self.animals = animals
        self.name = name
        self.age = age

    def __sub__(self, other):
        if isinstance(other, MyAnimals):
            return f"{self.name} покусав {other.name}"
        if isinstance(other, int):
            self.age += other
            return self.age
        return NotImplemented

    def __gt__(self, other):
        return self.age > other.age

    def __len__(self):
        return len(self.name)


a = MyAnimals("Собака", "Рекс", 2)
b = MyAnimals("Кіт", "Мурзик", 4)

print(a - b)
print(a - 1)
print(a > b)
print(b > a)
print(len(a))
