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



