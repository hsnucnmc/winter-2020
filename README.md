---
tags: 寒訓
---

# 2020 CNMC 寒訓
## 開始閱讀文件之前
有一些東西你們應該要在之前就學會了，請先想辦法答出來以下問題再開始看這份文件吧！
1. Apache 是什麼
2. web server 是什麼
3. port 80 跟 443 是什麼
4. MySQL 是什麼
5. PHP 是什麼

---

## reference
[wiki](https://wiki.cnmc.tw)
[teach file](https://cnmc.tw/teach)
[WordPress](https://tw.wordpress.org/)
[FreeBSD Handbook](https://www.freebsd.org/doc/zh_TW/books/handbook/)
### tools
[WinSCP](https://winscp.net/eng/download.php)
[PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
[VSCode](https://code.visualstudio.com)
## Before Starting
寒訓的上課方式跟平常社課是不一樣的，你們可以簡單理解為自學，理論上經過寒訓之後你們的實力會大增，好好期待吧><
如果不想用FreeBSD也沒關係，可以用ubuntu或linux之類的。
下面是你們的目標，盡力達到就好，當年我們寒訓也沒有幾個人成功，合起來大概有1.5/5人吧。
## Day1 apache
**keyword: FAMP(FreeBSD + Apache + MySQL + PHP)**
1. 弄出憑證，然後跟我們回報，再給你們網址。**keyword: certbot, httpd-ssl.conf**
2. 讓apache有php可以用。**keyword: php apache freebsd**
3. 弄好MySQL。**keyword: mysql freebsd**
4. 架好phpMyAdmin。**keyword: phpmyadmin freebsd**
5. 架好wordpress。**keyword: wordprss freebsd**

 > 憑證弄好了可以來這邊回報一下
 > [color=red]
 
 > 我要"kulimi.cnmc.tw"作為我的域名(希望
 > 220.135.245.148
 > [name=kulimi][color=orange]

## Day2 nginx
**keyword: nginx**
1. 把昨天弄出來的東西安穩的移植到nginx上。
## Day3 社內賽
[Online Judge](https://sirius.cnmc.tw)
從 9:00~17:00，三人一組，分兩組
要打的請留 IP 跟你是誰：
 > 140.131.149.27
 > [name=談書愷]
 > 140.131.149.31
 > [name=kulimi]
 > 140.131.149.28
 > [name=陳禹璋]
## Extra
這是未來校網會用的東西，遲早要研究的
建議弄台非FreeBSD的機器，不然可能會被雷
**keyword: docker, docker-compose**
1. 架出一個 container 裡面放網頁伺服器，用外部的 port 去接裡面的 port
 > 你們看到的 OJ 也是 docker 架的喔
 > [name=Sirius][color=blue]
## Q&A + 討論區
[提問的智慧](https://github.com/ryanhanwu/How-To-Ask-Questions-The-Smart-Way)
如果遇到什麼困難就丟上來，但是如果社長我覺得你的問題不值得回答（可以快速查到）或描述不夠清楚，就不會回答你，但是會告訴你我不回答。
請使用 quote:
 > 請問Unix系統要怎麼切到外接磁碟區域阿？
 > [name=kulimi][color=red]
 > > 查查看 mount，我也不熟QQ
 > > [name=Sirius][color=blue]
 > > 我以為他會自己 mount 進來欸
 > > [name=Sirius][color=blue]
 > > [看一下(?)](https://unix.stackexchange.com/questions/116375/how-do-i-access-files-on-an-external-hard-drive)
 > > [name=Sirius][color=blue]
 
 > @kulimi 你要丟你 certbot 的問題嗎
 > [name=Sirius][color=red]
 > > 我想再研究一下
 > > [name=kulimi][color=orange]
 
 > 請問通常而言apache的設定檔(configuration file)是指那個httpd.conf嗎？因為有一堆.conf的檔案所以我不太確定。(已解決)
 > [name=kulimi][color=red]
 > > `httpd.conf` 是主要設定檔，其他還有很多。其他設定檔跟 `httpd.conf` 的關係是 `httpd.conf` 會把其他設定檔 `Include`
 > > [name=Sirius][color=blue]

 > 他說`/etc/apache2/other/le_http_01_challenge_pre.conf`這個檔案第一行出錯，但是這個檔案並不存在，就算再創一個也會消失。~~複製錯行啦~~
 > [name=kulimi][color=red]
 > > 你可以試試看去`httpd.conf`把 rewrite engine 那行取消註解，應該是 `LoadMoudle rewrite_mod` 之類的。
 > > [name=Sirius][color=blue]
 > > >雖然沒有`Rewrite Engine`，但是我有找到`LoadModule rewrite_module libexec/apache2/mod_rewrite.so`
 > > > [name=kulimi][color=orange]
 > > > > 對就是這個www
 > > > > [name=Sirius][color=blue]
 > > > > > 真棒，進展到下一個問題
 > > > > > [name=kulimi][color=orange]
 

    bash-3.2$ sudo certbot --apache
    Password:
    Saving debug log to /var/log/letsencrypt/letsencrypt.log
    Plugins selected: Authenticator apache, Installer apache

    Which names would you like to activate HTTPS for?
        - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    1: kulimi.cnmc.tw
    - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    Select the appropriate numbers separated by commas and/or spaces, or leave input
    blank to select all options shown (Enter 'c' to cancel): 1
    Obtaining a new certificate
    Performing the following challenges:
    http-01 challenge for kulimi.cnmc.tw
    Error while running apachectl configtest.

    AH00526: Syntax error on line 1 of /etc/apache2/other/le_http_01_challenge_pre.conf:
    Invalid command 'RewriteEngine', perhaps misspelled or defined by a module not included in the server configuration

    Cleaning up challenges
    Error while running apachectl configtest.

    AH00526: Syntax error on line 1 of /etc/apache2/other/le_http_01_challenge_pre.conf:
    Invalid command 'RewriteEngine', perhaps misspelled or defined by a module not included in the server configuration

    bash-3.2$ cat /etc/apache2/other/le_http_01_challenge_pre.conf
    cat: /etc/apache2/other/le_http_01_challenge_pre.conf: No such file or directory
    bash-3.2$ sudo cat /etc/apache2/other/le_http_01_challenge_pre.conf
    cat: /etc/apache2/other/le_http_01_challenge_pre.conf: No such file or directory
    bash-3.2$

> 為啥我`ping kulimi.cnmc.tw`沒有反應，但是`ping 220.135.245.148`有？
> [name=kulimi][color=orange]
 
## 筆記
 > 善用 quote，讓我們知道是誰寫的
 > 多做共筆喔><
 > [name=Sirius][color=blue]

### Day1
> certbot 難裝但是免費，SQL裝不起來好難過。
> MacOS內建apache超爽的
> 可是certbot還是裝不起來
> 
> 有域名好爽喔哈哈
> [name=kulimi][color=orange]
### Day2

### Day3 writeup

### Extra