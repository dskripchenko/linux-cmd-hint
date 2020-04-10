## Шпаргалка по Linux ~~и тварям которые там обитают~~
- - -
* ```>``` - перенаправление потока вывода (```cat ./*.txt > ./all_txt_files.txt```)
* ```|``` - передача результата выполнения одной команды в другую (```head -n 15 ./example.txt | tail -n 1```)
* ```&``` - одновркменный запуск комант 
* ```||```  - последовательный запуск команд
* ```&&``` - последовательный запуск команд при условии что предыдущая команда завершилась с успехом
* ```sudo```  - получение прав администратора
* ```rm `cat filename` ``` - подстановка результата выполнения одной команды в другую
* Пользовательские алиасы кладутся в ```~/.bashrc```    (```alias cl='clear'```)
* shell script (```.sh```) начинается с указания пути к интерпритатору (```#bin/bash```), для исполнения на файле нужны права на исполнение

### Навигация
Однократное нажатие ```Tab``` - автодополнение, ```Tab + Tab``` - все варианты возможных команд/файлов,
```ctrl + R``` - набор команды с автодополнение из истории, выключается повторным нажатием сочетания клавиш
up, down история команд
* ```/``` Корень сервера
* ```./``` Текущий каталог
* ```../``` Родительский каталог
* ```~/``` Домашний каталог

#### Навигация по структуре каталогов
* ```cd``` Переход по указанному пути (абсолютный или относительный)
* ```pwd``` Выведет в терминале абсолютный путь текущего каталога
* ```ls``` Выведет в терминале список всех файлов в каталоге
* ```clear``` Очистит терминал от результатов выполнения предыдущих комманд
* ```mc``` Midnight Commander

### Операции над файлами и каталогами
* ```mkdir``` Создаст каталог по указанному пути
    * ```mkdir ./example``` Создаст каталог в текущей папке
    * ```mkdir /mkdir``` Создаст каталог в корне сервра
    * ```mkdir -p ./test/example``` Создаст цепочку каталогов в текущей папке
* ```rmdir``` Удалит каталог (```rmdir ./example``` Удалит каталог в текущей папке)
* ```touch``` Создаст файл (```touch ./example.txt``` Создаст файл в текущем каталоге)
* ```rm```  Удалит файл
    * ```rm ./example.txt``` Удалил файл в текущем каталоге
    * ```rm -R ./*``` Удалит все файлы и каталоги в текущей папке
* ```cp``` Копирует файл
    * ```cp ./example.txt ~/``` Скопирует файл в домашний каталог
    * ```cp -R ./example ~/``` Скопирует все содержимое каталога example в домашний каталог
* ```mv``` Перемещает файл
    * ```mv ./example.txt ~/``` Переместит файл в домашний каталог
    * ```mv ./example.txt ./example.cfg``` Переименует файл
* ```chmod``` Устанавливает права доступа к файлам
    * ```chmod 555 ./example.txt``` Установит права на чтение и исполнение для файла
    * ```chmod -R 777 ./```  Установит права на чтение запись и исполнение рекурсивно для всего каталога
* ```chown``` Устанавливает владельца файла (```chown username ./example``` Установит нового владельца файла)
* ```ln``` Создает ссылку 
    * ```ln ./example.txt ./test/example.txt``` Создаст жесткую ссылку на файл (второе имя файла)
    * ```ln -s ./example.txt ./test/example.txt``` Создаст символьную ссылку на файл (аналог ярлыка)
* ```zip``` Создает архив
    * ```zip ./file.zip ./example.txt``` Поместит файл в архив
    * ```zip -r ./folder.zip ./example/``` Рекурсивно добавит все файлы каталога в архив
* ```unzip``` Распаковывает архив (```unzip ./file.zip``` Распакует архив)

### Просмотр/редактирование файлов
* ```cat``` Выводит в консоль содержимие файла (```cat ./example.txt``` Выведет содержимое файла в консоль)
* ```mcedit``` Откроет файл во встроенном в mc редакторе (```mcedit ./example.txt```)
* ```mcview``` Откроет файл во встроенном в mc просмотрщике (```mcview ./example.txt```)
* ```head``` Выводит в консоль первые 10 строк файла
    * ```head ./example.txt``` Выведет первые 10 строк файла
    * ```head -n 35 ./example.txt``` Выведет первые 35 строк файла
* ```tail``` Выводит в консоль последние 10 строк файла
    * ```tail ./example.txt``` Выведет последние 10 строк файла
    * ```tail -n 40 ./example.txt``` Выведет последние 40 строк файла
    * ```tail -n 50 ./example.txt | head -n 3``` Выведет 48-50 строки файла с конца
    * ```head -n 15 ./example.txt | tail -n 1``` Выведет 15ю строку с начала
    
### Поиск
* ```grep``` Поиск по шаблону
    * ```grep 'search-text' ./*``` Выведет все строки файлов в текущем каталоге содержащих search-text
    * ```grep -lr 'search-text' ./*``` Выведет имена всех файлов, содержащих search-text в содержимом файла, в текущем и всех вложенных каталогах
* ```find``` Поиск файлов
    * ```find ./ -name 'exam*'``` Выведет список файлов имя которых соответствует шаблону в текущем каталоге
    * ```find ./ -user username``` Выведет список файлов пользователя username в текущем каталоге
    
### Доступ к удаленным серверам 
* ```scp``` Копирует файла с/на удаленный сервер
    * ```scp root@host:/home/test/example.txt ./``` Скопирует файл с удаленного сервера в текущую папку
    * ```scp -r root@host:/home/test ./``` Скпирует все файлы и каталоги с удаленного сервера в текущую папку
    * ```scp ./example.txt root@host:/home/test/``` Скопирует файл на удаленный сервер
* ```rsync``` Копирует изменившиеся файлы
    * ```rsync -av --rsh='ssh' ./ root@host:/home/test``` Скопирует изменившиеся файлы на удаленный сервер
    * ```rsync -av --rsh='ssh' root@host:/home/test ./``` Скопирует изменившиеся файлы с удаленного сервера
* ```ssh``` Протокол доступа к удаленному серверу
    * ```ssh root@host``` Подключится к удаленному серверу
    * ```ssh root@host reboot``` Выполнит команду на удаленном сервере
    * ```ssh -L 127.0.0.1:1111:mysql:3306  root@host``` Поднимот тунель на удаленный сервер
    
### Вспомогательные команды
* ```tee``` Дублирует стандартный ввод на стандартный вывод или на указанный в качестве атрибута  файл
    * ```cat ./example.txt | tee ./log.txt``` Выведет содержимое файла в стандартный поток и в файл
    * ```cat ./example.txt | tee -a ./log1.txt``` Выведет содержимое файла в стандартный поток и допишет содержимое в файл
* ```du``` Оценка занимаемого файлового пространства (```du -h -d0 ./``` Выведет размер занимаемый текущей директорией )
* ```df``` Cписок всех файловых систем, размер, занятое/свободное пространство (```df -h``` Выведет список всех подключенных файловых систам с подробной информацией)
- - -
## Минимальная настройка серверного окружения centos7-nginx-php73-mariadb

* ```yum update```
* ```yum install mc htop nginx mariadb-server -y```
* ```service start nginx```
* ```service start mariadb```
* ```mysql_secure_installation```
* ```yum install epel-release -y```
* ```rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm```
* ```yum-config-manager --disable remi-php54```
* ```yum-config-manager --enable remi-php73```
* ```yum install php php-xml php-soap php-xmlrpc php-mbstring php-json php-gd php-mcrypt php-imagick php-mysql php-pdo php-fpm -y```
* ```yum install mailx sendmail -y```
* ```yum install hg git -y```
* ```service firewalld start```
* ```firewall-cmd --permanent --zone=public --add-port=59876/tcp```
* ```firewall-cmd --permanent --zone=public --add-port=80/tcp```
* ```firewall-cmd --permanent --zone=public --add-port=443/tcp```
* ```firewall-cmd --permanent --zone=public --add-port=25/tcp```
* ```firewall-cmd --permanent --zone=public --add-port=465/tcp```
* ```firewall-cmd --permanent --zone=public --add-port=587/tcp```
* ```firewall-cmd --reload```
* ```firewall-cmd --zone=public --list-ports```
* ```mcedit /etc/ssh/sshd_config```
    * установить ```Port 59876```
* ```systemctl restart sshd.service```
- - -
## Базовая конфигурация nginx для yii/yii2/laravel
```
server {
    server_name example.com;
    return 301 $scheme://www.example.com$request_uri;
}

server {
    listen 80;
    server_name www.example.com;
    root /var/www/example/public;
    access_log /var/www/log/example.access.log;
    error_log /var/www/log/example.error.log;

    client_max_body_size 32m;

    location ~* ^.+\.(ogg|ogv|svg|svgz|eot|otf|woff|mp4|ttf|rss|atom|jpg|jpeg|gif|png|ico|zip|tgz|gz|rar|bz2|doc|xls|exe|ppt|tar|mid|midi|wav|bmp|rtf)$ {
        root /var/www/example/public;
        access_log off;
        expires 3d;
    }

    gzip on;
    gzip_disable "msie6";
    gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript application/javascript;

    location ~ \.php$ {
        fastcgi_pass 127.0.0.1:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params;
        expires 0;
    }
    # nginx configuration
    location / {
        index index.php index.html;
        if (!-e $request_filename){
            rewrite ^(.*)$ /index.php;
        }
    }
}

```
- - -
## Настройка серверного ftp c виртуальными пользователями
* ```yum install epel-release proftpd proftpd-utils -y```
* ```firewall-cmd --permanent --zone=public --add-port=20-21/tcp```
* ```firewall-cmd --permanent --zone=public --add-port=40900-40999/tcp```  
* ```firewall-cmd --reload``` 
* ```mkdir /etc/proftpd.d```
* ```ftpasswd --passwd --file=/etc/proftpd.d/ftpd.passwd --name=ftpuser --uid=48 --gid=48 --home=/var/www --shell=/sbin/nologin``` (добавит виртуального пользователя ```ftpuser``` c домашним каталогом в ```/var/www```)
* Настройка ```/etc/proftpd.conf``` 
    * ```
        UseIPv6 off 
        IdentLookups off 
        PassivePorts 40900 40999 
        RequireValidShell off 
        AuthUserFile /etc/proftpd.d/ftpd.passwd 
        AuthPAM off 
        LoadModule mod_auth_file.c
        AuthOrder mod_auth_file.c 
```
