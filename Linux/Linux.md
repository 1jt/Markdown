# Linux命令

## 一.用户管理

1. **adduser**
![Alt text](assets/Linux/image.png)

2. **useradd**
![Alt text](assets/Linux/image-6.png)
这两种方式的差别是登录shell会不同
![Alt text](assets/Linux/image-7.png)
![Alt text](assets/Linux/image-8.png)

3. **deluser**
![Alt text](assets/Linux/image-1.png)

4. **ifconfig**
![Alt text](assets/Linux/image-2.png)

5. **su**与**logout**
<https://blog.csdn.net/weixin_52280661/article/details/128202943>
![Alt text](assets/Linux/image-4.png)
![Alt text](assets/Linux/image-3.png)

6. ``Ctrl + D``可 以退出账户

7. [解决XShell无法连接Ubuntu中的root用户](https://blog.csdn.net/zhanshixiang/article/details/104348192)

## 二.常用指令

### 1. 系统

1. **init**

   ``init 0``直接关机
   ``init 3``
   ![Alt text](assets/Linux/image-10.png)
   ``init 5``
   ![Alt text](assets/Linux/image-11.png)
   ``init 6``直接重启
2. **systemctl get-default**
   获取当前运行级别

### 2. 帮助指令

   1. **man**
   ![Alt text](assets/Linux/image-12.png)
   2. **help**
   ![Alt text](assets/Linux/image-13.png)

### 3. 文档目录类

   1. **pwd**
   2. **ls**
   3. **cd**
   4. **mkdir**
   5. **rmdir**
    删除的是空目录
        >rm -rf /* 最恐怖的指令
   6. **touch**
    创建空文件
   7. **cp**
    拷贝文件到指定目录
    ![Alt text](assets/Linux/image-14.png)
   8. **rm**
        >-f 强制删除不提示
        >-r 递归删除整个文件夹
   9. **mv**
    移动文件与目录重命名
        >（同一个目录下就是重命名）
   10. **cat**
    查看文件内容，只能浏览不能修改，一般会带上 管道命令|more
        >-n 显示行号
   11. **more**
    方便进行交互
    ![Alt text](assets/Linux/image-15.png)
   12. **less**
    ![Alt text](assets/Linux/image-16.png)
   13. **echo**
    输出内容到控制台
    ![Alt text](assets/Linux/image-17.png)
   14. **head**
    用于显示文件的开头部分内容，默认情况下显示前10行
   15. **tail**
        > -f 可以实时监控文件变化
        > Ctrl + C 可以退出
   16. **>**
    输出重定向
    ![Alt text](assets/Linux/image-18.png)
   17. **>>**
    追加
    ![Alt text](assets/Linux/image-19.png)
   18. **ln**
    link 软链接/符号链接，类似快捷方式
    ![Alt text](assets/Linux/image-21.png)
    ![Alt text](assets/Linux/image-22.png)
   19. **cal**
    当前日历信息
    ![Alt text](assets/Linux/image-20.png)
   20. **history**
      ![Alt text](assets/Linux/image-23.png)
      ![Alt text](assets/Linux/image-24.png)

### 4. 时间日期类

   1. **data**
      ![Alt text](assets/Linux/image-25.png)
   2. **cal**
      ![Alt text](assets/Linux/image-26.png)

### 5. 搜索查找类

   1. **find**
   2. **locate**
      > 要先updatedb
   3. **which**
      ![Alt text](assets/Linux/image-27.png)
   4. **grep**
      > 经常和管道符号“|”一起使用

      ![Alt text](assets/Linux/image-28.png)

### 6. 压缩和解压缩类

   1. **gzip/gunzip**
      > （解）压缩文件

      ![Alt text](assets/Linux/image-29.png)
   2. **zip/unzip**
      > （解）压缩文件夹

      ![Alt text](assets/Linux/image-30.png)
   3. **tar**
      ![Alt text](assets/Linux/image-31.png)

## s三.组管理和权限管理
