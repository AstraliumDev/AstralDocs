![AstGuide.png](https://i.imgur.com/vQ8j1NO.png)

# Вступление AstralLinuxGuide (Unix System's)

### Последние изменения в этом репозитории

- [От <\/didirus>](https://github.com/DIDIRUS4) добавлена базовая информация по работе с nft \(nftables - современная
  утилита на замену iptables\).
- [От <\/didirus>](https://github.com/DIDIRUS4) небольшие изменения в дизайне и стиле этого репозитория.

# Дополнительная информация

- [MinecraftRecommendations.md](MinecraftRecommendations.md)
- [VanillaIssues.md](VanillaIssues.md)
- [LegacyInfo.md](LegacyInfo.md)

# Дополнительная информация о данном README.md

### Версия документа v3.3 от 24.10.2023

- Данная статья рассчитана на настройку под Ubuntu / Debian. Основные рекомендации также могут быть применены для ARM
  систем. Однако, если у вас Arch Linux или другие Unix системы - пожалуйста ознакомьтесь с документацией по установке
  пакетов на эту ОС или поищите альтернативные пакеты.


- < NOTICE > Для AUR репозиториев настоятельно рекомендуется проверять исходники скрипта установки. В любом случае это
  рекомендуется делать и для других репозиториев.


- < NOTICE > Некоторые функции могут работать неправильно или вовсе не работать на вашей системе.

### Ссылки на нас
- [Наш Telegram](https://t.me/AstraliumOrg)
- [Наш Discord](https://discord.gg/7XkGYJbtZg)
- [Наш Сайт](https://www.astralium.su)
- [Наш Github](https://github.com/AstraliumMC)

# Основные ссылки на контент

[Получить Adoptium Temurin](https://adoptium.net/) __| Нажмите, чтобы скачать Java |__

[Получить Fabric](https://fabricmc.net/) __| Нажмите, чтобы скачать Fabric |__

[Получить Paper/Folia/Velocity](https://papermc.io/) __| Нажмите, чтобы скачать PaperMC Software |__

# Настройка вашего Linux сервера

### Основное

- Основные рекомендуемые компоненты для вашей системы Linux.
  В основном все команды выполняются от `root` пользователя или с помощью `sudo` *(Если `sudo` отсутствует на вашей
  системе, то установите его через `apt` / `pamac` / `pacman` или альтернативную команду на вашей системе)*

### Обновление пакетов машины

- Для Ubuntu / Debian и форков этих систем -> `sudo apt update -y && sudo apt upgrade -y`


- Для Arch Linux и форков этой системы -> `sudo pamac update --no-confirm && sudo pamac upgrade --no-confirm`

### Полезные утилиты для вашего сервера

- htop - Утилита для мониторинга всех запущенных процессов
- ~atop - Считайте практически идентичным ПО, что и утилита выше
- ~~gtop - Считайте практически идентичным ПО, что и утилита выше
- screen - Важная утилита для создания сессий на вашей серверной машине
- ~zip unzip - Утилита для архивации/разархивации файлов в .zip (рекомендую tarball'ы (.tar.gz))
- ~iptables - Полезная утилита для настройки Netfilter & FireWall вашей системы
- ~ufw - Управление Firewall'ом IPTables, только проще
- ~firewalld - Управление Firewall'ом IPTables, только проще
- nftables - Управление Netfilter & FireWall системы (рекомендую)
- ~iptraf-ng - Мониторинг сети
- nload - Мониторинг сети в виде графика (рекомендую)
- vnstat - Мониторинг сети с выводом скорости и пакетов (рекомендую)
- wireshark - Продвинутое ПО для мониторинга трафика ваших сетевых интерфейсов с возможностью создания дампов .pcap (
  рекомендую)
- smartmontools - Позволяет протестировать оборудование системы (физические накопители HDD, SDD) (рекомендую)
- dnsutils - Управление DNS (Может потребоваться для некоторых утилит)
- neofetch - Утилита для красивого отображения вашей ОС и некоторых параметров
- ~fontconfig - Данный пакет шрифтов может потребоваться для некоторых утилит*

### Удобная установка всех полезных пакетов в одну строку + FIREWALLD (Работает с IPTables)

- `sudo apt update -y && sudo apt upgrade -y && sudo apt install htop screen ufw vnstat zip unzip iptables nload neofetch dnsutils iptraf-ng vnstat fontconfig smartmontools firewalld -y`

### Удобная установка всех полезных пакетов в одну строку + UFW (Работает с IPTables)

- `sudo apt update -y && sudo apt upgrade -y && sudo apt install htop screen ufw vnstat zip unzip iptables nload neofetch dnsutils iptraf-ng vnstat fontconfig smartmontools ufw -y`

### Удобная установка всех полезных пакетов в одну строку только с IPTables

- `sudo apt update -y && sudo apt upgrade -y && sudo apt install htop screen vnstat zip unzip iptables nload neofetch dnsutils iptraf-ng vnstat fontconfig smartmontools -y`

### Удобная установка всех НЕОБХОДИМЫХ (не все пакеты с префиксом '~' включены) пакетов в одну строку с NFTables

- `sudo apt update -y && sudo apt upgrade -y && sudo apt install htop screen vnstat nftables nload neofetch iptraf-ng vnstat smartmontools -y`

# Установка Java на вашу серверную машину

- Вы научитесь легко и просто устанавливать или удалять Java на вашей системе
- Для начала зайдите в SFTP клиент и перейдите в раздел ~/opt (Можно любой, но этот в качестве основы)
- В Linux изначально придумана команда для упаковки архивов и распаковки архивов
- Использовать команду tar можно с использованием следующих параметров:

```
-c | --create — создать архив
-a | --auto-compress — дополнительно сжать архив с компрессором который автоматически определить по расширению архива.
-r | --append — добавить файлы в конец существующего архива
-x | --extract, --get — извлечь файлы из архива
-f | --file — указать имя архива
-t | --list — отобразить список файлов и папок в архиве
-v | --verbose — выводить список обработанных файлов
-u | --update — Обновить архив новыми файлами
-d | --diff, --delete — Проверить начилие архивов, удалить файл из архива
```

- Пример перемещения файлов по системе Linux

```
< ! > НЕ ОБЯЗАТЕЛЬНЫЕ КОМАНДЫ < ! >

• mv /home/others/Test /others2

Также вы можете использовать флаг* -v чтобы увидеть подроную информацию о процессе
~ — тильда, дает понять системе, что это корневой каталог root (~)
Пример: Вы юзер test, то при вводе cd, вы попадете в каталог /home/test/
Т.е ~/others2 и т.д

• mv -v ~/home/others/Test ~/others2

Вы можете также использовать приставку sudo к команде mv

Теперь вы знакомы с командой для перемещения файлов, но рекомендуется еще раз закрепить материал
Попробуйте данные команды на каком-то пустом сервере, либо можете установить WSL2 на вашу систему
Рекомендуемый дистрибутив ОС для создания Проектов (Серверов) — Ubuntu, Debian
```

### Начало процесса установки Java на ваш Linux сервер

- Установка и распаковка архива при помощи "tar" — встроенная утилита упаковки/распаковки архива с файлами в Unix
  системах (Debian / Ubuntu / MacOS точно)

```
Архив уже должен быть установлен / перемещен в выбранную вами директорию
Чтобы установить архив, вы можете использовать в качестве передачи файлов SFTP приложения на выбор
WinSCP / FileZilla / Dolphin (KDE) / Nautilus (GNOME) / Termius, либо же скачать сразу из консоли - wget <url>

• curl https://api.papermc.io/v2/projects/paper/versions/1.20.2/builds/246/downloads/paper-1.20.2-246.jar -o paper.jar

Теперь давайте его распакуем — после распаковки появится папка с нашей Java

• tar -xvf archive.tar.gz

Например архив с Java называется:
Скачиваем к примеру Adoptium JDK Java 17 под x86 / arm (ex: aarch64) платформу (Ubuntu, Debian, Arch, MacOS)

Быстрая установка Adoptium Temurin Java Development Kit 17
• cd /opt && sudo wget https://github.com/adoptium/temurin17-binaries/releases/download/jdk-17.0.6%2B10/OpenJDK17U-jdk_x64_linux_hotspot_17.0.6_10.tar.gz && tar -xvf OpenJDK17U-jdk_x64_linux_hotspot_17.0.6_10.tar.gz && ln -svf /opt/jdk-17.0.6+10/bin/java /usr/bin/java && java -version

< ! > Название архива может быть иное < ! >
Информацию об установке Java ниже можете не применять при вводе команды выше.
Для распаковки архива потребувется ввести всего одну команду (Уже применена в примерной установке выше):

• tar -xvf OpenJDK17U-jdk_x64_linux_hotspot_17.0.6_10.tar.gz

• sudo wget <url>

Из примера выше
Команда для терминала -> curl https://api.papermc.io/v2/projects/paper/versions/1.20.2/builds/246/downloads/paper-1.20.2-246.jar -o paper.jar

В нашем случае это не PaperMC, а Java, поэтому:
• sudo wget https://github.com/adoptium/temurin17-binaries/releases/download/jdk-17.0.6%2B10/OpenJDK17U-jdk_x64_linux_hotspot_17.0.6_10.tar.gz

Также можно использовать утилиту CURL, заместо WGET
• sudo curl <url> -o <output_file.extension>

Все версии Java доступны по этой ссылке: https://github.com/orgs/adoptium/repositories
Мы рекомендуем использовать LTS релизы JDK 17 версии


Если вы сделали всё правильно, то теперь вы получите информацию о вашей Java при вводе данной команды:
• java -version
```

### Создание "Линка" для нашего файла Java в папке с самой Java

- Вы можете подробно изучить про команду ln и ее параметры

```
Линки — тоже самое что ярлык, те кто когда либо имели систему Windows / MacOS 
Могут знать про создание ярлыка при помощи клика ПКМ по файлу
Но у нас ведь нет интерфейса, поэтому будем использовать команду "ln"
*Кстати можно делать линки также через WinSCP — Клиент SFTP, FTP . . .
Создаем ярлык (линк) для нашего исполняемого файла

Выполните команду:
Заместо ... пишем название папки с Java — /opt/.../bin/java

• ln -svf /opt/.../bin/java /usr/bin/java

Если вы все сделали правильно, то вы успешно установили Java на вашу машину
Проверить активную Java
• java -version

Если вам вывело информацию о версии (Обычно это 2-3 строки), то все успешно.
Иначе, проверяйте под какую архитектуру вы скачали JDK архив.
```

### Удаление Java с нашего сервера

```
Мы не будем использовать бесполезные команды по типу: `sudo apt remove *java*`
Для начала перейдем в корень сервера ~
Далее переходим по пути ~/usr/bin
Используем удобный вам способ для поиска файлов — мне было удобно через WinSCP Клиент
Находим файл "Java" — он должен быть единственный в данной директории!
Спокойно без боязни удаляем его — Готово вы удалили активную Java с вашего сервера, однако
Она все еще существует как папку и архив по пути ~/opt
Можно сделать это через команды

• cd /usr/bin && sudo rm java

Проверить наличие активной Java, можно введя команду

• java -version

При успехе, у вас должно вывести ошибку.
```

### Настройка безопасного входа на сервер - Linux

```
В качестве альтернативы простым паролям, мы будем использовать Rsa_Keys с форматом шифрования SHA
Открываем приложение основной терминал системы (Kosnole, Yakuake или любой другой.)

• ssh-keygen # По умолчанию генерирует 2048 Битный ключ

• ssh-keygen -b 4096 # Генерация ключа с мощностью 4096 Бит (Лучше чем 2048)
• ssh-keygen -b 8192 # Генерация ключа с мощностью 8192 Бит (Лучше чем 4096)

Далее внимательно читаем логи, вы уже почти создали пару ключей на вашем ПК ~/users/ВашЮзер/.ssh
Чтобы передать ключ на наш сервер, воспользуемся данной командой (Вам потребуется войти с использованием "старого" пароля)
Однако, мы всегда можем делать это вручную, но можно и через команду ниже:

• cat ~/.ssh/id_rsa.pub | ssh USER@IP "mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys && chmod -R go= ~/.ssh && cat >> ~/.ssh/authorized_keys"

< ! > Подсказка для всех < ! >
Если вы не хотите использовать такой способ авторизации, то установите очень сильный, надежный, ультра мега крутоооой пароль :)
Самое главное не палите своего юзера, ведь только тогда вас не будут брутить, 
Т.к попросту не будут знать пользователя для старта брутфорса. 
В таком случае рекомендую использовать Firewall.
Давайте все же перейдем к нашим RSA ключикам.
Вы можете вручную просто вписать информацию из публичного RSA ключа в '~/.ssh/authorized_keys'
На своем устройстве получите информацию из файлы id_rsa.pub, например cat id_rsa.pub
Впишите данную информацию из файла id_rsa.pub в файл authorized_keys вашего юзера Linux '~/.ssh/authorized_keys'
При использовании данного способа, пожалуйста соблюдайте бдительность, чтобы ничего не сломать в вашей системе

Останется ввести только и вы примените изменения из подсказки выше:
• sudo systemctl restart ssh


... USER@IP ...
Подставьте ваши данные заместо шаблона
USER — Логин, ваш пользователь на серверной машине
IP — Ваш IP от серверной машины


ВНИМАНИЕ! Мы начинаем отключать парольную аутентификацию на сервере, будьте аккуратны
*Автор не несет ответвенности, если вы вдруг сломаете вход на вашу серверную машину,
Обязательно создавайте бэкапы ваших игровых серверов*

Перед этим убедитесь, что у вас установлены пакеты:

• apt install sudo
• apt install nano или apt install vim

sudo — Нужно использовать если у вас основной user != root
nano — Удобный редактор текста в терминате
vim — Редактор немного посложнее, но если освоитесь - будет очень удобно его использовать

Как сохранить файл через nano
CTRL + X , Y (yes), ENTER

Как сохранить файл через vim
После открытия файла
• vim file.txt
Для ввода информации нажмите I (i), у вас появтся надпись снизу слева --INSERT-- или --ВСТАВКА--
После чего заносите любую информацию в файл и нажимаете:
CTRL C, далее пишите :wq
:wq запишет и закроет файл.
:q! просто закроет файл.
Подробнее в документации к vim или nano.

Готово, теперь вы умеете сохранять файлы, но все таки перейдем к отключению парольной авторизации
Вводим команду:

• sudo nano /etc/ssh/sshd_config

Вам нужно найти или написать данную строчку:

PasswordAuthentication no

После сохраняем файл (Мы используем nano в качестве редактора текстовых файлов)
Далее нам необходимо перезагрузить SSH клиент
< ! > Советуем проверить доступ к SSH < ! >
Вернитесь в PowerShell и введите

• ssh USER@IP

• ssh USER@IP -i ./ключ

Если вы пытаетесь зайти через GNU Linux, то используйте команду ниже

• sudo ssh USER@IP -i <key>

... USER@IP
Подставьте ваши данные заместо шаблона
USER — Логин, ваш пользователь на серверной машине
IP — Ваш IP от серверной машины

Далее если все хорошо, перезагружаем ssh

• sudo systemctl restart ssh

Готово, теперь зайти на вашу серверную машину через пароли не получится, используем только ключи авторизации (rsa)

Для удобства входа через пароли можете использовать пакет данных sshpass
```

### Различные команды и бенчмарки, которые возможно вам понадобятся

```
В основном подойдет для мониторинга и наблюдения за жизнедеятельностью вашей серверной машины
Информация по системе

Скорость интернета на вашем сервере (Установка + автозапуск)
• sudo apt install speedtest-cli && speedtest-cli

Через бенчмарк
• sudo wget -qO- bench.sh | bash 

Информация о системе (Установка + автозапуск)
• sudo apt install neofetch && neofetch

Встроенные Linux команды (Примеры)
• lscpu
• lspci
• uname -a

```

# NFTables Мануал по базовому использованию и аргументам

```

• nft -a list ruleset - посмотреть весь список таблиц, цепочек и правил с их хендлами
• nft add table inet/ip/ip6 filter - добавить таблицу (создать) inet (ipv4+ipv6) / ip (ipv4) / ip6 (ipv6) filter (название таблицы)
• nft delete table inet filter - удалить таблицу filter
• nft add chain inet filter Name - создать пустую цепочку (не рекомендуется)
• nft add chain inet filter Name { type filter hook input/output priority 0/1/2... \; policy accept \; } - как пример мы можем создать цепочку правил на вход или выход (input/output соответственно с приоритетами (ниже - главнее) и разрешающей политикой для входа пакетов
• nft add chain inet filter Name { policy drop \; } - изменить политику цепочки на дроп пакетов (опасно, прежде чем добавлять данную политику на input и output необходимо разрешить SSH соединение для дальнейшего управления серверной машинокй, иначе вы потеряете доступ к машине и потребуется вход в рекавери режим или удаленную консоль (например, как у Hetzner Cloud)
• nft add rule inet filter Name iifname "eth0" tcp dport 25565 accept/drop - мы разрешим или дропнем пакеты при подключении к порту 25565 TCP на интерфейсе eth0 

Разрешаем входящие подключения к tcp и udb портам
Разрешим подключаться к серверу по ssh, но только со своего компьютера:

• sudo nft add rule inet filter input iifname eth0 ip saddr 172.28.80.14 tcp dport 22 counter accept
То есть мы добавляем правило (addr rule) в таблицу filter и в цепочку input (inet filter input).
Описываем правило:
Для аргумента входящего интерфейса eth0 (iifname eth0),
Для аргумента адреса источника 172.28.80.14 (ip saddr 172.28.80.14)
Для аргумента tcp порта назначения 22 (tcp dport 22).
Дальше указываем действия:
Чтобы команда nft list ruleset показывала счетчик пакетов, которые проходят правило, добавляем counter,
разрешаем прохождение таких пакетов (accept).
После чего мы можем посмотреть отображение нашего правила или правил с помощью nft list
• nft -a list ruleset
В своих правилах вы можете использовать следующее:

ip saddr <ip-адрес> — исходящий ip адрес;
ip daddr <ip-адрес> — ip адрес назначения (в цепочки input является адресом сервера к которому идет подключение);
tcp sport <порт> — исходящий tcp порт;
tcp dport <порт> — порт tcp назначения (в цепочки input является портом сервера к которому идет подключение);
udp sport <порт> — исходящий udp порт;
udp dport <порт> — порт udp назначения;
iifname <имя интерфейса> — имя входящего интерфейса;
oifname <имя интерфейса> — имя исходящего интерфейса.
В примере разрешаем подключаться к сервисам только из локальной сети:

• sudo nft add rule inet filter input iifname eth0 ip saddr 172.28.80.0/24 tcp dport {80, 443} counter accept
Разрешаем подключаться к loopback интерфейсу
Для того чтобы сервисы внутри системы могли нормально работать, обязательно нужно разрешить все подключения к loopback интерфейсу:

• sudo nft add rule inet filter input iifname lo counter accept
Разрешаем ping сервера
Разрешим пинговать наш сервер, другими словами разрешим входящие icmp запросы:

• sudo nft add rule inet filter input ip saddr 172.28.80.0/24 icmp type echo-request counter accept
Чтобы разрешить icmp нужно указать протокол и тип запроса:

icmp type echo-request — когда кто-то пингует наш сервер ему посылаются запросы (echo-request);
icmp type echo-reply — когда наш сервер кого-то пингует то в ответ он получает ответы (echo-reply).
Меняем политику цепочки input
После того как мы добавили все разрешающие правила в цепочке input, поменяем её политику на drop:

• sudo nft add chain inet filter input '{ policy drop; }'
То есть смена политик выполняется таким образом:

• nft add chain <семейство> <цепочка> <таблица> ‘{ policy accept; }’ — разрешающая политика;
• nft add chain <семейство> <цепочка> <таблица> ‘{ policy drop; }’ — запрещающая политика.

Также рекомендую всегда добавлять следующие условия/аргументы в фаерволл системы
iifname "lo" accept - разрешаем локальный трафик для избежания конфликтов в системе в случае, если у нас policy drop
ct state established,related,new accept - разрешаем коннтрейкинг стейты на уже созданные, новые соединения

В общем говоря, если вы блокируете весь входящий трафик, то вы должны вручную разрешать и настраивать вашу сеть под все ваши сервисы,
поскольку любые блокировки входящего / исходящего трафика для нужного ПО могут повлиять на стабильную работы вашей системы

Сохранение правил и последующая их загрузка системой при ребуте или перезагрузке службы nftables:
• echo '#!/usr/sbin/nft -f' > /etc/nftables.conf && echo 'flush ruleset' >> /etc/nftables.conf && nft list ruleset >> /etc/nftables.conf

Чтобы включить автоматическое сохранение правил и восстановление после запуска вашей системы, пропишите следующую команду
• sudo systemctl enable nftables.service && sudo systemctl start nftables.service && sudo systemctl status nftables.service
```

### SQL Мануал по базовому использованию и простым командам на SQL языке

```
Установка MySQL
• sudo apt install mysql-server

Установка MariaDB (Лучше чем MySQL, является его форком)
• sudo apt install mariadb-server

Вход в саму БД
• sudo mysql

Создать БД
• CREATE DATABASE IF NOT EXISTS DATABASE_NAME;

Удалить БД
• DROP DATABASE IF EXISTS DATABASE_NAME;

Список БД
• SHOW DATABASES;

Создать юзера
• CREATE USER IF NOT EXISTS 'DATABASE_USER'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'DATABASE_USER_NEW_PASSWORD';

Создать юзера для MariaDB
• CREATE USER IF NOT EXISTS 'DATABASE_USER'@'localhost' IDENTIFIED BY 'DATABASE_USER_NEW_PASSWORD';

Изменить пароль юзеру
• ALTER USER 'DATABASE_USER'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'DATABASE_USER_NEW_PASSWORD';

Изменить пароль юзеру для MariaDB
• ALTER USER 'DATABASE_USER'@'localhost' IDENTIFIED BY 'DATABASE_USER_NEW_PASSWORD';

Удалить юзера
• DROP USER IF EXISTS 'DATABASE_USER'@'localhost';

Список юзеров
• SELECT user, host FROM mysql.user;

Выдать права юзеру на определенную БД
• GRANT ALL PRIVILEGES ON database_name.table_name TO 'DATABASE_USER'@'localhost';

Выдать все права юзеру на все БД
• GRANT ALL PRIVILEGES ON *.* TO 'DATABASE_USER'@'localhost';

Список всех прав юзера БД
• SHOW GRANTS FOR 'DATABASE_USER'@'localhost';

Сделать дамп всей БД
• mysqldump -uDATABASE_USER -pDATABASE_USER_PASSWORD --all-databases > DATABASE_CUSTOM_DUMP_NAME.sql

Сделать дамп определенной БД
• mysqldump -uDATABASE_USER -pDATABASE_USER_PASSWORD DATABASE_NAME > DATABASE_CUSTOM_DUMP_NAME.sql

Если вы хотите скопировать ваш дамп БД в другое место
• cp /var/lib/mysql/DATABASE_CUSTOM_DAMP_NAME.sql /home/testuser/
```

### Отключение пароля для `$ sudo {cmd}`

```
Для начала создайте файл (Делать от sudo или root пользователя)
sudo visudo -f /etc/sudoers.d/sudowpass
• sudo nano /etc/sudoers.d/sudowpass

В файл sudowpass нужно вписать следующее:

YourUserHere ALL=(ALL) NOPASSWD:ALL

Или сделаем проще с автоопределением вашего юзера (Делать с правами рута) - $USER ALL=(ALL) NOPASSWD:ALL

• touch /etc/sudoers.d/sudowpass && echo "$USER ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/sudowpass && cat /etc/sudoers.d/sudowpass
```

### Передача файлов по SSH через `scp`

```
• scp USER@IP:/путь_для_файла_на_другой_сервер название_файлика_на_вашем_сервере

Использовать scp с кастомным портом SSH
Для примера передадим файл test.dat на наш сервер Linux
• scp -P 999 root@127.0.0.1:/home/path/to/path/test.dat /home/path/to/but/here/test.dat

У вас запросит пароль, если вы используете ключи, то добавьте -i
```

### Создание пользователя `замена ~ root`

```
Замените '$name' вашим новым кастомным юзером
• adduser $name

Выдача прав на sudoers для нового юзера
usermod -aG sudo $name
• adduser $name sudo

Забрать группу sudoers у $name
• deluser $name sudo

```

### Настройка языковых пакетов на Linux

```
• sudo dpkg-reconfigure locales
Выберите сначала Англ раскладку UTF=8
После выберите пунктом выше C.UTF-8 и нажмите Ok
Вы можете настроить языковые пакеты для себя.
```

# Раздел главных настроек нашего серверного ядра

### Защита вашего сервера

- Не используйте плагины с левых сайтов! Хотя я и использую плагины из других источников, однако я имею определенные
  знания для поиска дыр в них, поэтому использую в итоге плагины с чистым кодом. Вам определенно не рекомендую как
  новичкам (Возможно здесь имеются тоже люди, которые разбираются в этом, но всё таки статья ориентирована на начинающую
  категорию пользователей.

```
Если вы хотите сохранить безопасность вашего сервера и ваших игроков,
то лучше всего скачайте оригинальные плагины,
а если нужно купить, то лучше купите их. Однако, автор также использует общедоступные и приватные ресурсы от BM сообщества администраторов/разработчиков
```

- Закрывайте все ненужные порты, а нужные открывайте!

```
Это конечно не критично, но лучше всего закрыть все или лишние порты и открыть только необходимые. 
После установки UFW / FIREWALLD они автоматически закрываются, 
кроме 22*, однако мы рекомендуем вручную открыть SSH/SFTP порт. Внимательно смотрите стандартные политики, которые ставятся вместе с пакетом при устанвоке
```

# О создании игрового сервера в Minecraft

### Рекомендуемое ПО для запуска сервера

- Если вы планируете разрабатывать модовый сервер, то определенно рекомендую __[Fabric](https://fabricmc.net/)__

> Моды можно найти [на этой платформе](https://modrinth.com/mods)

- Если вы планируете разрабатывать обычный сервер, то определенно рекомендую __[PaperMC](https://papermc.io/)__

> Рекомендуемое ПО Для разработки ___Proxy___ сервера __[Velocity с сайта PaperMC](https://papermc.io/)__
> Плагины можно найти [на этой платформе](https://modrinth.com/plugins)
> Подробнее узнать доп. информацию

- [MinecraftRecommendations.md](MinecraftRecommendations.md)

### VIRTUAL/DEDICATED или PANEL сервер?

- __Автор__ данного поста НЕ ПОДДЕРЖИВАЕТ низкокачественные панельные хосты из-за их серьезных ограничений или
  уязвимостей. Если вы хотите создать
  качественный Проект, то вам определенно стоит присмотреться к использованию выделенных (dedicated) или виртуальных (
  virtual dedicated/private) серверов с полным
  доступом SSH (Secure Shell).

# Об авторе

### Какое ПО используется для разработок игровых проектов (Сервер-сайд)

- Я пользуюсь этим ПО: __[Fabric](https://fabricmc.net/) | [PaperMC](https://papermc.io/)__

### Какое ПО используется для разработок игровых клиентов (Клиент-сайд)

- Я пользуюсь этим ПО: __[Fabric](https://fabricmc.net/)__

### Какое ПО используется для подключения к серверу по SSH, SFTP

- Я пользовался этими ПО на Windows: __[Termius](https://termius.com/) | [WinSCP](https://winscp.net/eng/download.php)__
- Мое любимое ПО для Linux систем: __[Dolphin](https://apps.kde.org/ru/dolphin/) | [Yakuake](https://apps.kde.org/ru/yakuake/) | [Konsole](https://apps.kde.org/ru/konsole/) | [Nautilus](https://apps.gnome.org/Nautilus/)__
- Мое любимое ПО для MacOS: __Finder | Terminal | Terminal | Console__
- Глобальное свободное ПО, которое я бы рекомендовал к использованию: __Termius | FileZilla | DBeaver | VSCode |
  Intellij IDEA | JetBrains ToolBox__

# Disclaimer, as well as dedicated to copyright lovers <3
- Any mention &| exploitation of third-party resources &| products doesn't actually violate the copyrights of the companies &| organizations to which they belong, since all information in writing or software form types can be found in open sources of search engines, for example Yandex & Google.