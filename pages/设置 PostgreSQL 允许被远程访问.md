tags:: [[tagPostgreSQL]]

- ## 环境
	- 以以下环境、版本为例
	- 操作系统：CentOS7
	- PostgreSQL：9.4.6
- 找到 postgresql 的安装目录，每个版本的安装目录略有不同
- ## 修改 postgresql.conf
	- 编辑或添加下面一行，使 PostgreSQL 可以接受来自任意IP的连接请求
	- ```conf
	  listen_addresses = '*'
	  ```
- ## 修改 pg_hba.conf
	- `pg_hba.conf` 位置与 `postgresql.conf` 相同，虽然上面配置允许任意地址连接 PostgreSQL ，但是这在 pg 中还不够，我们还需在 `pg_hba.conf` 中配置服务端允许的认证方式。任意编辑器打开该文件，编辑或添加下面一行。
	- ```conf
	  # TYPE  DATABASE  USER  CIDR-ADDRESS  METHOD
	  host  all  all 0.0.0.0/0 md5
	  ```
	- 默认 pg 只允许本机通过密码认证登录，修改为上面内容后即可以对任意 IP 访问进行密码验证。对照上面的注释可以很容易搞明白每列的含义，具体的支持项可以查阅文末参考引用
	- 完成上两项配置后重启 PostgreSQL 服务，允许外网访问的配置就生效了