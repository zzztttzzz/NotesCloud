## 得到当前的shell script绝对存放路径

```bash
shPath=$(cd $(dirname $0); pwd)
```

* `dirname`可以得到传入变量的上一级相对路径例如：

  ```bash
  zqj@Y9000X:/$ dirname /a/b/c
  /a/b
  zqj@Y9000X:/$ dirname /a
  /
  zqj@Y9000X:/$ dirname ./a/b
  ./a
  ```

* `$0`代表了传给当前解释器的文件路径，可以是相对可以是绝对，取决于terminal中的运行文件的方式：
在~下新建`test.sh`文件，内容为：
  
  ```bash
  #!/bin/bash
  echo $0
  ```
  
  在terminal中运行效果：
  
  ```bash
  zqj@Y9000X:~$ bash test.sh
  test.sh
  zqj@Y9000X:~$ cd /
  zqj@Y9000X:/$ bash ~/test.sh
  /home/zqj/test.sh
  ```
  
* 所以要得到绝对路径需要首先`cd`到目录下然后`pwd`输出绝对路径，如果直接使用`shPath=$(pwd)`则会返回调用`test.sh`脚本的工作目录，导致出错。

## 统计当前文件夹下文件或者目录个数

```bash
ls -l |grep "^-"|wc -l   #文件
ls -l ./|grep "^d"|wc -l   #目录
```



## `scp`命令中断并继续传文件，关闭terminal也能继续

```bash
scp -P XXX [source] [destination]
Ctrl+z
disown -h %1
bg
```



## 删除空文件夹

```bash
rmdir *
```



## 统计文件夹大小

* `ls -ll`(以byte为单位)或`ls -lh`（以KB或MB为单位），缺点是只能查看文件大小，若是文件夹只会显示文件夹的大小。

* 使用`du`命令

  ```
  du -sh  				#统计总和以kb, Mb,Gb形式
  du -sl  				#统计总和显示byte
  du -h -max-depth=1 *  	#统计当前
  ```

  

## PBS作业管理

* `qsub`提交任务
* `qstat`查询任务
* `qdel`删除特定ID的任务



## ls返回值存放到一个数组中

* ```shell
  count=0
  for file in $(ls)
  do
    filelist[$c]=$file
    count=`expr $c + 1`
  done
  ```

* 数组的创建，使用括号：

  ```shell
  arr=(1 2 3 4 5)
  ```

  数组的下标使用中括号，配合大括号取变量：

  ```shell
  zqj@Y9000X:~$ echo ${arr[0]}
  1
  ```



## 删除旧的公钥

服务器地址变更，原有的RSA无法认证，删除

* ```shell
  ssh-keygen  -R "[ip]:port"
  ```

  