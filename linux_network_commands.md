# 🌐 Linux Network Commands

![ALT Linux](https://img.shields.io/badge/OS-ALT%20Linux-1A6EBF?style=for-the-badge&logo=linux&logoColor=white)
![Shell](https://img.shields.io/badge/Shell-Bash-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)
![Network](https://img.shields.io/badge/Topic-Networking-0078D4?style=for-the-badge&logo=cisco&logoColor=white)
![RPM](https://img.shields.io/badge/Пакеты-RPM%20%2B%20APT-red?style=for-the-badge)

> 📖 Полный справочник сетевых команд Linux — от базовых до продвинутых.

---

## 📋 Содержание

- [🌐 Linux Network Commands](#-linux-network-commands)
  - [📋 Содержание](#-содержание)
  - [🔍 Интерфейсы и адреса](#-интерфейсы-и-адреса)
  - [🗺️ Маршрутизация](#️-маршрутизация)
  - [📡 Проверка связи](#-проверка-связи)
  - [🌍 DNS](#-dns)
  - [🔌 Порты и соединения](#-порты-и-соединения)
  - [⬇️ Загрузка файлов](#️-загрузка-файлов)
  - [🎛️ Управление интерфейсами](#️-управление-интерфейсами)
  - [🔥 Firewall](#-firewall)
  - [🕵️ Анализ трафика](#️-анализ-трафика)
  - [🔐 SSH и туннели](#-ssh-и-туннели)
  - [📊 Пропускная способность](#-пропускная-способность)
  - [📶 Беспроводные сети](#-беспроводные-сети)
  - [🖧 Управление сетью](#-управление-сетью)
  - [🔒 VPN](#-vpn)
  - [🛠️ Разное](#️-разное)
  - [⚡ Шпаргалка: современное vs устаревшее](#-шпаргалка-современное-vs-устаревшее)

---

## 🔍 Интерфейсы и адреса

![modern](https://img.shields.io/badge/Утилита-iproute2-blue?style=flat-square)
![legacy](https://img.shields.io/badge/Устаревшее-net--tools-lightgrey?style=flat-square)

```bash
ip a                        # Показать все интерфейсы и IP-адреса
ip a show eth0              # Информация только по интерфейсу eth0
ifconfig                    # Устаревший аналог ip a (пакет net-tools)
```

---

## 🗺️ Маршрутизация

![modern](https://img.shields.io/badge/Утилита-iproute2-blue?style=flat-square)

```bash
ip route                    # Таблица маршрутизации
ip route show               # То же самое
route -n                    # Устаревший аналог (без резолвинга имён)
ip route add 192.168.2.0/24 via 192.168.1.1   # Добавить маршрут
ip route del 192.168.2.0/24                    # Удалить маршрут
```

---

## 📡 Проверка связи

![ping](https://img.shields.io/badge/Утилита-ping%20%2F%20traceroute-orange?style=flat-square)

```bash
ping 8.8.8.8                # Проверить доступность хоста (Ctrl+C — стоп)
ping -c 4 google.com        # Отправить ровно 4 пакета
traceroute google.com       # Показать путь пакета до хоста
mtr google.com              # Интерактивный traceroute в реальном времени
fping 192.168.1.1 192.168.1.2  # Ping нескольких хостов одновременно
arping 192.168.1.1          # Ping через ARP (Layer 2, в обход фаервола)
hping3 -S 192.168.1.1 -p 80 # Низкоуровневый TCP SYN на порт 80
```

---

## 🌍 DNS

![dns](https://img.shields.io/badge/Утилита-dig%20%2F%20nslookup-9cf?style=flat-square)

```bash
nslookup google.com         # Узнать IP по доменному имени
dig google.com              # Подробный DNS-запрос
dig google.com +short       # Только IP-адрес
dig @8.8.8.8 google.com     # DNS-запрос к конкретному серверу
dig google.com MX           # Запросить MX-записи (почта)
dig google.com NS           # Запросить NS-записи (серверы имён)
dig -x 8.8.8.8              # Обратный DNS: IP → домен
host google.com             # Простой DNS-резолвинг
whois google.com            # Информация о домене/IP
dnstracer google.com        # Трассировка DNS по всей цепочке
cat /etc/resolv.conf        # Посмотреть настройки DNS-серверов
```

---

## 🔌 Порты и соединения

![ss](https://img.shields.io/badge/Утилита-ss%20%2F%20netstat-blueviolet?style=flat-square)

```bash
ss -tuln                    # Все открытые TCP/UDP порты (listening)
ss -tulnp                   # То же + имя процесса на каждом порту
ss -s                       # Краткая статистика по сокетам
ss -o state established     # Только установленные соединения
ss -tp                      # TCP соединения + процессы
ss -4                       # Только IPv4
ss -6                       # Только IPv6
netstat -tuln               # Устаревший аналог ss
lsof -i :80                 # Какой процесс использует порт 80
conntrack -L                # Таблица отслеживания соединений (NAT)
```

---

## ⬇️ Загрузка файлов

![curl](https://img.shields.io/badge/Утилита-curl%20%2F%20wget-yellow?style=flat-square)

```bash
curl https://example.com            # Получить содержимое URL
curl -O https://example.com/file    # Скачать файл
curl -I https://google.com          # Показать только HTTP-заголовки
curl -v https://google.com          # Подробный вывод с заголовками
curl ifconfig.me                    # Узнать внешний IP
wget https://example.com/file       # Скачать файл
wget -c https://example.com/file    # Продолжить прерванную загрузку
```

---

## 🎛️ Управление интерфейсами

![ip](https://img.shields.io/badge/Утилита-ip%20link-blue?style=flat-square)
![requires_root](https://img.shields.io/badge/Права-sudo-red?style=flat-square)

```bash
ip link set eth0 up                    # Включить интерфейс
ip link set eth0 down                  # Выключить интерфейс
ip addr add 192.168.1.10/24 dev eth0   # Назначить IP-адрес интерфейсу
ip addr del 192.168.1.10/24 dev eth0   # Удалить IP-адрес
ethtool eth0                           # Информация о физическом интерфейсе
ethtool -S eth0                        # Статистика сетевой карты
ip -s link                             # Статистика по всем интерфейсам
```

---

## 🔥 Firewall

![iptables](https://img.shields.io/badge/Утилита-iptables%20%2F%20ufw-red?style=flat-square)
![requires_root](https://img.shields.io/badge/Права-sudo-red?style=flat-square)

```bash
iptables -L                 # Показать все правила фаервола
iptables -L -n -v           # Подробно, без резолвинга имён
ufw status                  # Статус UFW (Ubuntu)
ufw allow 22                # Разрешить порт 22 (SSH)
ufw deny 23                 # Запретить порт 23
ufw enable                  # Включить UFW
ufw disable                 # Выключить UFW
```

---

## 🕵️ Анализ трафика

![tcpdump](https://img.shields.io/badge/Утилита-tcpdump%20%2F%20tshark-darkgreen?style=flat-square)
![requires_root](https://img.shields.io/badge/Права-sudo-red?style=flat-square)

```bash
tcpdump -i eth0                 # Захват пакетов на интерфейсе eth0
tcpdump -i eth0 port 80         # Только трафик на порту 80
tcpdump -i any -w file.pcap     # Записать трафик в файл (для Wireshark)
tshark -i eth0                  # Консольный Wireshark
tshark -i eth0 -Y "http"        # Фильтр только HTTP трафика
ngrep -d eth0 "GET" tcp         # Искать строку в сетевых пакетах
tcpflow -i eth0 port 80         # Восстановить TCP-потоки из трафика
nethogs                         # Трафик по процессам в реальном времени
iftop -i eth0                   # Трафик по соединениям в реальном времени
nload eth0                      # Монитор входящего/исходящего трафика
bmon                            # Графический монитор трафика в терминале
```

---

## 🔐 SSH и туннели

![ssh](https://img.shields.io/badge/Утилита-OpenSSH-black?style=flat-square&logo=openssh)

```bash
ssh user@192.168.1.1               # Подключиться к хосту по SSH
ssh -p 2222 user@host              # Подключиться на нестандартный порт
scp file.txt user@host:/tmp        # Скопировать файл на удалённый хост
ssh-keygen                         # Сгенерировать SSH-ключ
ssh-copy-id user@host              # Скопировать публичный ключ на сервер
ssh -L 8080:localhost:80 user@host # Локальный SSH-туннель
ssh -R 8080:localhost:80 user@host # Обратный SSH-туннель
ssh -D 1080 user@host              # SOCKS5-прокси через SSH

# Утилита netcat (nc)
nc -l 4444                         # Открыть порт и слушать
nc 192.168.1.1 4444                # Подключиться к порту

# Утилита socat
socat TCP-LISTEN:8080,fork TCP:host:80  # Перенаправить порт
```

---

## 📊 Пропускная способность

![iperf](https://img.shields.io/badge/Утилита-iperf3-brightgreen?style=flat-square)

```bash
iperf3 -s                   # Запустить сервер для теста скорости
iperf3 -c 192.168.1.1       # Замерить скорость до сервера
speedtest-cli               # Тест скорости интернета
```

---

## 📶 Беспроводные сети

![wifi](https://img.shields.io/badge/Утилита-iw%20%2F%20iwconfig-blue?style=flat-square)

```bash
iw dev                      # Список беспроводных интерфейсов
iw wlan0 scan               # Сканировать Wi-Fi сети
iw wlan0 link               # Статус подключения Wi-Fi
iwconfig                    # Информация о беспроводных интерфейсах
iwlist wlan0 scan           # Сканировать Wi-Fi сети (устаревшее)
wavemon                     # Интерактивный монитор Wi-Fi сигнала
airmon-ng start wlan0       # Режим мониторинга для анализа трафика
```

---

## 🖧 Управление сетью

![etcnet](https://img.shields.io/badge/ALT%20Linux-etcnet-1A6EBF?style=flat-square)
![nmcli](https://img.shields.io/badge/Утилита-NetworkManager-teal?style=flat-square)

> ⚠️ **ALT Linux** на серверах использует собственную систему управления сетью — **etcnet**.
> Конфигурация хранится в `/etc/net/ifaces/<интерфейс>/`.
> NetworkManager типичен для десктопных редакций.

```bash
# --- etcnet (ALT Linux, серверные редакции) ---
ls /etc/net/ifaces/                     # Список настроенных интерфейсов
cat /etc/net/ifaces/eth0/ipv4address    # IP-адрес интерфейса eth0
cat /etc/net/ifaces/eth0/options        # Параметры интерфейса
service network restart                 # Перезапустить сеть (etcnet)
ifup eth0                               # Поднять интерфейс
ifdown eth0                             # Опустить интерфейс

# --- NetworkManager (ALT Linux, десктоп) ---
nmcli device status         # Статус всех сетевых устройств
nmcli connection show       # Список сохранённых подключений
nmcli connection up "Wi-Fi" # Активировать подключение по имени
nmtui                       # Удобный текстовый интерфейс NetworkManager

# --- Общее ---
hostname                    # Имя текущего хоста
hostname -i                 # IP-адрес (⚠️ флаг -I не работает на ALT Linux)
ip -4 addr show scope global | grep inet  # Все внешние IPv4-адреса
ip neigh                    # ARP-таблица (устройства в локальной сети)
arp -a                      # Устаревший аналог ip neigh
```

---

## 🔒 VPN

![vpn](https://img.shields.io/badge/Утилита-OpenVPN%20%2F%20WireGuard-purple?style=flat-square)

```bash
openvpn --config file.ovpn  # Подключиться по OpenVPN
wg show                     # Статус WireGuard интерфейсов
wg-quick up wg0             # Поднять WireGuard туннель
wg-quick down wg0           # Опустить WireGuard туннель
```

---

## 🛠️ Разное

```bash
nmap 192.168.1.1            # Сканировать порты хоста
nmap 192.168.1.0/24         # Сканировать всю подсеть
nmap -sV 192.168.1.1        # Определить версии сервисов
nmap -O 192.168.1.1         # Определить ОС хоста

openssl s_client -connect google.com:443  # Проверить SSL-сертификат

/proc/net/dev               # Низкоуровневая статистика из ядра Linux
```

---

## ⚡ Шпаргалка: современное vs устаревшее

| Устаревшее | Современное | Пакет |
|---|---|---|
| `ifconfig` | `ip a` | iproute2 |
| `route -n` | `ip route` | iproute2 |
| `netstat` | `ss` | iproute2 |
| `arp -a` | `ip neigh` | iproute2 |
| `iwconfig` | `iw` | iw |

---

> 💡 **Установка пакетов в ALT Linux:**
> ALT Linux использует **APT с RPM-пакетами** и репозиторий **Sisyphus**.
> ```bash
> sudo apt-get update                  # Обновить список пакетов
> sudo apt-get install <название>      # Установить пакет
> sudo apt-get remove <название>       # Удалить пакет
> apt-cache search <ключевое слово>    # Найти пакет в репозитории
> rpm -qa | grep <название>            # Проверить, установлен ли пакет
> ```
> **Сетевые пакеты для установки:**
> ```bash
> sudo apt-get install nmap            # Сканер портов
> sudo apt-get install traceroute      # Трассировка маршрута
> sudo apt-get install tcpdump         # Захват трафика
> sudo apt-get install iperf3          # Тест пропускной способности
> sudo apt-get install bind-utils      # dig, nslookup, host
> sudo apt-get install mtr             # Интерактивный traceroute
> sudo apt-get install net-tools       # ifconfig, netstat, route (устаревшие)
> sudo apt-get install etcnet          # Система управления сетью ALT Linux
> ```

---

![made with](https://img.shields.io/badge/Made%20with-❤️%20%26%20Markdown-ff69b4?style=for-the-badge)
