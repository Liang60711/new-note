# Docker Network
>Container 是個封閉的空間，有些功能開發是需要與其他 Containers甚至是外界串接的，例如 PHP, MYSQL, Apache, Nginx 彼此溝通，因此Docker network因應不同需求發展出了多種類別的network。

<br/>

## 分為以下幾種 Network
### 1. Bridge networks
>Docker 預設就是使用此網路模式，這種網路模式就像是 NAT 的網路模式，例如實體主機的 IP 是 192.168.1.10 ，會對應到 Container 裡面的 172.17.0.2，在啟動 Docker 的 service 時會有一個 docker0 的網路卡就是在做此網路的橋接。


2. Overlay networks
3. Host networking
4. Macvlan networks

<br/>

<br/>

# 指令
從主機查看 nginx container 的 IP 地址
```sh
docker container inspect --format "{{ .NetworkSettings.IPAddress}}" nginx
```

選擇 container 的 Network 類型
```sh
# --net=type
# 有 none, container, host, bridge, overlay 類型
docker container -it --net=none nginx
```