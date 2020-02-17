# README

Интерфейс для настройки демона [mbusd](https://github.com/3cky/mbusd)

Веб-приложение позволяющее настроить мост ModbusTCP-RTU через браузер.

### Особенности
* Основано на python3 и Flack
* Используется готовый демон _mbusd,_ который необходимо собрать под
конкретную платформу и положить исполняемый файл в каталог **bin**
* Поддерживается упаковка в 1 файл через _pyinstaller_
* Один иснстанс сервера и демона _mbusd_
* Настройки сохраняются только внутри одной сессии
* Порт для веб-интерфейса: 7123

### Сборка
1. Склонируйте репозиторий `mbusd`
2. Отредактируйте файл CMakeLists.txt:
    Закоментируйте строки:
```
#include(FindSystemd)

#TODO  ISC_Posix,  prog_libtool
# single-configuration generator setup
#SET(BASIC_C_FLAGS "-W -pedantic -fno-builtin-log -Wall")
#SET(CMAKE_C_FLAGS_RELEASE   "${BASIC_C_FLAGS} -O2")
#SET(CMAKE_C_FLAGS_DEBUG     "${BASIC_C_FLAGS} -g")
```

3. Установите [msys2](https://www.msys2.org/) для вашей архитектуры (x86/amd64)
4. Оспользуя консоль `msys2` установите нутри него gcc, make и cmake
```
$ pacman -Syy
$ pacman -S gcc make cmake
```

5. Соберите `mbusd`
```
$ cd /<disk>/path/to/mbusd
$ mkdir build && cd build
$ cmake ..
$ make
```

2. Скопируйте полученый исполняемый файл `mbusd.exe` в подкаталог bin проекта
3. Скопируйте библиотеку `msys-2.0.dll` в подкаталог bin проекта


### Запуск
`$ python ModbusBridge.py`

### Упаковка в 1 файл
Требуется модуль pyinstaller для python
Выполните команду
```py
$ pyinstaller -w -F 
    --add-data "bin;bin" 
    --add-data "static;static" 
    --add-data "templates;templates" 
    ModbusBridge.py 
```
В каталоге `dist` появится исполняемый файл, котрый можно
запускать на любой машине с Windows Vista и выше.
