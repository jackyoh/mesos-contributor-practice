## Runing Mesos Unit Test
### 執行測試程式之前需要做以下的設定
* 關閉 SWAP 指令如下
```
# swapoff -a
```
* 安裝 Docker
```
# yum install -y docker
# systemctl enable docker
# systemctl start docker
```

* CPU core 數需要 4 個以上

### 執行測試程式指令如下
```
# make check
```


### 執行單一程式指令測試如下
```
# make test
# cd $MESOS_HOME
# build/bin/mesos-test.sh --gtest_filter="AuthorizationTest*" --verbose
```