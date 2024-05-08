<img src="https://user-images.githubusercontent.com/9472095/52746593-c7529e80-2fd9-11e9-96a9-06c8f077d2c3.png"/>

## Описание
---
Создание ВМ с помощью Vagrant. 
Обновление ядра Linux.

## Запуск
---
Клонируем репозиторий `git clone https://github.com/mrM1tn1ck/yatube.git`
Выполняем команду `vagrant up`

## Обновление ядра Linux

---
Представленный Vagrantfile создаст ВМ на VirtualBox. Будут установлены все необходимые зависимости, обновления системы и исходники для компиляции ядра. 
Далее необходимо:
1. зайти в систему выполнив команду `vagrant ssh`
2. перейти в каталог `/usr/src/linux-6.8.9/` 
3. для обновления ядра Linux поочередно выполняем следующие команды:
``
```
make menuconfig
make
make install_modules
make install
```

## Troubleshooting
---
При возникновении ошибки связанной с сертификатом, можно отключить данную проверку, выполнив следующие команды из каталога `/usr/src/linux-6.8.9/`

```
scripts/config --disable SYSTEM_TRUSTED_KEYS
scripts/config --disable SYSTEM_REVOCATION_KEYS
```
