> [context.cpp](https://github.com/cocaine/cocaine-core/blob/master/src/context.cpp)

Контекст исполнения формирует основное окружение для cocaine-runtime. Файл довольно объёмный, поэтому многое будет опущено.

Основные функции и назначение контекста:

* Контекст добавляет, удаляет и хранит все сервисы, включая встроенные сервисы, плагины, логгер и локатор
* Приложения также запускаются как сервисы

### context_t

Контекст имеет два конструктора для создания контекста с указанием имени логгера или объекта логгера:

#### context_t(config_t config, const std::string& logger_name) `629-690`

#### context_t(config_t, config, logger) `692-717`

* `636`, `699`: создание [repository](repository.md) - основная точка хранения всех модулей кокаина
* `639`, `702`: загружаются встроенные модули: `isolate::process_t`, `gateway::adhoc_t`, `service::logging_t`, `service::node_t`, `service::storage_t`, `storage::files_t`
* `642`, `705`: загружаются плагины
* `645-687`, `705-714`: инициализируется логгер
* `689`, `716`: запуск системы

#### ~context_t()

* `725-726`: останавливается синхронизация ???
* `730-731`: останавливается [локатор](locator.md)
* `735-745`: останавливаются все сервисы
* `749`: очищается пул ???

#### void insert(const std::string& name, std::unique_ptr<actor_t>&& service)

Добавляет в контекст новый сервис `service` с именем `name`.

* `769`: порт по-умоляанию = 0 (любой)
* `774-776`: не добавлять сервис, если он уже существует
* `778-788`: если в конфигурации указан пул портов, то взять порт от туда
* `790-793`: открыть порт на адресе `endpoint`
* `795`: запустить сервис, передав ему открытый порт

#### auto remove(const std::string& name)

Удаляет сервис с именем `name` из контекста. Возвращает удалённый сервис.

* `825`: остановка сервиса
* `829-831`: если в конфигурации указан пул портов, вернуть туда освободившийся порт

#### auto locate(const std::string& name)

Находит сервис с именем `name`

#### void attach(const std::shared_ptr<io::socket<io::tcp>>& ptr, const std::shared_ptr<io::basic_dispatch_t>& dispatch)

???

#### void bootstrap()

Запуск контекста

* `861-871`: если в конфигурации указан пул портов, создать массив портов
* `884-908`: для всех сервисов, перечисленных в конфигурации пытаемся создать и добавить сервис. В случае неудачи, вывод об ошибках
* `910-948`: попытка создания и добавления локатора, в случае неудачи - сообщение об ошибках

### config_t

#### config_t(const std::string& config_path)

Инициализация конфигурации и чтение её из файла.

#### path

* config
* plugins
* runtime

#### network

* hostname
* uuid
* endpoint
* locator
* group
* ports
* gateway

#### services

#### storages

#### logging

#### version
