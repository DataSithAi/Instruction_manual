# 🖥️ Настройка современного терминала на ALT Linux

[![ZSH](https://img.shields.io/badge/ZSH-оболочка-1A2C34?style=for-the-badge&logo=gnu-bash&logoColor=white)](https://www.zsh.org/)
[![Oh My Zsh](https://img.shields.io/badge/Oh%20My%20Zsh-фреймворк-C5D928?style=for-the-badge&logo=zsh&logoColor=black)](https://ohmyz.sh/)
[![Powerlevel10k](https://img.shields.io/badge/Powerlevel10k-тема-blueviolet?style=for-the-badge)](https://github.com/romkatv/powerlevel10k)
[![Fira Code](https://img.shields.io/badge/Fira%20Code-Nerd%20Font-ff69b4?style=for-the-badge&logo=fontforge&logoColor=white)](https://github.com/tonsky/FiraCode)
[![eza](https://img.shields.io/badge/eza-замена%20ls-orange?style=for-the-badge)](https://github.com/eza-community/eza)
[![Alt Linux](https://img.shields.io/badge/ALT%20Workstation%20K-11.2-blue?style=for-the-badge&logo=linux&logoColor=white)](https://www.altlinux.org/)

> Полный стек для красивого, быстрого и удобного терминала.
> Все пакеты устанавливаются из **официальных репозиториев ALT p11** или официальных GitHub-репозиториев.

---

## 📋 Что будет установлено

| Инструмент | Назначение | Источник |
|---|---|---|
| **Fira Code Nerd Font** | Шрифт с лигатурами и иконками | GitHub / Nerd Fonts |
| **ZSH** | Современная оболочка вместо bash | apt-get |
| **Oh My Zsh** | Фреймворк для управления конфигурацией ZSH | GitHub |
| **Powerlevel10k** | Красивый и быстрый промпт с иконками | GitHub |
| **zsh-autosuggestions** | Серые подсказки команд из истории | GitHub |
| **zsh-syntax-highlighting** | Подсветка: зелёный = OK, красный = ошибка | GitHub |
| **eza** | Современная замена `ls` с иконками | apt-get |
| **bat** | Замена `cat` с подсветкой синтаксиса | apt-get |
| **duf** | Замена `df` — красивый вывод дисков | apt-get |
| **btop** | Замена `top` — мониторинг системы | apt-get |
| **ncdu** | Замена `du` — анализ дискового пространства | apt-get |
| **fd** | Замена `find` — быстрый поиск файлов | apt-get |
| **tealdeer** | Замена `man` — краткие примеры команд | apt-get |

---

## 🔤 Шаг 1 — Установить шрифт Fira Code Nerd Font

[![Fira Code GitHub](https://img.shields.io/badge/GitHub-tonsky%2FFiraCode-181717?style=for-the-badge&logo=github)](https://github.com/tonsky/FiraCode)
[![Nerd Fonts](https://img.shields.io/badge/Nerd%20Fonts-nerdfonts.com-green?style=for-the-badge)](https://www.nerdfonts.com/)
[![License](https://img.shields.io/badge/License-OFL--1.1-green?style=for-the-badge)](https://github.com/tonsky/FiraCode/blob/master/LICENSE)

> 💡 Шрифт нужно установить **до** настройки Powerlevel10k — иначе иконки в терминале будут отображаться некорректно.

Перейди на страницу [Releases](https://github.com/tonsky/FiraCode/releases) и скачай архив с **Nerd Font** патчем (`FiraCode.zip`).

> 💡 **Nerd Font** — версия шрифта, дополненная иконками для терминала.

### Распаковать во временную папку

```bash
unzip ~/Загрузки/FiraCode.zip -d /tmp/firacode
```

В архиве несколько начертаний:

| Начертание | Описание |
|---|---|
| **Light** | Тонкое |
| **Regular** | Обычное |
| **Medium** | Среднее ⭐ *(рекомендуется)* |
| **Bold** | Жирное |
| **Retina** | Для дисплеев с высоким DPI |

### Установить шрифт в систему

```bash
sudo cp "/tmp/firacode/Fira Code Medium Nerd Font Complete.ttf" /usr/share/fonts/
```

> 💡 **Для установки только для текущего пользователя** (без `sudo`):
> ```bash
> mkdir -p ~/.local/share/fonts
> cp "/tmp/firacode/Fira Code Medium Nerd Font Complete.ttf" ~/.local/share/fonts/
> ```

### Очистить временную папку

```bash
rm -rf /tmp/firacode
```

> 💡 `/tmp` очищается при перезагрузке автоматически, но лучше убрать сразу. Оригинальный `FiraCode.zip` остаётся в `Загрузки` нетронутым.

### Обновить кэш шрифтов

```bash
fc-cache -f -v
```

Убедись, что в конце вывода есть строка `fc-cache: succeeded`.

### Применить шрифт в Konsole (KDE)

```bash
kwriteconfig6 \
  --file konsolerc \
  --group 'General' \
  --key 'font' \
  'Fira Code Medium Nerd Font Complete,12,-1,5,50,0,0,0,0,0'
```

Проверь что настройка сохранилась:

```bash
kreadconfig6 --file konsolerc --group 'General' --key 'font'
# Ожидаемый вывод:
# Fira Code Medium Nerd Font Complete,12,-1,5,50,0,0,0,0,0
```

> ⚠️ **Перезапусти Konsole**, чтобы изменения вступили в силу.

### Проверить установку шрифта

```bash
fc-list | grep "Fira Code"
```

Ожидаемый вывод:
```
/usr/share/fonts/Fira Code Medium Nerd Font Complete.ttf: FiraCode Nerd Font:style=Medium,Regular
```

> ⚠️ **Важно:** системное имя шрифта — `FiraCode Nerd Font` (без пробела между Fira и Code). Именно это имя указывается в настройках приложений.

| Приложение | Настройка |
|---|---|
| **VS Code** | `settings.json` → `"editor.fontFamily": "FiraCode Nerd Font"` |
| **JetBrains IDE** | `File → Settings → Editor → Font` → `FiraCode Nerd Font` |
| **Konsole** | `kwriteconfig6` |
| **Vim / Neovim** | Настраивается через терминал, имя `FiraCode Nerd Font` |

---

## 🐚 Шаг 2 — Установить ZSH

[![ZSH](https://img.shields.io/badge/GitHub-zsh--users%2Fzsh-181717?style=flat-square&logo=github)](https://github.com/zsh-users/zsh)

```bash
sudo apt-get update
sudo apt-get install zsh
```

Проверь версию:

```bash
zsh --version
```

### Сделать ZSH оболочкой по умолчанию

> ⚠️ В ALT Linux обычный `chsh` требует прав — используй `sudo`:

```bash
sudo chsh -s $(which zsh) $USER
```

Проверь что изменение применилось:

```bash
grep $USER /etc/passwd
```

В конце строки должно быть `/usr/bin/zsh`:
```
executor:x:1000:1000::/home/executor:/usr/bin/zsh
```

> ⚠️ **Выйди из сессии и войди заново** — ZSH станет оболочкой по умолчанию.

### Первый запуск ZSH

При первом входе появится мастер `zsh-newuser-install`. Нажми **`0`** — это создаст пустой `~/.zshrc` (Oh My Zsh всё равно перезапишет его на следующем шаге).

---

## 🎨 Шаг 3 — Установить Oh My Zsh

[![Oh My Zsh GitHub](https://img.shields.io/badge/GitHub-ohmyzsh%2Fohmyzsh-181717?style=flat-square&logo=github)](https://github.com/ohmyzsh/ohmyzsh)

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Если `curl` не установлен — через `wget`:

```bash
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

> 💡 Установщик спросит про перезапись `~/.zshrc` — отвечай **`y`**. Старый файл сохранится как `~/.zshrc.pre-oh-my-zsh`.

---

## ⚡ Шаг 4 — Установить Powerlevel10k

[![Powerlevel10k GitHub](https://img.shields.io/badge/GitHub-romkatv%2Fpowerlevel10k-181717?style=flat-square&logo=github)](https://github.com/romkatv/powerlevel10k)

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git \
  ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

### Подключить тему

Заменяем тему одной командой:

```bash
sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="powerlevel10k\/powerlevel10k"/' ~/.zshrc
```

Проверь:

```bash
grep ZSH_THEME ~/.zshrc
# Ожидаемый вывод:
# ZSH_THEME="powerlevel10k/powerlevel10k"
```

Применяем:

```bash
source ~/.zshrc
```

> 🎛️ Автоматически запустится **интерактивный мастер настройки** — отвечай на вопросы про стиль промпта, иконки и цвета.
> Чтобы перезапустить мастер в любой момент:
> ```bash
> p10k configure
> ```

---

## 🔌 Шаг 5 — Установить плагины Oh My Zsh

[![zsh-autosuggestions](https://img.shields.io/badge/GitHub-zsh--autosuggestions-181717?style=flat-square&logo=github)](https://github.com/zsh-users/zsh-autosuggestions)
[![zsh-syntax-highlighting](https://img.shields.io/badge/GitHub-zsh--syntax--highlighting-181717?style=flat-square&logo=github)](https://github.com/zsh-users/zsh-syntax-highlighting)

```bash
# zsh-autosuggestions — подсказки из истории
git clone https://github.com/zsh-users/zsh-autosuggestions \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# zsh-syntax-highlighting — подсветка команд
git clone https://github.com/zsh-users/zsh-syntax-highlighting \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

### Подключить плагины

```bash
sed -i 's/plugins=(git)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting)/' ~/.zshrc
```

Проверь:

```bash
grep "^plugins" ~/.zshrc
# Ожидаемый вывод:
# plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```

Применяем:

```bash
source ~/.zshrc
```

> 💡 **Как работают плагины:**
> - `zsh-autosuggestions` — серый текст после курсора подсказывает команду из истории. Нажми `→` чтобы принять.
> - `zsh-syntax-highlighting` — команда подсвечивается **зелёным** если существует, **красным** если нет.

---

## 📦 Шаг 6 — Установить современные утилиты

Все пакеты есть в официальном репозитории ALT p11:

```bash
sudo apt-get install eza bat duf btop ncdu fd tealdeer
```

> ⚠️ **Важно про названия пакетов в ALT:**
> - `fd` — называется `fd` (не `fd-find` как в Debian/Ubuntu)
> - `tldr` — называется `tealdeer` (команда в терминале всё равно `tldr`)
> - `gping` — отсутствует в p11, есть только в Sisyphus

### Добавить алиасы в ~/.zshrc

```bash
cat >> ~/.zshrc << 'EOF'

# ===== Современные аналоги утилит =====

# Замена ls на eza
if [ -x "$(command -v eza)" ]; then
    alias ls="eza --long --all --group --icons --git"
fi

# Замена cat на bat
if [ -x "$(command -v bat)" ]; then
    alias cat='bat'
fi
export BAT_THEME="Visual Studio Dark+"

# Замена df на duf
if [ -x "$(command -v duf)" ]; then
    alias df='duf'
fi

# Замена find на fd
if [ -x "$(command -v fd)" ]; then
    alias find='fd'
fi

# Замена man на tldr
if [ -x "$(command -v tldr)" ]; then
    alias man='tldr'
fi

# Замена top на btop
if [ -x "$(command -v btop)" ]; then
    alias top='btop'
fi

# Замена du на ncdu
if [ -x "$(command -v ncdu)" ]; then
    alias du='ncdu'
fi

# Замена ping на gping
if [ -x "$(command -v gping)" ]; then
    alias ping='gping'
fi
EOF
```

Применяем:

```bash
source ~/.zshrc
```

> 💡 Все алиасы обёрнуты в проверку `if [ -x "$(command -v ...)" ]` — они активируются только если утилита установлена.

---

## ✅ Шаг 7 — Проверка всего стека

```bash
eza --version && bat --version && duf --version && btop --version && \
ncdu --version && fd --version && tldr --version
```

Ожидаемый вывод:
```
eza - A modern, maintained replacement for ls v0.23.4
bat 0.25.0
duf (built from source)
btop version: 1.2.13
ncdu 1.19
fd 10.3.0
tealdeer 1.6.1
```

---

## 🔀 Переключение между оболочками

Если захочешь вернуться на bash:

```bash
sudo chsh -s $(which bash) $USER
```

Вернуться обратно на ZSH:

```bash
sudo chsh -s $(which zsh) $USER
```

Проверить текущую оболочку по умолчанию:

```bash
grep $USER /etc/passwd
```

> 💡 После смены оболочки нужно **выйти из сессии и войти заново**.
> Все настройки ZSH, Oh My Zsh и плагины никуда не денутся — они просто не будут загружаться пока активен bash.

---

## 🔄 Обновление в будущем

```bash
# Обновить Oh My Zsh
omz update

# Обновить Powerlevel10k
git -C ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k pull

# Обновить плагины
git -C ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions pull
git -C ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting pull

# Обновить утилиты через apt-get
sudo apt-get install --only-upgrade eza bat duf btop ncdu fd tealdeer
```

---

## 📚 Официальные ссылки

- 🔗 [Fira Code — GitHub](https://github.com/tonsky/FiraCode)
- 🔗 [Nerd Fonts](https://www.nerdfonts.com/)
- 🔗 [ZSH — официальный сайт](https://www.zsh.org/)
- 🔗 [Oh My Zsh — GitHub](https://github.com/ohmyzsh/ohmyzsh)
- 🔗 [Powerlevel10k — GitHub](https://github.com/romkatv/powerlevel10k)
- 🔗 [eza — GitHub](https://github.com/eza-community/eza)
- 🔗 [bat — GitHub](https://github.com/sharkdp/bat)
- 🔗 [btop — GitHub](https://github.com/aristocratos/btop)
- 🔗 [ALT Linux пакеты](https://packages.altlinux.org/)

---

*Инструкция проверена на **ALT Workstation K 11.2 (Nemorosa)** x86_64 с окружением **KDE Plasma**.*
