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

[TOC]
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
如果不想用 FreeBSD 也沒關係，可以用 Ubuntu 或 Linux 之類的。
下面是你們的目標，盡力達到就好，當年我們寒訓也沒有幾個人成功，合起來大概有1.5/5人吧。  
這份筆記會幫你們保存到網管的 GitHub，以後出現問題可以上去看看。  
[repo](https://github.com/hsnucnmc/winter-2020)
## Day1 Apache
**keyword: FAMP(FreeBSD + Apache + MySQL + PHP)**
1. 弄出憑證，然後跟我們回報，再給你們網址。**keyword: certbot, httpd-ssl.conf**
2. 讓apache有php可以用。**keyword: php apache freebsd**
3. 弄好MySQL。**keyword: mysql freebsd**
4. 架好phpMyAdmin。**keyword: phpmyadmin freebsd**
5. 架好wordpress。**keyword: wordprss freebsd**

 > 憑證弄好了可以來這邊回報一下
 > [color=red]
 > > 我要"kulimi.cnmc.tw"作為我的域名(希望
 > > 220.135.245.148
 > > [name=kulimi][color=orange]
 > > 我要 ddos.cnmc.tw 拉
 > > 140.131.149.22
 > > [name=hahabox0]

## Day2 Nginx
**keyword: nginx**
1. 把昨天弄出來的東西安穩的移植到nginx上。
## Day3(2/7) 社內賽
[Online Judge](https://sirius.cnmc.tw)
從 9:00~18:00，一人一組，破台的人飲料一杯！  
請勿對比賽的機器攻擊！  
要打的請留 IP 跟你是誰：
 > 140.131.149.27
 > [name=談書愷]
 > 140.131.149.31  
 > Team name: ko-no-dio-da
 > [name=kulimi & 陳禹璋]
 > 140.131.149.30
 > [name=林杰]
 > 140.131.149.50
 > [name=趙子佾]
## Extra docker
這是未來校網會用的東西，遲早要研究的
建議弄台非 FreeBSD 的機器，不然可能會被雷
**keyword: docker, docker-compose**
1. 架出一個 container 裡面放網頁伺服器，用外部的 port 去接裡面的 port
 > 你們看到的 OJ 也是 docker 架的喔
 > [name=Sirius][color=blue]
## Q&A + 討論區

[提問的智慧](https://github.com/ryanhanwu/How-To-Ask-Questions-The-Smart-Way)
如果遇到什麼困難就丟上來，但是如果社長我覺得你的問題不值得回答（可以快速查到）或描述不夠清楚，就不會回答你，但是會告訴你我不回答。  
請使用 `quote`:
### Unix 切到外接磁碟
 > 請問Unix系統要怎麼切到外接磁碟區域阿？
 > [name=kulimi][color=orange]
 > > 查查看 mount，我也不熟QQ
 > > [name=Sirius][color=blue]
 > > 我以為他會自己 mount 進來欸
 > > [name=Sirius][color=blue]
 > > [看一下(?)](https://unix.stackexchange.com/questions/116375/how-do-i-access-files-on-an-external-hard-drive)
 > > [name=Sirius][color=blue]
---
### apache的設定檔是指 httpd.conf 嗎？
 > 請問通常而言apache的設定檔(configuration file)是指那個httpd.conf嗎？因為有一堆.conf的檔案所以我不太確定。(已解決)
 > [name=kulimi][color=orange]
 > > `httpd.conf` 是主要設定檔，其他還有很多。其他設定檔跟 `httpd.conf` 的關係是 `httpd.conf` 會把其他設定檔 `Include`
 > > [name=Sirius][color=blue]
---
### /etc/apache2/other/le_http_01_challenge_pre.conf 第一行出錯，但是這個檔案並不存在
 > 他說`/etc/apache2/other/le_http_01_challenge_pre.conf`這個檔案第一行出錯，但是這個檔案並不存在，就算再創一個也會消失。
 > [name=kulimi][color=orange]
 > > 你可以試試看去`httpd.conf`把 rewrite engine 那行取消註解，應該是 `LoadMoudle rewrite_mod` 之類的。
 > > [name=Sirius][color=blue]
 > > >雖然沒有`Rewrite Engine`，但是我有找到`LoadModule rewrite_module libexec/apache2/mod_rewrite.so`
 > > > [name=kulimi][color=orange]
 > > > > 對就是這個www
 > > > > [name=Sirius][color=blue]
 > > > > > 真棒，進展到下一個問題
 > > > > > [name=kulimi][color=orange]
 > >
 > > > 有空可以查查 `rewrite engine` 的功用
 > > > [name=Sirius][color=blue]
```=
AH00526: Syntax error on line 1 of /etc/apache2/other/le_http_01_challenge_pre.conf:
Invalid command 'RewriteEngine', perhaps misspelled or defined by a module not included in the server configuration

Cleaning up challenges
Error while running apachectl configtest.

AH00526: Syntax error on line 1 of /etc/apache2/other/le_http_01_challenge_pre.conf:
Invalid command 'RewriteEngine', perhaps misspelled or defined by a module not included in the server configuration

bash-3.2$ cat /etc/apache2/other/le_http_01_challenge_pre.conf
cat: /etc/apache2/other/le_http_01_challenge_pre.conf: No such file or directory
```
---
### ping 網址沒反應，但是 IP 有
> 為啥我`ping kulimi.cnmc.tw`沒有反應，但是`ping 220.135.245.148`有？
> [name=kulimi][color=orange]
> > 你在哪裡 ping，這看起來是 DNS 的紀錄還沒更新到
> > [name=Sirius][color=blue]
> > > 別的電腦上，至於 DNS 的紀錄也有別的問題提到了欸。
> > > [name=kulimi][color=orange]
> > > > 基本上這個問題等一陣子或是重開機等 DNS 紀錄更新好了就好
> > > > 也可以先試試 `drill kulimi.cnmc.tw` 之類的
> > > > [name=Sirius][color=blue]
> > > > > 後來我編輯了`DNS`的設定吧，就可以了，然後沒有`drill`這個指令
> > > > > [name=kulimi][color=orange]
> > > > > > 那應該要裝XD
> > > > > > 他是一個查 DNS 紀錄的工具，也可以用 `dig` 或 `telnet`
> > > > > > [name=Sirius][color=blue]
---
### nodename nor servname provided
 > 他說`nodename nor servname provided`，我在網路上有看到很多`ssh`產生此錯誤的解決方式，是在後面加上`.local`，但是我們不能這麼做，這到底該如何解決？  
 > ps.我現在`ping kulimi.cnmc.tw`可以正常運作  
 > ps.現在又不行了，ㄍㄋㄋ。好ㄉ  
 > [name=kulimi][color=orange]
 > > 查了一下，看起來是 DNS 出了問題，我晚點有空去看一下發生了什麼事，這不是你能處理的，先下一步
 > > [name=Sirius][color=blue]
 > > > 找到問題了，是我們沒調好
 > > > [name=Sirius][color=blue]
 > > > > 解決這個問題啦！謝謝學長！
 > > > > [name=kulimi][color=orange]
 ```= 
bash-3.2$ sudo certbot --apache
Password:
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator apache, Installer apache
An unexpected error occurred:
Traceback (most recent call last):
  File "/usr/local/Cellar/certbot/1.1.0/libexec/vendor/lib/python3.8/site-packages/urllib3/connection.py", line 156, in _new_conn
    conn = connection.create_connection
  File "/usr/local/Cellar/certbot/1.1.0/libexec/vendor/lib/python3.8/site-packages/urllib3/util/connection.py", line 61, in create_connection
    for res in socket.getaddrinfo(host, port, family, socket.SOCK_STREAM):
  File "/usr/local/Cellar/python@3.8/3.8.1/Frameworks/Python.framework/Versions/3.8/lib/python3.8/socket.py", line 918, in getaddrinfo
    for res in _socket.getaddrinfo(host, port, family, type, proto, flags):
socket.gaierror: [Errno 8] nodename nor servname provided, or not known
 ```
 ---
### 憑證弄出來但是沒上去 Apache
 > 他說`Congratulations! Your certificate and chain have been saved at:...`代表憑證已經弄出來啦。可是他又說他不能夠把憑證裝上去`- Unable to install the certificate`，然後剛剛去看了一下，還是顯示不安全。  
 > 他有說到`Cannot find an SSLCertificateFile directive in /files/private/etc/apache2/httpd-le-ssl.conf/IfModule/VirtualHost. VirtualHost was not modified`
 > 可是這個資料夾根本不存在，應該說根目錄下根本沒有`files/`，我也不知道`SSLCertificateFile`這是什麼，不過看起來有可能是指下面提到的`/etc/letsencrypt/live/kulimi.cnmc.tw/fullchain.pem`，最後我去看了一下他提到的`Virtual Host`，在`httpd.conf`有相關的設定，長得像下面那樣。
 > [name=kulimi][color=orange]
 > > 我喜歡你的問題。  
 > > 是這樣的，certbot 會幫你把憑證弄出來但是要怎麼用是你的事，也就是說，要讓他網頁伺服器上跑你需要手動對付他。我不知道 MacOS 的設定是如何，可以找找看一個叫做`httpd-ssl.conf`的檔案，裡面就會有 `SSLCertificateFile` 的地方可以設定，然後在你下面的紀錄的第10及12行，他有兩個檔案，兩個檔案都要放進 apache 的設定檔裡面。  
 > > [MacOS Apache Setup: SSL](https://getgrav.org/blog/macos-catalina-apache-ssl) 這篇文章可以看一下  
 > > 
 > > 至於他提到的 `virtual host`，那是一個目前用途還不太大但是很有趣的功能，簡單來說就是把不同的網站架在同一個網頁伺服器，要分別的方式可以用 port 或網址，現在要玩的話基本上只能用 port，用 port 基本上用途不大，要看實例的話可以去看看 cnmc.tw 跟 cnmc.tw:8080，他們就是 virtual host 用 ip 分別的。而上面提到的網址基本上會像是 a.sirius.cnmc.tw 跟 b.sirius.cnmc.tw 這樣，那需要你自己架一個 DNS server 才行了。
 > > [name=Sirius][color=blue]
 > > 


```=
Listen 220.135.245.148:80
Listen 80


<VirtualHost 220.135.245.148:80>
    DocumentRoot "/usr"
    ServerName kulimi.cnmc.tw

    # Other directives here
</VirtualHost>
```
```=
Select the appropriate number [1-2] then [enter] (press 'c' to cancel): 1
Keeping the existing certificate
Created an SSL vhost at /private/etc/apache2/httpd-le-ssl.conf
Cannot find an SSLCertificateFile directive in /files/private/etc/apache2/httpd-le-ssl.conf/IfModule/VirtualHost. VirtualHost was not modified
Unable to find an SSLCertificateFile directive

IMPORTANT NOTES:
 - Unable to install the certificate
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/kulimi.cnmc.tw/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/kulimi.cnmc.tw/privkey.pem
   Your cert will expire on 2020-05-05. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot again
   with the "certonly" option. To non-interactively renew *all* of
   your certificates, run "certbot renew"
```
 ---
## 筆記
 > 善用 quote，讓我們知道是誰寫的
 > 多做共筆喔><
 > [name=Sirius][color=blue]

### Day1
 > certbot 難裝但是免費，SQL裝不起來好難過。  
 > MacOS內建apache超爽的  
 > 
 > 有域名好爽喔哈哈  
 > 別的作業系統我不知道，但是MacOS的`Apache`使用方法和別人都不一樣，如果一直`apachectl restart`都沒有報錯但是網站都沒有正常運作的話，可以試試看`apachectl configtest`  
 > [name=kulimi][color=orange]
 > > 突然想到 FreeBSD 如果 Apache 有問題 restart 會報錯，而且要看狀況會用 service apache24 status
 > > [name=Sirius][color=blue]

 > 有人提到用 `openssl` 來弄憑證，這邊是網管第十屆的總組長寫的，文章裡面提到的"高中社團寒訓"就是去年的高二XD  
 > [Create a self-signed certificate using OpenSSL](https://blog.cssuen.tw/create-a-self-signed-certificate-using-openssl-240c7b0579d3)
 > [name=Sirius][color=blue]
### Day2
>裝了很多套件以後建議裝一個port tree
>[name=陳禹璋][color=green]
### Day3 writeup
 > 不要ㄎㄧㄤ掉，等比賽完再寫喔www
 > [name=Sirius][color=blue]
>>沒關係我已經ㄎㄧㄤ掉了  
>>真的很幹
>>[name=陳禹璋][color=green]

> 不要想太多，其實還蠻簡單的  
>  
> 好啦，我的觀念是先看`hint`，照著他說的做，八成可以直接跑出答案，再不行的話就根據他提供的線索，找到flag，而flag只會藏在幾個地方，題目，檔名和檔案裡面(還有路徑上)，所以就看它給你什麼題目，`find`找到那個檔案，`grep`爆開，或是更暴力一點，直接到根目錄下，開`root`，將根目錄以下所有檔案用`grep`掃過一遍都是可以的。如果什麼都沒有找到，那就是他被隱藏起來了，目前看過藏的方法有藏在兩個檔案的不同處、中間穿插無法顯示的字元，`flag`經過加密...。總而言之，就是兵來將擋，水來土掩，他拿什麼噁心你，你就想辦法噁心回去，見招拆招。  
> 
> 而多人組隊的策略就是，不要互相干擾，我跟他原本是設定他解奇數題，我解偶數題。解完再去幫對方，避免兩個人同時解一題的情況，因為兩人一起解兩題的速度遠小於兩人各解一題。  
> 
> 至於最後卡超久的telegram bot，思緒請盡量跳躍，想到什麼就試，不要誤解回傳的資訊，各個細節都要思考一下代表什麼意思。
> [name=kulimi][color=orange]

> telegram bot 真的有這麼可怕嗎XD
> [name=Sirius][color=blue]

[**official writeup**](https://tg.pe/xeCL)

### Extra