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

## topic



