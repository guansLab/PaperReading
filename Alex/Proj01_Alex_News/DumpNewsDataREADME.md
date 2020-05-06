This is DumpNewsDataREADME.md to introduce how to dump news data from alex@131.123.39.105<br/>

### Crawler Statement 
News has been collected from "Foxnews".<br/>
News has been collected automatically 4 times a day at 3am, 9am, 3pm and 9pm. <br/>

### Dump data from mysql

1. Contact Alex to get news data by email: suzhaoyuan555@gmail.com<br/>

2. News data form mysql could be dumped by software Navicat, and Navicat configuration is at below:
> General:<br/>
  Connection name: foxnews<br/>
  Host name/IP address: localhost<br/>
  port: 3306<br/>
  Username: root<br/>
  Password: 111111<br/>
  
> SSH:<br/>
  Host name/IP address: alex@131.123.39.105<br/>
  Port: 22<br/>
  Username: alex<br/>
  Password: alex@guan'slab<br/>
  

3. news data also could be dumped by mysql command.<br/>
Connecting to server<br/>
> ssh alex@131.123.39.105 <br/>
password: alex@guan'slab

&nbsp;&nbsp;Connecting to mysql<br/>
> mysql -uroot -p <br/>
password: 111111

> show databases; <br/>
use news; <br/>
select * from foxnews into outfile "/var/lib/mysql-files/foxnews.csv" <br/>
Then using ‘scp’ command move "foxnews.csv" to aim location.<br/><br/><br/>

last update: 6th May, 2020<br/>
There are 241 news in table foxnews at 23:00, 5th May, 2020.



