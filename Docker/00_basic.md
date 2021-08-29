# 安裝環境及設定
## 在 zsh 上安裝 docker auto-completion
```sh
# 1. 有安裝 on-my-zsh
vim ~/.zshrc

# 2. 將 plugins 中加入後，會自動下載外掛
plugins = (... docker docker-compose)

# 3. 存擋後重啟 zsh 設定
source ~/.zshrc
```


 <br/>

 <br/>
 
 
 # Docker 指令格式
新格式: `docker <command> <sub-command> [options]`  
舊格式(still works): `docker <command> [options]`

<br/>

<br/>

## Docker 各種 command 用途
https://miro.medium.com/max/4800/1*DkIQGsv9YsPgB0dQpIfikA.png

<br/>

<br/>

# 基本指令
## 查看版本
```sh
docker version
```

<br/>

## 查看 engine config 
```sh
docker info
```

<br/>

## 查看目前 image
```sh
docker image ls
```

```sh
docker images
```

<br/>

## 查看當前 container 
```sh
# -a 可以查看已關閉的 container
docker container ls
```

```sh
docker ps
```

<br/>


## 查看 container 指令
`docker container logs` 查看 container logs 紀錄
```sh
docker container logs <container name>
```

`docker container top` 查看正在執行的 process (一個 container 可能有多個 process)
```sh
docker container top <container name>
```

`docker container inspect` 查看 container 的 config 檔案
```sh
docker container inspect <container name>
```

`docker container stats` 查看 (檢控模式) container(s) 資源使用統計，類似工作管理員


```sh
docker container stats
```
<br/>


<br/>

## 刪除 container 
container 停止時，不會自動刪除，需手動進行刪除
```sh
# container id 可以只輸入前幾位
docker container rm <container id>
```
刪除所有已關閉的 container
```sh
docker container prune
```


<br/>


## 啟動 container
`docker run` 建立 container
```sh
# --detach, -d 在背景中執行
# --name <NAME>  自訂 container 名稱
# --publish, -p <localhost port: container port>   指定 port 號 

docker run --publish 8080:80 --detach --name website nginx
```
若有兩個 container 同時執行，不會 conflict，因為 container 不同，但 localhost 的 port 就不能重複。 
```sh
# host 的 8080 port redirect 到 container_1 的 80 port;
docker container run -d -p 8080:80 nginx

# host 的 80 port redirect 到 container_2 的 80 port;
docker container run -d -p 80:80 httpd
```



<br/>


## 停止 container
`docker stop`
```sh
# container id 可以打開頭前幾位即可
docker stop container <container id>
```

<br/>

<br/>

<br/>

# 系統指令
## 查看當前佔用 port 
```sh
lsof -i -n | grap LISTEN
```

<br/>

## 查看當前執行中 process 
```sh
ps aux
```




