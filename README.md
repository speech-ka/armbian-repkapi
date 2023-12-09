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
git clone --branch=master https://gitflic.ru/project/imptovskii/armbian-repkapi.git
cd armbian-repkapi
./compile.sh
```

Выбираем:
- Cбилдить ядро и U-Boot
- Сбилдить только U-Boot
- Сбилдить полный образ системы.

Затем ищем в списке repkapi3 и задаем параметры которые нам нужны:
- Тип ядра: Current, Legacy, Edge
- С рабочим столом или без и т.д.

И ожидаем завершения, в данный момент сборка работает от начала и до конца без ошибок.

### ВАЖНО

После первого запуска не обновляйте систему! Так как, у нас неофициальная сборка Armbian и о нашей плате официальные сборки не знают, надо заморозить обновление Ядра и UBoot загрузчкика.

- Пишем:
```
sudo armbian-config
```
- Переходим в System settings и выбираем Freeze.
![image](https://psv4.userapi.com/c237131/u306539345/docs/d56/11b3ab1df52e/12345.png)
- Нажимаем кнопку Freezee
![image](https://psv4.userapi.com/c909518/u306539345/docs/d10/26ca6e301b59/123456.png)
- Ждем
![image](https://psv4.userapi.com/c909518/u306539345/docs/d36/f3a68d1b45e7/1234567.png)
- Фон станет красным, не пугаемся это наоборот норма.
![image](https://psv4.userapi.com/c909518/u306539345/docs/d42/8a8c5a52a009/12345678.png)

## License
This software is published under the GPL-2.0 License license.
