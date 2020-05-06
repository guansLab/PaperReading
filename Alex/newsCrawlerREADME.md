This is a README.md to introduce how to dump news data from alex@131.123.39.105
last update: 6th May, 2020

### Crawler Statement 
News on foxnews frontpage website has been collected automatically 4 times a day at 3am, 9am, 3pm and 9pm. 

### Connecting to server
>> ssh alex@131.123.39.105 
password: alex@guan'slab

### Dump data from mysql

News data form mysql could be dumped by software Navicat, and Navicat configuration is at below:
>> General:
  Connection name: foxnews
  Host name/IP address: localhost
  port: 3306
  Username: root
  Password: 111111
  
  
>> SSH:
  Host name/IP address: alex@131.123.39.105
  Port: 22
  Username: alex
  Password: alex@guan'slab
  


>> mysql -uroot -p 
password: 111111

>> show databases; 
use news; 
select * from foxnews into outfile "/var/lib/mysql-files/foxnews.csv" 

Then using scp command move "foxnews.csv" to personal computer.






there are 241 news in table foxnews at 23:00



