准备测试下工具类RedisCluster.java

    原先的集群很久未曾使用，虚拟机绑定的ip已经产生变化，造成redis集群无法连接；因此看能否把虚拟机ip绑定，以及重新搭建redis集群
    
 > 删除每个reids0*目录下的nodes.conf文件
    
 >重新创建集群
    ```
    redis进群创建脚本 
    --replicas 1 表示自动为每个master节点分配一个slave节点
    前主（7001，7002，7003）后从（7004，7005，7006）
    ./redis-trib.rb create --replicas 1 192.168.188.132:7001 192.168.188.132:7002 192.168.188.132:7003 192.168.188.132:7004 192.168.188.132:7005 192.168.188.132:7006 

    ```
    
>集群关闭
    ```
    redis集群关闭脚本
    -h ip 不写默认连接127.0.0.1
    -p 端口 不写默认为6379
    redis01/redis-cli  -h 192.168.188.132 -p 7001 shutdown
    redis01/redis-cli  -h 192.168.188.132 -p 7002 shutdown
    redis01/redis-cli  -h 192.168.188.132 -p 7003 shutdown
    redis01/redis-cli  -h 192.168.188.132 -p 7004 shutdown
    redis01/redis-cli  -h 192.168.188.132 -p 7005 shutdown
    redis01/redis-cli  -h 192.168.188.132 -p 7006 shutdown
    
    ```
    