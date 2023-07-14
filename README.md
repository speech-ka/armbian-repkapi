# Armbian for RepkaPi
![image](https://user-images.githubusercontent.com/82046704/227979186-eb12d202-1f76-4736-8dc0-585b6bff3d8e.png)

Дисклеймер для свидетелей "Всероссикого распила", я никак не связан с НПО "RBS". Это мой лишь небольшой проект Open-Source по портированию Armbian.

Armbian for RepkaPi - Как очедвино из названия это небольшой проект по портированию Armbian. В данный момент проект находит в активной стадии разработки.
Первые рабочие билды уже лежат в релизах. Есть небольшие шараховатости но уже все более или менее работает.

## Что такое RepkaPi:
![image](https://user-images.githubusercontent.com/82046704/227980711-b0c4c54a-b631-4dd9-9beb-1ae1a1479b01.png)

Это одноплатный компьютер на ARM от Российского вендора НПО "RBS". В данный момент доступна модель RepkaPi 3.
Характеристики RepkaPi 3:
- SoC: Allwinner H5
- Ядра: 4 ядра Cortex-A53 частотой 1.4 GHz
- Видеоядро: Mali-450MP4
- ОЗУ: 1ГБ или 2ГБ
- Wi-Fi 802.11b/g/n Bluetooth V4.0 (HS) На модуле AP6212
- Ethernet 100Mb
- GPIO 40 Pin

## Для сборки потребуется:

- Ubuntu 22.04 Server
- От 4 потоков (начиная с семейства Sandy/Ivy Bridge) для более или менее быстрой сборки
- От 2 ГБ ОЗУ желательно 4 ГБ.

### Как собрать Armbian?
```
apt-get -y install git
git clone --branch=main https://gitflic.ru/project/imptovskii/armbian.git
cd armbian
./compile.sh
```

Выбираем:
- Cбилдить ядро и U-Boot
- Сбилдить только U-Boot
- Сбилдить полный образ системы.

Затем ищем в списке repkapi3 и задаем параметры которые нам нужны:
- Тип ядра: Current, Legacy, Edge
- С рабочим столом или без и т.д.

!В данный момент 23.05.2 собирается только со старым Legacy ядром 5.15.

И ожидаем завершения, в данный момент сборка работает от начала и до конца без ошибок.

## License

This software is published under the GPL-2.0 License license.
