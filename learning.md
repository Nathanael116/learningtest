### 1.1 第一阶段：创建版本控制
想要让git对一个目录进行版本控制需要以下步骤：
- 进入要管理的文件夹  

- 执行初始化命令  
  ```
  git init
  ```  
  
- 管理目录下的文件状态
  ```
  git status
  
  (注：新增的文件和修改过后的文件都是红色)
  ```
- 管理指定文件（红变绿）
  ```
  git add 文件名
  git add .
  ```
- 个人信息配置：用户名、邮箱【一次即可】
    ```
    git config --global user.email "you@example.com"
    git config --global user.name "Your Name"
    ```
- 生成版本
  ```
  git commit -m '描述信息'
  ```
- 查看版本记录
    ```
    git log
    ```
### 1.2 第二阶段：拓展新功能
  ```
  git add 
  git commit -m '描述信息'
  ```

### 1.3 第三阶段：回滚
- 回滚至之前版本
  ```
  git log
  git reset --hard 版本号
  ```
- 回滚至之后版本
  ```
  git reflog
  git reset --hard 版本号
  ```
### 1.5 第四阶段：商城&紧急修复bug

#### 1.5.1 分支
分支可以给使用者提供多个环境的可能，意味着你可以把你的工作从开发主线上分离开来，以免影响开发主线。

#### 1.5.2 紧急修复bug方案
  ![alt text](gitlearning-1.png)

#### 1.5.3 命令总结
- 查看分支
  ```
  git branch
  ```

- 创建分支
  ```
  git branch 分支名称
  ```
- 切换分支
  ```
  git checkout 分支名称
  ```
- 分支合并（可能产生冲突）
  ```
  git merge 要合并的分支
  注意：切换分支再合并
  ```
- 删除分支
  ```
  git branch -d 分支名称
  ```

#### 1.5.4 工作流
  ![alt text](gitlearning.png)

### 1.6 第五阶段：文件上传与下载

#### 1.6.1配置网络代理：

##### 配置代理配置
  要配置 Git 中关于 GitHub 代理的配置，可以使用以下命令：
  ```bash
  git config --global http.https://github.com.proxy http://127.0.0.1:端口
  git config --global https.https://github.com.proxy http://127.0.0.1:端口
  ```
  执行后，如果之前配置成功，会分别输出对应的代理地址（即 `http://127.0.0.1:7890`）。

##### 删除代理配置
  如果想要删除之前为 GitHub 配置的代理，恢复到配置前的状态，可以使用以下命令：
  ```bash
  git config --global --unset http.https://github.com.proxy
  git config --global --unset https.https://github.com.proxy
  ```
  执行这两条命令后，再用前面查看配置的命令检查，就不会有对应的代理配置输出了，Git 也就不会再为 GitHub 的 HTTP 和 HTTPS 请求使用代理了。

#### 1.6.2 文件管理

##### 上传文件

  1. 给远程仓库起别名
     ```
     git remote add origin 远程仓库地址
     ```
  2. 向远程推送代码
     ```
     git push -u origin 分支
     ```

##### 下载文件

  1. 克隆远程仓库代码
     ```
     git clone 远程仓库地址（内部已实现git remote add origin 远程仓库地址）
     ```
  2. 切换分支
     ```
     git checkout 分支
     ```

##### 异地开发（a地）
1. 切换到`dev`分支进行开发
   ```
   git checkout dev
   ```
2. 把`master`分支合并到`dev` 【仅一次】
   ```
   git merge master
   ```
3. 修改代码
4. 提交代码
   ```
   git add .
   git commit -m 'xx'
   git push origin dev
   ```

##### 异地开发（b地）
1. 切换到`dev`分支进行开发
   ```
   git checkout dev
   ```
2. 拉代码
   ```
   git pull origin dev
   ```
3. 继续开发
4. 提交代码
   ```
   git add .
   git commit -m 'xx'
   git push origin dev
   ```
##### 开发完毕
1. 将`dev`分支合并到`master`，进行上线
   ```
   git checkout master
   git merge dev
   git push origin master
   ```
2. 把`dev`分支也推送到远程
   ```
   git checkout dev
   git merge master
   git push origin dev
   ```

等价关系
```
git pull origin dev

git fetch origin dev
git merge origin/dev
```