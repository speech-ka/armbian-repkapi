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
git clone --branch=main https://github.com/Imptovskii/armbian-repkapi
cd armbian-repkapi
./compile.sh
```

Выбираем:
- Cбилдить ядро и U-Boot
- Сбилдить только U-Boot
- Сбилдить полный образ системы.

Затем ищем в списке repkapi3 и задаем параметры которые нам нужны. (Ядро Current или Old Stable, с рабочим столом или без и т.д.)

И ожидаем завершения, в данный момент сборка работает от начала и до конца без ошибок.

### Копируем DTB в /boot img образа.

Серьёзный косяк в текущей сборке это что в /boot отсутствует sun50i-h5-repka-pi3.dtb
Это решается использованием патчей, но как их писать не совсем понятно, думаю в скором времени разберусь.

/path/to/build/ - это путь до вашей папки со сборщиком

Создаем loop устройство для работы с образом диска.
```
sudo kpartx -av /path/to/build/armbian-repkapi/output/images/<Образ>.img
```

Затем вам программа kpartx высдаст название устройства например /dev/loop1p1. Только у вас будет уже своя цифра (/dev/loop1p1, /dev/loop2p1 и т.д.).

Монтируем
```
sudo mkdir /mnt/img
sudo mount -o loop /dev/mapper/loop<цифра>p1 /mnt/img/
```

Копируем DTB файл:
```
sudo cp /path/to/build/armbian-repkapi/cache/sources/u-boot/v2022.07-repka/arch/arm/dts/sun50i-h5-repka-pi3.dtb /mnt/img/boot/dtb-<версия ядра>-sunxi64/allwinner/
```

И обязательно размонтируем.
```
sudo umount /mnt/img
```
Затем через любой FTP или SFTP клиент выкачиваем артефакт он будет по след пути:
```
/path/to/build/armbian-repkapi/output/images/
```

### Build parameter examples

Show work in progress areas in interactive mode:

```bash
./compile.sh EXPERT="yes"
```

Build minimal CLI Armbian Focal image for Orangepi Zero. Use modern kernel and write image to the SD card:

```bash
./compile.sh \
BOARD=orangepizero \
BRANCH=current \
RELEASE=focal \
BUILD_MINIMAL=yes \
BUILD_DESKTOP=no \
KERNEL_ONLY=no \
KERNEL_CONFIGURE=no \
CARD_DEVICE="/dev/sdX"
```

## License

This software is published under the GPL-2.0 License license.
