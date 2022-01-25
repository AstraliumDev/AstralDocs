# Продвинутое создание сервера

![image](https://user-images.githubusercontent.com/77334306/146064955-f7458d87-38c0-40dd-8634-e27dc2a150b5.png)
![image](https://user-images.githubusercontent.com/77334306/146064668-abc41204-a41e-40f8-a098-6a5a992ad5be.png)
![image](https://user-images.githubusercontent.com/77334306/146064892-06b3d01d-02fe-48cb-8618-08536de0ad3f.png)
![image](https://user-images.githubusercontent.com/77334306/146582420-c57493a7-decf-49a8-b248-e29add8f8afe.png)
![image](https://user-images.githubusercontent.com/77334306/146582380-00aee364-fe49-4a47-bd7c-fdbf1a10412a.png)
![image](https://user-images.githubusercontent.com/77334306/146998663-f98e5ea0-cf90-4f39-a34a-1f20a2afe4d0.png)


RU
### Создайте свой личный Minecraft Проект с использованием продвинутой и удобной информации`

```
Версия документа v1.8

* Это не последние изменения данного документа, вскоре здесь будет появляться новая информация *

Некоторые рекомендации из пунктов могут работать некорректно на некоторых системах
За подробной поддержкой обращайтесь в мой дискорд - https://discord.gg/7XkGYJbtZg

Для полноценной настройки рекомендую использовать Adoptium OpenJDK LTS Java

<  !  >  ПОЖАЛУЙСТА ЧИТАЙТЕ ВНИМАТЕЛЬНО И НЕ ПРЕДЪЯВЛЯЙТЕ ПРЕТЕНЗИЙ РАЗРАБОТЧИКУ  <  !  >
```
# Основные ссылки на контент
[OpenJDK](https://adoptium.net/) __| Java |__

[FabricMC](https://fabricmc.net/) __| Fabric |__

[PaperMC](https://papermc.io/) __| Server Software |__

[PurPur](https://purpurmc.org/) __| Server Software |__

[Pufferfish](https://ci.pufferfish.host/) __| Server Software |__

[Velocity](https://velocitypowered.com/) __| Proxy Software |__

# Настройка выделенных и виртуальных серверов
### Базовые компоненты, архивация файлов, настройка безопасности

- Базовые компоненты для вашего сервера
- Все команды выполняются от ~ root пользователя, либо через sudo

### Обновление пакетов машины
```
sudo apt update

sudo apt upgrade
```
### Специально для Linux (CentOS 8)
```
yum

yum update

yum upgrade

dnf

sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

dnf install htop

dnf install screen
```

### Полезные утилиты для вашего сервера
```
sudo apt install htop  -  Утилита для мониторинга всех запущенных процессов (Подобно top, но красивее)

sudo apt install screen  -  Важная утилита для создания сессий на вашей серверной машине

sudo apt install zip unzip  -  Утилита для архивации файлов в .zip

sudo apt install iptables  -  Полезная утилита для настройки IPv4 и IPv6 флагов (Firewall) (Можно управлять портами)

apt install neofetch  -  Утилита для красивого отображения вашей ОС и некоторых параметров
```
- Обычно предустановлена на Ubuntu, но в нашем случае Debian ОС. Выполняет команды от имени root

```
apt install sudo
```

- Если потребуется подтвердить установку, то подтвердите отправив консоли Y (y)



### Специально для Oracle Cloud - откройте порт UDP/TCP 25565
```
sudo apt install firewalld

sudo firewall-cmd --permanent --zone=public --add-port=25565/tcp

sudo firewall-cmd --permanent --zone=public --add-port=25565/udp

sudo firewall-cmd --reload

# Важно! В конфиге server.properties нужно указывать IP: 0.0.0.0
# Если у вас Bungeecord / Velocity, укажите в конфиге Bungeecord / Velocity IP: 0.0.0.0:25565
```
### Установка Java на вашу серверную машину
- Вы научитесь легко и просто устанавливать и удалять Java с вашего сервера
- Для начала зайдите в SFTP клиент и перейдите в раздел ~/opt (Можно любой, но этот в качестве основы)
- В Linux изначально придумана команда для упаковки архивов и распаковки архивов
- Использовать команду tar можно с использованием следующих параметров:
```
# -c | --create — создать архив
# -a | --auto-compress — дополнительно сжать архив с компрессором который автоматически определить по расширению архива.
# -r | --append — добавить файлы в конец существующего архива
# -x | --extract, --get — извлечь файлы из архива
# -f | --file — указать имя архива
# -t | --list — отобразить список файлов и папок в архиве
# -v | --verbose — выводить список обработанных файлов
# -u | --update — Обновить архив новыми файлами
# -d | --diff, --delete — Проверить начилие архивов, удалить файл из архива
```

- Пример перемещения файлов по системе Linux (Не выполняйте эти команды просто так!)
```
# < ! > НЕ ОБЯЗАТЕЛЬНЫЕ КОМАНДЫ < ! >

mv /home/others/Test /others2

# Также вы можете использовать флаг* -v чтобы увидеть подроную информацию о процессе
# ~ — тильда, дает понять системе, что это корневой каталог root (~)
# Т.е ~/others2 и т.д

mv -v ~/home/others/Test ~/others2



# Вы можете также использовать приставку sudo к команде mv

# Теперь вы знакомы с командой для перемещения файлов, но рекомендуется еще раз закрепить материал
# Попробуйте данные команды на каком-то пустом сервере, либо можете установить WSL2 на вашу систему
# Рекомендуемый дистрибутив ОС — Ubuntu,Debian
```

### Начало процесса установки Java на ваш сервер
- Установка и распаковка архива при помощи "tar" — встроенный архиватор в Linux
```
# Архив уже должен быть установлен / перемещен в выбранную вами директорию
# Чтобы установить архив, вы можете использовать в качестве передачи файлов SFTP приложение
# WinSCP, либо же скачать сразу из консоли - wget <url>
# Команду писать без <>

# Теперь давайте его распакуем — после распаковки появится папка с нашей Java
# Выполните команду:

tar xf ИМЯ.tar.gz

# Обычно все пакеты имеют расширение .tar.gz
# Но мы ведь как раз используем "tar" ;)

# Например архив с Java называется:
OpenJDK16U-jdk_x64_linux_hotspot_16.0.1_9.tar.gz

# < ! > Название может быть иное, пожалуйста узнайте это < ! >

# Для распаковки архива потребувется ввести всего одну команду:

tar xf OpenJDK16U-jdk_x64_linux_hotspot_16.0.1_9.tar.gz

# На момент создания статьи последняя Java, которую лично я проверял у себя на Проектах
# Выполните данные команды для скачивания архива:

cd ДИРЕКТОРИЯ

sudo wget ССЫЛКА

... Далее команды распаковки и все действия выше

# ССЫЛКУ брать отсюда - https://adoptium.net/releases.html

# Если все сделано верно, то вы успешно распаковали Java в директорию
```

### Создание "Линка" для нашего файла Java в папке с самой Java
- Вы можете подробно изучить про команду ln и ее параметры
```
# Линки — тоже самое что ярлык, те кто когда либо имели систему Windows / MacOS 
# Могут знать про создание ярлыка при помощи клика ПКМ по файлу
# Но у нас ведь нет интерфейса, поэтому будем использовать команду "ln"
# *Кстати можно делать линки также через WinSCP — Клиент SFTP, FTP . . .
# Создаем ярлык (линк) для нашего исполняемого файла
# Выполните команду:

ln -svf /opt/.../bin/java /usr/bin/java

# Заместо ... пишем название папки с Java — /opt/jdk-16.0.1+9/bin/java

ln -svf /opt/jdk-16.0.1+9/bin/java /usr/bin/java

# Если вы все сделали правильно, то вы успешно установили Java на вашу машину
```

### Удаление Java с нашего сервера
- Многие скажут, что есть команда sudo apt remove *java* и т.д, но это самый простой способ — можно также и через команды 
```
# Для начала перейдем в корень сервера ~
# Далее переходим по пути ~/usr/bin
# Используем удобный вам способ для поиска файлов — мне было удобно через WinSCP Клиент
# Находим файл "Java" — он должен быть единственный в данной директории!
# Спокойно без боязни удаляем его — Готово вы удалили активную Java с вашего сервера, однако
# Она все еще существует как папку и архив по пути ~/opt
# Можно сделать это через команды

cd usr

cd bin

sudo rm java

# Проверить наличие активной Java, можно введя команду

java -version

# При успехе, у вас должно написаться, что Java не найдена
```

### Настройка безопасного входа на сервер - Linux
- В качестве альтернативы простым паролям, мы будем использовать rsa_keys шифрование SHA

- Генерация и установка ключей на сервер
```
# Для Windows:
# Открываем приложение PowerShell, либо другое из того, что у вас может быть

ssh-keygen

ssh-keygen -b 4096 # Генерация более надежного ключа

# Далее внимательно читаем логи, вы уже почти создали пару ключей на вашем ПК ~/users/ВашЮзер/.ssh

# Чтобы передать ключ на наш сервер, воспользуемся данной командой (Вам потребуется войти с использованием "старого" пароля)

cat ~/.ssh/id_rsa.pub | ssh USER@IP "mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys && chmod -R go= ~/.ssh && cat >> ~/.ssh/authorized_keys"

# ... USER@IP ...
# Подставьте ваши данные заместо шаблона
# USER — Логин, ваш пользователь на серверной машине
# IP — Ваш IP от серверной машины


# ВНИМАНИЕ! Мы начинаем отключать парольную аутентификацию на сервере, будьте аккуратны
# *Автор не несет ответвенности, если вы вдруг сломаете вход на вашу серверную машину,
# Обязательно создавайте бэкапы ваших игровых серверов*


# Перед этим убедитесь, что у вас установлены пакеты:

apt install sudo

apt install nano

# sudo — Нужно использовать если у вас основной user != root
# nano — Удобный редактор текста через SSH

# Как сохранить файл через nano

# CTRL + X , Y (yes), ENTER

# Готово, теперь вы умеете сохранять файлы, но все таки перейдем к отключению парольной авторизации
# Вводим команду:

sudo nano /etc/ssh/sshd_config

# Вам нужно найти или написать данную строчку:

PasswordAuthentication no

# После сохраняем файл (Мы используем nano в качестве редактора текстовых файлов)
# Далее нам необходимо перезагрузить SSH клиент
# < ! > Советуем проверить доступ к SSH < ! >
# Вернитесь в PowerShell и введите

ssh USER@IP

ssh USER@IP -i ./ключ

# ... USER@IP
# Подставьте ваши данные заместо шаблона
# USER — Логин, ваш пользователь на серверной машине
# IP — Ваш IP от серверной машины

# Далее если все хорошо, перезагружаем ssh

sudo systemctl restart ssh

# Готово, теперь зайти на вашу серверную машину через пароли не получится, используем только ключи авторизации (rsa)
```

### Различные команды и бенчи, которые возможно вам понадобятся
- В основном подойдет для мониторинга и наблюдения за жизнедеятельностью вашей серверной машины
```
# Информация по системе

# Через бенчмарк

sudo wget -qO- bench.sh | bash 

# Через неофетч (Удобнее чем 1-ый вариант, однако данный вариант не сможет показать скорость)

apt install neofetch

neofetch
```

### IPTables - Закрытие порта SSH, SFTP (22)
- На самом деле не рекомендую делать такое с динамическим IP, иначе вы рискуете потерять доступ к вашей серверной машине
```
# Базовые настройки IPTables | Запрет пинга на ваш дедик | Запрет входа с других айпи по SSH (только ваш)

iptables -A INPUT -s IP/32 -p icmp -j DROP

# Разрешить свой айпи для входа через SSH,SFTP - ПУНКТ ДЕЛАТЬ ПЕРВЫМ ИЗ ВСЕХ!

iptables -A INPUT -p tcp --dport 22 -s YourIP -j ACCEPT

# Дропнуть порт 22 (aka SSH, SFTP). < ! > ДЕЛАТЬ ПОСЛЕ РАЗРЕШЕНИЯ < ! >

iptables -A INPUT -p tcp --dport 22 -j DROP

# Установка

apt-get install iptables-persistent

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

### "WinRar" - Известный архиватор, но для Linux
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

### MySQL - Для Linux
```
# Установка
sudo apt install mysql-server

# Вход в саму БД
sudo mysql

# Создать БД

CREATE DATABASE IF NOT EXISTS DATABASE_NAME;

# Удалить БД

DROP DATABASE IF EXISTS DATABASE_NAME;

# Список БД

SHOW DATABASES;

# Создать юзера

CREATE USER IF NOT EXISTS 'DATABASE_USER'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'DATABASE_USER_NEW_PASSWORD';

# Изменить пароль юзеру

ALTER USER 'DATABASE_USER'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'DATABASE_USER_NEW_PASSWORD';

# Удалить юзера

DROP USER IF EXISTS 'DATABASE_USER'@'localhost';

# Список юзеров

SELECT user, host FROM mysql.user;

# Выдать права юзеру на определенную БД

GRANT ALL PRIVILEGES ON database_name.table_name TO 'DATABASE_USER'@'localhost';

# Выдать все права юзеру на все БД

GRANT ALL PRIVILEGES ON *.* TO 'DATABASE_USER'@'localhost';

# Список всех прав юзера БД

SHOW GRANTS FOR 'DATABASE_USER'@'localhost';

# Сделать дамп всей БД

mysqldump -uDATABASE_USER -pDATABASE_USER_PASSWORD --all-databases > DATABASE_CUSTOM_DUMP_NAME.sql

# Сделать дамп определенной БД

mysqldump -uDATABASE_USER -pDATABASE_USER_PASSWORD DATABASE_NAME > DATABASE_CUSTOM_DUMP_NAME.sql

# Если вы хотите скопировать ваш дамп БД в другое место

cp /var/lib/mysql/DATABASE_CUSTOM_DAMP_NAME.sql /home/testuser/
```

### Отключение пароля для `$ sudo {cmd}`
```
# Для начала создайте файл (делать от рута ~)

sudo visudo -f /etc/sudoers.d/sudowpass

# В файлик вписываем то что ниже

# You can replace $user
$user ALL=(ALL) NOPASSWD:ALL

```
### Передача файлов по SSH через `scp`
```
scp USER@IP:/путь_для_файла_на_другой_сервер название_файлика_на_вашем_сервере

# У вас запросит пароль, если вы используете ключи, то добавьте -i
```

# О создании игрового сервера в Minecraft
### Рекомендуемое ПО для запуска сервера
- Если вы планируете разрабатывать модовый сервер, то определенно рекомендую __[Fabric](https://fabricmc.net/)__
> Моды можно найти [здесь](https://modrinth.com/mods) или [здесь](https://www.curseforge.com/minecraft/mc-mods)
- Если вы планируете разрабатывать обычный сервер, то определенно рекомендую __[PaperMC](https://papermc.io/) | [PurPur](https://purpurmc.org/)__
> Рекомендуемое ПО Для разработки ___Proxy___ сервера __[Velocity](https://velocitypowered.com/) | [Velocity с сайта PaperMC](https://papermc.io/)__

### VDS/DEDICATED или PANEL HOSTING?
- __Автор__ данного поста не поддерживает панельные хосты из-за их ограничений пользования. Если вы хотите создать качественный Проект, то пожалуйста придерживайтесь использовать выделенных или виртуальных серверо с полным доступом к __SSH__ протоколу

# Об авторе
### Какое ПО используется для разработок игровых проектов (Сервер-сайд)
- Я пользуюсь этими ПО: __[Fabric](https://fabricmc.net/) | [PaperMC](https://papermc.io/) | [PurPur](https://purpurmc.org/) | [Pufferfish](https://ci.pufferfish.host/) | [Velocity](https://velocitypowered.com/)__
> __Pufferfish Links:__ _[Docs](https://docs.pufferfish.host/) | [Github](https://github.com/pufferfish-gg/Pufferfish)_
### Какое ПО используется для разработок игровых клиентов (Клиент-сайд)
- Я пользуюсь этим ПО: __[Fabric](https://fabricmc.net/)__
### Какое ПО используется для подключения к серверу по SSH, SFTP
- Я пользуюсь этими ПО: [Termius (SSH Полностью бесплано, SFTP Пробная версия, потом платно](https://termius.com/) [WinSCP (SFTP Полностью бесплатно)](https://winscp.net/eng/download.php)
### На чем создаю Проекты (ПК/Ноут, OS)
- Для многих это покажется странно, но я разрабатываю все свои Проекты на ноутбуке 
- Работаю в данный момент на Windows 11 (Планирую создать образ для Linux)


EN
# Advanced server creation

![image](https://user-images.githubusercontent.com/77334306/146064955-f7458d87-38c0-40dd-8634-e27dc2a150b5.png)
![image](https://user-images.githubusercontent.com/77334306/146064668-abc41204-a41e-40f8-a098-6a5a992ad5be.png)
![image](https://user-images.githubusercontent.com/77334306/146064892-06b3d01d-02fe-48cb-8618-08536de0ad3f.png)
![image](https://user-images.githubusercontent.com/77334306/146582420-c57493a7-decf-49a8-b248-e29add8f8afe.png)
![image](https://user-images.githubusercontent.com/77334306/146582380-00aee364-fe49-4a47-bd7c-fdbf1a10412a.png)
![image](https://user-images.githubusercontent.com/77334306/146998663-f98e5ea0-cf90-4f39-a34a-1f20a2afe4d0.png)



### Create your personal Minecraft Project using advanced and user-friendly information`

```
Document version v1.8

* These are not the latest changes to this document, new information will appear here soon *

Some recommendations from the points may not work correctly on some systems.
For detailed support, please contact my discord - https://discord.gg/7XkGYJbtZg

For full customization, I recommend using Adoptium OpenJDK LTS Java

<! > PLEASE READ CAREFULLY AND DO NOT MAKE CLAIMS TO THE DEVELOPER < ! >
```
# Main content links
[OpenJDK](https://adoptium.net/) __| Java |__

[FabricMC](https://fabricmc.net/) __| Fabric |__

[PaperMC](https://papermc.io/) __| Server Software |__

[PurPur](https://purpurmc.org/) __| Server Software |__

[Pufferfish](https://ci.pufferfish.host/) __| Server Software |__

[Velocity](https://velocitypowered.com/) __| Proxy Software |__

# Setting up dedicated and virtual servers
### Basic components, file archiving, security setup

- Basic components for your server
- All commands are executed as ~ root user, or via sudo

### Update machine packages
```
sudo apt update

sudo apt upgrade
```
### Linux specific (CentOS 8)
```
yum

yum update

yum upgrade

dnf

sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

dnf install htop

dnf installscreen
```

### Useful utilities for your server
```
sudo apt install htop - A utility to monitor all running processes (Similar to top, but prettier)

sudo apt install screen - An essential tool for creating sessions on your server machine

sudo apt install zip unzip - Utility to archive files to .zip

sudo apt install iptables - Useful utility to configure IPv4 and IPv6 flags (Firewall) (Can manage ports)

apt install neofetch - A utility to nicely display your OS and some options
```
- Usually pre-installed on Ubuntu, but in our case Debian OS. Executes commands as root

```
apt install sudo
```

- If you need to confirm the installation, then confirm by sending the console Y (y)



### Oracle Cloud specific - open UDP/TCP port 25565
```
sudo apt install firewalld

sudo firewall-cmd --permanent --zone=public --add-port=25565/tcp

sudo firewall-cmd --permanent --zone=public --add-port=25565/udp

sudo firewall-cmd --reload

# Important! In the server.properties config, you need to specify IP: 0.0.0.0
# If you have Bungeecord / Velocity, specify in the Bungeecord / Velocity IP config: 0.0.0.0:25565
```
### Install Java on your server machine
- You will learn how to easily install and remove Java from your server
- To get started, go to the SFTP client and go to the ~ / opt section (You can use any, but this one as a basis)
- Linux originally came up with a command to pack archives and unpack archives
- You can use the tar command with the following options:
```
# -c | --create - create an archive
# -a | --auto-compress - additionally compress the archive with a compressor that is automatically determined by the archive extension.
# -r | --append - append files to the end of an existing archive
#-x | --extract, --get - extract files from archive
# -f | --file - specify the name of the archive
# -t | --list - display a list of files and folders in the archive
# -v | --verbose - list processed files
# -u | --update - Update archive with new files
# -d | --diff, --delete — Check if archives exist, delete file from archive
```

- An example of moving files around a Linux system (Don't just run these commands!)
```
# < ! > NOT REQUIRED COMMANDS < ! >

mv /home/others/Test /others2

# You can also use the * -v flag to see detailed information about the process
# ~ - tilde, tells the system that this is the root directory (~)
# i.e. ~/others2 etc

mv -v ~/home/others/Test ~/others2



# You can also use the sudo prefix to the mv command

# Now you are familiar with the command to move files, but it is recommended to check the material again
# Try these commands on some empty server, or you can install WSL2 on your system
# Recommended OS distribution - Ubuntu, Debian
```

### Begin the Java installation process on your server
- Installing and unpacking the archive using "tar" - built-in archiver in Linux
```
# The archive should already be installed / moved to the directory you selected
# To install the archive, you can use the SFTP file transfer application
# WinSCP, or download directly from the console - wget <url>
# Write the command without <>

# Now let's unpack it - after unpacking, a folder with our Java will appear
# Run the command:

tar xf NAME.tar.gz

# Usually all packages have a .tar.gz extension
# But we're just using "tar" ;)

# For example, an archive with Java is called:
OpenJDK16U-jdk_x64_linux_hotspot_16.0.1_9.tar.gz

# < ! > The name may be different, please find out < ! >

# To unpack the archive, you need to enter only one command:

tar xf OpenJDK16U-jdk_x64_linux_hotspot_16.0.1_9.tar.gz

# At the time of writing the last Java, which I personally tested on my Projects
# Run these commands to download the archive:

cd DIRECTORY

sudo wget LINK

... Further unpacking commands and all the actions above

# LINK to take from here - https://adoptium.net/releases.html

# If everything is correct, then you have successfully unpacked Java into the directory
```

### Creating a "Link" for our Java file in the Java folder
- You can learn in detail about the ln command and its parameters
```
# Links are the same as a shortcut, those who have ever had a Windows / MacOS system 
# May know about creating a shortcut by right-clicking on a file
# But we don't have an interface, so we'll use the "ln" command
# *By the way, you can also make links through WinSCP - SFTP Client, FTP. . .
# Create a shortcut (link) for our executable file
# Run the command:

ln -svf /opt/.../bin/java /usr/bin/java

# Instead ... write the name of the folder with Java - /opt/jdk-16.0.1+9/bin/java

ln -svf /opt/jdk-16.0.1+9/bin/java /usr/bin/java

# If you did everything right, then you have successfully installed Java on your machine
```

### Removing Java from our server
- Many will say that there is a sudo apt remove *java* command, etc., but this is the easiest way - you can also use commands 
```
# First, let's go to the root of the server ~
# Next, go to ~/usr/bin
# We use a convenient way for you to search for files - it was convenient for me through the WinSCP Client
# Find the file "Java" - it should be the only one in this directory!
# Feel free to remove it without fear - Done, you have removed active Java from your server, however
# It still exists as a folder and archive in ~/opt
# Can be done via commands

cd usr

cd bin

sudo rm java

# You can check if Java is active by entering the command

java-version

# If successful, you should get a message that Java was not found
```

### Configuring secure server login - Linux
- As an alternative to simple passwords, we will use rsa_keys SHA encryption

- Generation and installation of keys on the server
```
# For Windows:
# Open the PowerShell application, or whatever you may have

ssh-keygen

ssh-keygen -b 4096 # Generate a stronger key

# Next, carefully read the logs, you have almost created a key pair on your PC ~/users/YourUser/.ssh

# To transfer the key to our server, use this command (You will need to log in using the "old" password)

cat ~/.ssh/id_rsa.pub | ssh USER@IP "mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys && chmod -R go= ~/.ssh && cat >> ~/.ssh/authorized_keys"

# ... USER@IP ...
# Substitute your data for the pattern
# USER - Login, your user on the server machine
# IP - Your IP from the server machine


# ATTENTION! We are starting to disable password authentication on the server, be careful
# *The author is not responsible if you suddenly break the login to your server machine,
# Be sure to back up your game servers*


# Before doing this, make sure you have the packages installed:

apt install sudo

apt install nano

# sudo - Should be used if your main user != root
# nano - Convenient text editor via SSH

# How to save a file via nano

# CTRL + X , Y (yes), ENTER

# Done, now you know how to save files, but still let's move on to disabling password authorization
# Enter the command:

sudo nano /etc/ssh/sshd_config

# You need to find or write this line:

PasswordAuthentication no

# After we save the file (We use nano as a text file editor)
# Next we need to restart the SSH client
# < ! > We recommend checking SSH access < ! >
# Return to PowerShell and type

ssh USER@IP

ssh USER@IP -i ./key

# ... USER@IP
# Substitute your data for the pattern
# USER - Login, your user on the server machine
# IP - Your IP from the server machine

# Next, if everything is fine, restart ssh

sudo systemctl restart ssh

# Done, now you won't be able to access your server machine through passwords, we use only authorization keys (rsa)
```

### Various commands and benches you may need
- Mainly suitable for monitoring and monitoring the life of your server machine
```
# System Information

# Via benchmark

sudo wget -qO-bench.sh | bash

# Through neofetch (More convenient than the 1st option, but this option will not be able to show the speed)

apt install neofetch

neofetch
```

### IPTables - Close SSH port, SFTP (22)
- I really don't recommend doing this with a dynamic IP, otherwise you risk losing access to your server machine
```
# Basic IPTables settings | Ping ban on your dedicated server | Deny login from other IPs via SSH (only yours)

iptables -A INPUT -s IP/32 -p icmp -j DROP

# Allow your ip to login via SSH, SFTP - THE ITEM TO DO FIRST OF ALL!

iptables -A INPUT -p tcp --dport 22 -s YourIP -j ACCEPT

# Drop port 22 (aka SSH, SFTP). <! > DO AFTER PERMISSION < ! >

iptables -A INPUT -p tcp --dport 22 -j DROP

# Installation

apt-get install iptables-persistent

# The iptables rules need to be created, then run the following command

service iptables-persistent start

# Since the utility is a daemon, it cannot be stopped, but you can clear the list of rules

service iptables-persistent flush

# Update rules if persistent was already set

dpkg-reconfigure iptables-persistent
```

### IPTables - Closing ports on multiple server machines

- Here you will learn in detail how to close ports easily and quickly
```
# Imagine that we have two VDS / VPS servers
# The first server branded X - This will be our Proxy server (Filter of various bots, packets (TCP))
# The second server branded Y - This will be our Survival server (Basic survival)
# On the X server, write the following commands in the given order, as given (From top to bottom)

iptables -A INPUT -s <IP Y> -j ACCEPT
iptables -A INPUT -s 127.0.0.1 -j ACCEPT

# On server Y, write the following commands in the given order, as given (From top to bottom)

iptables -A INPUT -p tcp -s <IP X> --dport <PORT Y (Survival)> -j ACCEPT
iptables -A INPUT -p tcp --dport <PORT Y (Survival)> -j DROP

# After manipulations on each VDS / VPS, you need to enter this command

apt install iptables-persistent

# If you already have it installed, then just update the rules using the command

dpkg-reconfigure iptables-persistent


# If you want, you can also see the list of your iptables rules on each of the virtual machines

iptables --list

# Find out the numbers of all rules

iptables -L --line-numbers

# You can delete rules in the following way

iptables -D INPUT NUMBER
```

### "WinRar" - Well-known archiver, but for Linux
```
# Installation
apt install zip unzip

# Where you need to create an archive - I have a folder / home
cd home

# Archiving a folder/file | Can be located in any path (You specify the specific path to the folder / file that you want to archive)
zip -r NAME.zip /home/BungeeCord

# For example in my case
# /home - server folder directory
# /BungeeCord - the bungee folder itself, you can use any for example: Survival, Anarchy, SkyBlock.

zip -r surv.zip /home/Survival

# If there is a SkyBlock folder with the server, then enter this command
# You can specify any server, you can also store the server along the path /servers/BungeeCord
# It is not necessary to use the /home partition for servers!

zip -r sb.zip /home/SkyBlock

# Or use the built-in tar
```

### MySQL - For Linux
```
# Installation
sudo apt install mysql server

# Login to the database itself
sudo mysql

# Create database

CREATE DATABASE IF NOT EXISTS DATABASE_NAME;

# Delete database

DROP DATABASE IF EXISTS DATABASE_NAME;

# Database list

SHOW DATABASES;

# Create user

CREATE USER IF NOT EXISTS 'DATABASE_USER'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'DATABASE_USER_NEW_PASSWORD';

# Change user password

ALTER USER 'DATABASE_USER'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'DATABASE_USER_NEW_PASSWORD';

# Delete user

DROP USER IF EXISTS 'DATABASE_USER'@'localhost';

# List of users

SELECT user, host FROM mysql.user;

# Give the user rights to a specific database

GRANT ALL PRIVILEGES ON database_name.table_name TO 'DATABASE_USER'@'localhost';

# Give all rights to the user on all databases

GRANT ALL PRIVILEGES ON *.* TO 'DATABASE_USER'@'localhost';

# List of all database user rights

SHOW GRANTS FOR 'DATABASE_USER'@'localhost';

# Dump the entire database

mysqldump -uDATABASE_USER -pDATABASE_USER_PASSWORD --all-databases > DATABASE_CUSTOM_DUMP_NAME.sql

# Dump a specific database

mysqldump -uDATABASE_USER -pDATABASE_USER_PASSWORD DATABASE_NAME > DATABASE_CUSTOM_DUMP_NAME.sql

# If you want to copy your database dump to another location

cp /var/lib/mysql/DATABASE_CUSTOM_DAMP_NAME.sql /home/testuser/
```

### Disable password for `$ sudo {cmd}`
```
# First create a file (do as root ~)

sudo visudo -f /etc/sudoers.d/sudowpass

# Enter the following into the file

# You can replace $user
$user ALL=(ALL) NOPASSWD:ALL

```
### SSH file transfer via `scp`
```
scp USER@IP :/path_for_file_to_other_server name_of_file_on_your_server

# You will be prompted for a password, if you are using keys then add -i
```

# About creating a game server in Minecraft
### Recommended software to run the server
- If you are planning to develop a modded server, then I definitely recommend __[Fabric](https://fabricmc.net/)__
> Mods can be found [here](https://modrinth.com/mods) or [here](https://www.curseforge.com/minecraft/mc-mods)
- If you are planning to develop a regular server, then I definitely recommend __[PaperMC](https://papermc.io/) | [PurPur](https://purpurmc.org/)__
> Recommended software For developing ___Proxy___ server __[Velocity](https://velocitypowered.com/) | [Velocity from PaperMC](https://papermc.io/)__

### VDS/DEDICATED or PANEL HOSTING?
- __Author__ of this post does not support panel hosts due to their usage restrictions. If you want to create a quality project, then please stick to using dedicated or virtual servers with full access to the __SSH__ protocol

# About the author
### What software is used to develop game projects (Server-side)
- I use these software: __[Fabric](https://fabricmc.net/) | [PaperMC](https://papermc.io/) | [PurPur](https://purpurmc.org/) | [Pufferfish](https://ci.pufferfish.host/) | [Velocity](https://velocitypowered.com/)__
> __Pufferfish Links:__ _[Docs](https://docs.pufferfish.host/) | [Github](https://github.com/pufferfish-gg/Pufferfish)_
### What software is used to develop game clients (Client side)
- I use this software: __[Fabric](https://fabricmc.net/)__
### What software is used to connect to the server via SSH, SFTP
- I use these softwares: [Termius (SSH Completely Free, SFTP Trial, then paid](https://termius.com/) [WinSCP (SFTP Completely Free)](https://winscp.net/eng/download .php)
### On what I create Projects (PC/Laptop, OS)
- It may seem strange to many, but I develop all my Projects on a laptop 
- I am currently working on Windows 11 (I plan to create an image for Linux)
