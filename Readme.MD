Описание
1) Создана виртуальная машина под управление ОС Ubuntu 22.04. Установлена СУБД ClickHouse. СУБД подключено к системе мониторинга Prometheus с визуализацией в Grafana.
2) В базе данных default создана таблица trips и в нее загружен датасет https://clickhouse.com/docs/en/getting-started/example-datasets/nyc-taxi
3) С помощью утилиты clickhouse-benchmark произведено тестирование. Тестирование включает в себя отправку 5 запрос (которые предварительно помещены в файл см. файл queries.txt), с количеством итераций 100.
Приложение: команда запуска -  clickhouse-benchmark -c 5 -i 100 --password [MyPassword] < queries.txt;
Приложение: console.png - отображает вывод консоли. Средняя скорость возврата данных 263,2 мебибайта в секунду
Приложение: query.png - отображает среднее поличество запросов в секунду
Приложение: memory.png - отображает увеличение потребления памяти при работе clickhouse-benchmark
Приложение: latency.png - отображает среднее время отклика на запрос, 360мс
4) Изучены конфигурационные файлы СУБД. 
5) Произведено конфигурирование СУБД:
 - В операционной системе отключен файл подкачки swap
 - В СУБД:
   - изменен уровень логирования на warning
   - max_threads выставлен в 4, по количеству ядер выделенных виртуальной машине
6) Изменение настроек привело к увеличению потребления ОЗУ, т.к. перестал использоваться файл подкачки
Приложение: memory2.png - отображает увеличение потребления памяти при работе clickhouse-benchmark после изменения настроек
Приложение: query2.png - среднее поличество запросов в секунду осталось прежним
Приложение: latency2.png - среднее время отклика на запрос осталось прежним, 360мс
Приложение: console2.png - отображает вывод консоли. Средняя скорость возврата данных умньшилась до 253,2 мебибайта в секунду

Вывод: На текущем датасете изменение настроек на производительность СУБД повлияло незначительно.