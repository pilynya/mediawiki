# mediawiki
dnf install docker-compose -y
systemctl enable --now docker
nano /root/wiki.yml

services:
  wiki:
    image: mediawiki
    restart: always
    ports:
      - 8080:80
    links:
      - mariadb
    volumes:
      - images:/var/www/html/images
      # - /root/LocalSettings.php:/var/www/html/LocalSettings.php
  mariadb: # <- This key defines the name of the database during setup
    image: mariadb
    restart: always
    environment:
      MYSQL_DATABASE: mediawiki
      MYSQL_USER: wiki
      MYSQL_PASSWORD: WikiP@ssw0rd
      MYSQL_ROOT_PASSWORD: P@ssw0rd
    volumes:
      - db:/var/lib/mysql

volumes:
  images:
  db:

![image](https://github.com/user-attachments/assets/c671ab0f-7d77-4e44-ac13-b99d2b38fbb6)

docker-compose -f /root/wiki.yml up -d <br/>

на клиенте в браузере заходим по http://192.168.150.2:8080 <br/>
настройка вики <br/>
далее 
далее

![image](https://github.com/user-attachments/assets/7c5eb5b2-c3cf-4f6d-839d-899504a57e7e)

пароль базы данных: WikiP@ssw0rd <br/>
далее <br/>

![image](https://github.com/user-attachments/assets/734cf7c1-0d56-4dfc-b49a-4aeb397c530f)
![image](https://github.com/user-attachments/assets/51c84ab4-64be-4ae3-b94c-f25e6159beaf)

пароль: WikiP@ssw0rd <br/>

![image](https://github.com/user-attachments/assets/1b3ab529-a60d-4df9-844e-78b3b044aee9)

с клиента подключаемся по ssh на br-srv и забираем файл настройки <br/>
scp student@hq-cli:'/home/student/Загрузки/LocalSettings.php' /root/LocalSettings.php <br/>

![image](https://github.com/user-attachments/assets/79587138-beac-4977-909b-2434edeed1b2)

далее в файле /root/wiki.yml убираем коммент со строки <br/>

![image](https://github.com/user-attachments/assets/926c8f2c-4bba-4a2c-a900-9d2554b9a1ac)

перечитываем конфиг вики <br/>
docker-compose -f /root/wiki.yml up -d <br/>
на клиенте проверяем работающую вики http://192.168.150.2:8080 <br/>
нажимаем править и удаляем весь текст с заглавной страницы, пишем что угодно и сохраняем изменения
![image](https://github.com/user-attachments/assets/15b713de-16df-4f22-90c3-164590020589)
