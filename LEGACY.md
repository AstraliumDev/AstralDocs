# Дополнительная информация • LEGACY.md
- Здесь будут опубликованы неактуальные команды/утилиты, чтобы не засорять главную страницу документации.

### Неактуальные пакеты
```
- ~ufw - Управление Firewall'ом IPTables, только проще
- ~firewalld - Управление Firewall'ом IPTables, только проще
- ~zip unzip - Утилита для архивации/разархивации файлов в .zip (рекомендую tarball'ы (.tar.gz))
- ~iptables - Полезная утилита для настройки Netfilter & FireWall вашей системы
- ~iptraf-ng - Мониторинг сети
- ~atop - Считайте практически идентичным ПО, что и утилита выше
- ~~gtop - Считайте практически идентичным ПО, что и утилита выше
- ~fontconfig - Данный пакет шрифтов может потребоваться для некоторых утилит*
```

### Специально для CentOS 8 (Не поддерживается автором статьи)
```
yum

yum update

yum upgrade

dnf

sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

dnf install htop

dnf install screen
```

### Oracle Cloud установка под Minecraft
```
# Использование с UFW утилитой
sudo ufw enable # <- По умолчанию он выключен, поэтому его следует включить.
sudo ufw allow 25565 comment "Данный порт открыт по UDP/TCP протоколам для всех входящих соединений"
sudo ufw reload # <- На всякий случай.

# Использование с FIREWALLD утилитой
sudo apt install firewalld # <- Установка пакета не требуется, если вы установили его в начале этой статьи.
sudo firewall-cmd --permanent --zone=public --add-port=25565/tcp
sudo firewall-cmd --permanent --zone=public --add-port=25565/udp
sudo firewall-cmd --reload # <- Обычно он всегда требует перезагрузки для того, чтобы новые правила вступили в силу.

# < ! > Обратите особое внимание во избежание утраты доступа к вашей Linux машине < ! >
# По умолчанию FIREWALLD и UFW утилиты закрывают все порты, конечно в них имеются исключения для 22/tcp порта,
# Однако в любом случае рекомендуется вручную открыть OpenSSH порт.
# Использование в UFW и FIREWALLD:

# sudo ufw allow 22/tcp comment "Порт для использования удалённого подключения к данной машине по SSH протоколу"
# sudo firewall-cmd --permanent --zone=public --add-port=25565/tcp
# sudo firewall-cmd --reload # <- Обычно он всегда требует перезагрузки для того, чтобы новые правила вступили в силу.

```

### "WinRar" - Известный архиватор, но для Linux (Лучше использовать tar)
```
# Установка
apt install zip unzip

# Там где нужно будет создать архив - у меня это папку /home
cd home

# Архивирование папки/файла | Можно находиться в любом пути (Вы указываете конкретно путь до папки/файла , который нужно заархивировать)
zip -r NAME.zip /home/BungeeCord

# Для примера в моем случае
# /home - дирректория папки с сервером
# /BungeeCord - сама папка с банджей, можно любую например: Survival, Anarchy, SkyBlock.

zip -r surv.zip /home/Survival

# Если имеется SkyBlock папка с сервером, то введите эту команду
# Указывать можно любой сервер, также вы можете например хранить сервер по пути /servers/BungeeCord
# Не обязательно использовать /home раздел для серверов!

zip -r sb.zip /home/SkyBlock

# Либо используйте встроенный tar
```

### IPTables (UFW/FIREWALLD) - Закрытие порта SSH, SFTP (22) + ICMP DROP

- На самом деле не рекомендую делать такое с динамическим IP, иначе вы рискуете потерять доступ к вашей серверной машине

```
# Быстродействие (Без закрытия SSH порта):
# sudo apt install ufw && sudo ufw allow 22/tcp && sudo nano /etc/ufw/before.rules
# Для before.rules:

# ok icmp codes for INPUT
-A ufw-before-input -p icmp --icmp-type destination-unreachable -j ACCEPT
-A ufw-before-input -p icmp --icmp-type time-exceeded -j ACCEPT
-A ufw-before-input -p icmp --icmp-type parameter-problem -j ACCEPT
-A ufw-before-input -p icmp --icmp-type echo-request -j ACCEPT

# ИЗМЕНИТЬ НА СЛЕДУЮЩЕЕ ЗНАЧЕНИЯ ufw-before-input
# ok icmp codes for INPUT
-A ufw-before-input -p icmp --icmp-type destination-unreachable -j DROP
-A ufw-before-input -p icmp --icmp-type time-exceeded -j DROP
-A ufw-before-input -p icmp --icmp-type parameter-problem -j DROP
-A ufw-before-input -p icmp --icmp-type echo-request -j DROP

# Сохраняем конфигурацию через наш nano редактор (CTRL X + Y + ENTER)
# Перезагружаем UFW

sudo ufw reload

# Теперь все пинги блокируются извне

# Ниже представлена информация из документации v2.0 (Прошлая)

# Базовые настройки IPTables | Запрет пинга на ваш дедик | Запрет входа с других айпи по SSH (только ваш)

iptables -A INPUT -s IP/32 -p icmp -j DROP

# Или через FirewallD

sudo firewall-cmd --add-icmp-block=echo-request --permanent

# Разрешить свой айпи для входа через SSH,SFTP - ПУНКТ ДЕЛАТЬ ПЕРВЫМ ИЗ ВСЕХ!

iptables -A INPUT -p tcp --dport 22 -s YourIP -j ACCEPT

# Дропнуть порт 22 (aka SSH, SFTP). < ! > ДЕЛАТЬ ПОСЛЕ РАЗРЕШЕНИЯ < ! >

iptables -A INPUT -p tcp --dport 22 -j DROP

# Установка

apt-get install iptables-persistent
# Можно обойтись без этого и просто настроить восстановление правил IPTables через crontab :)

# Правила iptables необходимо создать, затем выполнить следующую команду

service iptables-persistent start

# Поскольку утилита является демоном — прекратить ее работу нельзя, однако можно очистить список правил

service iptables-persistent flush

# Обновить правила, если persistent уже был установлен

dpkg-reconfigure iptables-persistent
```

### IPTables - Закрытие портов на нескольких серверных машинах

- Здесь вы подробно узнаете как легко и быстро закрыть порты

```
# Представим что у нас есть два сервера VDS / VPS
# Первый сервер под маркой X - Это у нас будет Proxy сервер (Фильтр различных ботов, пакетов (TCP))
# Второй сервер под маркой Y - Это у нас будет Survival сервер (Основное выживание)
# На сервере X пропишите следующие команды в данном порядке, как они даны (Свреху вниз)

iptables -A INPUT -s <IP Y> -j ACCEPT
iptables -A INPUT -s 127.0.0.1 -j ACCEPT

# На сервере Y пропишите следующие команды в данном порядке, как они даны (Сверху вниз)

iptables -A INPUT -p tcp -s <IP X> --dport <PORT Y (Survival)> -j ACCEPT
iptables -A INPUT -p tcp --dport <PORT Y (Survival)> -j DROP

# После манипуляций на каждом VDS / VPS нужно ввести данную команду

apt install iptables-persistent

# Если у вас он уже был установлен, то просто обновите правила используя команду

dpkg-reconfigure iptables-persistent


# Если хотите можете также ознакомиться со списком ваших правил iptables на каждой из виртуальных машин

iptables --list

# Узнать номера всех правил

iptables -L --line-numbers

# Удалять правила можно следующим способом

iptables -D INPUT ЧИСЛО
```


# Конец документа
__[Вернуться к главному оглавлению](README.md)__