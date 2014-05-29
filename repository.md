> [repository.cpp](https://github.com/cocaine/cocaine-core/blob/master/src/repository.cpp)

Хранилище сервисов предназначено для загруки динамических библиотек модулей и хранения всех модулей.

### repository_t

#### void load(const std::string& path_)

Загружает плагины по указанному пути. Если указана папка, загружаются все файлы с расширением `.cocaine-plugin`

#### void open(const std::string& target)

Производит непосредственно чтение динамической библиотеки и запускает метод `initialize()`.
