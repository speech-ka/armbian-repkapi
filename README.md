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

- Ubuntu 22.04 Server или Debian 12
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

## ВАЖНО

### Заморозка обновления ядра и загрузчика

После первого запуска не обновляйте систему! Так как, у нас неофициальная сборка Armbian и о нашей плате официальные сборки не знают, надо заморозить обновление Ядра и UBoot загрузчкика.

- Пишем:
```
sudo armbian-config
```
- Переходим в System settings и выбираем Freeze.

![image](https://i.postimg.cc/yxkNsJRW/12345.png)

- Нажимаем кнопку Freeze

![image](https://i.postimg.cc/fLWLqqTc/123456.png)

- Ждем

![image](https://i.postimg.cc/tgNJ5GyR/1234567.png)

- Фон станет красным, не пугаемся это наоборот норма.

![image](https://i.postimg.cc/bJ6v70sK/12345678.png)

### Задаем меняем зеркало репозитория Armbian на зеркало расположенное в РФ от Яндекса
Балансировщик http://apt.armbian.com часто кидает на url'ы которые недоступны с IP адресов расположенных в РФ, фиксируем работу на зеркале от Яндекса.
- Пишем:
```
sudo nano /etc/apt/sources.list.d/armbian.list
```
- Мы видим следующее:

![image](https://i.postimg.cc/rpkzxFBY/53332.png)

- Меняем http://apt.armbian.com на http://mirror.yandex.ru/mirrors/armbian/apt

![image](https://i.postimg.cc/rwWKDtPr/53333.png)

- Обновляем индекс и список пакетов apt:

```
sudo apt update
```

Так же вы можете заменить оригинальный репозиторий http://ports.ubuntu.com на http://mirror.yandex.ru/ubuntu-ports в файле /etc/apt/sources.list

## License
This software is published under the GPL-2.0 License license.
