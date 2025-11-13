# Jupyter

## Jupyter notebook 和Jupyterlab

> Jupyterlab 替代notebook

- 安装Jupyterlab

```bash
pip install jupyterlab
#安装中文界面
pip install jupyterlab-language-pack-zh-CN
```

- 初始化配置

```
jupyter lab --generate-config
```

- 启动（默认端口8888）

```bash
jupyter-lab --allow-root --ip=0.0.0.0 
```

在浏览器中访问：http://192.168.10.200:8888

> 可以关闭selinux，防火墙
>
> 或添加防火墙端口和服务
>
>  firewall-cmd --add-port=8888/tcp --permanent
>
>  firewall-cmd --add-service=http  --permanent

![image-20211230123339756](image-20211230123339756.png)

### Jupyterhub 多用户

- 安装相关软件包

  - ```
    pip install jupyterhub
    ```

  - ```bash
    yum install npm
    npm install -g configurable-http-proxy
    ```

- 初始化配置

  - ```bash
    jupyterhub --generate-config
    ```

    > 在当前目录下生成 jupyterhub_config.py 配置文件

- 配置文件

  ```bash
  # vi jupyterhub_config.py
  ## 添加以下内容
  c.JupyterHub.ip='0.0.0.0'
  c.JupyterHub.port=8000
  c.PAMAuthenticator.encoding='utf-8'
  c.LocalAuthenticator.create_system_users=True
  c.Authenticator.whitelist={'user01','user02','user03'}
  c.Authenticator.admin_users={'admin'}
  c.JupyterHub.statsd_prefix='jupyterhub'
  ```

- 创建用户组和用户

  ```bash
  groupadd jupyterhub
  useradd -g jupyterhub admin user01 user02 user03
  passwd admin
  .....
  ```

- 启动服务(默认端口8000)

  ```
  jupyterhub -f jupyterhub_config.py 
  ```

- 访问测试

  在浏览器下访问： http://192.168.10.200:8000

  ![image-20211230122844081](image-20211230122844081.png)

  
