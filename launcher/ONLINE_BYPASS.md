# Дополнительная информация о данном ONLINE_BYPASS.md
- Здесь будут опубликованы дополнительные письменные/видео материалы, чтобы не засорять основной README.md

### Prism Launcher (Original)

1. Запустите лаунчер впервые, чтобы он создал свои директории на вашем компьютере.
2. В меню «Папки» найдите «Корневую папку лаунчера» и скопируйте путь до неё.
3. Откройте терминал, командную строку или консоль и выполните команду «echo».

```bash
echo '{"accounts": [{"active":true,"entitlement":{"canPlayMinecraft":true,"ownsMinecraft":true},"type":"MSA"}],"formatVersion":3}' > C:Ваш/Путь/До/Папки/Лаунчера/accounts.json
```

4. Теперь вы можете создавать дополнительные автономные учётные записи.
5. Нельзя удалять все учётные записи, иначе при попытке добавить новую автономную учётную запись лаунчер попросит вас войти с лицензионной учётной записи. Вам придётся повторить действия, описанные в пункте 3.
6. В результате мы изменяем файл accounts.json для игры, используя пиратскую учётную запись.

### Modrinth Launcher (Original)
- **Пожалуйста, внимательно ознакомьтесь с информацией перед использованием терминальной команды.**

1. Запустите лаунчер, чтобы создать директории на вашем компьютере.
2. Рекомендуем закрыть лаунчер перед внесением изменений в файл JSON.
3. Откройте терминал, консоль или командную строку и выполните команду «echo».

- Найдите в тексте формата JSON фразу "username": "YourNickname".
- Это текстовый документ в формате JSON (подробнее можно почитать в интернете). Формат представляет собой пару "ключ": "значение".
- Нас интересует именно значение, его вы должны изменить на свой игровой никнейм. Например, "username": "123_Player_321" или "username": "MC_Pirate".
- Соблюдайте требования к игровым никнеймам, чтобы избежать проблем при дальнейшем взаимодействии с серверами. Неправильный никнейм, например, *&%*@£!@$*(_-%£, может нарушить работу игры. Вы можете использовать цифры от 0 до 9, буквы от a до z и от A до Z, а также символ нижнего подчёркивания (_).

#### Внимание для Modrinth App v0.8.0+
- С версии Modrinth v0.8.0+ учётные записи и другие метаданные хранятся в базе данных SQLite и обрабатываются с помощью SQL-запросов. Для доступа к этим данным можно использовать такие приложения СУБД, как DBeaver или DB Browser for SQLite.

##### Файл базы данных находится в папке ModrinthApp
- Appdata/Roaming на Windows;
- Library/Application Support на MacOS.

```bash
echo '{"users":{"9ce7ca25-dd82-4e94-8066-cb255cf019b2":{"id":"9ce7ca25-dd82-4e94-8066-cb255cf019b2","username":"YourNickname","access_token":"null","refresh_token":"null","expires":"2077-12-12T00:12:34.999999Z"}},"default_user":"9ce7ca25-dd82-4e94-8066-cb255cf019b2"}' > C:Ваш/Путь/До/Папки/Лаунчера/caches/metadata/minecraft_auth.json
```

4. Теперь у вас есть возможность устанавливать и играть в различные сборки Minecraft. Однако в самом лаунчере нельзя изменить игровой ник. Поэтому вы можете либо напрямую редактировать файл minecraft_auth.json, либо каждый раз выполнять определённую команду.
5. В итоге мы изменяем файл minecraft_auth.json, чтобы играть с пиратского аккаунта. Этот файл находится в корневой папке лаунчера в каталоге caches/metadata/minecraft_auth.json.

# Конец документа
__[Вернуться к главному оглавлению](../README.md)__