> [services/node/slave.cpp](https://github.com/cocaine/cocaine-core/blob/master/src/services/node/slave.cpp)

Кокаиновый раб. Представляет из себя обёртку для пользовательского приложения. Выполняет непосредственный запуск приложения. Устанавливает каналы связи. Выполняет необходимый обмен сообщениями.

### slave_t

#### slave_t(context, reactor, manifest, profile, id, engine):

Инициализация

* `118-123`: получить изоляцию
* `127-132`: подготовить аргументы
* `134`: запустить раба в изоляции
* `137-142`: читаем `stdout`. При появлении данных вызывается `on_output`

#### void bind(const std::shared_ptr<channel<io::socket<local>>>& channel_)

Подключиться к каналу связи

* `168-171`: при получении сообщения вызвать `on_message`

#### void assign(const std::shared_ptr<session_t>& session)

Назначить сессию связи

* `213`: подсоединить сессию к каналу связи

#### void stop()

Остановиться

#### void on_message(const message_t& message)

Пришло сообщение снаружи. Необходимо его обработать

* `236-238`: сообщение `heartbeat`, вызвать `on_ping`
* `240-246`: сообщение `terminate`, вызвать `on_death`
* `248-253`: сообщение `chunk`, вызвать `on_chunk`
* `255-261`: сообщение `error`, вызвать `on_error`
* `263-265`: сообщение `choke`, вызвать `on_choke`

#### void on_failure(const std::error_code& ec)

#### void on_ping()

#### void on_death(int code, const std::string& reason)

#### void on_chunk(uint64_t session_id, const std::string& chunk)

#### void on_error(uint64_t session_id, int code, const std::string& reason)

#### void on_choke(uint64_t session_id)

#### void on_timeout(ev::timer&, int)

#### void on_idle(ev::timer&, int)

#### size_t on_output(const char* data, size_t size)

#### void pump()

#### void dump()

#### void terminate(int code, const std::string& reason)
