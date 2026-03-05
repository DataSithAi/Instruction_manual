# <img src="https://img.shields.io/badge/GIGA_IDE_CE-2025.1-4A90D9?style=for-the-badge&logo=jetbrains&logoColor=white"/> Руководство по установке

[![ALT Linux](https://img.shields.io/badge/ALT_Workstation_K-11.2_Nemorosa-4A90D9?style=flat-square&logo=linux&logoColor=white)](https://www.altlinux.org/)
[![Архитектура](https://img.shields.io/badge/arch-x86__64-brightgreen?style=flat-square&logo=gnubash&logoColor=white)]()
[![Статус](https://img.shields.io/badge/статус-протестировано-success?style=flat-square&logo=checkmarx&logoColor=white)]()
[![Версия](https://img.shields.io/badge/версия-251.26927.53-blue?style=flat-square)]()

---

> **GigaIDE CE** — российская IDE на базе IntelliJ Platform от Сбера, с поддержкой GigaChat AI-ассистента прямо в редакторе.

---

## 📋 Содержание

- [Требования](#-требования)
- [Шаг 1 — Загрузка](#-шаг-1--загрузка)
- [Шаг 2 — Распаковка](#-шаг-2--распаковка)
- [Шаг 3 — Установка](#-шаг-3--установка)
- [Шаг 4 — Запуск](#-шаг-4--запуск)
- [Шаг 5 — Ярлык в меню](#-шаг-5--ярлык-в-меню)

---

## ✅ Требования

| Компонент | Минимум |
|---|---|
| 🐧 ОС | ALT Workstation K 11.2+ / любой Linux x86_64 |
| 💾 Диск | ~2 ГБ свободного места |
| 🧠 ОЗУ | 4 ГБ (рекомендуется 8+ ГБ) |
| ☕ Java | Встроена в дистрибутив (не требуется отдельно) |

---

## 📥 Шаг 1 — Загрузка

Скачай актуальный дистрибутив с официального сайта:

[![Скачать GigaIDE](https://img.shields.io/badge/Скачать_GigaIDE_CE-gigaide.ru-4A90D9?style=for-the-badge&logo=download&logoColor=white)](https://gigaide.ru)

После загрузки файл будет выглядеть так:

```
gigaideCE-251.26927.53.tar.gz   (~1.1 ГБ)
```

---

## 📦 Шаг 2 — Распаковка

Перейди в папку с загруженным файлом и распакуй архив:

```bash
cd ~/Загрузки
tar -xzf gigaideCE-251.26927.53.tar.gz
```

> ⚠️ **Примечание:** В процессе распаковки могут появиться предупреждения вида:
> ```
> tar: Игнорируется неизвестное ключевое слово расширенного заголовка «LIBARCHIVE.creationtime»
> ```
> Это **не ошибка** — просто tar на ALT Linux не знает это расширение macOS/BSD. Распаковка завершается успешно.

Убедись, что папка появилась:

```bash
ls -la | grep -i giga
# Ожидаемый вывод:
# drwxr-xr-x gigaide-CE-251.26927.53
```

---

## 🚀 Шаг 3 — Установка

Перемести распакованную папку в `/opt` — стандартное место для сторонних приложений в Linux:

```bash
sudo mv ~/Загрузки/gigaide-CE-251.26927.53 /opt/gigaide
```

Проверь содержимое директории `bin/`:

```bash
ls /opt/gigaide/bin/
```

Среди файлов должны быть:

| Файл | Назначение |
|---|---|
| `idea` | 🚀 Нативный лаунчер (**рекомендуется**) |
| `idea.sh` | Shell-скрипт запуска |
| `idea.png` | Иконка приложения |
| `idea.properties` | Настройки JVM |
| `idea64.vmoptions` | Параметры памяти JVM |
| `fsnotifier` | Наблюдатель за файловой системой |

---

## ▶️ Шаг 4 — Запуск

Запусти GigaIDE:

```bash
/opt/gigaide/bin/idea.sh
```

При первом запуске откроется экран приветствия **Welcome to GIGA IDE** с опциями:

- 📁 **New Project** — создать новый проект
- 📂 **Open** — открыть существующий
- 🔗 **Clone Repository** — склонировать из Git

---

## 🖥️ Шаг 5 — Ярлык в меню

Создай `.desktop`-файл, чтобы GigaIDE появилась в меню приложений и её можно было запускать без терминала:

```bash
cat > ~/.local/share/applications/gigaide.desktop << 'EOF'
[Desktop Entry]
Name=GigaIDE CE
Exec=/opt/gigaide/bin/idea %f
Icon=/opt/gigaide/bin/idea.png
Type=Application
Categories=Development;IDE;
StartupWMClass=gigaide
EOF
```

После этого GigaIDE появится в меню в разделе **Разработка**.

---


## 📁 Итоговая структура

```
/opt/gigaide/          ← основная директория IDE
├── bin/
│   ├── idea           ← нативный лаунчер
│   ├── idea.sh        ← shell-скрипт
│   ├── idea.png       ← иконка
│   └── ...
├── lib/               ← библиотеки
├── plugins/           ← плагины
└── jbr/               ← встроенная JVM

~/.local/share/applications/
└── gigaide.desktop    ← ярлык в меню
```

---

<div align="center">

[![ALT Linux](https://img.shields.io/badge/ALT_Linux-протестировано-success?style=flat-square&logo=linux&logoColor=white)]()
[![GigaIDE](https://img.shields.io/badge/GigaIDE_CE-2025.1-4A90D9?style=flat-square&logo=jetbrains&logoColor=white)]()
[![Лицензия](https://img.shields.io/badge/лицензия-Community_Edition-orange?style=flat-square)]()

*Инструкция подготовлена для ALT Workstation K 11.2 (Nemorosa) x86_64*

</div>
