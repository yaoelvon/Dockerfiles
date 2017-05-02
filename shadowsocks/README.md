## shadowsocks

### 打开姿势

``` sh
docker run -dt --name ss -p 6443:6443 mritd/shadowsocks -s "-s 0.0.0.0 -p 6443 -m aes-256-cfb -k test123 --fast-open"
```

### 支持选项

- `-s` : shadowsocks-libev 参数字符串
- `-k` : kcptun 参数字符串
- `-x` : 开启 kcptun 支持
- `-m` : 指定 shadowsocks 命令，默认为 `ss-server`

### 选项描述

`-s` 参数后指定一个 shadowsocks-libev 的参数字符串，所有参数将被拼接到 `ss-server` 后；
`-k` 参数后指定一个 kcptun 的参数字符串，所有参数将被拼接到 `kcptun` 后
`-x` 指定该参数后才会开启 kcptun 支持，否则将默认禁用 kcptun
`-m` 参数后指定一个 shadowsocks 命令，如 ss-local；不写默认为 ss-server，此参数用于将
     此镜像用于不同环境，如作为客户端使用等，可选项如下：
     `ss-local`、`ss-manager`、`ss-nat`、`ss-redir`、`ss-server`、`ss-tunnel`

### 命令示例

**Server 端**

``` sh
docker run -dt --name ss -p 6443:6443 -p 6500:6500/udp mritd/shadowsocks -s "-s :: -s 0.0.0.0 -p 6443 -m aes-256-cfb -k test123 --fast-open" -k "-t 127.0.0.1:6443 -l :6500 -mode fast2" -x
```

**以上命令相当于执行了**

``` sh
ss-server -s :: -s 0.0.0.0 -p 6443 -m aes-256-cfb -k test123 --fast-open
kcptun -t 127.0.0.1:6443 -l :6500 -mode fast2
```

**Client 端**

``` sh
docker run -dt --name ss -p 1080:1080 mritd/shadowsocks -m "ss-local" -s "-c /etc/shadowsocks-libev/test.json" 
```

**以上命令相当于执行了** 

``` sh
ss-local -c /etc/shadowsocks-libev/test.json
```

**关于 shadowsocks-libev 和 kcptun 都支持哪些参数请自行查阅官方文档，本镜像只做一个拼接**

**注意：kcptun 映射端口为 udp 模式(`6500:6500/udp`)，不写默认 tcp；shadowsocks 请监听 0.0.0.0**


### 环境变量支持


|环境变量|作用|取值|
|-------|---|---|
|SS_MODULE|shadowsocks 启动命令| `ss-local`、`ss-manager`、`ss-nat`、`ss-redir`、`ss-server`、`ss-tunnel`|
|SS_CONFIG|shadowsocks-libev 参数字符串|所有字符串内内容应当为 shadowsocks-libev 支持的选项参数|
|KCP_CONFIG|kcptun 参数字符串|所有字符串内内容应当为 kcptun 支持的选项参数|
|KCP_FLAG|是否开启 kcptun 支持|可选参数为 true 和 false，默认为 fasle 禁用 kcptun|


使用时可指定环境变量，如下

``` sh
docker run -dt --name ss -p 6443:6443 -p 6500:6500/udp -e SS_CONFIG="-s 0.0.0.0 -p 6443 -m aes-256-cfb -k test123 --fast-open" -e KCP_CONFIG="-t 127.0.0.1:6443 -l :6500 -mode fast2" -e KCP_FLAG="true" mritd/shadowsocks
```

### 樱花用户说明

本镜像 3.0.3 版本之后，原来的 `/root/entrypoint.sh` 被移动到了 `/entrypoint.sh` 其他选项参数
更新为只有两个参数 `-s`(shadowsocks) 和 `-k`(kcptun)，具体使用同上以下为在樱花上测试过的同时
开启 shadowsocks 和 kcptun 的命令

``` sh
/entrypoint.sh -s "-s 0.0.0.0 -p 6443 -m aes-256-cfb -k test123 --fast-open" -k "-t 127.0.0.1:6443 -l :6500 -mode fast2" -x
```

如果仅使用 shadowsocks 那么请去除 `-k` 和 `-x` 参数即可

参考：https://github.com/mritd/docker/tree/master/shadowsocks