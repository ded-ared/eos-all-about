# Установка полезных приложений

В этом разделе перечислены некоторые приложения, без которых лично мне никак не обойтись. Кроме того, к некоторым позволю себе оставить пару комментариев. За исключением единичных случаев, предпочитаю установку из репозиториев, поэтому здесь будут указаны команды, как установить именно этим способом.

Собственно, раздел создал затем, чтобы эти репозитории потом не искать.



## KeePassXC - Менеджер паролей

Чтобы установить [KeePassXC](https://keepassxc.org/), в терминале выполните поочередно команды:

```
sudo add-apt-repository ppa:phoerious/keepassxc
sudo apt install keepassxc
```

## Firefox

Очень рекомендую устанавливать Firefox через официальный PPA репозиторий Mozilla. 

1. Добавьте репозиторий:

```
sudo add-apt-repository ppa:mozillateam/ppa
```

2. Установите Firefox следующей командой:

```
sudo apt install -t 'o=LP-PPA-mozillateam' firefox
```

Здесь нужно с помощью параметра `-t` явно указать, откуда устанавливать программу.   
После установки можно поднять приоритет этого репозитория.

Для этого создайте файл `/etc/apt/preferences.d/mozillateamppa` командой

```
sudo vi /etc/apt/preferences.d/mozillateamppa
```

Добавьте в него следующее содержание:

```
Package: firefox*
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 501
```

### Установите на Firefox тему Elementary

Чтобы браузер Firefox выглядел органичной частью Elementary, установите [elementary-firefox-theme](https://github.com/Zonnev/elementaryos-firefox-theme).

![firefox](https://github.com/ded-ared/eos-all-about/blob/main/images/firefox.png)

### Избавьтесь от рекламы от Яндекса

Думаю, мало кто обходится нынче без блокировщика рекламы. Лично я пользуюсь **ublock**.

Ксожалению, по умолчанию, от рекламы Яндекса он не спасает, в почте она особенно раздражает.

Если вы тоже пользуетесь **ublock**, зайдите в его настройки и импортируйте вот эту строчку:

```
https://easylist-downloads.adblockplus.org/cntblock.txt
```
![ublock](https://github.com/ded-ared/eos-all-about/blob/main/images/ublock.png)

Как импортировать в другие блокировщики — не подскажу, но наверно не сложнее, чем в **ublock**.

---
