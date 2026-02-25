# 🐳 Docker Engine & Docker Compose на ALT Linux

![ALT Linux](https://img.shields.io/badge/OS-ALT%20Linux-blue?style=for-the-badge&logo=linux&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-29.2.1-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Docker Compose](https://img.shields.io/badge/Docker%20Compose-5.1.0-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.12.7-3776AB?style=for-the-badge&logo=python&logoColor=white)

---

## 📋 Содержание

- [Установка Docker Engine](#-установка-docker-engine)
- [Установка Docker Compose](#-установка-docker-compose)
- [Настройка и запуск](#-настройка-и-запуск)
- [Удаление Docker Compose](#-удаление-docker-compose)
- [Удаление Docker Engine](#-удаление-docker-engine)

---

## 🔧 Установка Docker Engine

Обновите пакеты и установите Docker Engine одной командой:

```bash
sudo apt-get update && sudo apt-get install docker-engine
```

Проверьте установленную версию:

```bash
docker --version
```

> ✅ Ожидаемый вывод: `Docker version 29.2.1, build a5c7197`

---

## 📦 Установка Docker Compose

### Шаг 1 — Проверьте наличие Python и pip

![Python](https://img.shields.io/badge/Требуется-Python%203-3776AB?style=flat-square&logo=python&logoColor=white)
![pip](https://img.shields.io/badge/Требуется-pip-3775A9?style=flat-square&logo=pypi&logoColor=white)

```bash
python3 --version
```

```bash
pip3 --version
```

Если `pip` не установлен:

```bash
sudo apt-get install -y python3-module-pip
```

### Шаг 2 — Получите номер последней версии

```bash
LATEST=$(curl -s https://api.github.com/repos/docker/compose/releases/latest \
  | grep '"tag_name"' \
  | sed -E 's/.*"v([^"]+)".*/\1/')
echo $LATEST
```

### Шаг 3 — Скачайте бинарник с GitHub

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/v${LATEST}/docker-compose-linux-x86_64" \
  -o /usr/local/bin/docker-compose
```

### Шаг 4 — Сделайте файл исполняемым

```bash
sudo chmod +x /usr/local/bin/docker-compose
```

### Шаг 5 — Проверьте установку

```bash
docker-compose --version
```

> ✅ Ожидаемый вывод: `Docker Compose version v5.1.0`

---

## ⚙️ Настройка и запуск

### Управление службой Docker

| Команда | Описание |
|--------|----------|
| `sudo service docker status` | Просмотр состояния службы |
| `sudo service docker start` | Запуск службы |
| `sudo service docker stop` | Остановка службы |
| `sudo systemctl enable docker` | Добавление в автозагрузку |

### Запуск службы и добавление в автозагрузку

```bash
sudo service docker start
sudo systemctl enable docker
```

### Добавление пользователя в группу docker

> 💡 Это позволит запускать Docker **без `sudo`**

```bash
sudo usermod -aG docker $USER
```

Перезапустите сессию для применения изменений:

```bash
exec su - $USER
```

Проверьте, что пользователь добавлен в группу `docker`:

```bash
groups
```

> ✅ В списке должно присутствовать слово `docker`

### Проверка работоспособности

```bash
docker run hello-world
```

Если всё установлено корректно, вы увидите:

```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

### Полезные команды

| Команда | Описание |
|--------|----------|
| `docker ps` | Список запущенных контейнеров |
| `docker ps -a` | Список всех контейнеров (включая остановленные) |
| `docker images` | Список скачанных образов |
| `docker rm <имя>` | Удалить контейнер |
| `docker rmi <образ>` | Удалить образ |

---

## 🗑️ Удаление Docker Compose

### Шаг 1 — Удалите бинарный файл

```bash
sudo rm /usr/local/bin/docker-compose
```

### Шаг 2 — Убедитесь, что Docker Compose удалён

```bash
docker-compose --version
```

> ✅ Если команда возвращает ошибку — удаление прошло успешно.

### Шаг 3 — Перезапустите систему

```bash
sudo reboot
```

---

## 🗑️ Удаление Docker Engine

> ⚠️ **Внимание:** Перед удалением Docker Engine рекомендуется сначала удалить Docker Compose и остановить все контейнеры.

### Шаг 1 — Остановите все запущенные контейнеры

```bash
docker stop $(docker ps -q)
```

### Шаг 2 — Остановите и отключите службу Docker

```bash
sudo service docker stop
sudo systemctl disable docker
```

### Шаг 3 — Удалите пакет Docker Engine

```bash
sudo apt-get remove --purge docker-engine
```

### Шаг 4 — Удалите все образы, контейнеры и тома (опционально)

> ⚠️ Это удалит **все данные Docker** — образы, контейнеры, тома и сети.

```bash
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

### Шаг 5 — Удалите пользователя из группы docker

```bash
sudo gpasswd -d $USER docker
```

### Шаг 6 — Убедитесь, что Docker удалён

```bash
docker --version
```

> ✅ Если команда возвращает ошибку — удаление прошло успешно.

### Шаг 7 — Перезапустите систему

```bash
sudo reboot
```

---

## 📊 Итоговый стек

| Компонент | Версия | Статус |
|-----------|--------|--------|
| 🐳 Docker Engine | 29.2.1 | ✅ Установлен |
| 🔧 Docker Compose | 5.1.0 | ✅ Установлен |
| 🐍 Python | 3.12.7 | ✅ Установлен |
| 📦 pip | 25.1.1 | ✅ Установлен |

---

![Maintained](https://img.shields.io/badge/Maintained-yes-green?style=flat-square)
![ALT Linux](https://img.shields.io/badge/ALT%20Workstation%20K-11.2%20Nemorosa-orange?style=flat-square&logo=linux)
