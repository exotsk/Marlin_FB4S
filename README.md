# Marlin 3D Printer Firmware for Flying Bear 4S

Это конфигурация [официального Marlin](https://github.com/MarlinFirmware/Marlin) для принтера Flying Bear 4S.

 На данной версии **не работает WIFI модуль**. Вариант работы с WIFI находится в ветке [FB4S_WIFI](https://github.com/Sergey1560/Marlin_FB4S/tree/FB4S_WIFI)

## Как скомпилировать прошивку

Видео Дмитрия Соркина [youtube](https://www.youtube.com/watch?v=HirIZk0rWOQ)

После компиляции, готовая прошивка лежит .pio/build/mks_robin_nano/Robin_nano35.bin

### Что нужно настроить, если собираете сами

Нужно настроить направления движения по осям под свои драйвера в файле [Configuration.h](./Marlin/Configuration.h) (параметры INVERT_?_DIR, строка 1134).

По умолчанию стоят настройки под стандартные драйвера FB4S на всех осях. В файле [Configuration.h](./Marlin/Configuration.h) уже есть несколько готовых наборов настроек:

* ALL_DRV_2208 - если установлены драйвера TMC 2208 или TMC 2209 на всех осях
* FB_4S_STOCK - если установлены драйвера A4988 на всех осях. Это конфигурация для FB4S с стандартными драйверами.
* FB_5_STOCK - конфигурация для FB 5 (2208 на осях X,Y и A4988 на Z,E)

В строке 1098 нужно выбрать только один из вариантов:

```C
#define ALL_DRV_2208
//#define FB_4S_STOCK
//#define FB_5_STOCK
```

### Первое, что нужно сделать, после прошивки

Первое, что нужно сделать после прошивки, это проинициализировать eeprom, сбросив настройки по-умолчанию. Делается это через меню Configuration -> Advanced settings -> Initialize eeprom.

## Графический интерфейс

Доступны несколько вариантов графического интерфейса. Выбор режима устанавливается в файле Marlin/Configuration.h. Нужно включить один из define-ов, а остальные отключить. Доступны следующие варианты:

```
#define TFT_480x320
#define FSMC_GRAPHICAL_TFT
#define TFT_LVGL_UI_FSMC
```

### Интерфейс Marlin, вариант "текстовый"

Это стандартный интерфейс Marlin который "растянут" с 128х64 на графический экран 480х320. Для использования этого режима в файле Marlin/Configuration.h нужно включить:

```
#define FSMC_GRAPHICAL_TFT
```

### Интерфейс Marlin, вариант "графический"

Это стандартный интерфес Marlin сделанный под графический экран с тач-панелью. Для использования этого режима в файле Marlin/Configuration.h нужно включить:

```
#define TFT_480x320
```

### Графический интерфейс от МКС

В версию 2.0.6 был принят код от МКС с графическим интерфейсом. Для работы интерфейса нужны изображения и шрифты, после сборки прошивки они находятся в .pio/build/mks_robin_nano35/assets Для загрузки изображений, папку assets нужно положить в корень карты памяти.

Для сборки прошивки с графическим интерфейсом нужно сделать следующие настройки:

* В файле Marlin/Configuration.h, закомментировать #define FSMC_GRAPHICAL_TFT
* В файле Marlin/Configuration.h, включить #define TFT_LVGL_UI_FSMC
* В файле Marlin/Configuration.h, закомментировать #define TOUCH_BUTTONS
* В файле Marlin/Configuration_adv.h, закомментировать #define ADVANCED_PAUSE_FEATURE
* В файле Marlin/Configuration.h, закомментировать #define LCD_BED_LEVELING

## Готовые сборки

Для записи прошивки просто скопируйте содержимое нужной папки на SD карту и включите принтер.

* Классический интерфейс, драйвера A4988 [Link](./firmware/classic/a4988)
* Классический интерфейс, драйвера 2208/2209 [Link](./firmware/classic/2208)
* Графический marlin, драйвера A4988 [Link](./firmware/classic/a4988)
* Графический marlin, драйвера 2208/2209 [Link](./firmware/classic/a4988)
* MKS TFT интерфейс, драйвера A4988 [Link](./firmware/mks_tft/2208)
* MKS TFT интерфейс, драйвера 2208/2209 [Link](./firmware/mks_tft/2208)
