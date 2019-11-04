# Docker LAMP with Contao Managed Edition

## Installation

1. Do not forgot to create the nginx-proxy
2. Add 127.0.0.1 test.local to Windows hosts-file
3. Initialize container
```bash
docker-compose build && docker-compose up -d
```
4. Mariadb cannot mount volume? Open Windows-Explorer and set all permission for default user at the project-dir
5. Follow Composer-Installation and install all dependencies (./composer install)
6. Open browser and type: http://test.local/ - Well done!

## Composer
1. Build container
```bash
docker build docker/composer -t test-local/composer
```  
2. Use composer 
```bash
sh composer install or ./composer install
```  

## PHP-CLI
1. Build container
```bash
docker build docker/php-cli -t test-local/php-cli
```  
2. Use composer 
```bash
./composer install
```  

## Debugging FPM (DBGp Proxy not needed)
1. Open PhpStorm-Settings and set debug-port: 9001
2. Set at browser extension the xdebug-key: docker-xdebug
3. You became a message to configure server: ServerName and Host is docker-xdebug. Port 80

## Debugging CLI (DBGp Proxy not needed)
1. Enable Debugger at PhpStorm
2. Set xdebug-key as Server (File | Settings | Languages & Frameworks | PHP | Servers): Name and Host
3. Set absolute Path to /app
4. Execute php file web/index.php
```bash
./php-cli web/index.php
`` 
