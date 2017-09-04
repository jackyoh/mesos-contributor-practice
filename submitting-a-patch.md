## Submitting a Patch
以下是在建立 Patch 的流程和需要準備的東西

### 在寫 code 之前的準備

* 註冊 [Apache JIRA](https://issues.apache.org/jira/browse/mesos/) 帳號

* 註冊 [Apache Review Board](https://reviews.apache.org/) 帳號

* 到 Apache 的 Git Repository 把 Mesos source code clone 到 local

* 加入 mailing list
    * dev-subscribe@mesos.apache.org
    * issues-subscribe@mesos.apache.org
    * reviews-subscribe@mesos.apache.org
    * builds-subscribe@mesos.apache.org

* 在 JIRA 上搜尋目前還沒有被 unassigned 的 issue 或是自己建立一個 issue

* Assign issue 給自己

* 在 `contributors.yaml` 檔案加入 name, emails, jira_user, reviewboard_user...等等的資訊, 並且要在 GitHub 上開 Pull Request

* 規劃要如何解決問題並且寫到 JIRA 的 comments 上

* 指定一個適合的 shepherd 在 patch 裡。 shepherd 是 Mesos 的 committer 他會給一些 feedback, 最後會把修改的程式 commit 到 Mesos source tree 

* shepherd 可以在 [committer](https://github.com/apache/mesos/blob/master/docs/committers.md) 的文件找到


### 建立 Patch
* 在開始修改 code 之前先撰寫測試程式, 證明程式是有 Bug 或是新增功能的 test case
 
* 實際去修改程式

* 修改完程式之後, 執行測試程式
```sh
$ make tests
S make check
```

* 如果要執行 single test 指令如下
```sh
$ build/bin/mesos-test.sh --gtest_filter="AuthorizationTest*" --verbose
```

* commit code 需要注意以下幾件事 
    * 在每一次 commit code 時，代表單一的程式邏輯改變，這樣會比較好閱讀程式
    * 修改程式邏輯 commit code 時，不要改錯字或是 code style，才不會造成程式很難閱讀
    * commit code 時註解需要使用過去式，並且第一句話要先說明總結(Summary)，然後不要超過 72 個字元
    
* 確認目前mesos local branch 的 code 要和 mesos remote master branch 的 code 同步, 指令如下
```sh
$ git checkout master
$ git pull
$ git checkout my_branch
$ git diff master
$ git rebase master
```

### Submit Patch
* 安裝 Review Board Command 工具, 指令如下
```sh
$ yum install -y RBTools
```
* 設定 post-review 指令如下
```sh
$ cd $MESOS_HOME
$ ln -s support/reviewboardrc .reviewboardrc
$ rbt status
```

* 執行 post-review 指令如下
```sh
$ python support/post-reviews.py
```

* 把 code 送出去

* 等待 Mesos developer 進行 code review 的動作, 他們會給一些 feedback
    * Review Board 的 comment 用來討論 code-specific
    * JIRA 的 comment 用來討論 design

* 等待收到 Mesos commiter 傳回的 Ship it

* 增加功能或修改 Bug 之後要確保文件已經更新了
