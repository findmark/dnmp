## Set Up Lnmp with Docker-compose

### Install Requirements

- Docker [https://docs.docker.com/install/]
- Docker-compose [https://docs.docker.com/compose/install/#install-compose]

### Get Source Code
```
git clone https://github.com/findmark/dnmp.git
```
    
### Run docker-compose
```
cd dnmp   
mv .env.sample .env (change the ports base on your local environment)
sudo docker-compose up (use -d for run in daemon mode)
```
### Check Out
- [localhost](http://localhost)

### Finally
That's it, enjoy! And if u like it, subscribe it, any suggestion will be very welcome.

### Host Conf Example
```
server
    {
        listen 80;
        server_name test.com;
        index index.html index.php;
        root  /var/www/test.com;

        #include /etc/nginx/conf.d/enable-php.conf;

        location ~ \.php$ {
            fastcgi_pass   php72:9000;
            fastcgi_index  index.php;
            include        fastcgi_params;
            fastcgi_param  PATH_INFO $fastcgi_path_info;
            fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        }

        location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$
        {
            expires      30d;
        }
        location  ~ .*.(js|css|gif|jpg|jpeg|png|bmp|swf)$   {
            add_header Cache-Control no-store;
        }
        location ~ /.well-known {
            allow all;
        }

        location ~ /\.
        {
            deny all;
        }

        #location / {
        #    try_files $uri $uri/ /index.php?$query_string;
        #}

        access_log off;
    }
```

### Test

```
<?php

/**
 * redis test
 */
$redis = new Redis();
$redis->connect('redis', 6379);
echo "Connection to server successfully<br/>";
$redis->set("tutorial-name", "Redis tutorial");
echo "Stored string in redis:: " . $redis->get("tutorial-name") . "<br/>";

/**
 * mysql test
 */

$dbhost = 'mysql:3306'; 
$dbuser = 'root';      
$dbpass = '123456';      
$conn = mysqli_connect($dbhost, $dbuser, $dbpass);
if(! $conn )
{
    die('Could not connect: ' . mysqli_error());
}
echo 'successfully connect to mysql！';
mysqli_close($conn);

/**
 * mongodb test
 */
$bulk = new MongoDB\Driver\BulkWrite;
$document = ['_id' => new MongoDB\BSON\ObjectID, 'name' => '菜鸟教程'];

$_id= $bulk->insert($document);

var_dump($_id);

$manager = new MongoDB\Driver\Manager("mongodb://localhost:27017");  
$writeConcern = new MongoDB\Driver\WriteConcern(MongoDB\Driver\WriteConcern::MAJORITY, 1000);
$result = $manager->executeBulkWrite('test.runoob', $bulk, $writeConcern);
```
