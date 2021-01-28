Oh My BackEnd
=============

Документ содержит список базовых навыков, которые **часто** требуются backend разработчику web-приложений.

Метка ⚡ означает что этот пункт для более глубокого и продвинутого изучения темы (если у Вас есть время). 

Каждый пункт подразумевает что:
- бекендер знает что это и какую проблему решает.
- бекендер знает для чего и когда следует применить.
- бекендер знает как с этим работать или знает где подсмотреть. 
- при разработке или проектировании бекендер помнит про них и учитывает в приложении. 

Как это работает "внутри" будет дополнительным бонусом в понимании темы. Если разбираться как работает "внутри" каждый пункт то потребуется очень много времени на изучение, как следствие изучайте по желанию и необходимости.

Каждый пункт легко гуглится и имеет страницу в wikipedia. Ссылки устанавливаются если есть альтернативная документация - более понятная и/или подробная.
Ссылка на вики ставятся что бы исключить ошибочного варианта статьи на вики. 

# Содержание

* [Этап 1. Виртуализация docker](#этап-1-виртуализация-docker)
* [Этап 2. Linux](#этап-2-linux)
* [Этап 3. Общие знания](#этап-3-общие-знания)
* [Этап 4. Сеть](#этап-4-сеть)
* [Этап 5. Базы данных](#этап-5-базы-данных)
* [Этап 6. Протокол HTTP](#этап-6-протокол-http)
* [Этап 7. Безопасность](#этап-7-безопасность)
* **[Этап 8. Тут должен быть ваш язык программирования](#этап-8-тут-должен-быть-ваш-язык-программирования)**
* [Этап 9. Электронная почта](#этап-9-электронная-почта)
* [Этап 10. Полнотексовый поиск через ElasticSearch](#этап-10-полнотексовый-поиск-через-elasticsearch)
* [Этап 11. Метрики](#этап-11-метрики)

# Этап 1. Виртуализация docker

Для начала надо поднять виртуальную машину для экспериментов и изысканий. 
Даже если уже имеет Linux на рабочей машине, всё равно поднимите виртуализацию. В случае чего, виртуальную машину всегда можно пересоздать.
Есть много систем виртуализаций, но docker выделяется среди них. Он один из популярных десктопных виртуализаций и близок с Kubernetes (aka k8s) - популярной серверной виртулизацией.

* установить [docker](https://www.docker.com/products/docker-desktop)
* запустить контейнер с Linux Ubuntu, последней [LTS версией](https://ru.wikipedia.org/wiki/Список_версий_Ubuntu#История_выпусков). Запустить bash (консоль) контейнера.
* установить удобное приложение для урпавления образами и контейнерами [Kitematic](https://kitematic.com/), [Portainer](https://hub.docker.com/r/portainer/portainer/) и тд. Либо сродниться с консольными командами docker. На некоторых OC десктопный docker уже имеет свой dashboard для управлениея образами и контейнерами. 
* ⚡ docker compose для поднятия кластера контейнеров

# Этап 2. Linux

Изучить установленый в контейнере Linux из этапа 1. Linux де-факто является серверной ос для большинства случаев web-приложений.

* Установка пакетов и обновление системы через `apt`/`apt-get`/`aptitude`
* Базовые навыки в bash. 
  * Базовый синтаксис bash.
    * Управляющи операторы `for` и `if`
    * Логические `;`, `&&`, `||`
  * Базовые команды для работы с файловой системой `cd`, `ls`, `find`, `cat`, `cp`, `mv`.
  * Команды обработки данных `tail`, `head`, `grep`, `awk`, `sed`. _Этот набор потребуется для сканирования и анализа логов, больших объёмов данных_
  * Команды работы с архивами `gzip`, `gunzip`, `tar`, `zcat`, `zless`, `zgrep`
  * Консольные редакторы `vim`(esc, `:q`, enter - выйти), `nano`. Откыть файл, внести изменения, сохранить. 
  * Консольный просмоторщик `less`. Открыть, найти слово, закрыть.
  * Конвееры команд через оператор `|`: `cmd1 | cmd2 | cmd3`
  * Фоновые задачи, оператор `&`, команды `jobs`, `fg`, `bg`.
  * [Перенаправление потоков](https://www.opennet.ru/docs/RUS/bash_scripting_guide/c11620.html), операторы `>`, `>>`, `<`
* Понятие `процесс`
  * Команды анализа процессов `top`/`htop`, `ps` (`ps aux`).
  * Родительский процесс, дочерний процесс.
  * Мастер-воркер процессы, демон (daemon)
  * Зомби процесс. Откуда берутся, как с ними бороться. 
  * [Отправка сигналов процессам](https://ru.wikipedia.org/wiki/Сигнал_(Unix))
    * Изучение команды `kill`, `pkill`, `killall`
    * Назначение сигналов [SIGKILL](https://ru.wikipedia.org/wiki/SIGKILL), [SIGTERM](https://ru.wikipedia.org/wiki/SIGTERM), [SIGINT](https://ru.wikipedia.org/wiki/SIGTERM), [SIGHUP](https://ru.wikipedia.org/wiki/SIGHUP), [SIGSEGV](https://ru.wikipedia.org/wiki/SIGSEGV)
  * Команада анализа работы процесса через `strace`.
* Изучение понятия `дескриптор`
  * Стандартные дескрипторы `STDIN`, `STDOUT`, `STDERR` и их нумерация в `shell`-ах
  * Ограничение на дескрипторы
  * Потоки, сокеты и unix-сокеты
  * Команада анализа открытых дескрипторов у процесса через `lsof`
* Права и доступы файловой системы
  * Супер пользователь, команды `su` и `sudo`
  * Флаги доступов `x`, `r`, `w` (что они значат для файлов и директорий)
  * Понимание описания доступов вида `--xr-xrwx` и `0137` (восмеричная) у файлов и директорий
  * Изменение прав доступов через команды `chmod`, `chown`
* Исполняемые файлы
  * [sha bang](https://ru.wikipedia.org/wiki/Шебанг_(Unix))
* Запуск и остановка сервисов systemd
* [SSH](https://ru.wikipedia.org/wiki/SSH)
  * Генерация собственного ssh-rsa ключа
  * Использование публичного ssh-rsa ключа для входа на удалённую машину (используйте второй контейнер с linux).
* Перенос контента между хостами. _Появляется потребность перекинуть логи, дамп базы и другие файлы между машинами или к себe._ 
  * `scp` — самый простой и "нативный" инструмент переноса файлов между хостами по ssh.
  * `rsync` — пожалуй самы мощный инструмент переноса файлов между хостами.
* Планировщик задач `crond`/`crontab`, `at`
* Оперативная память
  * Команда `free`, мета информация `/proc/meminfo`.
  * Ошибка `Out Of Memory` (OOM) и причина появления. OOM-киллер.
* Логи. Для чего и как посмотреть.
  * `dmesg` (driver messages) — важные сообщения от компонентов linux, включая от OOM-киллера.
  * `syslog` — системный лог

# Этап 3. Общие знания

Некоторые знания не возможно категоризировать. Но без них не обойтись. 

  * Регулярные выражения. Поиграться регулярными выражениями можно [тут](https://regex101.com/). Хоть каждый язык может иметь своё видение регулярных выражений, в общем смысле (и синтаксисе) они похожи.
  * Криптография 
    * Хеши и хеш функции, в том числе `crc32`, `md5`, `sha1`, `sha256`.
      * Цифровые подписи.
      * Cоль для подписей.
      * Коллизии хешей.
    * Симметричное и асимметричное шифрование.
    * Алгоритмы шифрования.
    * SSL и TLS.
  * Базовая работа с `git`
    * Комит изменений (commit)
    * Отправка изменений (push/pull)
    * Создание веток и тега (branch/tag)
    * Слияние веток (merge)
    * ⚡ [упороться полностью git-ом](https://git-scm.com/book/ru/v2)
  * Стуктуры хранения данных
    * Хеш таблицы
    * Очередь и стек
    * [Связный список](https://ru.wikipedia.org/wiki/Связный_список) и [двусвязный список](https://ru.wikipedia.org/wiki/Связный_список#Двусвязный_список_(двунаправленный_связный_список))
    * Бинарное дерево
  * Форматы хранения и передачи данных
    * Текстовые
      * JSON
      * YAML
      * XML
    * Бинарные
      * MessagePack
      * BSON (бинарный аналог JSON)
      * ProtoBuf (бинарный аналог XML)

# Этап 4. Сеть

Сеть в разработке самая важная и, часто, мало заметная часть.

  * Базовое понимание работы сети, протокл TCP и протокл UDP.
    * TCP пакет, UDP пакет
    * TCP: 
      * ⚡ Флаги ACK, SYN, FIN и прочие 
      * Буферы (window size)
    * ⚡ Сетевые издержки: Packet loss, Reordering, Jitter, Round-Trip Time (RTT aka лаг)
    * [проблемы TCP](https://www.youtube.com/watch?v=aXYJlizk3CQ)
  * IPv4, IPv6
  * DNS
    * [Как работает резолвинг доменов](https://temoto.github.io/a/kak-rabotayut-domeny.html)
    * [DNS записи](https://ru.wikipedia.org/wiki/Типы_ресурсных_записей_DNS)
      * Основные MX, CNAME, NS, A, AAAA, TXT
      * ⚡ Прочие записи
    * Консольные команды работы с доменами: whois, dig, host
  * Трассировки маршрутов.
  * ⚡ анализ трафика через tcpdump + wireshark

# Этап 5. Базы данных

Без баз данных - никуда. Самая частый вид баз данных - реляционные. 

  * SQL базы данных MySQL/Postgres/итд. MySQL подразумевает как MySQL от Oracle, так и различные модификации как MariaDB, Percona XTraDB
    * Базовый синтаксис запросов `SELECT`/`INSERT`/`UPDATE`/`DELETE`
    * Создание и модификация таблиц
      * Типы колонок таблиц их назначение их различие (на примере MySQL и схожих)
        * tinyint/smallint/int/bigint
        * tinytext/text/mediumtext/longtext
        * set/enum
        * char/varchar
        * decimal
        * double
        * прочие
      * Создание и применеие ALTER запросов.
    * Анализ выполнения запросов через `EXPLAIN`, понимание результатов `EXPLAIN`.
    * Ведение логов медленных запросов — slow_log.
    * [Понимание работы индексов](https://ruhighload.com/Индексы+в+mysql)
      * Назначение PRIMARY индексов
      * Назначение UNIQUE/обычный индексов
      * Составные индексы.
        * Понимание какие поля в какой последовательности добавлять в индекс при фиьтрации и сортировке одновременно.
      * ⚡ Алгоритм построения индексов `BTREE`
     * Объединение таблиц `LEFT JOIN`, `RIGHT JOIN`, `INNER JOIN`, `OUTER JOIN`, `JOIN`
     * Группировка данных через `GROUP BY`
       * Фильтрация после группировки
       * Функции работы с группами MAX/MIN/AVG/итд
     * Понимание и назначение внешних ключей (`foreign key`)
     * Транзакции
       * Уровни изоляций транзакций
       * Deadlock и как его не допускать
     * ⚡ Триггеры на `INSERT`/`UPDATE`/`DELETE`
     * Хранение деревьев 
       * parent-child
       * nested sets
  * noSQL базы данных MongoDB/DocumentDB
    * Типы данных в коллекциях их назначение и их различие.
    * Анализ выполнения запросов через `explain()`, понимание его результатов.
    * Понимание работы индексов (аналогично SQL индексам с небольшими отличиями)
    * Вложенные объекты, массивы.
    * ⚡ Агрегации
  * Redis
    * [базовая работа с ключами](https://redis.io/commands#generic)
    * [работа со списками](https://redis.io/commands#list)
    * [работа с хешами](https://redis.io/commands#hash)
    * [работа с набором](https://redis.io/commands#set) и [сортированным набором](https://redis.io/commands#sorted_set)
    * ⚡ Структура хранения данных [skip list](https://ru.wikipedia.org/wiki/Список_с_пропусками)

# Этап 6. Протокол HTTP

Каждый WEB разработчик должен понимать протокол HTTP. Разработчик который не знает HTTP протокол — это как сапожник без сапог.

  * [Понимание общего формата протокола](https://developer.mozilla.org/ru/docs/Web/HTTP/Overview): где заголовки, а где тело.
  * Сродниться со вкладкой Сеть/Network в инспекторе браузера, где можно наблюдать HTTP запросы.
  * [Методы HTTP запросов](https://developer.mozilla.org/ru/docs/Web/HTTP/Methods).  Их назначение и ограничения.
    * Основные [GET](https://developer.mozilla.org/ru/docs/Web/HTTP/Methods/GET), [POST](https://developer.mozilla.org/ru/docs/Web/HTTP/Methods/POST), [HEAD](https://developer.mozilla.org/ru/docs/Web/HTTP/Methods/HEAD)
    * Прочие `PUT`, `DELETE` итд.
  * [Коды HTTP ответов](https://ru.wikipedia.org/wiki/Список_кодов_состояния_HTTP)
    * Основные (частые): 200, 301, 302, 304, 400, 401, 403, 404, 500, 502, 503, 504
    * Другие
  * Заголовки HTTP запроса
    * [MIME тип](https://developer.mozilla.org/ru/docs/Web/HTTP/Basics_of_HTTP/MIME_types) (тип документа) и заголовок типа [Content-Type](https://developer.mozilla.org/ru/docs/Web/HTTP/Заголовки/Content-Type). 
    * Системные заголовоки Host, Content-Length
    * [Кеширование HTTP](https://developer.mozilla.org/ru/docs/Web/HTTP/Кэширование) и изучение HTTP заголовков упарвления кешом Cache-Control, Expires, Vary, ETag, Last-Modified
  * [Куки](https://developer.mozilla.org/ru/docs/Web/HTTP/%D0%9A%D1%83%D0%BA%D0%B8)
  * [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/ru/docs/Web/HTTP/CORS)
  * [Content-Security-Policy (CSP)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy)
  * Различия версий протокола HTTP/1.0, HTTP/1.1 
  * Тело HTTP запроса
    * Формат передачи `application/x-www-form-urlencoded`
    * Формат передачи [multipart/form-data](https://ru.wikipedia.org/wiki/Multipart/form-data)
    * Влияние заголовков (Content-Length, [Content-Encoding](https://developer.mozilla.org/ru/docs/Web/HTTP/Headers/Content-Encoding), [Transfer-Encoding](https://developer.mozilla.org/ru/docs/Web/HTTP/Headers/Transfer-Encoding)) на тело 
  * Консольные команды HTTP запросов `curl`, `wget`
  * ⚡ HTTP/2.0 протокол и HTTP/3.0
  * ⚡ WebSocket протокол
  * HTTP API форматы
    * [REST API](https://ru.wikipedia.org/wiki/REST)
    * RPC
    * ⚡ [GraphQL](https://habr.com/ru/post/326986/)
  * Web сервера
    * [Nginx](https://nginx.org). Самый распространённый Web-сервер. Вероятность натолкнуться на него во время разработки web-приложения - велика.
      * [Ознакомление с базовыми возможностями](https://nginx.org/ru/docs/beginners_guide.html) 
      * ⚡ [Масштабируемая конфигурация nginx](https://www.youtube.com/watch?v=jf3wIN-FwW4)
      * Написание простых локаций в `/etc/nginx/nginx.conf` раздачи файлов
      * HTTP, FastCGI проксирование

# Этап 7. Безопасность

  * Виды управления доступом
    * ACL
    * RBAC
  * Аутентификация
    * [Basic](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication)
    * [OAuth2](https://www.digitalocean.com/community/tutorials/oauth-2-ru)
    * Ldap
  * Виды атак
    * Фишинг сайта
    * Инъекции (например SQL-иньекции)
    * XSS атака
    * DoS/DDoS
      * HTTP-флуд и ping-флуд
      * ⚡ Атака Fraggle (UDP-флуд)
      * ⚡ SYN flood (потребуются знанания TCP)
      * Медленный запрос
    * Атака посредника (Man In The Middle, MITM)
    * Брутфорс (например бурфорс паролей)
    * Спуфинг


# Этап 8. Тут должен быть ваш язык программирования

Языков программирования большое множество. Поэтому этот этап будет задевать только часто встречающиеся вопросы в большинстве популярных языков программирования. Принцип работы с этим разделом: гуглите `%ваш_язык_программирования% %пункт_из_этапа%`. Учтите, что **некоторых пунктов может не быть в вашем языке**.

  * Что такое интерпертатор, компилятор, JIT, оп-код, байт-код. Что из этого использует ваш язык?
  * Ваш язык программирования
    * Базовые (примитивные) типы данных в языке.
    * Объекты/классы/прототипы/структуры.
    * Ссылки, слабые ссылки.
    * Garbage Collector.
    * Преобразование типов.
    * Слабая/сильная типизация в коде. На что влияет и как с этим жить.
    * Проблемы в коде
      * Бесконечные циклы
      * Рекурсии
      * Ошибка сегментации (и ее связь с сигналом SIGSEGV)
  * Распараллеливание
    * Различие процессов (созданные через [fork](https://ru.wikipedia.org/wiki/Fork)) от потоков (thread)
      * Поведение дескрипторов до и после fork
    * Потоки (threads) 
      * Истинные потоки (pthreads, posix-threads)
      * Зелёные потоки (Green threads)
      * Блокировки Mutex и Семафоры
    * Процессы
      * Разделяемая память (Shared memory)
      * Межпроцессное взаимодействие (IPC)
    * Корутины
    * Проблемы распараллеливания
      * Race Condition
  * Битовые операции: `not`, `and`, `or`, `xor`, сдвиг влево, сдвиг вправо
  * Кеширование данных
    * Частые алгоритмы кеша [LRU](https://ru.wikipedia.org/wiki/Алгоритмы_кэширования#Least_recently_used_(Вытеснение_давно_неиспользуемых)), LFU
    * ⚡ [Иные алгоритмы кеширования](https://ru.wikipedia.org/wiki/Алгоритмы_кэширования)
    * Прогревание кеша, инвалидация кеша
  * Сессии (пользователей)
    * Как инициировать
    * Где храняться
    * Параллельное использование одной сессии несколькими запросами
  * Принципы программирования
    * KISS
    * IoC
  * Юнит тестирование
    * Ознакомление с системой тестирования в вашем языке
    * Test-Driven Development (TDD)
  * Специфика работы IO (сокетов, дескрипторов, потоков)
    * Буфферы IO
    * Асинхронный IO
  * Пакетный менеджер или менеджер зависимостей.
  * Работа HTTP сервера.

# Этап 9. Электронная почта

Работа с эл. письмами неотъемлемая часть web разработки (да и не только).
Если не придется создавать письма вручную то читать "сырое" письмо придется.

* [Спецификация письма MIME](https://www.opennet.ru/docs/RUS/inet_server/servers_glava2_5.html)
  * Основные заголовки: `Return-Path`, `Received`, `From`, `To`, `Cc`, `Bcc`, `Reply-To`, `Subject`, `Message-ID`
  * прочие заголовки
  * указание кодироквки
  * кодирование полей и тела в base64
* ⚡ Протоколы передачи почты POP3, IMAP

# Этап 10. Полнотексовый поиск через ElasticSearch

Каждый разработчик сталкивается с необходимостью полнотекстового поиска, да и вцелом быстрого поиска по куче аттрибутов и текстов. 
Для этого используются различные полнотекстовые поисковые движки такие как [ElasticSearch](https://www.elastic.co/), [SphinxSearch](http://sphinxsearch.com/), [ManticoreSearch](https://manticoresearch.com/) и тд. 
Самый распространненый полнотексовый поисковый движок с большим комунити — ElasticSearch.

* Установить Cerebro для работы с ElasticSearch.
* Индексы и их алиасы. Как с ними работать и их ограничения.
* Базовые запросы
  * Запросы поиска
  * Запросы добавления/обновления/удаления документов
  * bulk запросы
* Подключение морфологий
* mapping и их шаблоны
* ⚡ агрегации
* работа с nested-документами
* ⚡ [ELK](https://www.elastic.co/what-is/elk-stack)

# Этап 11. Метрики 

Любое приложение должно уметь генерировать _полезные_ метрики для системы сбора и анализа метрик. По факту сейчас среди opensource акуален [Prometheus](https://prometheus.io/) (или подобные) для сбора и анализа метрик и [Grafana](https://grafana.com/) для их отображения и настройки алертов.

* Prometheus
  * Типы метрик
     * count
     * gauge
     * histogram
     * summary
  * Варианты отправки метрик: push и pull
  * Запросы (лучше и наглядней делать из Graphana)
    * [Синтаксис](https://prometheus.io/docs/prometheus/latest/querying/basics/)
      * Лейблы
      * Векторы
      * Интервалы
      * Оперторы
    * [Функции](https://prometheus.io/docs/prometheus/latest/querying/functions/), особенно:
      * rate
      * irate
* Graphana 
  * Создание дашбордов
  * Создание графиков
  * Настройка алертов

