import json
import os

class UserSystem:
    def __init__(self, filename="users.json"):
        self.filename = filename
        self.users = self.load_users()

    def load_users(self):
        """Загружает пользователей из файла."""
        if os.path.exists(self.filename):
            with open(self.filename, 'r', encoding='utf-8') as f:
                return json.load(f)
        return {}

    def save_users(self):
        """Сохраняет пользователей в файл."""
        with open(self.filename, 'w', encoding='utf-8') as f:
            json.dump(self.users, f, ensure_ascii=False, indent=4)

    def register(self, username, password):
        """Регистрирует нового пользователя."""
        if username in self.users:
            print("Пользователь с таким именем уже существует.")
            return False
        self.users[username] = password
        self.save_users()
        print(f"Пользователь '{username}' зарегистрирован.")
        return True

    def login(self, username, password):
        """Входит в систему для существующего пользователя."""
        if username in self.users and self.users[username] == password:
            print(f"Добро пожаловать, {username}!")
            return True
        print("Неверное имя пользователя или пароль.")
        return False

    def run(self):
        """Основной цикл программы."""
        while True:
            print("\nМеню:")
            print("1. Регистрация")
            print("2. Вход")
            print("3. Выход")

            choice = input("Выберите действие: ")

            if choice == "1":
                username = input("Введите имя пользователя: ")
                password = input("Введите пароль: ")
                self.register(username, password)
            elif choice == "2":
                username = input("Введите имя пользователя: ")
                password = input("Введите пароль: ")
                self.login(username, password)
            elif choice == "3":
                print("Выход из программы. Спасибо!")
                break
            else:
                print("Некорректный выбор, попробуйте снова.")

# Запуск системы
if __name__ == "__main__":
    user_system = UserSystem()
    user_system.run()
