

NAS - файлопомойка, на которой аноним может хранить терабайты полезной нагрузки. Можно сделать из говна и палок, и плакать **когда** (не если, а когда) рейд бесповоротно сдохнет, или можно попробовать сделать его отказоустойчивым, насколько это возможно. Для этого тебе навряд ли хватит этой вики, но как отправная точка она пойдёт. 
100% гарантий сохранности данных он не обеспечит в любом случае, поэтому **важное** всегда нужно **бэкапить** на отдельный носитель, например, внешний хард, флешку, оптический диск; запаковать в зашифрованный архив с большим ключом или LUKS/VeraCrypt криптоконтейнер, и залить на бесплатное облако. А лучше бекапить важное сразу в несколько разных мест. Вытащить данные со сдохшего рейда практически невозможно. А ещё все здесь написанное - опыт рандомного хуя, и он может в чём-то ошибиться.  
Тебя предупредили.  

С другой стороны, хорошо сделанный NAS будет всяко понадежней и пообъемней твоего харда. Он продолжит работать даже когда сдохнут два или более диска в нем (зависит от конфига рейда), и кроме как файлопомойка, доступная с любого устройства в твоей локалке, может долгие годы служить твоим домашним сервером, с которого ты сможешь стримить аниму на телевизор/телефон/планшет, качать и круглосуточно раздавать торренты, добавляя их хоть с телефона; на нем ты сможешь поднять свою парашу, сделать хранилище доступным из интернета, защитить данные от шифровальщиков, поднять почтовик со спаморезалкой, jabber-сервер, и т.д. Его возможности ограничены только бюджетом, железом, твоими навыками, упорством и воображением.

Хранилище, как и любой другой пека, состоит из железа, софта и периферии:

1. Железо
	- Корпус
	- Харды 
	- Мать
	- Процессор
	- Оперативная память
	- Блок питания
	- Охлаждение
	- SAS-контроллер (необязательно)
	- Кабели
2. Софт
	- ОС
	- Программный RAID
	- Службы (их комбинации бесконечны, нет смысла перечислять)
3. Периферия
	- Источник бесперебойного питания (UPS)

Готовые NAS либо стоят слишком дорого, либо слишком немощные. Оптимальнее собрать самому.

### 1. Железо

#### Корпус

Корпус хранилища должен вмещать все комплектующие, в том числе и все харды. Харды должны охлаждаться ниже 40C в работе. Остальное - дело вкуса, вариантов много. Можно и нужно брать б/у.  
Хорошо, если в нем есть корзина для хардов с доступом снаружи для быстрой замены, но домашний NAS пойдет и без этого, ведь всегда можно его выключить, разобрать и обслужить. За удобство придется доплатить, бюджет можно потратить на детали поважнее.  
Некоторые корпуса, например, Node304, имеют внутренние корзины с виброподвесами, чтобы харды не так шумели. Вместо этого вполне можно заюзать резиновые проставки под болты, крепящие харды к корпусу. Блоки питания, поставляемые вкупе с корпусами, обычно откровенно хуёвые, и их придется заменить, поэтому тоже нахуй. Про это [чуть дальше][psu].

На али и ебее продаются внутренние корзины для хардов (HDD Cage Rack), которые можно закрепить внутри системника, и на которые можно повесить кулер. Например, такая хуйня: ![](https://raw.githubusercontent.com/Autism-Corporation/Cheburnet-information-for-Anon-from-Anon/master/pic/nas%20korzina.jpg)

Учти, что размер корпуса ограничит выбор матерей по их форм-фактору. Я вот, например, заебался искать mini-itx мамку с поддержкой ecc оперативки для корпуса node304, но результат того стоил. Разумнее все же будет купить корпус хотя бы под microATX.

#### Харды (носители данных)

Вообще могут использоваться любые носители, не ограничиваясь хардами, но по цене за гигабайт харды в 2019 году лидируют.

На хардах лучше не экономить и брать новые.

Для файлопомойки подойдут "зеленые" серии на <6k rpm (rotations per second), они тише, меньше греются и меньше вибрируют, чем >6k rpm. Но вообще похуй, смотри по бюджету, отзывам и здравому смыслу. Шум важен не всем, NAS можно поставить в дальний угол халупы, и пусть он себе шумит там.  
[По статистике](https://www.backblaze.com/blog/2018-hard-drive-failure-rates/) и по опыту одного хуя (меня) меньше всего подводят харды HGST и Toshiba. WD купили HGST, поэтому я бы смотрел на старые модели, которые выпускались именно под брендом HGST. А лучше Toshiba.  
Seagate однозначно идет лесом, лично видел больше десяти дохлых на работе, в том числе и в своем системнике.
WD не использовал, говорят что у них проблемы с парковкой головок и что они тоже сыпятся. Кто-то рекомендует, хуй знает. Все харды сыпятся рано или поздно.  
Для своего NAS брал шесть 3ТБ Toshiba HDWD130UZSVA, проблем за полгода ещё не было.

Если собираешься собирать RAID, лучше закажи диски одного объема из разных партий. Например, модель одна и та же, а партии разные. Так меньше вероятность нарваться на одновременный отказ сразу нескольких дисков. Попроси об этом в комментарии к заказу или вообще закажи по телефону.

Размер 3.5" харда: 101.6 x 26.1 x 147 мм ШxВxД

Ёмкими дисками потребительского класса лучше не увлекаться, т.к. у них по спецификации допустимый Unrecoverable error rate == 1 per 10E14 bits read, то бишь один бит на каждые прочтённые 11.3687 ТБайт. Фактический рейт может быть ещё выше, это аукнется при ребилде рейда, когда вместо полезной инфы из блока четности восстановится мусор и появится тихое повреждение данных, которое хуй обнаружишь, если не используешь файловую систему с проверкой контрольных сумм блоков, вроде ZFS. [Об этом написано дальше][zfs]. А то и ребилд зафейлится, и есть риск потерять весь рейд целиком без возможности восстановления если повредится блок с метаданными.

[Цитата:](https://www.ixbt.com/storage/nas-howto-part2.shtml)
> Пусть у нас есть RAID 5 из пяти 3Т-дисков, в котором один из дисков отказал. Массив надо перестраивать, при этом придется прочитать 4 диска × 3T = 12Т =1,2·10^13 байт = 0,96·10^14 бит информации, причем независимо от степени заполнения массива — ведь на уровне RAID о файлах ничего неизвестно. Исправные диски пользовательского класса имеют законное право дать один сбой в среднем на 1·10^14 бит (см. напр. спецификации WD Red). То есть с очень большой вероятностью мы получим сбой реконструкции просто по спецификации диска.

Диски корпоративного класса имеют URE 1*10^15, то бишь каждый бит за 113.6868 прочтенных ТБайт. Это круто, но такие диски стоят слишком дохуя для домашнего NAS. Выходом может быть использование файловых систем с контрольными суммами блоков [ZFS][zfs] и избыточное резервирование на уровне [RAID][raid]. Например, зеркала raid1, или отдать под четность два харда из массива в raid6 или даже целых три в raid7.

#### Мать

Можно попробовать взять б/у, предварительно хорошо протестировав линпаком, мемтестом с заведомо рабочими планками оперативы, и другими стресс-тестами час-другой, но лучше все же не рисковать. На мамке, бывает, вздуваются конденсаторы и летят цепи питания, отваливаются разъемы на задней панели. Может наебнуться сокет если какой-нибудь сильный долбоеб неправильно вставлял в него процессор, или ещё что-нибудь. Я в мамках не спец, поэтому не рисковал и брал "типа новую" с авиты ASRock Rack E3C226D2I под LGA1150 сокет, т.к. был доступен такой процессор.

Хорошо, если на мамке есть много sata-разъемов, штук так от шести. Отлично, если мамка поддерживает ECC-оперативку (ZFS без неё поднимать себе дороже). Охуительно, если в NAS используется мать серверного класса, например, штеуд или asrock rack; обычно на таких мамках нет аудиоразъемов, зато есть годные цепи питания, сетевые адаптеры и чипсеты, плюс BMC бонусом, который есть KVM over IP с возможностью смонтировать iso-образ по сети как диск в приводе.

Выбор мамки ограничивается форм-фактором корпуса, сокетами доступных процессоров и типом памяти.  
Я вот напоролся, когда решил сэкономить и взял сначала относительно дешевый xeon под 1155, а потом судорожно искал mini-itx мамку с поддержкой ECC памяти под него. Нашёл в ДС только одно объявление, да и то там intel-мамка оказалась нерабочей. Пришлось возвращать камушек продавцу, хорошо хоть он говниться не стал.

Кстати, мамки Pegatron сразу нахуй, ибо китайское говно, в котором даже в bios не зайти.

#### Процессор

Можно брать б/у, потестировав у продавца минут 20 линпаком. Хули ему будет-то, камушку?

Камушек обязан поддерживать ECC-оперативку, если собираешься использовать ZFS. У штеуда это все ветки Xeon, и, внезапно, все i3-камушки. У амуде ECC-память поддерживают все камушки. Но это не точно, на слово мне не верь, лучше сам посмотри даташиты на их сайтах. 

Для простой файлопомойки под ZFS хватит и двуядерного i3. Хочешь вдобавок перекодировать видео на лету или крутить пару легких виртуалок? Бери хотя бы младший Xeon. И т.д, ну ты понял. Про AMD не знаю, не использовал. Себе поставил e3-1231v3.

У i5 и i7 есть проблемы с перегревом под разгоном из-за говнопасты под крышкой вместо нормального припоя. Если уж припёрло гнать, гугли скальпирование и жидкий металл с герметиком. Есть риск расколоть камень кривыми руками. Я не гнал, ибо нахуй нужно на NAS? i5, i7 и atom не поддерживают ECC память. По производительности Ivy Bridge не сильно уступает Haswell'у, судя по бенчам; стоит значительно дешевле, но и мамку под него найти труднее. Mini-ITX мамок с поддержкой ECC под 1155 и вовсе не найти в ДС в 2019 году.

#### Оперативная память

Можно брать б/у, если memtest не нашёл ошибок за ночь, или хотя бы за полчаса-час. 

**ОСТОРОЖНО, НЕ ОБЪЕБИСЬ!** Если собрался брать ECC-память, проверь что и мамка, и процессор поддерживают такой тип памяти. ECC бывает нескольких видов: небуферизированная (unbuffered, UDIMM) и регистровая буферизированная (RDIMM, FB-DIMM, LR-DIMM). [См. вики: Registered memory](https://en.wikipedia.org/wiki/Registered_memory)

Буферизированная память поддерживается камнями xeon класса e5-* и выше. Такая память стоит дешевле, т.к. её просто дохуя на рынке, но процессор и мать под неё стоят дороже.  
e3-* и i3-* поддерживают только unbuffered ECC (UDIMM). Её меньше на рынке, и она стоит дороже буферизированной. С трудом нашёл и взял сильно б/у 2x8GB UDIMM DDR3, вытащенной из какой-то циски.

#### Блок питания

На БП экономить себе дороже. Хороший БП не греется и не шумит, т.к. имеет высокий КПД, выдает стабильное напряжение и ток; а в случае проблем в электросети или из-за старости подохнет сам, и не потянет за собой остальное, и без того недешёвое железо. Такой БП без проблем поддерживает перепады входного напряжения от 110 до 230 вольт. Лучше брать новый, со временем они приходят в негодность: высыхают/вздуваются конденсаторы, изнашивается кулер.

Хорошими БП считаются те, которые имеют сертификат 80+Gold и выше. Ну или хотя бы 80+Silver. Но лучше Gold+.
Выбирал по [расфасованному списку БП](https://docs.google.com/spreadsheets/d/1bEcFiMdLWPtPu3c1JsvsLIbcYANlLUVO1ICQdh-jxsg/edit#gid=0), которым поделился аноним из /hw/. Брал Chieftec GPM-550S. 

Для расчета мощности БП можно использовать какой-нибудь калькулятор, [вроде такого](https://outervision.com/power-supply-calculator). При этом ты посчитаешь предельную мощность БП. Он прослужит тебе дольше, если будет использоваться не в предельном-стрессовом режиме, а на ~30-50% номинальной мощности. Поэтому стоит умножить получившийся результат на 1.25. 

Вручную посчитать минимальную мощь БП по 12-вольтовой линии можно так:
	- 35 Вт для каждого харда 
	- ~6 Вт на каждую планку оперативки
	- ~10 Вт на HBA SAS-контроллер
	- TDP процессора
	- ~15-30 Вт на кулер
	- Ваттаж мамки
	- Сложить цифры выше и умножить это все на 1.25
Также стоит учесть, что харды при запуске потребляют на раскрутку около 2.1 Ампер на каждый. Умножь 2.1 на число хардов и убедись, что выбранный тобой БП обеспечивает в номинальном режиме такой ток.  
БП можно брать мощнее, чем расчитал, и потерями при хорошем КПД (80+Gold) можно принебречь.

#### Охлаждение
#### SAS-контроллер (необязательно)
#### Кабели


### 2. Софт
### 3. Периферия



### Источники

NAS для дома своими руками: https://www.ixbt.com/storage/nas-howto-part2.shtml


Для софтового рейда нужен бесперебойник для пека, см. дыра по записи RAID.
Не увлекаться емкими дисками:
> Пусть у нас есть RAID 5 из пяти 3Т-дисков, в котором один из дисков отказал. Массив надо перестраивать, при этом придется прочитать 4 диска × 3T = 12Т =1,2·1013 байт = 0,96·1014 бит информации, причем независимо от степени заполнения массива — ведь на уровне RAID о файлах ничего неизвестно. Исправные диски пользовательского класса имеют законное право дать один сбой в среднем на 1·1014 бит (см. напр. спецификации WD Red). То есть с очень большой вероятностью мы получим сбой реконструкции просто по спецификации диска.

Возможно, дешевле будет купить готовый NAS. Проверить.
30k - верхний предел. Нереально уложиться.

Минимальный размер бомжкорзины для 5 дисков:
	128 x 146 x 166 mm	https://ru.aliexpress.com/item/3-5-5x5-25-SATA-SAS-HDD-Cage-Rack/32898175441.html?spm=a2g0v.search0302.3.1.3b1d1c8cqzuRCm&ws_ab_test=searchweb0_0%2Csearchweb201602_0_453_10911_454_10914_10618_536_317_537_319_10059_10696_10084_10083_10887_10307_321_10889_322_10902_10065_10068_10301_10103_10884_10303_10820%2Csearchweb201603_0%2CppcSwitch_0&algo_pvid=fe6cc5d6-00df-409a-9aca-ac556ee719d0&algo_expid=fe6cc5d6-00df-409a-9aca-ac556ee719d0-0

Корпус:
	- mini-ITX Fractal Design Node 304 White - 6к, дохуя за корпус, но 6 отсеков 3.5" и охуенно выглядит.
		4 500 б/у
	
HDD:
	- Лучше брать "зеленые" серии на <6k rpm, они тише, меньше греются и меньше вибрируют, чем >6k rpm
	- Для системы нужен отдельный носитель (нужен ли?), хотя бы флешка или лучше low-end ssd в m.2
  3.5":
	101.6 x 26.1 x 147 mm ШxВxД
	- 3 TB 5k Toshiba HDWD130UZSVA <--
	- 3 TB 5.5k пиздат, нет в продаже toshiba HDWA130UZSVA
	- 3 TB 6k toshiba HDWU130UZSVA
	
SATA misc:
	HBA:
		- говорят, что SATA-контроллеры все поголовно говно
		- говорят, что можно надеяться только на SAS-контроллеры от LSI, Avago, Broadcom
		- говорят, что использовать SATA port multiplier'ы - распространенная ошибка
		- можно поискать по авито б/у, в SAS-контроллере вроде нечему ломаться
		- к нему нужен Y-data кабель (два для шести хардов, не видел дешёвых кабелей кроме SFF-8087 -> 4xSATA+SideBand) (видел за 700 руб)
		- SFF8484->4xSATA дороги, от 1.1к на маркете, на авито ещё дороже
		- Использовать рекомендуют только SAS-2+:
			- SAS-1: 3.0 Gbit/s, introduced in 2004[6] (говно мамонта, может глючить с современным железом)
			- SAS-2: 6.0 Gbit/s, available since February 2009 (лучший кандидат для дома по цене/качеству)
			- SAS-3: 12.0 Gbit/s, available since March 2013
			- SAS-4: 22.5 Gbit/s called "24G",[7]standard completed in 2017[6][1]
	Y-power cable:
		> Molex connectors, are designed for significant currents (up to 11A). 
		> SATA power connectors are designed only for up to 4.5A.
		> Y-cables should connect to the source using a Molex connector, not a SATA connector, and should be limited to 3-4 drives
	SAS-controller:
		- SAS1 непригоден, т.к. ограничивает макс. размер диска до 2.2ТБ, ограничена полоса пропускания, это говно мамонта может быть хреново совместимо с современным железом, поэтому рассматривать только SAS2+
		- Для ZFS SAS-контроллер должен работать в режиме Host Bus Adapter (HBA), аппаратный RAID недопустим
	
Память:
	- желательно с ECC
	- не меньше 8 GB. Говорят, желательно 16GB. Подсчитать точное количество для ZFS на ZRAID2, 9 ТБ из 5x3TB
	Варианты:
		- https://www.avito.ru/moskva/tovary_dlya_kompyutera/8gb_2rx8_pc3_10600e_12800e_14900e_ecc_udimm_ddr3_501093370
		- https://www.avito.ru/moskva/tovary_dlya_kompyutera/pamyat_ddr_ddr2_ddr3_1103924729	
	> It is hard to go wrong with RAM from any of the big DRAM producers: Micron (and their Crucial
brand), Samsung and Hynix – in no particular order.
	- minimum 1GB per 1TB storage for ZFS
	- PC3 10600E 12800E 14900E ECC udimm DDR3
	- поддерживает DDR3L
	

Мать:
	- 203 x 170 mm max
	- необходимо с поддержкой ECC :(. Иначе при очередном scrub могут "восстановиться" ошибки, которых фактически нет.
	- опционально с поддержкой m2 под систему и SLOG 
	- рекомендуют NIC от Intel. Realtek нельзя, он несовместим с бздёй.
	- Можно б/у mini-ITX, miniDTX
	> около 6к, ASRock J4105-ITX - новая, современная, вряд ли подойдет.
	- BLACKLIST:
		- ASRock Rack C2750D4I/C2550D4I mass die-off (C2x50D4I boards)
		- Intel C2000 mass die-off
			> Intel’s C2000 SoCs manufactured up to early 2017 were prone to degrade...
	- 8k lga1150 Max. 2x8GB DDR3 ASRock Rack E3C226D2I - https://www.avito.ru/moskva/tovary_dlya_kompyutera/novaya_materinskaya_plata_dlya_nas_mini_itx_formata_1013028667
	- 5.5k lga1150 max 2x8GB UDIMM Asus P9D-I https://www.avito.ru/moskva/tovary_dlya_kompyutera/novye_materinskie_platy_asus_p9d-i_1110627276
	- Haswell mini-itx mboars with server chipsets: (222, 224, 226)
		- ASRock Rack E3C226D2I
		- ASRock Rack E3C224D2I
		- ASUS P9D-I
		
	
Проц:
	- x64 2+ cores 2.5GHz+
	- Intel Core i5 and Core i7, as well as consumer Atom, do not support ECC functionality :(
	- i3 is surprisingly supporting ECC
	LGA1150:
		- Intel Pentium G3220
		- Intel Core i3-4330
		- Intel Xeon E3-1220 v3
	LGA1151:
		- Intel Pentium G4400
		- Intel Pentium G4600
		- Intel Core i3-6300
		- Intel Xeon E3-1220 v5 and so forth
	embedded:
		- Intel C2550 (Avoton) - DDR3
		- Xeon-D
	- Внезапно выяснилось, что TDP у IvyBridge меньше, чем у Haswell на одних и тех же моделях, последние имеют более новую микроархитектуру и большее число транзисторов, но техпроцесс одинаковый - 22нм. При этом сейчас (2019) на авите зионы e3-1230v2 стоят в два раза дешевле, чем e3-1230v3. Прирост производительности у хасвелла мизерный, судя по бенчам. Осталось только mini-itx мамку найти под IB(1155) с ECC, что очень трудно. Я с трудом-то под 1150 сокет нашёл.
	- Оказалось, что матерей mini-itx с поддержкой ecc под 1155 не найти. Было одно только объявление, и там мать не работала. Обошёл весь Савёловский, но нихуя не нашёл. Пришлось возвращать процессор обратно, хорошо хоть продавец понимающий оказался и не стал говниться.
	
	

бп:
	- Подсчитать минимум мощи по 12 вольт. линии:
		- 35 watts for each drive: 35 x 6 = 210 - минимум для хардов
		- ~2.1 ампер на хард при старте > 13A
		- ~6 watts per stick of memory	
		- ~10 watts per LSI 8 port HBA
		- TDP процессора
		- ~15-30 watts per fan
		- ваттаж мамки
		- умножить это все на 1.25
	- As for efficiency, any decent contemporary PSU should do 80+ Gold
	- OCP at 40A for <=500W must be present! (over current protection)
	- не меньше 450W на шесть хардов с e3-1230v3 по примерной прикидке отсюда https://www.ixsystems.com/community/threads/proper-power-supply-sizing-guidance.38811/
	- Seasonic G-Series (рекомендует FreeNAS)
	- Corsair VS, CX and CS, should be avoided. Corsair RM and better should be decent choices
	- Калькулятор (занижает нужную мощь, рассматривать как минимум, который нужно умножить на 1.25 и ещё маленько): https://outervision.com/power-supply-calculator
	> In terms of watts, a supply that is running at about 30-50% of its rated load is likely to be within its peak efficiency window, but is also likely to be relatively unstressed, leading to a longer life and reduced likelihood of premature failure.
	> You also need to estimate (by adding up the start currents for all the drives, usually around 2 amps each, and then estimating other 12V loads such as fans, CPU's, etc.) the 12V load, and verify that that will remain under the rated capacity of the power supply. You can CHEAT at this by hooking up the system without powering on the drives, letting it run memtest86, and checking power consumption. Take the watts, divide by 12, and that's a bad overestimate of the maximum 12V amps that the base system takes. Then you add the peak amps for all the drives, maybe add 10% more, check against the power supply rating, and there you have an easily derived pass-or-fail.
	- Рекомендуют:
		- chieftec bdf
		- FSP 600PNR-I
		- THERMALTAKE TR2 S
	- Не рекомендуют:
		- БП от Aerocool
		
	
	
UPS:
	- Необходим! zpool может наебнуться при неправильном выключении. SLOG может недописаться без BBU.
	- 3.5k FSP AGA400 PPF2401701 Off-Line, 400VA/240W
	- только на ноду от UPS нужно минимум 600 VA, а ведь ещё есть и десктоп
	
Охлаждение:
	- Харды должны быть охлаждены ниже 40C.
	- 2 – передние 92-мм вентиляторы серии Silent R2 с гидравлическими подшипниками, 1300 об/мин (совместимо с 80-мм вентиляторами) – в комплекте.
	- 1 – задний 140-мм вентилятор серии Silent R2 с гидродинамическим подшипником, 1000 об/мин (совместимо с 120-мм вентиляторами) – в комплекте.
	- Кулер процессора высотой до 165мм
	

	
> My system has 32GB of DDR3-1600 Kingston ECC(KVR16E11K4/32) RAM, Supermicro X9SCM-F-O(IPMI support a plus) with dual Intel Gb NICs and VGA built-in, and an Intel E3-1230V2 CPU and uses only 35 watts idle with no hard drives. The motherboard, CPU, and RAM cost me about $700 USD(cheaper now) and provides amazing performance and reliability. If you want to save some money and still enjoy ECC the Pentium G2020 is an excellent option.
	
SLOG:
	- обязан иметь защиту от отключения питания (PLP power loss protection)
	- для домашней 1GBe сети, наверно, нахуй не нужен
	- SSD/Optane для SLOG
	- ~2.5k, 16GB Intel MEMPEK1W016GAXT
	- ~2.5k, 16GB Intel MEMPEK1W016GA01
	- чего-нибудь побольше, один хуй на 1GbE разницы не увижу
	- и вообще, нужен ли он мне? Всегда можно прикупить как апгрейд, если скорость без него не устроит.
	
	


	


ZFS требует: 8 GB RAM min! Лучше 16+GB. x64. ZFS умеет в дедупликацию (дедуп жрет раму как не в себя, дома не нужно). ZFS защищает^W помогает защититься от дыры по записи. К ней обязательно нужна ECC RAM и PLP на всех кешах и буферах (батарейки на контроллерах и SLOG, либо кеши на запись отключить, что приводит к снижению быстродействия). Контрольные суммы - это заебись, но это не спасет, если при очередном scrub будут "восстановлены" поврежденные данные из-за flipped bits in RAM due to "cosmic rays".
Бздя есть на AArch64, но поддержка вроде экспериментальная. Нахуй нужно, когда полно x64?


Софт:
	- Уведомления по email о smart и [продумать ещё о чем]
	- SMART monitoring
	- Автовыключение с уведомлением по email при UPS level < 60%
	- Регулярные scrub по крону каждые две недели
	- Scrub и SMART long test НИКОГДА не должны запускаться одновременно, иначе scrub никогда не закончится.
	- Сжатие LZ4 (говорят, что оно почти прозрачно по производительности, а место экономит. Поискать цифры)
	- ZIL в RAM (не нужен? ZIL is only useful for sync writes. For all other writes the ZIL is not used. This means if you aren’t using NFS and don’t have a workload that uses sync writes, a ZIL is pointless.)
	- Дедупликация (идет нахуй, требует слишком много рамы и ARC)

ZFS File System is called a Dataset. It is layered above ZPool.
ZPool: [vdev, vdev, ...] (ZPool - same as Volume)
	- If _ANY_ VDev in ZPool is failed then _ENTIRE_ ZPool is corrupted and can not be restored!
	- It's possible to add new VDevs to existing ZPool
VDev:
	- VDev is a group of disk drives that are allocated together and intended to work together as a single virtual device to store data.
	- VDev are allocated in RAIDZ formats (for R5 and R6 or Mirror for R0)
	- If VDev can't provide 100% of its data using checksums or mirrors, the VDev will fail. 
	- If any VDev in ZPool failed then entire ZPool is failed and can not be restored :(
ZIL: (ZFS Intent Log)
	- used for speeding up sync write (perhaps I don't need it for home NAS)
	- is a non-volatile write cache for zpool
	- Write speed matters. SSD is recommended for it.
	- SLOG - Separate SSD allocated for ZIL
	
	
	
Вероятность успешного ребилда:
https://en.wikipedia.org/wiki/RAID#URE
> ... unrecoverable bit error (UBE) rate is typically guaranteed to be less than one bit in 10^15 for enterprise-class drives ... and less than one bit in 10^14 for desktop-class drives
> an URE during a RAID 5 rebuild typically leads to a complete rebuild failure
-> RAID 5 is dead. Use smth else instead.

> https://www.datarc.ru/articles/pochemu-raid6-perestanet-rabotat.html
Вероятность не получить URE для R5 из 4 x 2ТБ = (1 – 1 /(24 414 062 500)) ^ (3*3 907 029 168) = 0,618724054
Pr <= (1 - (1/UREsc))^(Nrd * Dsc), where
	Pr 	  - Probabaility of successful RAID rebuild
	UREsc - sector count after which Unrecoverable Read Error will occur by disk specification
	Nrd   - Number of remaining working disks (for R5 = Ntotal - 1)
	Dsc	  - sector count of single disk in array (assuming minimum disk capacity)

For non-enterprise hard drives, NRE/URE rate is normally 1 per 10^14 bits read, which means that NRE/URE occurs every 11.37TB	

Либо большая вероятность восстановления и малый объем массива, либо наоборот. Либо стоимость массива увеличивается до космической.

[19:40] [] вот тут говорят, что при ошибке чтения при ребилде, ZFS пометит файл как поврежденный и позволит восстановить остальные файлы
[19:40] [] https://serverfault.com/questions/937547/if-a-raid5-system-experiences-a-ure-during-rebuild-is-all-the-data-lost
[19:42] [] другое дело, что остальные выжившие диски будут сильно нагружены и возрастает вероятность выхода из строя ещё одного из дисков, тогда уже совсем пиздец
[19:43] [] выходом может быть использование R6 или R7, но это ещё минус диск или два из общего объема

[20:46] [] Во, нашёл про потерю данных на R5
[20:47] [] Говорят, что он умер ещё в 2009
[20:47] [] https://www.ixsystems.com/community/threads/5x-4tb-raidz1-array-rebuilding-with-nre-ure-issue.13719/
[20:47] [] > 1. ZFS will continue the rebuild, but you will have some amount of corruption. It could range from a single file being corrupted to metadata corruption that causes a lot of files to be lost or the zpool to be unmountable(a loss of all data).
[20:47] [] > 5. Make a RAIDZ2/RAID6.
[20:49] [] > As long as you don't have a third disk in that "stripe" of data that has an error, then the recovery should proceed normally.

Есть и какой-то другой подход к подсчету вероятностей полной потери данных:
https://www.servethehome.com/raid-calculator/raid-reliability-calculator-simple-mttdl-model/
С ней RAIDZ2 из 5 х 3ТБ, если принять URE за 10^13 c пессимистичным MTBF 36.5к, полностью наебнется в течение трех лет с вероятностью 0.16533 %, 10 лет - 0.55002 %
С этим можно жить.

https://fiddle.jshell.net/Biduleohm/paq5u7z5/1/show/light/
Вот этот калькулятор говорит, что в таком конфиге свободным рекомендуют оставить 1.611 ТиБ, получится фактически поиметь 6.444 ТиБ вместо маркетологических 9 ТБ. Такие дела. 
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
***
Только NAS.

Для софтового рейда нужен бесперебойник для пека, см. дыра по записи RAID.
Не увлекаться емкими дисками:
> Пусть у нас есть RAID 5 из пяти 3Т-дисков, в котором один из дисков отказал. Массив надо перестраивать, при этом придется прочитать 4 диска × 3T = 12Т =1,2·1013 байт = 0,96·1014 бит информации, причем независимо от степени заполнения массива — ведь на уровне RAID о файлах ничего неизвестно. Исправные диски пользовательского класса имеют законное право дать один сбой в среднем на 1·1014 бит (см. напр. спецификации WD Red). То есть с очень большой вероятностью мы получим сбой реконструкции просто по спецификации диска.

Возможно, дешевле будет купить готовый NAS. Проверить.
30k - верхний предел. Нереально уложиться.

Минимальный размер бомжкорзины для 5 дисков:
	128 x 146 x 166 mm	https://ru.aliexpress.com/item/3-5-5x5-25-SATA-SAS-HDD-Cage-Rack/32898175441.html?spm=a2g0v.search0302.3.1.3b1d1c8cqzuRCm&ws_ab_test=searchweb0_0%2Csearchweb201602_0_453_10911_454_10914_10618_536_317_537_319_10059_10696_10084_10083_10887_10307_321_10889_322_10902_10065_10068_10301_10103_10884_10303_10820%2Csearchweb201603_0%2CppcSwitch_0&algo_pvid=fe6cc5d6-00df-409a-9aca-ac556ee719d0&algo_expid=fe6cc5d6-00df-409a-9aca-ac556ee719d0-0

Корпус:
	- mini-ITX Fractal Design Node 304 White - 6к, дохуя за корпус, но 6 отсеков 3.5" и охуенно выглядит.
		4 500 б/у
	
HDD:
	- Лучше брать "зеленые" серии на <6k rpm, они тише, меньше греются и меньше вибрируют, чем >6k rpm
	- Для системы нужен отдельный носитель (нужен ли?), хотя бы флешка или лучше low-end ssd в m.2
  3.5":
	101.6 x 26.1 x 147 mm ШxВxД
	- 3 TB 5k Toshiba HDWD130UZSVA <--
	- 3 TB 5.5k пиздат, нет в продаже toshiba HDWA130UZSVA
	- 3 TB 6k toshiba HDWU130UZSVA
	
SATA misc:
	HBA:
		- говорят, что SATA-контроллеры все поголовно говно
		- говорят, что можно надеяться только на SAS-контроллеры от LSI, Avago, Broadcom
		- говорят, что использовать SATA port multiplier'ы - распространенная ошибка
		- можно поискать по авито б/у, в SAS-контроллере вроде нечему ломаться
		- к нему нужен Y-data кабель (два для шести хардов, не видел дешёвых кабелей кроме SFF-8087 -> 4xSATA+SideBand) (видел за 700 руб)
		- SFF8484->4xSATA дороги, от 1.1к на маркете, на авито ещё дороже
		- Использовать рекомендуют только SAS-2+:
			- SAS-1: 3.0 Gbit/s, introduced in 2004[6] (говно мамонта, может глючить с современным железом)
			- SAS-2: 6.0 Gbit/s, available since February 2009 (лучший кандидат для дома по цене/качеству)
			- SAS-3: 12.0 Gbit/s, available since March 2013
			- SAS-4: 22.5 Gbit/s called "24G",[7]standard completed in 2017[6][1]
	Y-power cable:
		> Molex connectors, are designed for significant currents (up to 11A). 
		> SATA power connectors are designed only for up to 4.5A.
		> Y-cables should connect to the source using a Molex connector, not a SATA connector, and should be limited to 3-4 drives
	SAS-controller:
		- SAS1 непригоден, т.к. ограничивает макс. размер диска до 2.2ТБ, ограничена полоса пропускания, это говно мамонта может быть хреново совместимо с современным железом, поэтому рассматривать только SAS2+
		- Для ZFS SAS-контроллер должен работать в режиме Host Bus Adapter (HBA), аппаратный RAID недопустим
	
Память:
	- желательно с ECC
	- не меньше 8 GB. Говорят, желательно 16GB. Подсчитать точное количество для ZFS на ZRAID2, 9 ТБ из 5x3TB
	Варианты:
		- https://www.avito.ru/moskva/tovary_dlya_kompyutera/8gb_2rx8_pc3_10600e_12800e_14900e_ecc_udimm_ddr3_501093370
		- https://www.avito.ru/moskva/tovary_dlya_kompyutera/pamyat_ddr_ddr2_ddr3_1103924729	
	> It is hard to go wrong with RAM from any of the big DRAM producers: Micron (and their Crucial
brand), Samsung and Hynix – in no particular order.
	- minimum 1GB per 1TB storage for ZFS
	- PC3 10600E 12800E 14900E ECC udimm DDR3
	- поддерживает DDR3L
	

Мать:
	- 203 x 170 mm max
	- необходимо с поддержкой ECC :(. Иначе при очередном scrub могут "восстановиться" ошибки, которых фактически нет.
	- опционально с поддержкой m2 под систему и SLOG 
	- рекомендуют NIC от Intel. Realtek нельзя, он несовместим с бздёй.
	- Можно б/у mini-ITX, miniDTX
	> около 6к, ASRock J4105-ITX - новая, современная, вряд ли подойдет.
	- BLACKLIST:
		- ASRock Rack C2750D4I/C2550D4I mass die-off (C2x50D4I boards)
		- Intel C2000 mass die-off
			> Intel’s C2000 SoCs manufactured up to early 2017 were prone to degrade...
	- 8k lga1150 Max. 2x8GB DDR3 ASRock Rack E3C226D2I - https://www.avito.ru/moskva/tovary_dlya_kompyutera/novaya_materinskaya_plata_dlya_nas_mini_itx_formata_1013028667
	- 5.5k lga1150 max 2x8GB UDIMM Asus P9D-I https://www.avito.ru/moskva/tovary_dlya_kompyutera/novye_materinskie_platy_asus_p9d-i_1110627276
	- Haswell mini-itx mboars with server chipsets: (222, 224, 226)
		- ASRock Rack E3C226D2I
		- ASRock Rack E3C224D2I
		- ASUS P9D-I
		
	
Проц:
	- x64 2+ cores 2.5GHz+
	- Intel Core i5 and Core i7, as well as consumer Atom, do not support ECC functionality :(
	- i3 is surprisingly supporting ECC
	LGA1150:
		- Intel Pentium G3220
		- Intel Core i3-4330
		- Intel Xeon E3-1220 v3
	LGA1151:
		- Intel Pentium G4400
		- Intel Pentium G4600
		- Intel Core i3-6300
		- Intel Xeon E3-1220 v5 and so forth
	embedded:
		- Intel C2550 (Avoton) - DDR3
		- Xeon-D
	- Внезапно выяснилось, что TDP у IvyBridge меньше, чем у Haswell на одних и тех же моделях, последние имеют более новую микроархитектуру и большее число транзисторов, но техпроцесс одинаковый - 22нм. При этом сейчас (2019) на авите зионы e3-1230v2 стоят в два раза дешевле, чем e3-1230v3. Прирост производительности у хасвелла мизерный, судя по бенчам. Осталось только mini-itx мамку найти под IB(1155) с ECC, что очень трудно. Я с трудом-то под 1150 сокет нашёл.
	- Оказалось, что матерей mini-itx с поддержкой ecc под 1155 не найти. Было одно только объявление, и там мать не работала. Обошёл весь Савёловский, но нихуя не нашёл. Пришлось возвращать процессор обратно, хорошо хоть продавец понимающий оказался и не стал говниться.
	
	

бп:
	- Подсчитать минимум мощи по 12 вольт. линии:
		- 35 watts for each drive: 35 x 6 = 210 - минимум для хардов
		- ~2.1 ампер на хард при старте > 13A
		- ~6 watts per stick of memory	
		- ~10 watts per LSI 8 port HBA
		- TDP процессора
		- ~15-30 watts per fan
		- ваттаж мамки
		- умножить это все на 1.25
	- As for efficiency, any decent contemporary PSU should do 80+ Gold
	- OCP at 40A for <=500W must be present! (over current protection)
	- не меньше 450W на шесть хардов с e3-1230v3 по примерной прикидке отсюда https://www.ixsystems.com/community/threads/proper-power-supply-sizing-guidance.38811/
	- Seasonic G-Series (рекомендует FreeNAS)
	- Corsair VS, CX and CS, should be avoided. Corsair RM and better should be decent choices
	- Калькулятор (занижает нужную мощь, рассматривать как минимум, который нужно умножить на 1.25 и ещё маленько): https://outervision.com/power-supply-calculator
	> In terms of watts, a supply that is running at about 30-50% of its rated load is likely to be within its peak efficiency window, but is also likely to be relatively unstressed, leading to a longer life and reduced likelihood of premature failure.
	> You also need to estimate (by adding up the start currents for all the drives, usually around 2 amps each, and then estimating other 12V loads such as fans, CPU's, etc.) the 12V load, and verify that that will remain under the rated capacity of the power supply. You can CHEAT at this by hooking up the system without powering on the drives, letting it run memtest86, and checking power consumption. Take the watts, divide by 12, and that's a bad overestimate of the maximum 12V amps that the base system takes. Then you add the peak amps for all the drives, maybe add 10% more, check against the power supply rating, and there you have an easily derived pass-or-fail.
	- Рекомендуют:
		- chieftec bdf
		- FSP 600PNR-I
		- THERMALTAKE TR2 S
	- Не рекомендуют:
		- БП от Aerocool
		
	
	
UPS:
	- Необходим! zpool может наебнуться при неправильном выключении. SLOG может недописаться без BBU.
	- 3.5k FSP AGA400 PPF2401701 Off-Line, 400VA/240W
	- только на ноду от UPS нужно минимум 600 VA, а ведь ещё есть и десктоп
	
Охлаждение:
	- Харды должны быть охлаждены ниже 40C.
	- 2 – передние 92-мм вентиляторы серии Silent R2 с гидравлическими подшипниками, 1300 об/мин (совместимо с 80-мм вентиляторами) – в комплекте.
	- 1 – задний 140-мм вентилятор серии Silent R2 с гидродинамическим подшипником, 1000 об/мин (совместимо с 120-мм вентиляторами) – в комплекте.
	- Кулер процессора высотой до 165мм
	

	
> My system has 32GB of DDR3-1600 Kingston ECC(KVR16E11K4/32) RAM, Supermicro X9SCM-F-O(IPMI support a plus) with dual Intel Gb NICs and VGA built-in, and an Intel E3-1230V2 CPU and uses only 35 watts idle with no hard drives. The motherboard, CPU, and RAM cost me about $700 USD(cheaper now) and provides amazing performance and reliability. If you want to save some money and still enjoy ECC the Pentium G2020 is an excellent option.
	
SLOG:
	- обязан иметь защиту от отключения питания (PLP power loss protection)
	- для домашней 1GBe сети, наверно, нахуй не нужен
	- SSD/Optane для SLOG
	- ~2.5k, 16GB Intel MEMPEK1W016GAXT
	- ~2.5k, 16GB Intel MEMPEK1W016GA01
	- чего-нибудь побольше, один хуй на 1GbE разницы не увижу
	- и вообще, нужен ли он мне? Всегда можно прикупить как апгрейд, если скорость без него не устроит.
	
	


	


ZFS требует: 8 GB RAM min! Лучше 16+GB. x64. ZFS умеет в дедупликацию (дедуп жрет раму как не в себя, дома не нужно). ZFS защищает^W помогает защититься от дыры по записи. К ней обязательно нужна ECC RAM и PLP на всех кешах и буферах (батарейки на контроллерах и SLOG, либо кеши на запись отключить, что приводит к снижению быстродействия). Контрольные суммы - это заебись, но это не спасет, если при очередном scrub будут "восстановлены" поврежденные данные из-за flipped bits in RAM due to "cosmic rays".
Бздя есть на AArch64, но поддержка вроде экспериментальная. Нахуй нужно, когда полно x64?


Софт:
	- Уведомления по email о smart и [продумать ещё о чем]
	- SMART monitoring
	- Автовыключение с уведомлением по email при UPS level < 60%
	- Регулярные scrub по крону каждые две недели
	- Scrub и SMART long test НИКОГДА не должны запускаться одновременно, иначе scrub никогда не закончится.
	- Сжатие LZ4 (говорят, что оно почти прозрачно по производительности, а место экономит. Поискать цифры)
	- ZIL в RAM (не нужен? ZIL is only useful for sync writes. For all other writes the ZIL is not used. This means if you aren’t using NFS and don’t have a workload that uses sync writes, a ZIL is pointless.)
	- Дедупликация (идет нахуй, требует слишком много рамы и ARC)

ZFS File System is called a Dataset. It is layered above ZPool.
ZPool: [vdev, vdev, ...] (ZPool - same as Volume)
	- If _ANY_ VDev in ZPool is failed then _ENTIRE_ ZPool is corrupted and can not be restored!
	- It's possible to add new VDevs to existing ZPool
VDev:
	- VDev is a group of disk drives that are allocated together and intended to work together as a single virtual device to store data.
	- VDev are allocated in RAIDZ formats (for R5 and R6 or Mirror for R0)
	- If VDev can't provide 100% of its data using checksums or mirrors, the VDev will fail. 
	- If any VDev in ZPool failed then entire ZPool is failed and can not be restored :(
ZIL: (ZFS Intent Log)
	- used for speeding up sync write (perhaps I don't need it for home NAS)
	- is a non-volatile write cache for zpool
	- Write speed matters. SSD is recommended for it.
	- SLOG - Separate SSD allocated for ZIL
	
	
	
Вероятность успешного ребилда:
https://en.wikipedia.org/wiki/RAID#URE
> ... unrecoverable bit error (UBE) rate is typically guaranteed to be less than one bit in 10^15 for enterprise-class drives ... and less than one bit in 10^14 for desktop-class drives
> an URE during a RAID 5 rebuild typically leads to a complete rebuild failure
-> RAID 5 is dead. Use smth else instead.

> https://www.datarc.ru/articles/pochemu-raid6-perestanet-rabotat.html
Вероятность не получить URE для R5 из 4 x 2ТБ = (1 – 1 /(24 414 062 500)) ^ (3*3 907 029 168) = 0,618724054
Pr <= (1 - (1/UREsc))^(Nrd * Dsc), where
	Pr 	  - Probabaility of successful RAID rebuild
	UREsc - sector count after which Unrecoverable Read Error will occur by disk specification
	Nrd   - Number of remaining working disks (for R5 = Ntotal - 1)
	Dsc	  - sector count of single disk in array (assuming minimum disk capacity)

For non-enterprise hard drives, NRE/URE rate is normally 1 per 10^14 bits read, which means that NRE/URE occurs every 11.37TB	

Либо большая вероятность восстановления и малый объем массива, либо наоборот. Либо стоимость массива увеличивается до космической.

[19:40] [] вот тут говорят, что при ошибке чтения при ребилде, ZFS пометит файл как поврежденный и позволит восстановить остальные файлы
[19:40] [] https://serverfault.com/questions/937547/if-a-raid5-system-experiences-a-ure-during-rebuild-is-all-the-data-lost
[19:42] [] другое дело, что остальные выжившие диски будут сильно нагружены и возрастает вероятность выхода из строя ещё одного из дисков, тогда уже совсем пиздец
[19:43] [] выходом может быть использование R6 или R7, но это ещё минус диск или два из общего объема

[20:46] [] Во, нашёл про потерю данных на R5
[20:47] [] Говорят, что он умер ещё в 2009
[20:47] [] https://www.ixsystems.com/community/threads/5x-4tb-raidz1-array-rebuilding-with-nre-ure-issue.13719/
[20:47] [] > 1. ZFS will continue the rebuild, but you will have some amount of corruption. It could range from a single file being corrupted to metadata corruption that causes a lot of files to be lost or the zpool to be unmountable(a loss of all data).
[20:47] [] > 5. Make a RAIDZ2/RAID6.
[20:49] [] > As long as you don't have a third disk in that "stripe" of data that has an error, then the recovery should proceed normally.

Есть и какой-то другой подход к подсчету вероятностей полной потери данных:
https://www.servethehome.com/raid-calculator/raid-reliability-calculator-simple-mttdl-model/
С ней RAIDZ2 из 5 х 3ТБ, если принять URE за 10^13 c пессимистичным MTBF 36.5к, полностью наебнется в течение трех лет с вероятностью 0.16533 %, 10 лет - 0.55002 %
С этим можно жить.

https://fiddle.jshell.net/Biduleohm/paq5u7z5/1/show/light/
Вот этот калькулятор говорит, что в таком конфиге свободным рекомендуют оставить 1.611 ТиБ, получится фактически поиметь 6.444 ТиБ вместо маркетологических 9 ТБ. Такие дела. 




***

***

***

***
