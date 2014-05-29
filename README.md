## Кокаин для разработчиков

Данное руководство является результатом исследования исходного кода кокаина. Я постараюсь описать основное назначение компонент кокаина и принципы их взаимодействия так, как я это понимаю, изучая код.

Кокаин активно использует библиотеку [libboost](http://www.boost.org/), поэтому неплохо было бы ознакомиться с её описанием.

Для организации асинхронного ввода/вывода используется библиотека [libev](http://software.schmorp.de/pkg/libev.html). Неплохое описание [здесь](http://highloadblog.ru/articles/16.html).

Дерево исходного кода:

|папка/файл|описание|
|----------|--------|
|`[+] gateways`||
|`----[c] adhoc.cpp`|Простая маршрутизация событий методом перебора нод|
|`[+] isolates`||
|`----[+] process`||
|`--------[c] archive.cpp`||
|`--------[c] spooler.cpp`||
|`----[c] process.cpp`||
|`[+] runtime`||
|`----[c] pid_file.cpp`|Вспомогательный класс для работы с pid-файлом|
|`----[c] runtime.cpp`|[Запуск cocaine-runtime](runtime.md)|
|`[+] services`||
|`----[+] node`|[Основная логика для работы с приложениями](node)|
|`--------[c] app.cpp`|[Непосредственно приложение](node/app.md)|
|`--------[c] engine.cpp`|[Исполнитель приложений (engine)](node/engine.md)|
|`--------[c] manifest.cpp`|Класс для чтения манифеста|
|`--------[c] profile.cpp`|Класс для чтения профиля|
|`--------[c] queue.cpp`||
|`--------[c] session.cpp`|Сессия взаимодействия приложения с облаком|
|`--------[c] slave.cpp`|[Кокаиновый раб](node/slave.md)|
|`----[c] counter.cpp`|Сервис Counter|
|`----[c] logging.cpp`|Сервис Logging. Логи|
|`----[c] node.cpp`|[Сервис Node](node.md)|
|`----[c] storage.cpp`|Сервис Storage. Работа с хранилищем|
|`[+] storages`||
|`----[c] files.cpp`|Простое файловое хранилище|
|`[c] actor.cpp`||
|`[c] api.cpp`||
|`[c] chamber.cpp`||
|`[c] context.cpp`|[Контекст исполнения приложений](context.md)|
|`[c] crypto.cpp`||
|`[c] dispatch.cpp`||
|`[c] dynamic.cpp`||
|`[c] engine.cpp`||
|`[c] essentials.cpp`||
|`[c] group.cpp`||
|`[c] locator.cpp`|[Сервис Locator](locator.md)|
|`[c] logging.cpp`||
|`[c] raft.cpp`||
|`[c] repository.cpp`|[Хранилище сервисов](repository.md)|
|`[c] routing.inl`||
|`[c] session.cpp`||
|`[c] synchronization.inl`||
|`[c] unique_id.cpp`||

