
### 安装

官网地址：[Setup - ngrok](https://dashboard.ngrok.com/get-started/setup/macos)
按照官网教程进行安装，一定要设置authtoken

### 单启动
ngrok http http://localhost:8081

### 多应用启动（需要配置）
查看你的配置文件地址：[Configuration File | ngrok documentation](https://ngrok.com/docs/agent/config/)
找到配置文件 ngrok.yml 编辑：ngrok config check

```yaml
version: "3"
agent:
    authtoken: 2ywpuWXaEgwbcURjlxcoOFcJ24I_7ZihTqcBDa1uYGxiXtCYL
tunnels:
  sdk:
    addr: 8877
    proto: http
  af:
    addr: 8081
    proto: http
```


启动命令：

```sh
ngrok start --all
```

### 检测

http://localhost:4040/inspect/http