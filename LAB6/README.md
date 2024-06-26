# Лабораторная работа № 6. Внедрение маршрутизации между виртуальными локальными сетями

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_topology.PNG)

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_Addresses_table.PNG)

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_VLAN_table.PNG)

## Задачи:
### Часть 1. Создание сети и настройка основных параметров устройства
### Часть 2. Создание сетей VLAN и назначение портов коммутатора
### Часть 3. Настройка транка 802.1Q между коммутаторами
### Часть 4. Настройка маршрутизации между сетями VLAN
### Часть 5. Проверка работоспособности маршрутизации между VLAN
#
## Общие сведения/сценарий
В целях повышения производительности сети большие широковещательные домены 2-го уровня делят на домены меньшего размера. Для этого современные коммутаторы используют виртуальные локальные сети (VLAN). VLAN также можно использовать в качестве меры безопасности, отделяя конфиденциальный трафик данных от остальной части сети. Сети VLAN облегчают процесс проектирования сети, обеспечивающей помощь в достижении целей организации. Для связи между VLAN требуется устройство, работающее на уровне 3 модели OSI. Добавление маршрутизации между VLAN позволяет организации разделять и разделять широковещательные домены, одновременно позволяя им обмениваться данными друг с другом.
#
Транковые каналы сети VLAN используются для распространения сетей VLAN по различным устройствам. Транковые каналы разрешают передачу трафика из множества сетей VLAN через один канал, не нанося вред идентификации и сегментации сети VLAN. Особый вид маршрутизации между VLAN, называемый «Router-on-a-Stick», использует магистраль от маршрутизатора к коммутатору, чтобы все VLAN могли переходить к маршрутизатору.
#
В этой лабораторной работе требуется создать VLAN на обоих коммутаторах в топологии, назначить VLAN для коммутации портов доступа, убедиться, что VLAN работают должным образом, создать транки VLAN между двумя коммутаторами и между S1 и R1, настроить маршрутизацию между VLAN на R1 для разрешения связи между хостами в разных VLAN независимо от подсети, в которой находится хост.
#
**Примечание**: Маршрутизаторы, используемые в практических лабораторных работах CCNA, - это Cisco 4221 с Cisco IOS XE Release 16.9.4 (образ universalk9). В лабораторных работах используются коммутаторы Cisco Catalyst 2960 с Cisco IOS версии 15.2(2) (образ lanbasek9). Можно использовать другие маршрутизаторы, коммутаторы и версии Cisco IOS. В зависимости от модели устройства и версии Cisco IOS доступные команды и результаты их выполнения могут отличаться от тех, которые показаны в лабораторных работах. Правильные идентификаторы интерфейса см. в сводной таблице по интерфейсам маршрутизаторов в конце лабораторной работы.
#
**Примечание.** Следует убедиться, что у всех маршрутизаторов и коммутаторов была удалена начальная конфигурация. 
#
## Необходимые ресурсы:
 - 1 маршрутизатор (Cisco 4321 с универсальным образом Cisco IOS XE версии 16.9.4 или аналогичным);
 - 2 коммутатора (Cisco 2960 с операционной системой Cisco IOS 15.2(2) (образ lanbasek9) или аналогичная модель);
 - 2 ПК (ОС Windows с программой эмуляции терминалов, такой как Cisco Packet Tracer);
 - консольные кабели для настройки устройств Cisco IOS через консольные порты;
 - кабели Ethernet, расположенные в соответствии с топологией.
#
## Часть 1. Создание сети и настройка основных параметров устройства
В первой части лабораторной работы предстоит создать топологию сети и настроить базовые параметры для узлов ПК и коммутаторов.
#
### Шаг 1. Создание сети согласно топологии.
Подключили устройства, как показано в топологии, и подсоединили необходимые кабели.
### Шаг 2. Настройка базовых параметров для маршрутизатора.
 1. Подключились к маршрутизатору с помощью консоли и активировали привилегированный режим EXEC.
 2. Вошли в режим конфигурации.
 3. Назначили маршрутизатору имя устройства
 4. Отключили поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
 5. Назначили **class** в качестве зашифрованного пароля привилегированного режима EXEC.
 6. Назначили **cisco** в качестве пароля консоли и включили вход в систему по паролю.
 7. Зашифровали открытые пароли.
 8. Создали баннер, который предупреждает о запрете несанкционированного доступа к устройству.
 9. Сохранили текущую конфигурацию в файл загрузочной конфигурации.
 10. Настроили на маршрутизаторе время.
 Закрыли окно настройки.

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_P1_S2_1.JPG)

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_P1_S2-2.JPG)

### Шаг 3. Настройка базовых параметров для каждого коммутатора.
1. Присвоили коммутатору имя устройства.
2. Отключили поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов. 
3. Назначили **class** в качестве зашифрованного пароля привилегированного режима EXEC.
4. Назначили **cisco** в качестве пароля консоли и включили вход в систему по паролю.
5. Зашифровали открытые пароли.
6. Создали баннер с предупреждением о запрете несанкционированного доступа к устройству.
7. Настроили на коммутаторах время. 
8. Сохранили текущую конфигурацию в качестве начальной.

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_P1_S3_1.JPG)

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_P1_S3-2.JPG)

### Шаг 4. Настройка узлов ПК.
Адреса ПК можно посмотреть в таблице адресации.

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_P1_S4.JPG)

## Часть 2. Создание сетей VLAN и назначение портов коммутатора
Во второй части мы создадим VLAN, как указано в таблице выше, на обоих коммутаторах. Затем назначим VLAN соответствующему интерфейсу и проверим настройки конфигурации. Выполним следующие задачи на каждом коммутаторе.
### Шаг 1. Создание сети VLAN на коммутаторах.
 - Создали и назвали необходимые VLAN на каждом коммутаторе из таблицы выше.

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_P2_S1_a.JPG)

 - Настроили интерфейс управления и шлюз по умолчанию на каждом коммутаторе, используя информацию об IP-адресе в таблице адресации.
 - Назначили все неиспользуемые порты коммутатора VLAN Parking_Lot, настроили их для статического режима доступа и административно деактивировали их.

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_P2_S1_bc.JPG)

**Примечание.** Команда interface range полезна для выполнения этой задачи с минимальным количеством команд.


### Шаг 2. Назначение сети VLAN соответствующим интерфейсам коммутатора.
 - Назначили используемые порты соответствующей VLAN (указанной в таблице VLAN выше) и настроили их для режима статического доступа.
 - Убедились, что VLAN назначены на правильные интерфейсы

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_P2_S2.JPG)

## Часть 3. Конфигурация магистрального канала стандарта 802.1Q между коммутаторами
В части 3 вручную настроим интерфейс F0/1 как транк.
### Шаг 1. Настройка магистрального интерфейса F0/1 на коммутаторах S1 и S2.
 - Настроили статический транкинг на интерфейсе F0/1 для обоих коммутаторов.
 - Установили native VLAN 1000 на обоих коммутаторах.
 - Указали, что VLAN 10, 20, 30 и 1000 могут проходить по транку.
 - Проверили транки, native VLAN и разрешенные VLAN через транк.

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_P3_S1.JPG)

### Шаг 2. Ручная настройка магистрального интерфейса F0/5 на коммутаторе S1.
 - Настроили интерфейс S1 F0/5 с теми же параметрами транка, что и F0/1. Это транк до маршрутизатора.
 - Сохранили текущую конфигурацию в файл загрузочной конфигурации.
 - Проверили транкинг.

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_P3_S2.JPG)

#### Если G0/0/1 на R1 будет отключен, порт f0/5 коммутатора S1 не будет отображён.

## Часть 4. Настройка маршрутизации между сетями VLAN
### Шаг 1. Настройка маршрутизатора.
 - Активировали интерфейс G0/0/1 на маршрутизаторе после выполнения нижеуказанных действий.
 - Настроили подинтерфейсы для каждой VLAN, как указано в таблице IP-адресации. Все подинтерфейсы используют инкапсуляцию 802.1Q. Убедились, что подинтерфейсу для native VLAN не назначен IP-адрес. Включили описание для каждого подинтерфейса.
 - Убедились, что вспомогательные интерфейсы работают.

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_P4_S1.JPG)

## Часть 5. Проверка работоспособности маршрутизации между VLAN
### Шаг 1. Выполнение тестов с PC-A. 
**Примечание.** Возможно придётся отключить брандмауэр ПК для работы **ping**.
- Отправили эхо-запрос с PC-A на шлюз по умолчанию.
- Отправили эхо-запрос с PC-A на PC-B.
- Отправили команду **ping** с компьютера PC-A на коммутатор S2.

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_P5_S1.JPG)

### Шаг 2. Проведение теста с PC-B.
В окне командной строки на PC-B выполнили команду **tracert** на адрес PC-A.

![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_P5_S2n.JPG)

#### В результатах отображаются промежуточные IP-адреса роутера R1 (192.168.30.1), который является для PC-B гейтвеем и компьютера PC-A (192.168.20.3), поскольку компьютер PC-B (192.168.30.3) расположен в отличной от PC-А сети и обращается к роутеру R1.


![](https://github.com/IvShikov/OtusLab/blob/main/LAB6/Lab6_Routers_interfaces_table.PNG)

**Примечание**. Чтобы определить конфигурацию маршрутизатора, можно посмотреть на интерфейсы и установить тип маршрутизатора и количество его интерфейсов. Перечислить все комбинации конфигураций для каждого класса маршрутизаторов невозможно. Эта таблица содержит идентификаторы для возможных комбинаций интерфейсов Ethernet и последовательных интерфейсов на устройстве. Другие типы интерфейсов в таблице не представлены, хотя они могут присутствовать в данном конкретном маршрутизаторе. В качестве примера можно привести интерфейс ISDN BRI. Строка в скобках — это официальное сокращение, которое можно использовать в командах Cisco IOS для обозначения интерфейса.
