# 🐍 Установка и настройка Anaconda + PySpark + Jupyter Notebook

![OS](https://img.shields.io/badge/OS-ALT_Workstation_K_11.2_Nemorosa-blue?style=for-the-badge&logo=linux&logoColor=white)
![Anaconda](https://img.shields.io/badge/Anaconda-44A833?style=for-the-badge&logo=anaconda&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Apache Spark](https://img.shields.io/badge/Apache_Spark-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white)

---

## 📋 Содержание

- [🐍 Установка и настройка Anaconda + PySpark + Jupyter Notebook](#-установка-и-настройка-anaconda--pyspark--jupyter-notebook)
  - [📋 Содержание](#-содержание)
  - [💻 Требования](#-требования)
  - [📥 Шаг 1 — Загрузка установочного файла](#-шаг-1--загрузка-установочного-файла)
  - [🔑 Шаг 2 — Делаем установочный файл исполняемым](#-шаг-2--делаем-установочный-файл-исполняемым)
  - [▶️ Шаг 3 — Запуск установки](#️-шаг-3--запуск-установки)
  - [📄 Шаг 4 — Принятие лицензионного соглашения](#-шаг-4--принятие-лицензионного-соглашения)
  - [📂 Шаг 5 — Выбор места установки](#-шаг-5--выбор-места-установки)
  - [⚙️ Шаг 6 — Инициализация conda](#️-шаг-6--инициализация-conda)
    - [Блок автоинициализации в `.zshrc`](#блок-автоинициализации-в-zshrc)
  - [✅ Шаг 7 — Завершение установки и проверка](#-шаг-7--завершение-установки-и-проверка)
  - [🔄 Шаг 8 — Обновление Anaconda](#-шаг-8--обновление-anaconda)
  - [🔛 Шаг 9 — Управление автозапуском среды conda](#-шаг-9--управление-автозапуском-среды-conda)
  - [⚡ Шаг 10 — Настройка PySpark](#-шаг-10--настройка-pyspark)
    - [✅ Проверка конфигурации](#-проверка-конфигурации)
  - [🚀 Шаг 11 — Проверка связки Spark + Jupyter](#-шаг-11--проверка-связки-spark--jupyter)
    - [Остановка сеанса Spark](#остановка-сеанса-spark)
  - [📁 Шаг 12 — Настройка рабочей директории Jupyter](#-шаг-12--настройка-рабочей-директории-jupyter)
  - [📌 Итоговая структура проекта](#-итоговая-структура-проекта)

---

## 💻 Требования

| Компонент | Версия |
|-----------|--------|
| ОС | ALT Workstation K 11.2 (Nemorosa) x86_64 (Или любой другой Linux)|
| Shell | zsh + Oh My Zsh (Не обязательно можно использовать bash)|
| Java | JDK 11+ (для Apache Spark) |
| Apache Spark | установлен в `/opt/spark` |

---

## 📥 Шаг 1 — Загрузка установочного файла

Перейдите на официальный сайт и скачайте актуальный дистрибутив для Linux x86_64:

🔗 **https://www.anaconda.com/download**

Выберите версию: **Linux — 64-Bit (x86) Installer**

> ⚠️ Всегда скачивайте актуальную версию с официального сайта — ссылки на конкретные файлы устаревают.

Перейдите в нужную директорию (обычно это домашняя директория `/home/yourusername/`) и загрузите установочный файл с помощью `wget`, указав актуальное имя файла:

```bash
wget https://repo.anaconda.com/archive/Anaconda3-XXXX.XX-X-Linux-x86_64.sh
```

---

## 🔑 Шаг 2 — Делаем установочный файл исполняемым

Сделайте скрипт установки исполняемым с помощью команды `chmod`:

```bash
chmod +x Anaconda3-XXXX.XX-X-Linux-x86_64.sh
```

---

## ▶️ Шаг 3 — Запуск установки

Запустите скрипт установки:

```bash
./Anaconda3-XXXX.XX-X-Linux-x86_64.sh
```

---

## 📄 Шаг 4 — Принятие лицензионного соглашения

Прочитайте и примите лицензионное соглашение, нажимая `ENTER`, пока не увидите вопрос о согласии, и введите `yes`.

---

## 📂 Шаг 5 — Выбор места установки

Укажите место установки Anaconda. Если вас устраивает предложенный путь `/home/yourusername/anaconda3`, просто нажмите `ENTER`.

---

## ⚙️ Шаг 6 — Инициализация conda

При запросе на добавление Anaconda в файл инициализации выберите `yes`. Это добавит Anaconda в ваш `PATH`, чтобы вы могли использовать conda из любого каталога в терминале. После завершения установки закройте и повторно откройте терминал.

### Блок автоинициализации в `.zshrc`

Conda автоматически добавит в `~/.zshrc` следующий блок:

```zsh
# >>> conda initialize >>>
__conda_setup="$('/home/ВашеИмяПользователя/anaconda3/bin/conda' 'shell.zsh' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/ВашеИмяПользователя/anaconda3/etc/profile.d/conda.sh" ]; then
        . "/home/ВашеИмяПользователя/anaconda3/etc/profile.d/conda.sh"
    else
        export PATH="/home/ВашеИмяПользователя/anaconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

---

## ✅ Шаг 7 — Завершение установки и проверка

После завершения установки закройте и повторно откройте терминал, чтобы изменения вступили в силу. Проверьте установку:

```bash
conda list
```

```bash
conda --version
```

Если установка прошла успешно, вы увидите список пакетов и версию conda. В начале строки терминала должно появиться `(base)` 🐍.

---

## 🔄 Шаг 8 — Обновление Anaconda

```bash
conda update conda
```

---

## 🔛 Шаг 9 — Управление автозапуском среды conda

**Отключить** автоматическую активацию базовой среды при запуске терминала:

```bash
conda config --set auto_activate_base false
```

> После этого при открытии нового терминала команда `conda` будет доступна, но базовая среда не будет активироваться автоматически.

**Активировать** среду conda вручную:

```bash
conda activate
```

**Деактивировать** среду conda:

```bash
conda deactivate
```

**Включить** автоматическую активацию обратно:

```bash
conda config --set auto_activate_base true
```

---

## ⚡ Шаг 10 — Настройка PySpark

Добавьте в `~/.zshrc` пути для Spark и укажите Python от Anaconda:

```zsh
# Настройка путей Spark
export SPARK_HOME=/opt/spark
export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin

# Python для PySpark (раскомментировать нужный)
export PYSPARK_PYTHON=/home/ВашеИмяПользователя/anaconda3/bin/python  # Anaconda 3.13.9   Рекомендуется
# export PYSPARK_PYTHON=/usr/bin/python3                   # Системный 3.12.7
# export PYSPARK_PYTHON=/usr/local/bin/python3.14          # Python 3.14.3
```

Примените изменения:

```bash
source ~/.zshrc
```

### ✅ Проверка конфигурации

Убедитесь, что все три компонента указывают на один интерпретатор:

```bash
which jupyter    # → /home/ИмяПользователя/anaconda3/bin/jupyter
which python     # → /home/ИмяПользователя/anaconda3/bin/python
echo $PYSPARK_PYTHON  # → /home/ИмяПользователя/anaconda3/bin/python
```

> 💡 Все три пути должны совпадать — это исключает конфликты между Jupyter и PySpark.

---

## 🚀 Шаг 11 — Проверка связки Spark + Jupyter

Запустите Jupyter Notebook:

```bash
jupyter notebook
```

Создайте новый ноутбук и выполните следующий код:

```python
# Импортируем библиотеку findspark для работы с путями Spark
import findspark
findspark.init('/opt/spark')  # Указывает на установку Spark
```

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("test") \
    .master("local[*]") \
    .getOrCreate()

# Подавить лишние предупреждения в выводе
spark.sparkContext.setLogLevel("ERROR")

spark.range(5).show()
```

Ожидаемый результат:

```
+---+
| id|
+---+
|  0|
|  1|
|  2|
|  3|
|  4|
+---+
```

> ℹ️ Предупреждения `jdk.incubator.vector` и `Unable to load native-hadoop library` — **не критичны** для локального режима `local[*]`.

### Остановка сеанса Spark

После завершения работы всегда останавливайте сеанс:

```python
spark.stop()
```

---

## 📁 Шаг 12 — Настройка рабочей директории Jupyter

По умолчанию Jupyter открывается в домашней директории. Чтобы он сразу открывался в нужной папке, настройте конфигурацию.

**Создайте файл конфигурации** (если ещё не существует):

```bash
jupyter notebook --generate-config
```

Файл будет создан по пути `~/.jupyter/jupyter_notebook_config.py`.

**Откройте файл:**

```bash
nano ~/.jupyter/jupyter_notebook_config.py
```

Используйте поиск `Ctrl+W` и введите `root_dir`.

**Найдите строку:**

```python
# c.ServerApp.root_dir = ''
```

**Замените на** (без `#` в начале и без лишних пробелов):

```python
c.ServerApp.root_dir = '/home/ВашеИмяПользователя/ВашаДиректория'
```

Сохраните: `Ctrl+O` → `Enter` → `Ctrl+X`

> ⚠️ Убедитесь, что в начале строки **нет пробелов** — это частая причина того, что настройка не применяется.

Перезапустите Jupyter — он будет открываться сразу в указанной папке. 🎉

---

## 📌 Итоговая структура проекта

```
~/
├── anaconda3/            # Дистрибутив Anaconda
├── My_jupyter_notebook/  # Рабочая директория Jupyter
├── My_Spark/             # Проекты Apache Spark
└── python_projects/      # Python проекты
```

---

![Status](https://img.shields.io/badge/Статус-Проверено-success?style=for-the-badge)
![ALT Linux](https://img.shields.io/badge/ALT_Linux-Compatible-blue?style=for-the-badge)
