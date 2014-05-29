> [node.cpp](https://github.com/cocaine/cocaine-core/blob/master/src/services/node.cpp)

Сервис ноды при запуске кокаина старутет все приложения из списка запуска (`runlist`). Основная логика работы приложений реализована в файлах в папке [node](node)

### node_t

#### node_t(context_t& context, reactor_t& reactor, const std::string& name, const dynamic_t& args)

Инициализация сервиса

* `49-51`: Установить обработчики событий запуска, остановки и перечисления приложений
* `56-74`: Прочитать из хранилища `core` все файлы в папке `runlists`. И если таковые имеются, вызвать событие `on_start_app` для их запуска

#### ~node_t()

* `78-90`: Остановить все запущенные приложения

#### dynamic_t on_start_app(const runlist_t& runlist)

Запустить все приложения, указанные в `runlist`

#### dynamic_t on_pause_app(const std::vector<std::string>& applist)

Приостановить все приложения, указанные в `applist`

#### dynamic_t on_list()

Возвращает список всех приложений
