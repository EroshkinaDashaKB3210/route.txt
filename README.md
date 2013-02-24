route.txt
=========
Microsoft Windows [Version 6.1.7601]
(c) Корпорация Майкрософт (Microsoft Corp.), 2009. Все права защищены.

C:\Users\Даша>route

Обработка таблиц сетевых маршрутов.

ROUTE [-f] [-p] [-4|-6] command [destination]
                  [MASK netmask]  [gateway] [METRIC metric]  [IF interface]

  -f           Очистка таблиц маршрутов от записей всех шлюзов.  При указании
               одной из команд таблицы очищаются до выполнения команды.

  -p           При использовании с командой ADD задает сохранение маршрута
               при перезагрузке системы. По умолчанию маршруты не сохраняются
               при перезагрузке. Пропускается для остальных команд,
               изменяющих соответствующие постоянные маршруты. Этот
               параметр не поддерживается в Windows 95.

  -4             Обязательное использование протокола IPv4.

  -6           Обязательное использование протокола IPv6.

  command      Одна из следующих команд:
                 PRINT     Печать маршрута
                 ADD       Добавление маршрута
                 DELETE    Удаление маршрута
                 CHANGE    Изменение существующего маршрута
  destination  Адресуемый узел.
  MASK         Указывает, что следующий параметр интерпретируется как маска
               сети.
  netmask      Значение маски подсети для записи данного маршрута.
               Если этот параметр не задан, по умолчанию используется
               значение 255.255.255.255.
  gateway      Шлюз.
  interface    Номер интерфейса для указанного маршрута.
  METRIC       Определение метрики, т.е. цены для адресуемого узла.

Поиск всех символических имен узлов проводится в файле сетевой базы данных
NETWORKS. Поиск символических имен шлюзов проводится в файле базы данных имен
узлов HOSTS.

Для команд PRINT и DELETE можно указать узел и шлюз с помощью подстановочных
знаков или опустить параметр "шлюз".

Если адресуемый узел содержит подстановочные знаки * или ?, он используется
в качестве шаблона, и печатаются только соответствующие ему маршруты. Знак '*'
соответствует любой строке, а '?' - одному знаку.
Примеры: 157.*.1, 157.*, 127.*, *224*.

Соответствие шаблону поддерживает только команда PRINT.
Диагностические сообщения:
    Недопустимое значение MASK вызывает ошибку, если (УЗЕЛ МАСКА) != УЗЕЛ.
    Например> route ADD 157.0.0.0 MASK 155.0.0.0 157.55.80.1 IF 1
             Добавление маршрута завершится ошибкой, поскольку указан недопустим
ый параметр маски. (Узел & Маска) != Узел.

Примеры:

    > route PRINT
    > route PRINT -4
    > route PRINT -6
    > route PRINT 157*          .... Печать только узлов, начинающихся со 157

    > route ADD 157.0.0.0 MASK 255.0.0.0  157.55.80.1 METRIC 3 IF 2
             узел^      ^маска      ^шлюз     метрика^    ^
                                                         интерфейс^
      Если IF не задан, то производится попытка найти лучший интерфейс для
      указанного шлюза.
    > route ADD 3ffe::/32 3ffe::1

    > route CHANGE 157.0.0.0 MASK 255.0.0.0 157.55.80.5 METRIC 2 IF 2

      Параметр CHANGE используется только для изменения шлюза или метрики.

    > route DELETE 157.0.0.0
    > route DELETE 3ffe::/32

C:\Users\Даша>
