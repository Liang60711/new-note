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

## 查看 container 紀錄
```sh
docker container logs <container name>
```


<br/>

## docker run
建立 container
```sh
# --detach 在背景中執行
# --name <NAME>  自訂 container 名稱
# --publish <localhost port: container port>   指定 port 號 

docker run --publish 8080:80 --detach --name website nginx
```


<br/>

## docker stop
```sh
# container id 可以打開頭前幾位即可
docker stop container <container id>
```

<br/>

## 查看當前佔用 port 
```sh
lsof -i -n | grap LISTEN
```

<br/>







