# 🖥️ Инструкция по установке шрифта `Fira Code Medium Nerd Font Complete` на операционную систему `ALT Workstation K 11.2` и настройка шрифта в `Konsole` по умолчанию.

[![Fira Code](https://img.shields.io/badge/Fira%20Code-Nerd%20Font-blueviolet?style=for-the-badge&logo=fontforge&logoColor=white)](https://github.com/tonsky/FiraCode)
[![Alt Linux](https://img.shields.io/badge/Alt%20Linux-compatible-blue?style=for-the-badge&logo=linux&logoColor=white)](https://www.altlinux.org/)
[![License](https://img.shields.io/badge/License-OFL--1.1-green?style=for-the-badge)](https://github.com/tonsky/FiraCode/blob/master/LICENSE)

> **Fira Code** — моноширинный шрифт с лигатурами для программистов.
> Отлично подходит для терминала, редактора кода и IDE.

---

## 📦 Шаг 1 — Скачать архив с шрифтом

Перейди на официальный GitHub репозиторий и скачай архив:

[![GitHub](https://img.shields.io/badge/GitHub-tonsky%2FFiraCode-181717?style=for-the-badge&logo=github)](https://github.com/tonsky/FiraCode)

На странице [Releases](https://github.com/tonsky/FiraCode/releases) скачай последнюю версию архива с **Nerd Font** патчем (например, `FiraCode.zip`).

> 💡 **Nerd Font** — это версия шрифта, дополненная иконками для терминала (файловые менеджеры, статусные строки и т.д.)

---

## 📂 Шаг 2 — Распаковать архив во временную папку

Распакуем шрифты в `/tmp`, чтобы не засорять папку `Загрузки`:

```bash
unzip ~/Загрузки/FiraCode.zip -d /tmp/firacode
```

После распаковки в папке появятся файлы в форматах `.ttf` и `.otf` для разных начертаний:
- **Light** — тонкое
- **Regular** — обычное
- **Medium** — среднее ⭐ *(рекомендуется)*
- **Bold** — жирное
- **Retina** — для дисплеев с высоким DPI

> 💡 Оригинальный `FiraCode.zip` остаётся в `Загрузки` нетронутым — на случай если понадобится снова.

---

## 🗂️ Шаг 3 — Установить шрифт в систему

Скопируй нужный файл в системную директорию шрифтов:

```bash
sudo cp "/tmp/firacode/Fira Code Medium Nerd Font Complete.ttf" /usr/share/fonts/
```

> 💡 **Совет:** Для установки только для текущего пользователя (без `sudo`) используй:
> ```bash
> mkdir -p ~/.local/share/fonts
> cp "/tmp/firacode/Fira Code Medium Nerd Font Complete.ttf" ~/.local/share/fonts/
> ```

Теперь удалим временную папку:

```bash
rm -rf /tmp/firacode
```

> 💡 Папка `/tmp` и так очищается автоматически при перезагрузке, но лучше убрать вручную сразу.

---

## 🔄 Шаг 4 — Обновить кэш шрифтов

```bash
fc-cache -f -v
```

Флаги:
- `-f` — принудительное обновление (игнорировать кэш)
- `-v` — подробный вывод

Убедись, что в выводе есть строка `fc-cache: succeeded`.

---

## ⚙️ Шаг 5 — Применить шрифт в Konsole (KDE)

Если ты используешь Konsole, можно применить шрифт через `kwriteconfig6`:

```bash
kwriteconfig6 \
  --file konsolerc \
  --group 'General' \
  --key 'font' \
  'Fira Code Medium Nerd Font Complete,12,-1,5,50,0,0,0,0,0'
```

Проверь, что настройка сохранилась:

```bash
kreadconfig6 --file konsolerc --group 'General' --key 'font'
# Ожидаемый вывод:
# Fira Code Medium Nerd Font Complete,12,-1,5,50,0,0,0,0,0
```

> ⚠️ После изменения конфига **перезапусти Konsole**, чтобы изменения вступили в силу.

---

## ✅ Проверка установки

Убедись, что шрифт распознан системой:

```bash
fc-list | grep "Fira Code"
```

Если шрифт установлен — он появится в списке.

---

## 🎨 Настройка в других приложениях

| Приложение | Путь к настройкам |
|---|---|
| **VS Code** | `settings.json` → `"editor.fontFamily": "Fira Code"` |
| **JetBrains IDE** | `File → Settings → Editor → Font` |
| **Konsole** | `Настройки → Профили → Шрифт` или через `kwriteconfig6` |
| **Vim / Neovim** | Настраивается через терминал |

---

## 📚 Полезные ссылки

- 🔗 [Официальный репозиторий Fira Code](https://github.com/tonsky/FiraCode)
- 🔗 [Nerd Fonts — патченые шрифты для терминала](https://www.nerdfonts.com/)
- 🔗 [Alt Linux Wiki](https://www.altlinux.org/)

---

*Инструкция проверена на **Alt Linux** с окружением **KDE Plasma**.*
