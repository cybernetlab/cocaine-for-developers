> [services/node/app.cpp](https://github.com/cocaine/cocaine-core/blob/master/src/services/node/app.cpp)

Данный класс описывает непосредственно приложение. Приложение можно запустить, остановить, получить о нём информацию и отправить ему событие. Приложение запускается в отдельном потоке (`tread`) как новый сервис.

### app_t

#### app_t(context_t& context, const std::string& name, const std::string& profile)

Инициализация приложения

* `282-291`: Получить изолятор для приложений
* `296-310`: Создать `engine` и `engine_control` и связать их локально

#### void start()

Запуск приложения

* `322`: Создать новый `thread` для исполнителя (`engine`)
* `327-331`: Создать новый сервис для приложения и добавить его в контекст выполнения

#### void stop()

Остановить приложение

* `464-467`: Удалить сервис приложения из контекста выполнения
* `469-482`: Долждаться завершения приложения

#### dynamic_t info()

Получить информацию о приложении

#### std::shared_ptr<api::stream_t> enqueue(const api::event_t& event, const std::shared_ptr<api::stream_t>& upstream)
#### std::shared_ptr<api::stream_t> enqueue(const api::event_t& event, const std::shared_ptr<api::stream_t>& upstream, const std::string& tag)

Отправить в приложение событие `event` с данными `upstream` и тегом `tag`
