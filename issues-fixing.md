# Возможные проблемы и способы их устранения

* [Дублируется иконка в доке Plank](#дублируется-иконка-в-доке-plank)

* [Отключается Bluetooth](#отключается-bluetooth)

---

## Дублируется иконка в доке Plank

В доке Plank при запуске приложения, установленного через Flatpak, иногда можно обнаружить задвоенную иконку.

![duplicate-icon](https://github.com/ded-ared/eos-all-about/blob/main/images/duplicate-icon-plank.png)

Чтобы избавиться от этого [глюка системы](https://github.com/elementary/dock/issues/64), найдите и отредактируйте десктопный файл приложения с расширением `.desktop`, добавив в него строку `StartupWMClass=<ЗНАЧЕНИЕ>`.

Ниже приведена пошаговая инструкция (на примере приложения **Transmission**).

1. Узнайте <ЗНАЧЕНИЕ>, которое нужно добавить в строку с классом для десктопного файла.
   
   1. Запустите приложение, у которого задвоилась иконка.
   
   2. Откройте терминал и введите команду: `xprop WM_CLASS`. Ваш курсор должен измениться на крестик.
   
   3. Наведите видоизмененный курсор на окно приложения и кликните по нему. В терминале появится значение, которое нужно добавить.
   
   ![](https://github.com/ded-ared/eos-all-about/blob/main/images/duplicate-icon-plank-value.png)

2. Найдите и откройте в текстовом редакторе файл приложения с расширением `.desktop`.   
   У меня он оказался вот здесь (см. путь ниже). Если ваше приложение установлено через Flatpak, ищите файл в этом же направлении.

```
/home/<ИМЯ_ПОЛЬЗОВАТЕЛЯ>/.local/share/flatpak/app/com.transmissionbt.Transmission/current/3d0fb3864db64add64e036679cccf94bd31d38ddcdd5b22ea263ad742b9ff458/export/share/applications/com.transmissionbt.Transmission.desktop
```

3. Вставьте в конце раздела [Desktop Entry] строку `StartupWMClass=transmission-gtk`
   
   ![](https://github.com/ded-ared/eos-all-about/blob/main/images/duplicate-icon-plank-string.png)

4. Сохраните изменения в файле и перезагрузите операционную систему. Можно перезапустить сеанс, но рекомендуется перезагрузка.

5. Запустите приложение. Дубликат иконки больше не должен появляться в доке.

> ⚠️ **Примечание**
> 
> После обновления приложения задвоенная иконка может вновь объявиться. В этом случае нужно заново добавить параметр `StartupWMClass=<ЗНАЧЕНИЕ>` в десктопный файл, как описано выше.

---

## Отключается Bluetooth

В один прекрасный момент на моем ноутбуке отвалился Bluetooth, как мне показалось — без видимых причин.

⚠️ Проявлялось это так:

- Значок в панели неактивен и при попытке включить Bluetooth ничего не происходило, даже прежде подключенные устройства не показывались.

- В настройках системы тоже тишина, крутится индикатор, якобы что-то сканируется, но по факту не сканируется ничего. Наушники, которые всегда сопрягались без проблем, не воспринимались ноутбуком никак.

ℹ️ Путем гуглокопания, нашел способ проверить, не заблокирован ли Bluetooth воообще.

```
sudo rfkill list
```

Оказалось, что да, Bluetooth у меня по какой-то причине заблокирован.

С помощью команды

```
sudo rfkill unblock bluetooth
```

разблокировал, но счастье длилось только до очередной перезагрузки.

ℹ️ Второй способ разблокировки нашелся методом научного тыка: нужно было включить и потом отключить авиарежим клавиатурой или через значок вай-фая в панели. В этом случае Bluetooth чудным образом тоже просыпался и начинал нормально работать.

Что же, каждый раз вот так разблокировать Bluetooth после включения ноутбука? Это же бред какой-то.

❓ Стал вспоминать, что я такого делал, в каких настройках копался, чего устанавливал, после чего случилась такая оказия.

❗ Причина нашлась совершенно случайно, как всегда. Пока курил гугл в поисках, прочитал что-то про спящий режим, в который могут уходить устройства в целях экономии питания и вспомнил, что буквально вчера слепо доверился чьему-то совету в интернете и установил [утилиту TLP](https://g-soft.info/articles/5784/uluchshenie-vremeni-avtonomnoy-raboty-noutbuka-v-ubuntu-s-pomoschyu-tlp/), которая вроде как улучшает энергосбережение.

> В статье говорилось, что нужно всего лишь установить, активировать и забыть, утилита все сделает сама (собственно, она все сама и сделала, только втихаря).

✅ После вспышки в сознании "а что если это оно и есть!?"

* Деактивировал эту штуку `sudo systemctl disable tlp.service`.

* Удалил ее на фиг `sudo apt purge tlp`.

* Подчистил хвосты `sudo apt autoremove` + `sudo apt autoclean` (на всякий случай)

* Перезагрузился и...

Уфф... все вернулось на круги своя.

❎ Вполне возможно, надо было хорошо ознакомиться с утилитой, установить интерфейс, покопаться в настройках (наверняка можно было все починить, не удаляя коварную TLP), но я подумал, что ноут от батареи использую редко, система вроде и так не особо батарею напрягает, так что ну его от греха подальше.

> Урок мне чайнику на будущее: нужно внимательнее знакомиться с матчастью прежде чем доверять первому источнику и что-то ковырять в системе.

---
