# Лабораторная работа №1. Базовая настройка коммутатора

# Задачи:

## Часть 1. Проверка конфигурации коммутатора по умолчанию

## Часть 2. Создание сети и настройка основных параметров устройства

### 
- Настройка базовых параметров коммутатора.
- Настройка IP-адреса для ПК.

## Часть 3. Проверка сетевых подключений

###
- Отображение конфигурации устройства.
- Тестирование сквозного соединения при помощи эхо-запроса.
- Тестирование возможности удаленного управления с помощью Telnet.
###

# Необходимые ресурсы:

- 1 коммутатор (Cisco 2960 с ПО Cisco IOS версии 15.2(2) с образом lanbasek9 или аналогичная модель)
- 1 ПК (под управлением Windows с программой эмуляции терминала)
- 1 консольный кабель для настройки устройства на базе Cisco IOS через консольный порт.
- 1 кабель Ethernet, как показано в топологии.
##

## Часть 1 Создание сети и проверка настроек коммутатора по умолчанию

![Lab1_1](https://github.com/Groly2741/OTUS-Labs-Grishaeva1/assets/164208420/f8c13452-35a0-4134-9ef0-2ba5809b02d8)

### Шаг 1 Создание сети согласно топологии.

#### a. Подсоединён консольный кабель, как показано в топологии. На данном этапе не подключается кабель Ethernet компьютера PC-A.
#### b. Установлено консольное подключение к коммутатору с компьютера PC-A с помощью Cisco Packet Tracer.
#### Для первоначальной настройки коммутатора нужно использовать консольное подключение и нельзя подключиться к коммутатору через Telnet или SSH, потому что что у нового коммутатора изначально нет данных и IP-адреса, а telnet и ssh для установления соединения требуется IP-адрес.

### Шаг 2 Проверка настройки коммутатора по умолчанию.

 #### На данном этапе проверяются такие параметры коммутатора по умолчанию, как текущие настройки коммутатора, данные IOS, свойства интерфейса, сведения о VLAN и флеш-память.
 #### Все команды IOS коммутатора можно выполнять из привилегированного режима. Доступ к привилегированному режиму нужно ограничить с помощью пароля, чтобы предотвратить неавторизованное использование устройства — через этот режим можно получить прямой доступ к режиму глобальной конфигурации и командам, используемым для настройки рабочих параметров.
 #### Пароли можно будет настроить чуть позже.
 #### К привилегированному набору команд относятся команды пользовательского режима, а также команда configure, при помощи которой выполняется доступ к остальным командным режимам. 
#### Чтобы войти в привилегированный режим EXEC, ввели команду enable.
 
### Начальный вид консоли без настроек
![](https://github.com/Groly2741/OTUS-Labs-Grishaeva1/assets/164208420/3730443e-473f-4a27-afa8-412333fd2042)


#### Изучили текущий файл running configuration.

 - На коммутаторе 2960 имеется 24 интерфейса FastEthernet 
 - На коммутаторе 2960 имеется 2 интерфейса GigabitEthernet 
 - Каков диапазон значений, отображаемых в vty-линиях?

#### Изучили файл загрузочной конфигурации (startup configuration), который содержится в энергонезависимом ОЗУ (NVRAM): startup-config is not present. Это сообщение выводится потому, что он отсутствует.
#### Изучили характеристики SVI для VLAN 1:
##### IP-адрес сети VLAN 1 не назначен: Vlan1 is administratively down, line protocol is down, Internet protocol processing disabled
##### Hardware is CPU Interface, address is 000b.be1c.c345 (bia 000b.be1c.c345)
##### Мы видим следующие выходные данные:
Output queue: 0/40 (size/max)
5 minute input rate 0 bits/sec, 0 packets/sec
5 minute output rate 0 bits/sec, 0 packets/sec
1682 packets input, 530955 bytes, 0 no buffer
Received 0 broadcasts (0 IP multicast)
0 runts, 0 giants, 0 throttles
0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
563859 packets output, 0 bytes, 0 underruns
0 output errors, 23 interface resets
0 output buffer failures, 0 output buffers swapped out

#### Подсоединили кабель Ethernet компьютера PC-A к порту 6 на коммутаторе и изучили IP-свойства интерфейса SVI сети VLAN 1. Дождались согласования параметров скорости и дуплекса между коммутатором и ПК.
Мы видим нижеследующие выходные данные:
Switch#show ip interface vlan1
Vlan1 is administratively down, line protocol is down
Internet protocol processing disabled
 - Изучили сведения о версии ОС Cisco IOS на коммутаторе: коммутатор работает под управлением версии 15.0(2)SE4.  
 - Файл образа системы называется C2960-LANBASEK9-M.
 - Изучили свойства по умолчанию интерфейса FastEthernet, который используется компьютером PC-A: 
Switch# show interface f0/6
**FastEthernet0/6 is up, line protocol is up (connected)**
Hardware is Lance, address is 00d0.58ed.b306 (bia 00d0.58ed.b306)
BW 100000 Kbit, DLY 1000 usec,
reliability 255/255, txload 1/255, rxload 1/255
Encapsulation ARPA, loopback not set
Keepalive set (10 sec)
**Full-duplex, 100Mb/s**
input flow-control is off, output flow-control is off
ARP type: ARPA, ARP Timeout 04:00:00
Last input 00:00:08, output 00:00:05, output hang never
Last clearing of "show interface" counters never
Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
Queueing strategy: fifo
Output queue :0/40 (size/max)
5 minute input rate 0 bits/sec, 0 packets/sec
5 minute output rate 0 bits/sec, 0 packets/sec
956 packets input, 193351 bytes, 0 no buffer
Received 956 broadcasts, 0 runts, 0 giants, 0 throttles
0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
0 watchdog, 0 multicast, 0 pause input
0 input packets with dribble condition detected
2357 packets output, 263570 bytes, 0 underruns

#### Интерфейс включен.
#### MAC-адрес у интерфейса: 00d0.58ed.b306
#### В интерфейсе заданы настройки скорости в 100Mb/s и дуплекса Full-duplex.

### Изучили флеш-память.
#### Выполнили команду Switch# show flash, чтобы изучить содержимое флеш-каталога.
1 -rw- 4670455 <no date> 2960-lanbasek9-mz.150-2.SE4.bin
64016384 bytes total (59345929 bytes free)
#### В конце имени файла указано расширение *.bin. Каталоги не имеют расширения файла.
#### Образу Cisco IOS присвоено имя  **2960-lanbasek9-mz.150-2.SE4.bin**
##

## Часть 2. Настройка базовых параметров сетевых устройств

### Шаг 1. Настроили базовые параметры коммутатора.

 - В режиме глобальной конфигурации скопировали следующие базовые параметры конфигурации и вставили их в файл на коммутаторе S1.
no ip domain-lookup
hostname S1
service password-encryption
enable secret class
banner motd #
Unauthorized access is strictly prohibited. #
 - Назначили IP-адрес (192.168.1.2) интерфейсу SVI на коммутаторе. Благодаря этому получили возможность удаленного управления коммутатором. Согласно конфигурации по умолчанию, коммутатором можно управлять через VLAN 1.

 - Доступ через порт консоли также следует ограничить с помощью пароля. Использовали **cisco** в качестве пароля для входа в консоль в этом задании. Конфигурация по умолчанию разрешает все консольные подключения без пароля. Чтобы консольные сообщения не прерывали выполнение команд, использовали параметр **logging synchronous**.

S1(config)# line con 0
S1(config-line)# logging synchronous

 - Настроили каналы виртуального соединения для удаленного управления (vty), чтобы коммутатор разрешил доступ через Telnet. Если не настроить пароль VTY, будет невозможно подключиться к коммутатору по протоколу Telnet.

Команда login нужна для включения доступа к VTY.

### Шаг 2 Настройка IP-адреса на компьютере PC-A.

#### Назначили компьютеру IP-адрес 192.168.1.2 и маску подсети 255.255.255.0 в соответствии с таблицей адресации.


![Lab1_8](https://github.com/Groly2741/OTUS-Labs-Grishaeva1/assets/164208420/4599a140-9d37-4f37-9a03-44e86617b9e3)

##
## Часть 3. Проверка сетевых подключений

### Шаг 1 Отображение конфигурации коммутатора.

#### Использовали консольное подключение на компьютере PC-A для отображения и проверки конфигурации коммутатора. Команда show run позволяет постранично отобразить всю текущую конфигурацию. Для пролистывания использовали клавишу пробела.
#### Пример конфигурации приведен ниже. 

Проверка параметров VLAN 1

S1# show interface vlan 1
S1#show run

Building configuration...

  

Current configuration : 1318 bytes

!

version 15.0

no service timestamps log datetime msec

no service timestamps debug datetime msec

service password-encryption

!

hostname S1

!

enable secret 5 $1$mERr$9cTjUIEqNGurQiFU.ZeCi1

!

!

!

no ip domain-lookup

!

!

!

spanning-tree mode pvst

spanning-tree extend system-id

!

interface FastEthernet0/1

!

interface FastEthernet0/2

!

interface FastEthernet0/3

!

interface FastEthernet0/4

!

interface FastEthernet0/5

!

interface FastEthernet0/6

!

interface FastEthernet0/7

!

interface FastEthernet0/8

!

interface FastEthernet0/9

!

interface FastEthernet0/10

!

interface FastEthernet0/11

!

interface FastEthernet0/12

!

interface FastEthernet0/13

!

interface FastEthernet0/14

!

interface FastEthernet0/15

!

interface FastEthernet0/16

!

interface FastEthernet0/17

!

interface FastEthernet0/18

!

interface FastEthernet0/19

!

interface FastEthernet0/20

!

interface FastEthernet0/21

!

interface FastEthernet0/22

!

interface FastEthernet0/23

!

interface FastEthernet0/24

!

interface GigabitEthernet0/1

!

interface GigabitEthernet0/2

!

interface Vlan1

ip address 192.168.1.2 255.255.255.0

!

banner motd ^C

Unauthorized access is strictly prohibited. ^C

!

!

!

line con 0

password 7 0822455D0A16

logging synchronous

login

!

line vty 0 4

password 7 0822455D0A16

login

line vty 5 15

password 7 0822455D0A16

login

!

!

!

!

end

#### Полоса пропускания этого интерфейса - BW 100000 Kbit

### Шаг 2 Тестирование сквозного соединения посредством эхо-запроса.

В командной строке компьютера PC-A с помощью утилиты ping проверили связь сначала с адресом PC-A.
C:\> ping 192.168.1.10
Из командной строки компьютера PC-A отправили эхо-запрос на административный адрес интерфейса SVI коммутатора S1.
C:\> ping 192.168.1.2

Поскольку компьютеру PC-A нужно преобразовать МАС-адрес коммутатора S1 с помощью ARP, время ожидания передачи первого пакета может истечь. Эхо-запрос прошёл успешно.

![Lab1_9](https://github.com/Groly2741/OTUS-Labs-Grishaeva1/assets/164208420/2f73a292-dcda-46f6-aa82-f243908bbab4)

#### Шаг 3 Проверка удалённого управления коммутатором S1.
#### Использовали удалённый доступ к устройству с помощью Telnet. В этой лабораторной работе устройства PC-A и S1 расположены рядом. В производственной сети коммутатор может находиться в коммутационном шкафу на последнем этаже, в то время как административный компьютер находится на первом этаже. На данном этапе нам предстоит использовать Telnet для удаленного доступа к коммутатору S1 через его административный адрес SVI. Telnet — это небезопасный протокол, но мы можем использовать его для проверки удаленного доступа. В случае с Telnet вся информация, включая пароли и команды, отправляется через сеанс в незашифрованном виде. 
##### a. Открыли программу эмуляции терминала с возможностью Telnet.
##### b. Выбрали сервер Telnet и указали адрес управления SVI для подключения к S1. Пароль: cisco.
##### c. После ввода пароля cisco оказались в командной строке пользовательского режима. Для перехода в исполнительский режим EXEC ввели команду enable и использовали секретный пароль class.
##### d. Сохранили конфигурацию.
##### e. Чтобы завершить сеанс Telnet, ввели exit. Закрыли окно настройки.

![Lab1_10](https://github.com/Groly2741/OTUS-Labs-Grishaeva1/assets/164208420/839fdac3-e9e4-4d83-9dce-0011e73f57f8)

##

### Необходимо настраивать пароль VTY для коммутатора, чтобы была возможность  подключиться к коммутатору по протоколу Telnet.
### Чтобы пароли не отправлялись в незашифрованном виде, их необходимо зашифровать с помощью команды service password-encryption в CLI.
