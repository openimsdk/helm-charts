# openim-charts

# 前提条件
用户要自己安装了k8s，并且最少有两个域名（一个域名用来做minio的api访问，一个接口用来做openimserver的api访问），
配置了好了storageclass（本实例用nfs-client为例）。ps，下个版本会推出居于一个域名的访问和居于ip的url访问。

# 安装中间件
helm add im-infra https://xxxxx.xxx
helm install im-mysql im-infra/mysql -f mysql-config.yaml
helm install im-kafka im-infra/kafka -f kafka-config.yaml
helm install im-minio im-infra/minio -f minio-config.yaml
helm install im-mongodb im-infra/mongodb -f mongodb-config.yaml
helm install im-redis im-infra/redis -f redis-config.yaml
说明：这五个配置文件，都配置了账户信息，其中minio-config.yaml还配置了域名信息

# 安装openimserver服务
helm install openimserver -f open-im-server-config.yaml -f notification.yaml ./open-im-server/
说明：要在文件open-im-server-config.yaml配置域名信息，账户信息默认和中间件的*-config.yaml是同步的，
如果前面安装了中间件时候修改了config.yaml请同步修改open-im-server-config.yaml

# 安装openimchat服务
helm install openimchat -f chat-server-config.yaml ./chat-server/
说明：要在文件chat-server-config.yaml配置域名信息，账户信息默认和中间件的*-config.yaml是同步的，
如果前面安装了中间件时候修改了config.yaml请同步修改chat-server-config.yaml

# 安装webfront
helm install imwebfront -f webfront-config.yaml ./webfront/
说明：要在webfront-config.yaml配置域名信息

# 安装adminfront
helm install imadminfront -f adminfront-config.yaml ./adminfront/
说明：要在adminfront-config.yaml.yaml配置域名信息