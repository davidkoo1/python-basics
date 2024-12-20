# Модули Python, используемые при работе с датой и временем

Дата в Python это не предопределенный тип данных, но Python может импортировать один из нескольких модулей для работы с датой как объект.

1. **Модуль `datetime`:**
   Модуль `datetime` предоставляет классы для манипуляции датами и временем. Он включает в себя работу с датами, временем, а также комбинацией даты и времени.

   **Основные функции и классы:**
   - `datetime.datetime`: для работы с датой и временем (например, текущее время).
   - `datetime.date`: для работы с датой (год, месяц, день).
   - `datetime.time`: для работы с временем (часы, минуты, секунды).
   - `datetime.timedelta`: для представления разницы между датами и временем.
   - `datetime.strptime()` и `datetime.strftime()`: для парсинга строк в объекты `datetime` и обратно.
   
   **Пример:**
   ```python
   from datetime import datetime, timedelta

   # Текущее время
   now = datetime.now()
   print(f"Текущее время: {now}")

   # Создание даты из строки
   date_str = "2024-12-04"
   date_obj = datetime.strptime(date_str, "%Y-%m-%d")
   print(f"Дата из строки: {date_obj}")

   # Разница между датами
   diff = timedelta(days=5)
   future_date = now + diff
   print(f"Дата через 5 дней: {future_date}")
   ```
   ### Форматные спецификаторы даты и времени:

- **%y**: Год в двухзначном формате.  
- **%Y**: Год в четырехзначном формате.  
- **%m**: Месяц в виде двухзначного числа.  
- **%b**: Аббревиатура названия месяца.  
- **%B**: Полное название месяца.  
- **%d**: День месяца в виде двухзначного числа.  
- **%j**: Порядковый номер дня в году.  
- **%U**: Номер недели года, начиная с воскресенья.  
- **%W**: Номер недели года, начиная с понедельника.  
- **%w**: День недели в числовом формате (0 для воскресенья, 6 для субботы).

2. **Модуль `time`:**
   Модуль `time` позволяет работать с временем в более низкоуровневом виде. Он в основном используется для работы с системным временем и задержками в программе.

   **Основные функции:**
   - `time.time()`: возвращает текущее время в секундах с эпохи (1 января 1970 года).
   - `time.sleep()`: задержка выполнения программы на заданное количество секунд.
   - `time.localtime()` и `time.gmtime()`: конвертируют время в структурированное представление.
   - `time.strftime()` и `time.strptime()`: для форматирования и парсинга строк, аналогичные методам в `datetime`.

   **Пример:**
   ```python
   import time

   # Время в секундах с эпохи
   current_time = time.time()
   print(f"Текущее время с эпохи: {current_time}")

   # Задержка в 2 секунды
   print("Начало паузы")
   time.sleep(2)
   print("Пауза завершена")
   ```
   
Объект `struct_time` в Python — это структура данных, используемая для представления времени в виде кортежа из 9 элементов. Он предоставляется модулем `time` и часто используется для преобразования между форматами времени (например, строкой и меткой времени).

### Структура объекта `struct_time`:
Кортеж `struct_time` содержит следующие поля:

1. **tm_year**: Год (например, 2024).  
2. **tm_mon**: Месяц (1–12).  
3. **tm_mday**: День месяца (1–31).  
4. **tm_hour**: Часы (0–23).  
5. **tm_min**: Минуты (0–59).  
6. **tm_sec**: Секунды (0–61, где значения 60 и 61 могут возникать из-за високосных секунд).  
7. **tm_wday**: День недели (0 — понедельник, 6 — воскресенье).  
8. **tm_yday**: День года (1–366).  
9. **tm_isdst**: Индикатор летнего времени (-1, 0, 1):
   - `1`: Летнее время активно.  
   - `0`: Летнее время не активно.  
   - `-1`: Информация неизвестна.  

### Примеры получения `struct_time`:

1. **Текущее локальное время**:
   ```python
   import time
   current_time = time.localtime()
   print(current_time)
   ```

2. **Время в формате UTC**:
   ```python
   utc_time = time.gmtime()
   print(utc_time)
   ```

3. **Создание `struct_time` из метки времени**:
   ```python
   timestamp = 1672531200  # Пример метки времени
   struct_time_obj = time.localtime(timestamp)
   print(struct_time_obj)
   ```

### Преимущества:
- Удобен для работы с временными данными, такими как преобразования между форматами, вычисления временных интервалов, и проверки времени.
- Поддерживается множеством методов и функций из модулей `time` и `datetime`.  

### Пример использования:
```python
import time

# Получить текущее время
current_time = time.localtime()

# Доступ к элементам
print("Год:", current_time.tm_year)
print("Месяц:", current_time.tm_mon)
print("День:", current_time.tm_mday)
```

---

Метод `strptime()` из модуля `datetime` используется для парсинга строки, содержащей дату и/или время, в объект `datetime`. Он позволяет задать формат входной строки, чтобы правильно интерпретировать дату и время.

### Синтаксис:
```python
from datetime import datetime
datetime.strptime(date_string, format)
```

### Параметры:
- **`date_string`**: Строка, содержащая дату/время, которую нужно преобразовать.  
- **`format`**: Формат строки, определяющий, как `date_string` будет интерпретироваться. Используются те же спецификаторы, что и в методе `strftime()` (например, `%Y`, `%m`, `%d` и другие).

### Возвращаемое значение:
Возвращает объект `datetime`, соответствующий указанной строке и формату.

### Пример использования:
1. **Парсинг даты и времени**:
   ```python
   from datetime import datetime

   date_str = "2024-12-05 14:30:00"
   date_obj = datetime.strptime(date_str, "%Y-%m-%d %H:%M:%S")
   print(date_obj)  # 2024-12-05 14:30:00
   ```

2. **Парсинг только даты**:
   ```python
   date_str = "05-12-2024"
   date_obj = datetime.strptime(date_str, "%d-%m-%Y")
   print(date_obj)  # 2024-12-05 00:00:00
   ```

3. **Парсинг времени**:
   ```python
   time_str = "14:30"
   time_obj = datetime.strptime(time_str, "%H:%M")
   print(time_obj.time())  # 14:30:00
   ```

### Возможные ошибки:
- **`ValueError`**: Возникает, если строка не соответствует указанному формату. Например:
  ```python
  date_str = "2024/12/05"
  date_obj = datetime.strptime(date_str, "%Y-%m-%d")  # Ошибка
  ```

### Практические замечания:
- Используйте `strptime()` для преобразования строкового формата даты/времени в объект `datetime` для удобных вычислений или форматирования.
- Для обратного преобразования (`datetime` → строка) используйте метод `strftime()`.

---

3. **Модуль `calendar`:**
   Модуль `calendar` предоставляет функции для работы с календарем, такими как вывод месяцев и проверка високосных лет.

   **Основные функции:**
   - `calendar.month()`: выводит месяц в виде строки.
   - `calendar.isleap()`: проверяет, является ли год високосным.
   - `calendar.weekday()`: возвращает день недели для заданной даты.

   **Пример:**
   ```python
   import calendar

   # Проверка, является ли год 2024 високосным
   print(f"2024 високосный год? {calendar.isleap(2024)}")

   # Вывод календаря на декабрь 2024 года
   print(calendar.month(2024, 12))
   ```
 Основной класс этого модуля — **`Calendar`**, от которого наследуются другие специализированные классы.

### Основные классы модуля `calendar`:

1. **`Calendar`**  
   Основной класс для работы с календарями. Позволяет задавать первый день недели (по умолчанию понедельник).  
   **Синтаксис**:  
   ```python
   calendar.Calendar([firstweekday])
   ```  

2. **`TextCalendar`**  
   Класс для отображения календаря в текстовом формате. Можно задать первый день недели.  
   **Синтаксис**:  
   ```python
   calendar.TextCalendar([firstweekday])
   ```  

3. **`LocaleTextCalendar`**  
   Класс для отображения календаря в текстовом формате с учетом локали. Названия месяцев и дней отображаются в зависимости от заданной локали.  
   **Синтаксис**:  
   ```python
   calendar.LocaleTextCalendar([firstweekday[, locale]])
   ```  

4. **`HTMLCalendar`**  
   Класс для создания календаря в формате HTML. Выводится строка HTML-кода, представляющая календарь в виде таблицы.  
   **Синтаксис**:  
   ```python
   calendar.HTMLCalendar([firstweekday])
   ```  

5. **`LocaleHTMLCalendar`**  
   Класс для создания локализованного календаря в формате HTML. Названия месяцев и дней зависят от указанной локали.  
   **Синтаксис**:  
   ```python
   calendar.LocaleHTMLCalendar([firstweekday[, locale]])
   ```

### Примеры использования:
1. **Вывод текстового календаря**:
   ```python
   import calendar

   text_cal = calendar.TextCalendar(firstweekday=6)  # Неделя начинается с воскресенья
   print(text_cal.formatmonth(2024, 12))
   ```

2. **Локализованный текстовый календарь**:
   ```python
   import calendar

   locale_cal = calendar.LocaleTextCalendar(locale='ru_RU')
   print(locale_cal.formatmonth(2024, 12))
   ```

3. **Календарь в HTML формате**:
   ```python
   import calendar

   html_cal = calendar.HTMLCalendar(firstweekday=0)  # Неделя начинается с понедельника
   print(html_cal.formatmonth(2024, 12))
   ```

---

### Модуль `math`

Модуль `math` в Python предоставляет доступ к множеству математических функций, таких как арифметические операции, тригонометрия, логарифмы и другие числовые операции.

**Основные функции и константы:**
- `math.sqrt(x)`: квадратный корень из числа `x`.
- `math.factorial(x)`: вычисление факториала числа `x`.
- `math.sin(x)`, `math.cos(x)`, `math.tan(x)`: тригонометрические функции.
- `math.log(x, base)`: логарифм числа `x` по основанию `base`.
- `math.pi`: значение числа π.
- `math.e`: значение числа e.

**Пример:**
```python
import math

# Квадратный корень
print(math.sqrt(16))  # 4.0

# Синус угла в радианах
print(math.sin(math.radians(90)))  # 1.0

# Логарифм по основанию 10
print(math.log(100, 10))  # 2.0

# Факториал
print(math.factorial(5))  # 120

# Число π
print(math.pi)  # 3.141592653589793
```

Модуль `math` полезен для выполнения сложных математических операций и часто используется в научных и инженерных задачах.