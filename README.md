# Telegram bot

Телеграм бот "Frank" - ваш персональный астролог, который поможет вам получить актуальные предсказания на каждый день.

Вы можете узнать гороскоп на вчерашний, сегодняшний и завтрашний день, чтобы быть в курсе всех изменений и событий, которые могут произойти в вашей жизни. Настроение, успехи в работе, отношения с близкими - "Frank" поможет вам разобраться во всех этих аспектах вашей жизни.

Кроме того, вы можете получить предсказания на неделю и месяц вперед, чтобы иметь представление о главных событиях, которые вас ожидают. Благоприятные периоды для начала новых дел, возможные препятствия на пути к успеху - "Frank" всегда будет рядом, чтобы поделиться с вами своими знаниями и советами.

Если вас интересует более глубокое погружение в мир предсказаний, "Frank" также предлагает расклад таро. Каждая карта таро имеет свое значение и символизирует определенные события в жизни человека.

Благодаря "Frank" вы сможете быть в курсе всех изменений в вашей жизни и принимать более осознанные решения.

Попробуйте ["Frank"](https://t.me/frank_as_frankenstein_bot "Наш друг Frank")

## Настройка окружения

Лучше всего использовать Linux. OSX тоже будет нормально работать.

Можно использовать Windows, но для компиляции и запуска потребуется WSL (Windows Subsystem for Linux). В этом случае сначала установите WSL, а дальшейшие инструкции выполняйте уже в Linux окружении.

Рекомендуется использовать Ubuntu версии **22.04**. Минимальные версии поддерживаемых компиляторов и способ их установки в Ubuntu:

- **g++-12**
```bash
$ sudo apt-get install g++-12
```
- **clang++-16**
```bash
$ wget https://apt.llvm.org/llvm.sh
$ chmod +x llvm.sh
$ sudo ./llvm.sh 16 all
```

## Установка CMake

* На **Ubuntu** `sudo apt-get -y install cmake`
* На **MacOS** `brew install cmake`

## Установка зависимостей

 * На **Ubuntu** `sudo apt-get install libpoco-dev`
 * На **MacOS** `brew install poco --build-from-source --cc=gcc-8`

 ## Запуск бота

 ```bash
horo-tgbot$ mkdir ./build
horo-tgbot$ cd ./build
horo-tgbot/build$ cmake ./..
horo-tgbot/build$ make
horo-tgbot/build$ ./bot-run $(< ./../token)
 ```

## Документация по методам 

Получение гороскопа через API в зависимости от знака (`sign`) на:
* Вчерашний день
* Сегодняшний день
* Завтрашний день
* Неделю
* Месяц

```cpp
std::string GetDaily(std::string day, std::string sign);
std::string GetMonthly(std::string sign);
std::string GetWeekly(std::string sign);
```

Получение обновлений (новых сообщений), аргументы:
* `offset` - начиная с какого обновления (номер) мы хотим получать
* `timeout` - через какое время хотим получить (частота) 

```cpp
std::vector<Update> GetUpdates(std::optional<int64_t> offset = std::nullopt,
                               std::optional<int64_t> timeout = std::nullopt);
```

Отправка сообщения, аргументы:
* `chat_id` - идентификатор чата, в который мы отправляем сообщение
* `text` - текст сообщения
* `reply_to_message_id` - идентификатор сообщения, на которое мы отвечаем
* `reply_markup` - набор маркап кнопок, пример "♎ Весы ♎"

```cpp
Message SendMessage(int64_t chat_id, std::optional<std::string> text = std::nullopt,
                    std::optional<int64_t> reply_to_message_id = std::nullopt,
                    std::optional<std::vector<std::string>> reply_markup = std::nullopt);
```

Отправка фото, аргументы:
* `chat_id` - идентификатор чата, в который мы отправляем фото
* `file` - относительынй путь до изображения, которые мы хотим отправить

```cpp
Message SendPhoto(int64_t chat_id, std::string file);
```