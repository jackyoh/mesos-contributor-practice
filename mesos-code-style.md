## Test clang for Mesos code style

### 在CentOS 7.3 安裝 Clang 指令如下
```
# yum install -y epel-release
# yum install -y clang
```

### 使用 clang-format 將 code 排版
```
# clang-format -i -style=google *.cpp
```

有想要把 clang-format 這個工具整合到 CentOS 7.3 上 vim 但沒有成功, 之後有使用Ubuntu 14.04 執行成功


### 在 Ubuntu 14.04 執行 clang, 步驟如下

* 安裝指令如下：
```
# sudo apt-add-repository "deb http://llvm.org/apt/trusty/ llvm-toolchain-trusty main"
# sudo apt-get update
# sudo apt-get install clang-format-3.8
```

* 需要在 $HOME 資料夾下面建立 .vimrc 的檔案，內容如下
```
map <C-K> :pyf /usr/share/vim/addons/syntax/clang-format-3.8.py<cr>
imap <C-K> <c-o>:pyf /usr/share/vim/addons/syntax/clang-format-3.8.py<cr>
```
這樣就可以在 vi 編輯下執行程式碼的編排，主要的執行方式就是在 vi 執行 NORMAL、 VISUAL 和 INSERT Mode 都可以安下 ctrl + k 執行編排程式碼的動作

另外如果 vi 要進入 VISUAL Mode 的主要方式是先按 Esc 再按 v 鍵


### Mesos Naming
* 一般變數命名主要是用 lowerCamelCase 和 snake_case
* Constant Names 主要是用 SCREAMING_SNAKE_CASE
* Function Names 主要是用 lowerCamelCase 和 snake_case
* Class Name 主要是用 UpperCamelCase

### 註解(Comments)
* 每個句子的結尾都要用標點符號標記
* 使用 ```//`` 中間要空一隔空白
```
// Hello World
```
* 如果在註解裡有寫 object/variable/function name 要用反引號框住
```
// Use `SchedulerDriver::acceptOffers()` to send several offer
```

### 縮排
* Access modifier 不縮排, 如(```public:```, ```private:```)
* Constructor initializer 使用 2 個空白

### Templates 定義如下
```
template <typename T>
```

### 延續前一行(Continuation)
* assignment statement 如果換新的一行, 要比前一行多 2 個縮排
```
Try<Duration> failoverTimeout =
  Duration::create(FrameworkInfo().failover_timeout());
```

### 每個檔案最後要加空白

### 檔案的 Header
* 要有 "ASF" 和 "Apache License Version 2.0" header

### include 標頭檔的順序
* include 標頭檔的順序是按照英文字母的順序排序