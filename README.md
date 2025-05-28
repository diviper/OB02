# 🧑‍💼 Система управления пользователями

[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Tests](https://github.com/diviper/studyOB1/actions/workflows/tests.yml/badge.svg)](https://github.com/diviper/studyOB1/actions/workflows/tests.yml)
[![Coverage](https://img.shields.io/badge/coverage-58%25-yellow)](https://github.com/diviper/studyOB1/actions)
[![PyPI](https://img.shields.io/pypi/v/user-management-system)](https://pypi.org/project/user-management-system/)

Современная система управления пользователями с поддержкой ролей, написанная на Python. Проект включает полный набор инструментов для разработки, тестирования и развертывания.

## 📋 Оглавление

- [Возможности](#-возможности)
- [Требования](#-требования)
- [Установка](#-установка)
- [Быстрый старт](#-быстрый-старт)
- [Документация](#-документация)
- [Разработка](#-разработка)
- [Тестирование](#-тестирование)
- [Вклад в проект](#-вклад-в-проект)
- [Лицензия](#-лицензия)

## 🌟 Возможности

- 🔐 **Аутентификация и авторизация**
  - Регистрация и вход пользователей
  - JWT-токены для доступа к API
  - Разграничение прав доступа

- 👥 **Управление пользователями**
  - Создание и редактирование профилей
  - Гибкая система ролей и разрешений
  - Поиск и фильтрация пользователей

- 🛡️ **Безопасность**
  - Хеширование паролей с использованием bcrypt
  - Валидация входных данных
  - Защита от CSRF и других уязвимостей

- 📊 **Логирование и аудит**
  - Детальное логирование действий
  - Отслеживание изменений
  - Экспорт данных

- 🧪 **Качество кода**
  - Покрытие тестами
  - Проверка типов
  - Автоматическое форматирование кода

## 🚀 Быстрый старт

### Установка

```bash
# Установка из PyPI
pip install user-management-system

# Или установка из исходников
git clone https://github.com/diviper/studyOB1.git
cd studyOB1
pip install -e .
```

### Настройка

1. Создайте файл `.env` в корне проекта:
   ```bash
   cp .env.example .env
   ```

2. Настройте переменные окружения:
   ```
   DEBUG=True
   SECRET_KEY=ваш-секретный-ключ
   DATABASE_URL=sqlite:///db.sqlite3
   ```

### Пример использования

```python
from user_management import User, Admin

# Создание администратора
admin = Admin(user_id=1, name="Администратор")
admin.set_password("secure_password")

# Создание пользователя
user = User(user_id=2, name="Иван Иванов")
user.set_password("user_password")

# Добавление пользователя администратором
admin.add_user(user)

# Проверка пароля
if user.check_password("user_password"):
    print("Пароль верный!")
```

## 📚 Документация

### Модели данных

#### Пользователь (User)

```python
class User:
    def __init__(self, user_id: int, name: str, email: str = None):
        self.user_id = user_id
        self.name = name
        self.email = email
        self.is_active = True
        self.roles = set()

    def set_password(self, password: str) -> None:
        """Установка хеша пароля."""
        self.password_hash = hash_password(password)

    def check_password(self, password: str) -> bool:
        """Проверка пароля."""
        return verify_password(password, self.password_hash)
```

#### Администратор (Admin)

```python
class Admin(User):
    def add_user(self, user: User) -> bool:
        """Добавление нового пользователя."""
        # Реализация
        pass

    def remove_user(self, user_id: int) -> bool:
        """Удаление пользователя по ID."""
        # Реализация
        pass
```

### API

#### Эндпоинты

- `POST /api/auth/register` - Регистрация нового пользователя
- `POST /api/auth/login` - Вход в систему
- `GET /api/users` - Список пользователей (требуются права администратора)
- `GET /api/users/{user_id}` - Получение информации о пользователе

## 🛠️ Разработка

### Установка для разработки

```bash
# Клонирование репозитория
git clone https://github.com/diviper/studyOB1.git
cd studyOB1

# Создание виртуального окружения
python -m venv venv
source venv/bin/activate  # или .\venv\Scripts\activate на Windows

# Установка зависимостей
pip install -e ".[dev]"

# Настройка pre-commit хуков
pre-commit install
```

### Запуск сервера разработки

```bash
uvicorn user_management.main:app --reload
```

### Форматирование кода

```bash
# Автоматическое форматирование
black .

# Сортировка импортов
isort .

# Проверка стиля
flake8
```

## 🧪 Тестирование

### Запуск тестов

```bash
# Все тесты
pytest

# С покрытием кода
pytest --cov=user_management

# Генерация отчета о покрытии
pytest --cov=user_management --cov-report=html
```

### Типы тестов

- **Модульные тесты**: `tests/unit/`
- **Интеграционные тесты**: `tests/integration/`
- **E2E тесты**: `tests/e2e/`

## 🤝 Вклад в проект

1. Сделайте форк репозитория
2. Создайте ветку для новой фичи: `git checkout -b feature/new-feature`
3. Сделайте коммит изменений: `git commit -am 'Добавлен новый функционал'`
4. Отправьте изменения: `git push origin feature/new-feature`
5. Создайте Pull Request

## 📜 Лицензия

Этот проект распространяется под лицензией MIT. См. файл [LICENSE](LICENSE) для получения дополнительной информации.

## 📞 Контакты

По вопросам и предложениям обращайтесь:
- Email: your.email@example.com
- Issues: https://github.com/diviper/studyOB1/issues

## 🚀 Быстрый старт

### Базовое использование

```python
from user_management import User, Admin, UserRole, UserProfile
from datetime import datetime

# Создаем администратора
admin = Admin(
    user_id=1,
    name="Алексей Админов",
    email="admin@example.com"
)
admin.set_password("admin123")

# Создаем пользователя
user = User(
    user_id=2,
    name="Иван Иванов",
    email="user@example.com"
)
user.set_password("user123")

# Добавляем пользователя в систему
admin.add_user(user)

# Создаем и назначаем роль
editor_role = UserRole(
    name="editor",
    permissions=["create_post", "edit_post"],
    description="Редактор контента"
)
admin.update_user_role(user.user_id, editor_role)

# Обновляем профиль пользователя
user.update_profile(
    phone="+79123456789",
    address="ул. Примерная, д. 123"
)

# Проверяем разрешения
if user.has_permission("create_post"):
    print("У пользователя есть права на создание постов")
```

## 📚 Документация

### Классы

#### `User`
Базовый класс пользователя системы.

**Атрибуты:**
- `user_id: int` - Уникальный идентификатор пользователя
- `name: str` - Имя пользователя
- `email: Optional[str]` - Электронная почта
- `access_level: str` - Уровень доступа (по умолчанию 'user')
- `profile: UserProfile` - Дополнительная информация о пользователе
- `roles: List[UserRole]` - Список ролей пользователя

**Методы:**
- `set_password(password: str) -> None` - Устанавливает хеш пароля
- `check_password(password: str) -> bool` - Проверяет пароль
- `update_profile(**kwargs) -> None` - Обновляет профиль пользователя
- `add_role(role: UserRole) -> None` - Добавляет роль пользователю
- `has_permission(permission: str) -> bool` - Проверяет наличие разрешения
- `to_dict() -> Dict[str, Any]` - Конвертирует объект в словарь

#### `Admin`
Класс администратора, наследующийся от `User`.

**Дополнительные методы:**
- `add_user(user: User) -> bool` - Добавляет пользователя в систему
- `remove_user(user_id: int) -> bool` - Удаляет пользователя
- `get_user(user_id: int) -> Optional[User]` - Возвращает пользователя по ID
- `list_users() -> List[Dict[str, Any]]` - Возвращает список пользователей
- `search_users(**criteria) -> List[User]` - Ищет пользователей по критериям
- `update_user_role(user_id: int, role: UserRole) -> bool` - Обновляет роль пользователя

#### `UserProfile`
Модель профиля пользователя.

**Атрибуты:**
- `phone: Optional[str]` - Номер телефона
- `address: Optional[str]` - Адрес
- `created_at: datetime` - Дата создания
- `last_login: Optional[datetime]` - Дата последнего входа
- `is_active: bool` - Активен ли пользователь

#### `UserRole`
Модель роли пользователя.

**Атрибуты:**
- `name: str` - Название роли
- `permissions: List[str]` - Список разрешений
- `description: str` - Описание роли

## 🛠️ Разработка

### Установка для разработки

1. Клонируйте репозиторий:
   ```bash
   git clone https://github.com/yourusername/user-management-system.git
   cd user-management-system
   ```

2. Установите зависимости для разработки:
   ```bash
   pip install -e ".[dev]"
   ```

3. Установите pre-commit хуки:
   ```bash
   pre-commit install
   ```

### Структура проекта

# Пытаемся добавить пользователя с существующим ID
admin.add_user(User(2, "Дубликат"))  # False, пользователь не добавлен

# Выводим список пользователей
admin.list_users()
# Выведет:
# Список пользователей (всего: 2):
# 1. Пользователь ID: 2, Имя: Иван Иванов, Уровень доступа: user
# 2. Пользователь ID: 3, Имя: Мария Петрова, Уровень доступа: user

# Удаляем пользователя
admin.remove_user(2)  # True
```

### Изменение данных пользователя

```python
user = User(4, "Сергей Сидоров")
print(user.name)  # Сергей Сидоров

# Изменяем имя
user.name = "Сергей Николаев"
print(user.name)  # Сергей Николаев

# Пытаемся установить некорректное имя
try:
    user.name = ""  # Пустое имя
    # Будет вызвано исключение ValueError: Имя пользователя должно быть непустой строкой
except ValueError as e:
    print(f"Ошибка: {e}")
```

## 🧪 Тестирование

### Запуск тестов

```bash
# Запуск всех тестов
pytest tests/ -v

# Запуск с покрытием кода
pytest --cov=user_management tests/

# Генерация отчета о покрытии
pytest --cov=user_management --cov-report=html tests/
```

### Доступные тесты

- `TestUser` - тестирование базового функционала пользователя
  - Создание пользователя
  - Валидация данных
  - Управление профилем
  - Работа с паролями

- `TestAdmin` - тестирование функционала администратора
  - Управление пользователями
  - Назначение ролей
  - Поиск пользователей

### Интеграция с CI/CD

Проект настроен на автоматический запуск тестов при каждом push в репозиторий через GitHub Actions. Проверки включают:
- Запуск тестов
- Проверку стиля кода (black, isort)
- Проверку типов (mypy)
- Проверку безопасности зависимостей (safety)

## 🛠️ Разработка

### Установка для разработки

1. Установите зависимости разработки:
   ```bash
   pip install -e ".[dev]"
   ```

2. Настройте pre-commit хуки:
   ```bash
   pre-commit install
   ```

### Форматирование кода

```bash
# Автоматическое форматирование
black .
isort .

# Проверка стиля
flake8
```

### Создание релиза

1. Обновите версию в `pyproject.toml`
2. Обновите `CHANGELOG.md`
3. Создайте тег с версией:
   ```bash
   git tag -a v0.1.0 -m "Initial release"
   git push origin v0.1.0
   ```

## 🤝 Вклад в проект

Приветствуются запросы на включение (pull requests) и сообщения об ошибках (issues).

1. Форкните репозиторий
2. Создайте ветку для вашей функции (`git checkout -b feature/amazing-feature`)
3. Зафиксируйте изменения (`git commit -m 'Add some amazing feature'`)
4. Отправьте изменения в ваш форк (`git push origin feature/amazing-feature`)
5. Откройте Pull Request

## 📄 Лицензия

Этот проект распространяется под лицензией MIT. См. файл `LICENSE` для дополнительной информации.

---

## 📞 Контакты

**Чурэн Дмитрий Сергеевич**

- Telegram: [@diviper](https://t.me/diviper)
- Email: [churendmitriy@gmail.com](mailto:churendmitriy@gmail.com)

---

<div align="center">
  <p>Создано с ❤️ для упрощения управления пользователями</p>
  <p>Если у вас есть вопросы или предложения, не стесняйтесь связаться!</p>
</div>
