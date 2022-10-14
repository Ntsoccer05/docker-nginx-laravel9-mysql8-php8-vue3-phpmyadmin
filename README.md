srcフォルダを作って以下の形にする  

適当なフォルダ名  
├─ docker  
│    ├─ php  
│    │   └─ Dockerfile  
│    │   └─ php.ini  
│    ├─ nginx  
│    │    └─ Dockerfile  
│    │    └─ default.conf  
│    └─ mysql  
│         └─ Dockerfile  
│         └─ my.cnf  
│      
├─ src  
│    └─ ここにLaravelのPJディレクトが作られる  
│─ .env  
│─ .gitignore     
└─ docker-compose.yml  
  
docker compose build  
docker compose up -d  

docker compose exec app bash  

composer create-project --prefer-dist "laravel/laravel" .  

以下修正  
/src/.env  
APP_URL=http://localhost:1000  # nginxのポートと合わせる  
DB_CONNECTION=mysql  
DB_HOST=db   #docker-compose.ymlのdbのコンテナ名  
DB_PORT=3306  
#START docker-compose.ymlのdbで設定したもの  
DB_DATABASE=db  
DB_USERNAME=test  
DB_PASSWORD=test  
#END docker-compose.ymlのdbで設定したもの  
  
php artisan migrate  
  
npm install && npm run dev  
  
以下を追加  
src\vite.config.js  
```
server: {  
   host: true,  
   hmr: {  
     host: 'localhost'  
   }  
},  
```
    
