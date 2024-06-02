# Лабораторная работа №9. Реализация DHCPv4 
# Задачи:
## Часть 1. Создание сети и настройка основных параметров устройства
## Часть 2. Настройка и проверка двух серверов DHCPv4 на R1
## Часть 3. Настройка и проверка DHCP-ретрансляции на R2
###
# Общие сведения и сценарий:
Протокол динамической конфигурации сетевого узла (DHCP) — сетевой протокол, позволяющий сетевым администраторам управлять и автоматизировать назначение IP-адресов. Без использования DHCP  для IPv4 администратору необходимо вручную назначать и настраивать IP-адреса, предпочтительные DNS-серверы и шлюзы по умолчанию. По мере увеличения сети и перемещении устройств из одной внутренней сети в другую это становится административной проблемой.
В предложенном сценарии размеры компании увеличились, и сетевые администраторы больше не имеют возможности назначать IP-адреса для устройств вручную. Ваша задача заключается в настройке маршрутизатора R1 для назначения IPv4-адресов в двух разных подсетях. 
Примечание: Маршрутизаторы, используемые в практических лабораторных работах CCNA, - это Cisco 4221 с Cisco IOS XE Release 16.9.4 (образ universalk9). В лабораторных работах используются коммутаторы Cisco Catalyst 2960 с Cisco IOS версии 15.2(2) (образ lanbasek9). Можно использовать другие маршрутизаторы, коммутаторы и версии Cisco IOS. В зависимости от модели устройства и версии Cisco IOS доступные команды и результаты их выполнения могут отличаться от тех, которые показаны в лабораторных работах. Правильные идентификаторы интерфейса см. в сводной таблице по интерфейсам маршрутизаторов в конце лабораторной работы.
**Примечание.** Нужно убедиться, что у всех маршрутизаторов и коммутаторов была удалена начальная конфигурация. Если вы не уверены в этом, обратитесь к инструктору.
# Необходимые ресурсы:
 - 2 маршрутизатора (Cisco 4221 с универсальным образом Cisco IOS XE версии 16.9.4 или аналогичным);
 - 2 коммутатора (Cisco 2960 с образом lanbasek9 Cisco IOS версии 15.2 (2) или аналогичным) - опционально;
 - 2 ПК (ОС Windows с программой эмуляции терминалов, такой как Cisco Packet Tracer);
 - Консольные кабели для настройки устройств Cisco IOS через консольные порты;
 - Кабели Ethernet, расположенные в соответствии с топологией.
##
## Часть 1. Создание сети и настройка основных параметров устройства
В первой части лабораторной работы нам предстоит создать топологию сети и настроить базовые параметры для узлов ПК и коммутаторов.
### Шаг 1. Создание схемы адресации.
Подсеть сети 192.168.1.0/24 в соответствии со следующими требованиями:
 - Одна подсеть «Подсеть A», поддерживающая 58 хостов (клиентская VLAN на R1). Записали первый IP-адрес в таблице адресации для R1 G0/0/1.100 .
 - Одна подсеть «Подсеть B», поддерживающая 28 хостов (управляющая VLAN на R1). Записали первый IP-адрес в таблице адресации для R1 G0/0/1.200. Записали второй IP-адрес в таблице адресов для S1 VLAN 200 и ввели соответствующий шлюз по умолчанию.
 - Одна подсеть «Подсеть C», поддерживающая 12 узлов (клиентская сеть на R2). Записали первый IP-адрес в таблице адресации для R2 G0/0/1.
### Шаг 2. Создание сети согласно топологии.
Подключили устройства, как показано в топологии, и подсоединили необходимые кабели.
### Шаг 3. Произведение базовой настройки маршрутизаторов.
 - Назначили маршрутизатору имя устройства.
 - Отключили поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введённые команды таким образом, как будто они являются именами узлов. 
 - Назначили **class** в качестве зашифрованного пароля привилегированного режима EXEC.
 - Назначили **cisco** в качестве пароля консоли и включили вход в систему по паролю.
 - Назначили **cisco** в качестве пароля VTY и включили вход в систему по паролю.
 - Выполнили шифрование открытых паролей.
 - Создали баннер с предупреждением о запрете несанкционированного доступа к устройству.
 - Сохранили текущую конфигурации в файл загрузочной конфигурации.
 - Установили часы на маршрутизаторе на сегодняшнее время и дату.
 **Примечание.** Вопросительный знак (?) позволяет открыть справку с правильной последовательностью параметров, необходимых для выполнения этой команды.
### Шаг 4. Настройка маршрутизации между сетями VLAN на маршрутизаторе R1.
 - Активировали интерфейс G0/0/1 на маршрутизаторе.
 - Настроили подинтерфейсы для каждой VLAN в соответствии с требованиями таблицы IP-адресации. Все субинтерфейсы используют инкапсуляцию 802.1Q и назначаются первый полезный адрес из вычисленного пула IP-адресов. Убедились, что подинтерфейсу для native VLAN не назначен IP-адрес. Включили описание для каждого подинтерфейса.
 - Убедились, что вспомогательные интерфейсы работают.
### Шаг 5. Настройка G0/1 на R2, затем G0/0/0 и статической маршрутизации для обоих маршрутизаторов.
 - Настроили G0/0/1 на R2 с первым IP-адресом подсети C, рассчитанным ранее.
 - Настроили интерфейс G0/0/0 для каждого маршрутизатора на основе приведенной выше таблицы IP-адресации.
 - Настроили маршрута по умолчанию на каждом маршрутизаторе, указываемом на IP-адрес G0/0/0 на другом маршрутизаторе.
 - Убедились, что статическая маршрутизация работает с помощью пинга до адреса G0/0/1 R2 от R1.
 - Сохранили текущую конфигурацию в файл загрузочной конфигурации.
### Шаг 6. Настройка базовых параметров каждого коммутатора.
 - Присвоили коммутатору имя устройства.
 - Отключили поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введённые команды таким образом, как будто они являются именами узлов. 
 - Назначили **class** в качестве зашифрованного пароля привилегированного режима EXEC.
 - Назначили **cisco** в качестве пароля консоли и включили вход в систему по паролю.
 - Назначили **cisco** в качестве пароля VTY и включили вход в систему по паролю.
 - Выполнили шифрование открытых паролей.
 - Создали баннер с предупреждением о запрете несанкционированного доступа к устройству.
 - Сохранили текущую конфигурации в файл загрузочной конфигурации.
 - Установили часы на маршрутизаторе на сегодняшнее время и дату.
 **Примечание.** Вопросительный знак (?) позволяет открыть справку с правильной последовательностью параметров, необходимых для выполнения этой команды.
### Шаг 7. Создайте сети VLAN на коммутаторе S1.
**Примечание.**  S2 настроен только с базовыми настройками. 
 - Создали необходимые VLAN на коммутаторе 1 и присвойте им имена из приведенной выше таблицы.
 - Настроили и активировали интерфейс управления на S1 (VLAN 200), используя второй IP-адрес из подсети, рассчитанный ранее. Кроме того установили шлюз по умолчанию на S1.
 - Настроили и активировали интерфейс управления на S2 (VLAN 1), используя второй IP-адрес из подсети, рассчитанный ранее. Кроме того, установили шлюз по умолчанию на S2
 - Назначили все неиспользуемые порты S1 VLAN Parking_Lot, настроили их для статического режима доступа и административно деактивировали их. На S2 административно деактивировали все неиспользуемые порты.
**Примечание.** Команда interface range полезна для выполнения этой задачи с минимальным количеством команд.
### Шаг 8. Назначение сети VLAN соответствующим интерфейсам коммутатора.
 - Назначили используемые порты соответствующей VLAN (указанной в таблице VLAN выше) и настроили их для режима статического доступа.
 - Убедились, что VLAN назначены на правильные интерфейсы.
**Вопрос**: Интерфейс F0/5 указан в VLAN 1, потому что?
### Шаг 9. Настройка интерфейса S1 F0/5 в качестве транка 802.1Q вручную.
 - Изменили режим порта коммутатора, чтобы принудительно создать магистральный канал.
 - В рамках конфигурации транка  установили для native  VLAN значение 1000.
 - В качестве другой части конфигурации магистрали указали, что VLAN 100, 200 и 1000 могут проходить по транку.
 - Сохранили текущую конфигурацию в файл загрузочной конфигурации.
 - Проверили состояние транка.
**Вопрос**: Если бы ПК был подключен к сети с помощью DHCP, у него был бы IP-адрес ?
## Часть 2. Настройка и проверка двух серверов DHCPv4 на R1
В части 2 необходимо настроить и проверить сервер DHCPv4 на R1. Сервер DHCPv4 будет обслуживать две подсети, подсеть A и подсеть C.
### Шаг 1. Настройка R1 с пулами DHCPv4 для двух поддерживаемых подсетей. Ниже приведен только пул DHCP для подсети A
 - Исключили первые пять используемых адресов из каждого пула адресов.
 - Открыли окно конфигурации.
 - Создали пул DHCP (использовали уникальное имя для каждого пула).
 - Указали сеть, поддерживающую этот DHCP-сервер.
 - В качестве имени домена указали CCNA-lab.com.
 - Настроили соответствующий шлюз по умолчанию для каждого пула DHCP.
 - Настроили время аренды на 2 дня 12 часов и 30 минут.
 - Затем настроили второй пул DHCPv4, используя имя пула R2_Client_LAN и вычислили сеть, маршрутизатор по умолчанию, и использовали то же имя домена и время аренды, что и предыдущий пул DHCP.
### Шаг 2. Сохранение конфигурации.
Сохранили текущую конфигурацию в файл загрузочной конфигурации.
### Шаг 3. Проверка конфигурации сервера DHCPv4
 - Чтобы просмотреть сведения о пуле, выполнили команду **show ip dhcp pool** .
 - Выполнили команду **show ip dhcp bindings** для проверки установленных назначений адресов DHCP.
 - Выполнили команду **show ip dhcp server statistics** для проверки сообщений DHCP.
### Шаг 4. Попытка получить IP-адрес от DHCP на PC-A
 - Из командной строки компьютера PC-A выполнили команду **ipconfig /all.**
 - После завершения процесса обновления выполнили команду **ipconfig** для просмотра новой информации об IP-адресе.
 - Проверили подключение с помощью пинга IP-адреса интерфейса R0 G0/0/1.
## Часть 3. Настройка и проверка DHCP-ретрансляции на R2
В части 3 настраивается R2 для ретрансляции DHCP-запросов из локальной сети на интерфейсе G0/0/1 на DHCP-сервер (R1).
### Шаг 1. Настройка R2 в качестве агента DHCP-ретрансляции для локальной сети на G0/0/1.
 - Настроили команду **ip helper-address** на G0/0/1, указав IP-адрес G0/0/0 R1.
 - Сохранили конфигурацию.
### Шаг 2. Попытка получить IP-адрес от DHCP на PC-B.
 - Из командной строки компьютера PC-B выполнили команду **ipconfig /all**.
 - После завершения процесса обновления выполнили команду **ipconfig** для просмотра новой информации об IP-адресе.
 - Проверили подключение с помощью пинга IP-адреса интерфейса R1 G0/0/1.
 - Выполнили **show ip dhcp binding** для R1 для проверки назначений адресов в DHCP.
 - Выполнили команду **show ip dhcp server statistics** для проверки сообщений DHCP.