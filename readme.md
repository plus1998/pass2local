# 开发套件说明
因为腾讯系列开发基本都需要域名+SSL证书


所以开发阶段通过 nginx -> frps -> frpc -> local server 的形式打通到本地


本项目更多是为了提供一个思路，具体实现路径可以自己研究

# 使用说明

> 前置条件：域名已解析到服务器

### 1. 下载frp

```
https://github.com/fatedier/frp/releases/
```
解压 -> 
将frps frpc 拷贝到对应目录

> 绝大多数服务器通常是linux_amd64（已内置）如有特殊情况自行下载

> 本地自行下载对应的版本frpc

### 2. 服务器部署

1. 配置nginx
```shell
cd nginx
cp frp.conf /etc/nginx/conf.d/frp.conf
```

2. 启动frp
```shell
cd frps
chmod 777 frps
frps -c frps.toml
```

> 可以使用nohup等其他方式启动

3. Let`s Encrypt证书

> Ubuntu为例

```shell
# 安装snapd
sudo apt update
sudo apt install snapd
sudo snap install core; sudo snap refresh core
# 安装certbot
sudo snap install --classic certbot
# 获取证书
sudo /snap/bin/certbot --nginx
# 按照提示填写邮箱、同意一些条款即可
# 如果nginx配置没错，会自动获取到域名，输入识别到的域名需要完成部署
```

### 本地部署

```shell
cd frpc
chmod 777 frpc
frpc -c frpc.toml
```

> 可以将启动命令配置到package.json -> scripts中, 跟dev命令一起启动


### 测试

访问 https://yourdomain.com