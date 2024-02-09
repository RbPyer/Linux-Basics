# Базовая работа на OC Linux (Ubuntu Server) by Oswyndel (school-21)



## Содержание:

1. [Установка ОС](#part-1-установка-ос)  
2. [Создание пользователя](#part-2-создание-пользователя)  
3. [Настройка сети ОС](#part-3-настройка-сети-ос)   
4. [Обновление ОС](#part-4-обновление-ос)  
5. [Использование команды  sudo](#part-5-использование-команды-sudo)  
6. [Установка и настройка службы времени](#part-6-установка-и-настройка-службы-времени)  
7. [Установка и использование текстовых редакторов](#part-7-установка-и-использование-текстовых-редакторов)  
8. [Установка и базовая настройка сервиса SSHD](#part-8-установка-и-базовая-настройка-сервиса-sshd)   
9. [Установка и использование утилит top, htop](#part-9-установка-и-использование-утилит-top-htop)   
10. [Использование утилиты fdisk](#part-10-использование-утилиты-fdisk)   
11. [Использование утилиты df](#part-11-использование-утилиты-df)    
12. [Использование утилиты du](#part-12-использование-утилиты-du)    
13. [Установка и использование утилиты ncdu](#part-13-установка-и-использование-утилиты-ncdu)    
14. [Работа с системными журналами](#part-14-работа-с-системными-журналами)     
15. [Использование планировщика заданий CRON](#part-15-использование-планировщика-заданий-cron)   




## Part 1. Установка ОС

 ---

**== Задание ==**

##### Установи **Ubuntu 22.04 Server LTS** без графического интерфейса. (Используем программу для виртуализации - VirtualBox)

- Графический интерфейс должен отсутствовать.

- Узнай версию Ubuntu, выполнив команду \
`cat /etc/issue.`
- Вставь скриншот с выводом команды.

 ---

Скачать iso-образ Ubuntu Server можно на их [официальном сайте](https://ubuntu.com/download/server).


- скриншот вывода ```cat /etc/issue```

![part1](screenshots/part1.png)


## Part 2. Создание пользователя

---

**== Задание ==**

##### Создай пользователя, отличного от созданного при установке. Пользователь должен быть добавлен в группу `adm`.

- Вставь скриншот вызова команды для создания пользователя.
- Новый пользователь должен быть в выводе команды \
`cat /etc/passwd`
- Вставь скриншот с выводом команды.

---


- скриншот вызова команды для создания пользователя. Для этого используем команду ```sudo adduser <new_user>```.
 После этого добавляем его в группу adm (нахождение в этой группе позволяет читать логи из директории ```/var/log```):
 ```
 sudo usermod -G -a <group> <user>
 ```

![part_2_1](screenshots/part2_1.png)
![part_2_1_1](screenshots/part_2_1_1.png)

P.S.
Полезные флаги для usergmod:

- ```-G``` - дополнительные группы, в которые нужно добавить пользователя
- ```-g``` - изменить основную группу для пользователя
- ```-R``` - удалить пользователя из группы.
-----

- скриншот вывода ```cat /etc/passwd```

![part_2_2](screenshots/part2_2.png)


## Part 3. Настройка сети ОС


---
**== Задание ==**

##### Задай название машины вида user-1.
##### Установи временную зону, соответствующую твоему текущему местоположению.  
##### Выведи названия сетевых интерфейсов с помощью консольной команды.
- В отчёте дай объяснение наличию интерфейса lo.  
##### Используя консольную команду, получи ip адрес устройства, на котором ты работаешь, от DHCP сервера. 
- В отчёте дай расшифровку DHCP.  
##### Определи и выведи на экран внешний ip-адрес шлюза (ip) и внутренний IP-адрес шлюза, он же ip-адрес по умолчанию (gw). 
##### Задай статичные (заданные вручную, а не полученные от DHCP сервера) настройки ip, gw, dns (используй публичный DNS серверы, например 1.1.1.1 или 8.8.8.8).  
##### Перезагрузи виртуальную машину. Убедись, что статичные сетевые настройки (ip, gw, dns) соответствуют заданным в предыдущем пункте.  

- В отчёте опиши, что сделал для выполнения всех семи пунктов (можно как текстом, так и скриншотами).
- Успешно пропингуй удаленные хосты 1.1.1.1 и ya.ru и вставь в отчёт скрин с выводом команды. В выводе команды должна быть фраза «0% packet loss».

---



- задаём название машины вида user-1. Для этого используем команду:
 ```sudo hostnamectl set-hostname <new host_name>```

![part_3_1_1](screenshots/part_3_1_1.png)

После перезагрузки изменения вступили в силу.

![part_3_1_2](screenshots/part_3_1_2.png)

- в ```systemd``` есть своя утилита для настройки даты и часового пояса - ```timedatectl```. 
Узнать текущий часовой пояс машины можно, выполнив команду ```timedatectl status```:

![part_3_2_1](screenshots/part_3_2_1.png)

- для просмотра всех имеющихся часовых зон мы можем выполнить команду ```timedatectl list-timezones```:

![part_3_2_2](screenshots/part_3_2_2.png)


- для изменения текущей часовой зоны выполним команду вида ```sudo timedatectl set-timezone <zone>```. После выполнения вновь выведем текущую часовую зону и увидим, что она действительно изменилась:

![part_3_2_2](screenshots/part_3_2_3.png)

----

### Справка о сетевых интерфейсах

**Сетевой интерфейс** - это точка взаимодействия между компьютером и сетью. Он представляет собой аппаратное или программное обеспечение, которое позволяет компьютеру подключаться к сети и обмениваться данными с другими устройствами.

Если говорить простыми словами, то сетевой интерфейс - это как дверь, через которую компьютер "выходит" в интернет или другую сеть. Без этой "двери" компьютер не сможет общаться с другими устройствами.

Сетевой интерфейс может быть физическим, например, сетевая карта в компьютере или Wi-Fi адаптер. Он также может быть программным, например, виртуальная сетевая карта в виртуальной машине или программное обеспечение, которое позволяет компьютеру подключаться к сети.


----


- чтобы вывести названия всех сетевых интерфейсов, используем встроенную утилиту ```ip```. Для компактного вывода информации о списке всех сетевых интерфейсов используем команду ```ip -br link show```:

![part_3_3_1](screenshots/part_3_3_1.png)

Мы видим, что один из сетевых интерфейсов - lo. Что это?


----
### Справка о lo

**Интерфейс lo (loopback)** - это виртуальный сетевой интерфейс, который присутствует на большинстве операционных систем. Он используется для тестирования сетевых приложений и сервисов, а также для обеспечения доступа к локальной машине из сети.

Если говорить простыми словами, то интерфейс lo - это как зеркало, которое позволяет компьютеру "увидеть" самого себя. Он позволяет отправлять и получать пакеты данных, которые не покидают компьютер.

Например, если вы хотите проверить, работает ли ваш веб-сервер, вы можете отправить запрос на адрес 127.0.0.1 (это стандартный IP-адрес для интерфейса lo), и ваш компьютер ответит на этот запрос.

Также интерфейс lo используется для обеспечения доступа к локальной машине из сети. Например, если вы хотите получить доступ к файлам на вашем компьютере из интернета, вы можете настроить перенаправление портов на интерфейс lo.


----

### Справка о DHCP
**DHCP (Dynamic Host Configuration Protocol)** - это протокол, который позволяет автоматически назначать IP-адреса устройствам в сети. 

Если говорить простыми словами, то DHCP - это как почтальон, который разносит письма (IP-адреса) по домам (компьютерам). 

Когда компьютер подключается к сети, он отправляет запрос на DHCP-сервер, который назначает ему IP-адрес. Этот адрес может быть временным или постоянным, в зависимости от настроек сервера. 

DHCP-сервер также может назначать другие параметры, такие как маска подсети, адрес шлюза и DNS-серверы. Это позволяет компьютерам в сети общаться друг с другом и получать доступ к интернету.

Таким образом, DHCP упрощает процесс настройки сети, так как не нужно вручную назначать IP-адреса каждому устройству.

----


- чтобы узнать ip-адрес устройства, полученный от DHCP-сервера, выполним команду ```cat /var/log/syslog | grep -i 'dhcp'```:


![part_3_4](screenshots/part_3_4.png)


Мы видим, что нашему устройству был присвоен адрес ```10.0.2.15/24```.

Также его можно узнать и чуть проще, выполнив команду ```ip addr show```:

![part_3_4_1](screenshots/part_3_4_1.png)



- Для того чтобы узнать внешний IP адрес cвоего устройства, можно открыть специальный сайт, который посмотрит, с какого IP Вы его открыли, и скажет его Вам. Один из таких сайтов - ifconfig.me. Обратимся к нему с помощью ```curl ifconfig.co``` и получим желаемый внешний ip-адрес:


![part_3_5](screenshots/part_3_5.png)


- чтобы узнать внутренний ip-адоес, выполним команду ```hostname -I```:

![part_3_5_1](screenshots/part_3_5_1.png)


----

В чём разница между внутренним и внешним ip-адресами?

**Внешний IP-адрес** - это адрес, который присваивается вашему устройству или сети провайдером интернет-услуг. Он позволяет другим устройствам в интернете находить и общаться с вашим устройством.

**Внутренний IP-адрес** - это адрес, который присваивается вашему устройству или сети внутри вашей локальной сети. Он используется только для обмена данными между устройствами в вашей сети.

Если говорить простыми словами, то внешний IP-адрес - это как ваш домашний адрес, который знают все в городе, а внутренний IP-адрес - это как номер вашей квартиры, который знают только ваши соседи.

----


- Попробуем задать статичные настройки ip, gw (gateway), DNS.

Что такое gw в данном контексте?

----
### Справка о Gateway


**Gateway в рамках компьютерных сетей** - это аппаратное или программное обеспечение, которое позволяет сопрягать разные компьютерные сети, использующие разные протоколы. Он конвертирует протоколы одного типа физической среды в протоколы другой физической среды. Например, при подключении компьютера к интернету обычно используется сетевой шлюз. Маршрутизатор (роутер) является одним из примеров аппаратных сетевых шлюзов. Основная задача сетевого шлюза - конвертировать протокол между сетями. Шлюз по умолчанию - это сетевой шлюз, на который пакет отправляется в том случае, если маршрут к сети назначения пакета не известен. Он применяется в сетях с хорошо выраженными центральными маршрутизаторами, в малых сетях, в клиентских сегментах сетей.‍

----


- Протокол DHCP автоматически присваивает устройству IP. Чтобы этого не происходило, необходимо отключить облачную инициализацию. Открываем файл конфигурации ```subiquity-disable-cloudinit-networking.cfg``` в каталоге ```/etc/cloud/cloud.cfg.d/``` и проверим отсутствие конфигурации:

  ```sudo vim /etc/cloud/cloud.cfg.d/subiquity-disable-cloudinit-networking.cfg```


![part_3_5_2](screenshots/part_3_5_2.png)


- Перейдём к конфигурации Netplan. **Netplan** - это относительно новая утилита для осуществления настройки сети в Ubuntu. Более подробно о ней можно прочитать [тут](https://habr.com/ru/articles/448400/ "статья на хабре"). В данном случае файл конфигурации - это ```oo-installer-config.yaml```. Откроем его в текстовом редакторе ```vim```:

```sudo vim /etc/netplan/00-installer-config.yaml```

![part_3_5_3](screenshots/part_3_5_3.png)

- Пропишем новые настройки для нашего конфигурационного файла *

![part_3_5_4](screenshots/part_3_5_4.png)


*, **где**:

- **version** — версия YAML. На момент обновления статьи, была 2.
- **ethernets** — настройка сетевых адаптеров ethernet.
- **ens3** — настройки для соответствующих сетевых адаптеров
- **dhcp4** — будет ли получать сетевой адаптер IP-адрес автоматически. Возможны варианты yes/true — получать адрес автоматически; no/false — адрес должен быть назначен вручную.
- **addresses** — задает IP-адреса через запятую.
- **routes** — настройка маршрутов. Для шлюза по умолчанию используем опцию и значение to: default. Ранее использовалась директива gateway4, но теперь она считается устаревшей (при применении настройки с ней система вернет предупреждение gateway4 has been deprecated, use default routes instead). Также обратите внимание на вариант с 0.0.0.0 — в более ранних версиях системы вариат с default выдаст ошибку, и нужно использовать конфигурацию с четыремя нулями.
- **nameservers** — настройка серверов имен (DNS).


- Затем сохраняем изменения с помощью команды ```netplan apply``` и перезагружаемся командой ```reboot```:


![part_3_5_5](screenshots/part_3_5_5.png)


- Проверяем полученные изменения командой ```cat /etc/netplan/00-installer-config.yaml```:

![part_3_5_6](screenshots/part_3_5_6.png)


-Успешно пингуем удаленные хосты 1.1.1.1 и ya.ru командами ```ping 1.1.1.1``` и ```ping ya.ru```:

![part_3_5_7](screenshots/part_3_5_7.png)


----

### Справка о ping


**ping** — утилита для проверки целостности и качества соединений в сетях. Утилита отправляет запросы указанному узлу сети и фиксирует поступающие ответы. Время между отправкой запроса и получением ответа позволяет определять двусторонние задержки по маршруту и частоту потери пакетов, то есть косвенно определять загруженность на каналах передачи данных и промежуточных устройствах.


----


## Part 4. Обновление ОС


---

**== Задание ==**

##### Обнови системные пакеты до последней на момент выполнения задания версии.  

- После обновления системных пакетов, если ввести команду обновления повторно, должно появиться сообщение, что обновления отсутствуют;
- Вставь скриншот с этим сообщением в отчёт.

---


- пакетный менеджер в дистрибутиве Ubuntu, как известно, - ```apt```. Для обновления всех пакетов, а также обновления информации из самого apt репозитория пропишем команду ```sudo apt update && sudo apt upgrade```:


![part_4_1](screenshots/part_4_1.png)

- после обновления продублируем команду выше и увидим отсутствие новых обновлений:

![part_4_2](screenshots/part_4_2.png)



## Part 5. Использование команды sudo

---

**== Задание ==**

##### Разреши пользователю, созданному в [Part 2](#part-2-создание-пользователя),выполнять команду sudo.

- В отчёте объясни *истинное* назначение команды sudo (про то, что это слово - «волшебное», писать не стоит);  
- Поменяй hostname ОС от имени пользователя, созданного в пункте [Part 2](#part-2-создание-пользователя) (используя sudo);
- Вставь скрин с изменённым hostname в отчёт.

---



----

### Справка о sudo


**Команда sudo** - substitute user and do, подменить пользователя и выполнить. Главное назначение sudo — это выполнить команду от имени другого пользователя, чаще всего от root. Смысл выполнения команды от root в том, что у него повышенные права доступа и, применяя sudo, обычный пользователь может выполнить те команды, на которые у него недостаточно прав доступа.

----

- проверим, что у пользователя ```alex```, созданного в Part 2, отсутствуют права sudo. Для этого напишем команду ```sudo -l -U alex```:

![part_5_1](screenshots/part_5_1.png)

- затем наделим ```alex``` правами sudo и сменим пользователя на alex с помощью команд ```sudo usermod -aG sudo alex``` и ```su alex```:

![part_5_2](screenshots/part_5_2.png)


- выполним изменение hostname на любое (в данном случае ```user-2```), после чего пропишем ```reboot```:

![part_5_3](screenshots/part_5_3.png)


## Part 6. Установка и настройка службы времени

---

**== Задание ==**

##### Настрой службу автоматической синхронизации времени.  

- Выведи время часового пояса, в котором ты сейчас находишься.
- Вывод следующей команды должен содержать `NTPSynchronized=yes`: \
  `timedatectl show`
- Вставь скрины с корректным временем и выводом команды в отчёт.

---

![part_6](screenshots/part_6.png)


## Part 7. Установка и использование текстовых редакторов

_`-` Только не плачь._

_`-` Ладно..._


---

**== Задание ==**

##### Установи текстовые редакторы **VIM** (+ любые два по желанию **NANO**, **MCEDIT**, **JOE** и т.д.)  
##### Используя каждый из трех выбранных редакторов, создай файл *test_X.txt*, где X -- название редактора, в котором создан файл. Напиши в нём свой никнейм, закрой файл с сохранением изменений.  
- В отчёт вставь скриншоты:
  - Из каждого редактора с содержимым файла перед закрытием;
- В отчёте укажи, что сделал для выхода с сохранением изменений.
##### Используя каждый из трех выбранных редакторов, открой файл на редактирование, отредактируй файл, заменив никнейм на строку «21 School 21», закрой файл без сохранения изменений.
- В отчёт вставь скриншоты:
    - Из каждого редактора с содержимым файла после редактирования;
- В отчёте укажи, что сделал для выхода без сохранения изменений.
##### Используя каждый из трех выбранных редакторов, отредактируй файл ещё раз (по аналогии с предыдущим пунктом), а затем освой функции поиска по содержимому файла (слово) и замены слова на любое другое.
- В отчёт вставь скриншоты:
    - Из каждого редактора с результатами поиска слова;
    - Из каждого редактора с командами, введёнными для замены слова на другое.

---


- Для установки текстовых редакторов выполним команду ```sudo apt install vim && sudo apt install nano && sudo apt install mcedit```


### Для vim:

- ```vim test_vim.txt```. Чтобы внести изменения - ```I```, чтобы сохранить изменения - ```esc -> shift + : -> wq```. ```wq``` - write and quite.

![part_7_1](screenshots/part_7_1.png)


- для выхода без изменений - ```esc -> shift + : -> q!```. Проверим, что изменения не сохранились:

![part_7_2](screenshots/part_7_2.png)
![part_7_3](screenshots/part_7_3.png)

- Поиск: ```Esc + /<word_to_search>```; Замена: ```:%s/<change_this>/<to_this>```:

![part_7_4](screenshots/part_7_4.png)
![part_7_5](screenshots/part_7_5.png)


### Для nano:

- Для выхода с сохранением нужно выполнить ```Ctrl + O```, затем ```Ctrl + X```:

![part_7_6](screenshots/part_7_6.png)

- Для выхода без сохранения нужно нажать ```Esc```, затем ```Ctrl + X```:

![part_7_7](screenshots/part_7_7.png)
![part_7_8](screenshots/part_7_8.png)

- Поиск: ```Ctrl + W``` 

![part_7_9](screenshots/part_7_9.png)

- Замена: ```Ctrl + \```

![part_7_10](screenshots/part_7_10.png)
![part_7_11](screenshots/part_7_11.png)
![part_7_12](screenshots/part_7_12.png)


### MCEdit


- Для выхода с сохранением необходимо нажать ```F10``` и выбрать ```yes```:
![part_7_13](screenshots/part_7_13.png)


- Для выхода с сохранением необходимо нажать ```F10``` и выбрать ```no```:

![part_7_14](screenshots/part_7_14.png)
![part_7_15](screenshots/part_7_15.png)



- Поиск: ```F7```; Замена: ```F4```

![part_7_16](screenshots/part_7_16.png)
![part_7_17](screenshots/part_7_17.png)
![part_7_18](screenshots/part_7_18.png)
![part_7_19](screenshots/part_7_19.png)




## Part 8. Установка и базовая настройка сервиса SSHD


---

**== Задание ==**

##### Установи службу SSHd.  
##### Добавь автостарт службы при загрузке системы.  
##### Перенастрой службу SSHd на порт 2022.  
##### Используя команду ps, покажи наличие процесса sshd. Для этого к команде нужно подобрать ключи.
- В отчёте объясни значение команды и каждого ключа в ней.
##### Перезагрузи систему.
- В отчёте опиши, что сделал для выполнения всех пяти пунктов (можно как текстом, так и скриншотами).
- Вывод команды netstat -tan должен содержать  \
`tcp 0 0 0.0.0.0:2022 0.0.0.0:* LISTEN`  \
(если команды netstat нет, то ее нужно установить)
- Скрин с выводом команды вставь в отчёт.
- В отчёте объясни значение ключей -tan, значение каждого столбца вывода, значение 0.0.0.0.

---




- Служба ```sshd``` отвечает за обработку входящих подключений к серверу по VPN. Для её установки выполним команду ```sudo apt install openssh-server```. Для добавления в автозагрузку пропишем ```sudo systemctl enable ssh```. Проверим статус службы командой ```systemctl status ssh```:

![part_8_1](screenshots/part_8_1.png)

- Для перенастройки службы SSHd откроем файл sshd_config командой ```sudo vim /etc/ssh/sshd_config```. По умолчанию порт будет задан 22, изменим его на 2022:

![part_8_2](screenshots/part_8_2.png)
![part_8_3](screenshots/part_8_3.png)

- Используя команду ```ps```, покажем наличие процесса ```sshd```. ```ax``` – будут показаны все процессы подробно. ```u``` — выводит пользователя и еще доп информацию. ```grep sshd``` выводит только те строчки, где есть ```sshd```:

![part_8_4](screenshots/part_8_4.png)

- Пропишем ```reboot```, а затем ```netstat -tan```:


![part_8_5](screenshots/part_8_5.png)


----
### Справка о netstat

**netstat** (network statistics) — утилита командной строки, выводящая на дисплей состояние TCP-соединений (как входящих, так и исходящих), таблицы маршрутизации, число сетевых интерфейсов и сетевую статистику по протоколам.

Для установки netstat выполним команду:
```sudo apt install net-tools```

Команда netstat показывает статистику приема и отправки пакетов, а также информацию об ошибках приема и отправки.
-a - Вывод всех активных подключений TCP и прослушиваемых компьютером портов TCP и UDP.
-n - Вывод активных подключений TCP с отображением адресов и номеров портов в числовом формате без попыток определения имен.
Тогда, если netstat -na - просмотр всех открытых протоколов, то netstat -tan - просмотр всех открытых ТСР-протоколов.

----



## Part 9. Установка и использование утилит top, htop


---

**== Задание ==**

##### Установи и запусти утилиты top и htop.  

- По выводу команды top определи и напиши в отчёте:
  - uptime
  - количество авторизованных пользователей
  - общую загрузку системы
  - общее количество процессов
  - загрузку cpu
  - загрузку памяти
  - pid процесса занимающего больше всего памяти
  - pid процесса, занимающего больше всего процессорного времени
- В отчёт вставь скрин с выводом команды htop:
  - отсортированному по PID, PERCENT_CPU, PERCENT_MEM, TIME
  - отфильтрованному для процесса sshd
  - с процессом syslog, найденным, используя поиск 
  - с добавленным выводом hostname, clock и uptime  

---



- утилиты ```top``` и ```htop``` предназначены для управления процессами, запущенными на устройстве. 


### top


![part_9_1](screenshots/part_9_1.png)

---

Колонки, которые выводит программа очень похожи на ps:

- **PID** - идентификатор процесса;
- **USER** - имя пользователя, от имени которого выполняется процесс;
- **PR** - приоритет планировщика, установленный для процесса;
- **NI** - рекомендуемый приоритет процесса. Это значение можно менять, может не совпадать с реальным приоритетом планировщика;
- **VIRT** - всё, что находится в памяти, используется или зарезервировано для использования;
- **RES** - всё, что находится в оперативной памяти и относится к процессу. Расшифровывается как Resident Memory Size, указывается в килобайтах;
- **SHR** - часть памяти из RES, которую занимают ресурсы, доступные для использования другим процессам. Расшифровывается - Shared Memory Size.
- **S** - состояние процесса: D - ожидает завершения операции, R - запущен, S - спит, T - остановлен, t - остановлен отладчиком, Z - зомби;
- **%CPU** - процент использования ресурсов процессора;
- **%MEM** - процент использования ресурсов оперативной памяти на основе колонки RES;
- **TIME** - обще процессорное время, которое процесс использовал с момента запуска;
- **COMAND** - команда, с помощью которой был запущен процесс.

---


- uptime - 19 мин
- количество авторизованных пользователей - 1
- общую загрузку системы - 0
- общее количество процессов - 99
- загрузка cpu - 0%
- загрузку памяти - 171.4 из 1964.1
- pid процесса занимающего больше всего памяти - 1
- pid процесса, занимающего больше всего процессорного времени - 1042



### htop
- htop сортируется следующим образом: ```htop --sort-key PID```

- сортировка по ```PID```:

![part_9_2](screenshots/part_9_2.png)

- сортировка по ```PERCENT_CPU```:

![part_9_3](screenshots/part_9_3.png)


- сортировка по ```PERCENT_MEM```:

![part_9_4](screenshots/part_9_4.png)


- сортировка по ```TIME```:

![part_9_5](screenshots/part_9_5.png)



- фильтрация для процесса ```sshd```:

![part_9_6](screenshots/part_9_6.png)


- вывод с процессом ```syslog```, найденным с помощью поиска:

![part_9_7](screenshots/part_9_7.png)


- вывод с добавленными ```hostname```, ```clock``` и ```uptime```

![part_9_8](screenshots/part_9_8.png)




## Part 10. Использование утилиты fdisk

---

**== Задание ==**

##### Запусти команду fdisk -l.

- В отчёте напиши название жесткого диска, его размер и количество секторов, а также размер swap.

---



- пропишем ```fdisk -l```:

![part_10](screenshots/part_10.png)


> Название диска: VBOX HARDDISK  
> Размер диска: 15.34 Гигабайт  
> Количество секторов: 32159840  
> Размер swap:  512 байт


## Part 11. Использование утилиты df

---

**== Задание ==**

##### Запусти команду df.  
- В отчёте напиши для корневого раздела (/):
  - размер раздела
  - размер занятого пространства
  - размер свободного пространства
  - процент использования
- Определи и напиши в отчёт единицу измерения в выводе.  

##### Запусти команду df -Th.
- В отчёте напиши для корневого раздела (/):
    - размер раздела
    - размер занятого пространства
    - размер свободного пространства
    - процент использования
- Определи и напиши в отчёт тип файловой системы для раздела.

---

### Справка об утилите df

**df** -  утилита в UNIX и UNIX-подобных системах, показывает список всех файловых систем по именам устройств, сообщает их размер, занятое и свободное пространство и точки монтирования.  

Основные опции утилиты:

- ```-a```, ```--all``` - отобразить все файловые системы, в том числе виртуальные, псевдо и недоступные;
- ```-B``` - изменить размер одного блока перед выводом данных, например, можно использовать BM, чтобы вывести все данные в мегабайтах;
- ```-h``` - выводить размеры в читаемом виде, в мегабайтах или гигабайтах;
- ```-H``` - выводить все размеры в гигабайтах;
- ```-i``` - выводить информацию об inode;
- ```-k``` - выводить размеры в килобайтах;
- ```--output``` - использовать специальный формат вывода, если не задано, выводит все поля. Доступны такие варианты: 'source', 'fstype', 'itotal', 'iused', 'iavail', 'ipcent', 'size', 'used', 'avail', 'pcent', 'file' и 'target';
- ```-P``` - использовать формат вывода POSIX;
- ```--total``` - выводить всю информацию про использованное и доступное место;
- ```-t```, ```--type``` - выводить информацию только про указанные файловые системы;
- ```-x``` - выводить информацию обо всех, кроме указанных файловых систем;

---

- вывод ```df```:

![part_11_1](screenshots/part_11_1.png)

для корневого раздела (/):
- размер раздела - 10218772
- размер занятого пространства - 5022600
- размер свободного пространства - 4655500
- процент использования - 52%
- единица измерения - Килобайт


- вывод ```df -Th```:

![part_11_2](screenshots/part_11_2.png)


для корневого раздела (/):
- размер раздела - 9.8
- размер занятого пространства - 4.8
- размер свободного пространства - 4.5
- процент использования - 52%
- единица измерения - Гигабайт



## Part 12. Использование утилиты du

---

**== Задание ==**

##### Запусти команду du
##### Выведи размер папок /home, /var, /var/log (в байтах, в человекочитаемом виде)
##### Выведи размер всего содержимого в /var/log (не общее, а каждого вложенного элемента, используя *)

- В отчёт вставь скрины с выводом всех использованных команд.

---



**du** (аббревиатура от англ. disk usage) — стандартная Unix-программа для оценки занимаемого файлового пространства. 


- вывод команды ```du```:

![part_12_1](screenshots/part_12_1.png)


- размер папок ```/home```, ```/var```, ```/var/log``` (в байтах, в человекочитаемом виде):

![part_12_2](screenshots/part_12_2.png)

- размер всего содержимого в ```/var/log``` (не общее, а каждого вложенного элемента, используя *):

![part_12_3](screenshots/part_12_3.png)
![part_12_4](screenshots/part_12_4.png)


## Part 13. Установка и использование утилиты ncdu

---

**== Задание ==**

##### Установи утилиту ncdu
##### Выведи размер папок /home, /var, /var/log

- Размеры должны примерно совпадать с полученными в [Part 12](#part-12-использование-утилиты-du).

- В отчёт вставь скрины с выводом использованных команд.

---




**Ncdu (NCurses Disk Usage)** является инструментом командной строки для просмотра и анализа использования дискового пространства на Linux. Он может показать древовидные каталоги и дать отчет о свободном  пространстве на HDD, используемого в отдельных каталогах. Таким образом, очень легко отследить сколько занимает места файлы / каталоги. 


- ```ncdu /home```:

![part_13_1](screenshots/part_13_1.png)


- ```ncdu /var```:

![part_13_2](screenshots/part_13_2.png)


- ```ncdu /var/log```:

![part_13_3](screenshots/part_13_3.png)



## Part 14. Работа с системными журналами


---

**== Задание ==**

##### Открой для просмотра:
##### 1. /var/log/dmesg
##### 2. /var/log/syslog
##### 3. /var/log/auth.log  

- Напиши в отчёте время последней успешной авторизации, имя пользователя и метод входа в систему;
- Перезапусти службу SSHd;
- Вставь в отчёт скрин с сообщением о рестарте службы (искать в логах).

---


- ```/var/log/dmesg``` — драйвера устройств. Одноименной командой можно просмотреть вывод содержимого файла. Размер журнала ограничен, когда файл достигнет своего предела, старые сообщения будут перезаписаны более новыми.

![part_14_1](screenshots/part_14_1.png)


- ```/var/log/syslog``` — глобальный системный журнал, в котором пишутся сообщения с момента запуска системы, от ядра Linux, различных служб, обнаруженных устройствах, сетевых интерфейсов и много другого.

![part_14_2](screenshots/part_14_2.png)


- ```/var/log/auth.log``` — информация об авторизации пользователей, включая удачные и неудачные попытки входа в систему, а также задействованные механизмы аутентификации.

![part_14_3](screenshots/part_14_3.png)

Активацию sudo не будем считать за авторизацию. Тогда:  

> Последняя успешная авторизация: Jan 31 17:00:16  
> Имя пользователя: neuron  
> Метод входа в систему: by uid = 0 (User Identifier). Суперпользователь всегда должен иметь UID, равный нулю (0).


- перезапустим службу sshd ```systemctl restart sshd``` и увидим это в логах:

![part_14_4](screenshots/part_14_4.png)


## Part 15. Использование планировщика заданий CRON

---

**== Задание ==**

##### Используя планировщик заданий, запусти команду uptime через каждые 2 минуты.
- Найди в системных журналах строчки (минимум две в заданном временном диапазоне) о выполнении;
- Выведи на экран список текущих заданий для CRON;
- Вставь в отчёт скрины со строчками о выполнении и списком текущих задач.

##### Удали все задания из планировщика заданий.
- В отчёт вставь скрин со списком текущих заданий для CRON.

---




```Cron``` - это сервис, как и большинство других сервисов Linux, он запускается при старте системы и работает в фоновом режиме. Его основная задача выполнять нужные процессы в нужное время. Существует несколько конфигурационных файлов, из которых он берет информацию о том что и когда нужно выполнять. Сервис открывает файл /etc/crontab, в котором указаны все нужные данные. 


- команда ```crontab -e``` открывает временный файл, в котором уже представлены все текущие задания cron (можно добавить новые) для текущего пользователя.  

![part_15_1](screenshots/part_15_1.png)


- команда ```crontab -l``` выводит список текущих заданий cron:

![part_15_3](screenshots/part_15_3.png)

- пронаблюдаем в логах uptime каждые 2 минуты:

![part_15_2](screenshots/part_15_2.png)


- удалим все задания из планировщика заданий:

![part_15_4](screenshots/part_15_4.png)


