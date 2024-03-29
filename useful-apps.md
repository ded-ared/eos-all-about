# Установка нужных приложений

В этом разделе перечислены некоторые приложения, без которых лично мне никак не обойтись. Кроме того, к некоторым позволю себе оставить пару комментариев. За исключением единичных случаев, предпочитаю установку из репозиториев, поэтому здесь будут указаны команды, как установить именно этим способом.

Собственно, раздел создал затем, чтобы эти репозитории потом не искать.

> ⚠️ Примечание.
> 
> * Поскольку многие программы устанавливаются через PPA репозитории, предварительно [установите возможность этими репозиториями пользоваться](/after-install.md#добавить-возможность-устанавливать-программы-из-репозиториев-рра).
> 
> * Здесь далеко не весь список приложений. С неперечисленными обычно заморочек не возникает.

**Содержание**

* [KeePassXC - менеджер паролей](#keepassxc---менеджер-паролей)

* [Firefox + bonus](#firefox)
  
  * [Установить тему Elementary](#установите-на-firefox-тему-elementary)
  
  * [Избавиться от рекламы Яндекса](#избавьтесь-от-рекламы-яндекса)

* [Ksnip - Для снимков экрана](#ksnip---скриншотер)

* [Conky - Системный монитор](#conky---системный-монитор)

* [gThumb - Просмотр изображений](#gthumb---просмотрщик-изображений)

* [GIMP, Photopea, Photoshop - Графические редакторы](#gimp-или-photopea-или-photoshop-)

* [Foliate - Чтение книг](#foliate---читалка-книг)

* [Gparted - для форматирования флешек и др.](#gparted)

* [MPV Player](#mpv-player)

---

## KeePassXC - Менеджер паролей

Чтобы установить [KeePassXC](https://keepassxc.org/), в терминале выполните поочередно команды:

```
sudo add-apt-repository ppa:phoerious/keepassxc
sudo apt install keepassxc
```

![keepassxc](https://github.com/ded-ared/eos-all-about/blob/main/images/keepassxc.png)

---

## Firefox

Очень рекомендую устанавливать Firefox через официальный PPA репозиторий Mozilla. 

1. Добавьте репозиторий:

```
sudo add-apt-repository ppa:mozillateam/ppa
```

2. Установите Firefox следующей командой (параметр `-t` явно указывает, откуда устанавливать программу):

```
sudo apt install -t 'o=LP-PPA-mozillateam' firefox
```

3. После установки поднимите приоритет этого репозитория. Для этого создайте файл `/etc/apt/preferences.d/mozillateamppa` командой

```
sudo vi /etc/apt/preferences.d/mozillateamppa
```

4. Добавьте в созданный файл следующее содержание:

```
Package: firefox*
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 501
```

### Установите на Firefox тему Elementary

Чтобы браузер Firefox выглядел органичной частью Elementary, установите [elementary-firefox-theme](https://github.com/Zonnev/elementaryos-firefox-theme).

![firefox](https://github.com/ded-ared/eos-all-about/blob/main/images/firefox.png)

### Избавьтесь от рекламы Яндекса

Думаю, мало кто обходится нынче без блокировщика рекламы. Лично я пользуюсь **ublock**.

К сожалению, по умолчанию от рекламы Яндекса он не спасает, а в почтовом интерфейсе она особенно раздражает.

Если вы тоже пользуетесь **ublock**, зайдите в его настройки и импортируйте вот эту строчку:

```
https://easylist-downloads.adblockplus.org/cntblock.txt
```

![ublock](https://github.com/ded-ared/eos-all-about/blob/main/images/ublock.png)

Также добавьте вот эти строчки

```
ya.ru##.dist-overlay__content_button-theme_light.dist-overlay__content
ya.ru##.simple-popup__overlay_shown.simple-popup__overlay_theme_modal.simple-popup__overlay
```

на вкладке "Мои фильтры".

Как импортировать в другие блокировщики — не подскажу, но наверно не сложнее, чем в **ublock**.

---

## KSnip - Скриншотер

В Линуксе хороший инструмент для снимков экрана с возможностью редактирования — это вообще больной вопрос.

По роду работы, мне этот инструмент крайне необходим. Нужно не просто снимок экрана сделать, а еще и пристойно обработать его: добавить рамки, стрелки, надписи, выноски, блюр, и чтобы все это удобно настраивалось, а не было прибито гвоздями куда попало. На Windows с этим все в порядке, там есть идеальный во всех отношениях [FastStone Capture](https://www.faststone.org/FSCaptureDetail.htm), но он только для винды, а в Линуксе и близко ничего такого нет 😢

После долгих поисков, я остановился на [Ksnip](https://github.com/ksnip/ksnip) (более-менее сносно). Это приложение использует библиотеки Qt, поэтому будет не лишним воспользоваться [Qt адаптером](/after-install.md#подключить-поддержку-тем-gtk-для-qt-приложений).

> ⚠️ Рекомендую [скачать deb пакет](https://github.com/ksnip/ksnip/releases) и установить из него. Как установить программу из скачанного DEB пакета, можете прочитать [здесь](https://help.reg.ru/support/servery-vps/oblachnyye-servery/ustanovka-programmnogo-obespecheniya/ustanovka-programm-i-paketov-formata-deb#2).

![ksnip](https://github.com/ded-ared/eos-all-about/blob/main/images/ksnip.png)

> 🔵 Если не понравится, можно попробовать [Shutter](https://shutter-project.org/), репозиторий для Elementary OS7 есть уже в системе, можно установить через `sudo apt install shutter`. Себе его не установил только по той причине, что на моей машине эта прога работала со странностями (при выделении части экрана почему-то не видно рамку, очень неудобно и непонятно, как исправить).

---

## Conky - Системный монитор

Программа [Conky](https://losst.pro/nastrojka-conky) выводит на экран информацию о процессоре, памяти, жестком диске, сетевом подключении, запущенных процессах и многом другом, что происходит в системе. Особенность Conky в том, что данные выводятся на рабочий стол в виде виджета с невероятными и неограниченными настройками.

В сети можно найти множество готовых настроек Conky, которые превратят ваш рабочий стол в панель управления космическим кораблем.

Вот, например, как выглядит эта штука на моем рабочем столе:

![conky](https://github.com/ded-ared/eos-all-about/blob/main/images/conky.png)

Состоит из двух компонентов: дефолтного файла и [revolutionary_clocks](https://www.gnome-look.org/p/1006556/)

Для установки такого варианта, выполните следующее:

1. Установите Conky, выполнив в терминале команду:

```
sudo apt install conky conky-all
```

2. Установите сенсоры (нужны для определения температуры железа):

```
sudo apt install lm-sensors
```

3. В домашней папке создайте скрытую папку `~/.Conky/`

4. Разархивируйте в нее две [скачанные папки](https://disk.yandex.ru/d/exuqS3j7mH3XrQ).

5. Создайте в домашней папке папку `~/.fonts/`, если еще этого не сделали и положите туда шрифты из скачанного каталога `/revolutionary_clocks/fonts`

![conky-folder](https://github.com/ded-ared/eos-all-about/blob/main/images/conky-home-folder.png)

6. Перейдите в **Параметры системы → Приложения → Автозапуск** и добавьте по отдельности следующие команды в автозагрузку:

```
.Conky/revolutionary_clocks/rev_midi/start_conky.sh
```

```
conky -c /home/<user_name_folder>/.Conky/default/conky.conf
```

> ⚠️ **<user_name_folder>** в строке - это имя пользователя в системе, например `conky -c /home/johnny/.Conky/default/conky.conf`

![conky-auto](https://github.com/ded-ared/eos-all-about/blob/main/images/conky-auto.png)

7. Перезагрузите компьютер.

На рабочем столе должны появиться виджеты Conky (часы проявляются чуть дольше).

> ⚠️ Очень возможно, что у вас какие-то элементы виджета "поползут" или датчики не будут работать корректно. Тут, к сожалению, ничего не поделать.   
> Насколько я понял, настройки часов зависят от разрешения монитора, датчики температуры и сеть могут по-разному обоозначаться на разных машинах, так что придется поизучать конфигурационные файлы и повозиться, чтобы скорректировать.

---

## gThumb - Просмотрщик изображений

Штатный просмотрщик Elementary хорош для единичного просмотра фото, например, если открыть изображение из файлового менеджера. Но для просмотра по папкам лично мне удобнее [gThumb](https://wiki.gnome.org/Apps/Gthumb).

Чтобы установить gThumb из репозитория, выполните в терминале:

```
sudo add-apt-repository ppa:ubuntuhandbook1/apps
sudo apt update
sudo apt install gthumb
```

## GIMP или Photopea или Photoshop (!)

🔵 Если нужен графический редактор в качестве аналога Фотошопа (вечная печаль Линукса), первое, что рекомендуют - это [GIMP](https://flathub.org/apps/details/org.gimp.GIMP):

Установить можно так:

```
sudo add-apt-repository ppa:ubuntuhandbook1/gimp
sudo apt update
sudo apt install gimp
```

🔵 Другой весьма интересный онлайн редактор, очень похожий на Фотошоп - это [Photopea](https://www.photopea.com/)

Для домашнего пользования более чем достаточно. Очень рекомендую.

![photopea](https://github.com/ded-ared/eos-all-about/blob/main/images/photopea.png)

🔵 Но самая лучшая замена Фотошопу - это [Photoshop](https://github.com/CSMarckitus/Photoshop)

Ссылка ведет на инструкцию (на английском языке), как это можно сделать.

Там много нюансов. Сам я не устанавливал, не хочу пользоваться [Wine](https://www.winehq.org/) (который обязателен тут) по личным неосознанным причинам, но если сильно нужно, пробуйте.

![photoshop](https://github.com/ded-ared/eos-all-about/blob/main/images/photoshop-21.png)

---

## Foliate - Читалка книг

[Foliate](https://johnfactotum.github.io/foliate/) - замечательная читалка книг с библиотеками, где можно бесплатно накачать книжек на английском. Читать книги с компьютера конечно же можно тоже.

Установить вот так:

```
sudo add-apt-repository ppa:apandada1/foliate
sudo apt update
sudo apt install foliate
```

![foliate](https://github.com/ded-ared/eos-all-about/blob/main/images/foliate.png)

---

## Gparted

Эта программа может делать практически что угодно с вашими дисками, но по большому счету нужна при установке системы для разметки дискового пространства, а после установки — для форматирования флешек. Печально и странно, что штатных средств в Elementary для такой простой и нужной операции нет.

🔵 Чтобы установить Gparted, выполните в терминале:

```
sudo apt install gparted
```

🔵 Чтобы отформатировать флешку:

1. Запустите Gparted.

2. В правом верхнем углу программы из выпадающего списка выберите вашу флешку.

3. В верхнем меню перейдите в "**Раздел → Форматировать в**" и выберите нужный формат (например, NTFS).   
   Либо нажмите правой кнопкой мыши по разделу и в контекстном меню выберите **Форматировать в**.

4. В верхнем меню перейдите в "**Правка → Выполнить все операции**" или нажмите **Ctrl + Enter**.

![gparted-flash](https://github.com/ded-ared/eos-all-about/blob/main/images/gparted.png)

---

## MPV Player

Вдоволь намучившись с родным видеоплеером Elementary, который то не хотел показывать картинку, то молчал, как рыба об лёд, я установил MPV Player, чему безмерно рад. С ним немного сложновато новичку, зато качество воспроизведения — супер, а с конфигурационным файлом можно научиться обращаться.

Рекомендую [скачать deb-пакет](https://non-gnu.uvt.nl/debian/jammy/mpv/mpv_0.35.1+fruit.3_amd64.deb) и установить из него. Как установить, читайте [здесь](https://help.reg.ru/support/servery-vps/oblachnyye-servery/ustanovka-programmnogo-obespecheniya/ustanovka-programm-i-paketov-formata-deb#2).

Кому не подойдут настройки по умолчанию, найти в сети другие — несложно. Вот так выглядит плеер у меня:

![](https://github.com/ded-ared/eos-all-about/blob/main/images/mpv.png)

Мои настройки лежат [здесь](https://github.com/ded-ared/eos-all-about/tree/main/apps-settings/mpv) (тема Modern с некоторыми изменениями). Если устанавливали из DEB пакета, все содержимое нужно поместить в папку `/home/<ИМЯ-ПОЛЬЗОВАТЕЛЯ>/.config/mpv/`

Если такой папки нет, создайте.

---
