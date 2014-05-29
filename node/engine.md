> [services/node/engine.cpp](https://github.com/cocaine/cocaine-core/blob/master/src/services/node/engine.cpp)

### engine_t

#### engine_t(context, reactor, manifest, profile, control)

Инициализация исполнителя

* `90-99`: создать локальное соединения для связи с приложением. При соединений вызвать `on_connection`
* `101-111`: установить контролирующее соединение. При появлении в соединении сообщений вызывать `on_control`
* `113-118`: получить изолятор

#### ~engine_t()

* `123`: удалить локальное соединение

#### void run()

Выполнить запуск

#### std::shared_ptr<api::stream_t> enqueue(const api::event_t& event, const std::shared_ptr<api::stream_t>& upstream)

Послать приложению событие

#### void engine_t::erase(const std::string& id, int code, const std::string& reason)

Удалить приложение из пула приложений

#### void on_connection(const std::shared_ptr<io::socket<local>>& socket_)

Вызывается при подключении кокаинового раба

* `225-234`: при рукопожатии выполнить `on_handshake`

#### void on_handshake(int fd, const message_t& message)

Раб протягивает руку для рукопожатия

#### void on_control(const message_t& message)

Реагировать на упраляющие сообщения от `app_t`

```
...
```

#### void stop()

Остановить исполнитель
