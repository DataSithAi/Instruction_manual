# 🐍 Установка PyCharm на ALT Workstation K 11.2

![OS](https://img.shields.io/badge/OS-ALT_Workstation_K_11.2-4A90D9?style=for-the-badge&logo=linux&logoColor=white)
![PyCharm](https://img.shields.io/badge/PyCharm-2025.x-21D789?style=for-the-badge&logo=pycharm&logoColor=white)
![Arch](https://img.shields.io/badge/Arch-x86__64-ED8B00?style=for-the-badge&logo=intel&logoColor=white)
![Status](https://img.shields.io/badge/Статус-Проверено-success?style=for-the-badge)

---

## 📋 Содержание

1. [Требования](#-требования)
2. [Скачивание PyCharm](#-шаг-1--скачивание-pycharm)
3. [Установка](#-шаг-2--установка)
4. [Первый запуск](#-шаг-3--первый-запуск)
5. [Создание ярлыка в меню](#-шаг-4--создание-ярлыка-в-меню)
6. [Исправление ярлыка](#-шаг-5--исправление-ярлыка-нативный-запуск)
7. [Настройка интерпретатора Anaconda](#-шаг-6--настройка-интерпретатора-anaconda)
8. [Виртуальное окружение Conda](#-шаг-7--виртуальное-окружение-conda)
9. [Готово](#-готово)
10. [Удаление PyCharm](#-удаление-pycharm)

---

## ✅ Требования

![RAM](https://img.shields.io/badge/RAM-минимум_4GB-blue?style=flat-square)
![Disk](https://img.shields.io/badge/Диск-минимум_3.5GB-blue?style=flat-square)
![Python](https://img.shields.io/badge/Python-3.x-yellow?style=flat-square&logo=python)

- Операционная система: **ALT Workstation K 11.2 (Nemorosa) x86_64**
- Права **sudo** для установки в `/opt/`
- Подключение к интернету

---

## 📥 Шаг 1 — Скачивание PyCharm

Перейдите на официальный сайт JetBrains и скачайте архив:

> 🔗 **https://www.jetbrains.com/pycharm/download/**

Выберите версию для **Linux** (файл с расширением `.tar.gz`):

---

## 🔧 Шаг 2 — Установка

### 2.1 Создайте директорию в `/opt/`

```bash
sudo mkdir -p /opt/pycharm
```

### 2.2 Распакуйте архив

```bash
sudo tar -xzf ~/Загрузки/pycharm-*.tar.gz -C /opt/
```

> ⏳ Распаковка занимает около 20–30 секунд.

### 2.3 Проверьте результат

```bash
ls /opt/
```

Вы должны увидеть папку `pycharm-20XX.X.X`:

```
drwxr-xr-x  root  root  /opt/pycharm-2025.3.3
```

---

## 🚀 Шаг 3 — Первый запуск

```bash
/opt/pycharm-2025.3.3/bin/pycharm.sh
```

> 💡 При первом запуске PyCharm создаст проект по умолчанию и откроет страницу «Что нового».

---

## 💻 Шаг 4 — Создание ярлыка в меню

Чтобы запускать PyCharm из меню приложений, создайте Desktop Entry:

В меню PyCharm выберите:

```
Tools → Create Desktop Entry
```

В появившемся окне:

- ☐ **Без галочки** — ярлык только для текущего пользователя *(рекомендуется)*
- ☑ **С галочкой** — ярлык для всех пользователей *(требует sudo)*

Нажмите **OK**.

---

## 🔨 Шаг 5 — Исправление ярлыка (нативный запуск)

По умолчанию ярлык запускает PyCharm через скрипт `pycharm.sh`, из-за чего появляется уведомление:

> ⚠️ *"The IDE seems to be launched with a script launcher. Please consider switching to a native launcher for better experience."*

Исправим это одной командой — заменим `pycharm.sh` на нативный бинарник `pycharm`:

```bash
sed -i 's|bin/pycharm.sh|bin/pycharm|g' ~/.local/share/applications/jetbrains-pycharm.desktop
```

Проверьте результат:

```bash
grep Exec ~/.local/share/applications/jetbrains-pycharm.desktop
```

Ожидаемый вывод:

```
Exec="/opt/pycharm-2025.3.3/bin/pycharm" %f
```

✅ Теперь уведомление больше не появится!

---

## 🐍 Шаг 6 — Настройка интерпретатора Anaconda

По умолчанию PyCharm использует системный Python, из-за чего при работе с Jupyter может появиться ошибка:

> ⚠️ *"Modify packages of System Python is forbidden. To modify use another interpreter."*

Чтобы это исправить, нужно переключить интерпретатор на Anaconda. Это нужно делать **для каждого нового проекта**.

### 6.1 Откройте настройки интерпретатора

```
File → Settings → Python → Interpreter
```

### 6.2 Добавьте новый интерпретатор

Нажмите **Add Interpreter** (справа вверху) → **Add Local Interpreter**.

### 6.3 Выберите Conda

В открывшемся окне:

- Переключитесь с **Generate new** на **Select existing**
- В поле **Type** выберите **Conda**
- PyCharm автоматически определит путь:
  - **Path to conda:** `/home/ВАШ_ПОЛЬЗОВАТЕЛЬ/anaconda3/bin/conda`
  - **Environment:** `/home/ВАШ_ПОЛЬЗОВАТЕЛЬ/anaconda3`

Нажмите **OK**, затем ещё раз **OK** в окне Settings.

> 💡 После этого PyCharm запустит собственный Jupyter сервер автоматически — запускать `jupyter notebook` в терминале вручную больше не нужно.

---

## 📦 Шаг 7 — Виртуальное окружение Conda

Если у вас уже настроена Anaconda — отдельное `venv` создавать **не обязательно**. Базового окружения Anaconda вполне достаточно для большинства задач.

### Когда стоит создать отдельное conda-окружение

- Вы работаете над **несколькими проектами** с разными зависимостями
- Хотите **изолировать пакеты** одного проекта от другого
- Боитесь случайно **сломать базовое** окружение `anaconda3`

### Когда можно обойтись без окружения

- Это небольшой учебный или тестовый проект
- Вы используете стандартные пакеты, уже входящие в Anaconda

### Как создать conda-окружение

```bash
conda create -n my_project python=3.13
conda activate my_project
```

> 💡 Укажите ту версию Python, которая установлена в вашей базовой среде Anaconda. Проверить можно командой `python --version` в терминале с активированной Anaconda.

После создания окружения выберите его в PyCharm как интерпретатор так же, как описано в Шаге 6, но в поле **Environment** выберите `my_project` вместо базового `anaconda3`.

---

## 🎉 Готово!

![Done](https://img.shields.io/badge/Установка-Завершена-brightgreen?style=for-the-badge&logo=checkmarx&logoColor=white)

PyCharm успешно установлен и настроен. Теперь вы можете:

- Запускать PyCharm **из меню приложений** — без лишних уведомлений
- Запускать PyCharm **из терминала**: `/opt/pycharm-*/bin/pycharm`
- Работать с Jupyter Notebook прямо в PyCharm — без запуска сервера вручную

---

## 🗂 Удаление PyCharm

![Uninstall](https://img.shields.io/badge/Удаление-Полное-red?style=for-the-badge&logo=trash&logoColor=white)

### 1. Удалите папку с программой

```bash
sudo rm -rf /opt/pycharm-2025.3.3
sudo rm -rf /opt/pycharm
```

### 2. Удалите ярлык из меню

```bash
rm -f ~/.local/share/applications/jetbrains-pycharm.desktop
```

### 3. Удалите настройки и кэш

```bash
rm -rf ~/.config/JetBrains/PyCharm*
rm -rf ~/.cache/JetBrains/PyCharm*
rm -rf ~/.local/share/JetBrains/PyCharm*
```

### 4. Проверьте, что всё удалено

```bash
ls /opt/ | grep pycharm
ls ~/.local/share/applications/ | grep pycharm
ls ~/.config/JetBrains/ 2>/dev/null
```

> ✅ Если команды ничего не вывели — PyCharm удалён полностью.

---

*Инструкция проверена на ALT Workstation K 11.2 (Nemorosa) x86_64 · PyCharm 2025.3.3*
