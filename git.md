## git

### 1、版本控制

- 集中式（svn）
  - 有点：
    - 代码存在单一服务器，便于项目管理
  - 缺点：
    - 服务器宕机：员工写的代码得不到保障
    - 服务器炸了：整个历史记录都会丢失
- 分布式（git）
  - 优点：
    - git每次存储的都是项目的完整快照，需要的硬盘空间相对要大一些，但git团队对代码做了极致的压缩，最终需要的实际空间只比svn大一点

### 2、区域

- 工作区
  - 程序员增删改查文件代码的地方
- 暂存区
  - 记录工作区的文件修改记录
- 版本库
  - 存储暂存区提交过来的新文件版本

### 3、底层命令

- clear：清除屏幕
- echo 'xxxx'：在控制台输出信息
- echo 'xxxx' > test.txt：创建test.txt文件，并将信息输入文件中
- ll：列出当前目录下的子文件和子目录
- find 目录名：列出指定目录下的子孙文件和子孙目录
- find 目录名 -type f：将对应目录下的文件列出
- rm 文件名：删除指定文件
- mv 源文件 重命名：重命名，相当于删了一个文件然后新增了一个文件
- cat 文件url：查看文件内容
- vim 文件url：
  - 按 i 进入文本编辑（输入法为英文状态下）
  - 按esc退出编辑模式
  - 按 :q! 强制退出
  - 按 :wq 保存退出
  - 按 :set nu 设置行号
- echo "xxx" | git hash-object -w --stdin
  - 将内容xxx以hash方式存入git数据库（git对象），该内容会生成一段hash编码，前两位作为目录名，其他位作为文件名
  - -w：将内容进行存储，若不指定此项，则不会将内容存储到git，只返回hash值
  - -stdin：从标准输入读取内容，若不指定，则命令末尾需给出待存储的文件路径
- git cat-file -p hash值：查看git数据库中的文件内容
- git cat-file -t hash值：查看git数据库中的文件类型
- git update-index --add --cacheinfo 100644 hash值 文件名：将文件加入到暂存区
  - 首次添加文件到暂存区需要加--add，之后不用再加
- git ls-files -s：查看暂存区文件
- git write-tree：将暂存区文件生成树对象

### 4、高级命令

- git init：初始化

- 会在文件夹中创建一个.git的隐藏文件，这个就是版本库
- ![image-20220406214021481](C:\Users\hq\AppData\Roaming\Typora\typora-user-images\image-20220406214021481.png)

- git add ./：将文件提交到暂存区（先生成git对象再记录到暂存区）
- git commit -a -m "注释"：将文件生成树对象，提交到git版本库中
  - -a：跳过暂存区，只有被跟踪过的文件可以。
- git status：检查文件状态（已暂存、已提交、已修改）
- git diff：查看哪些更新还未暂存的数据
- git diff --cached/staged：查看哪些已暂存还未提交的数据
- git log --oneline：查看历史记录
  - --oneline：表示每次记录放一行查看
- git rm 文件名：将指定文件删除并将修改添加到暂存区
- git mv 原文件名 新文件名：将文件重命名并添加到暂存区

### 6、分支

- 分支的本质是一个提交对象，所有的分支都会有机会被HEAD引用，但每次HEAD只能指向一个分支，当我们有新的分支提交时，HEAD会携带当前的分支往前移动
- git branch：显示分支列表
- git branch 分支名：创建分支
- git checkout 分支名：切换分支
- git checkout -b 分支名：创建新的分支并切换
  - 切换分支会改变HEAD、暂存区和工作目录
  - 在切换分支前，确保当前分支的文件都是已提交状态，否则会将无效文件带到主分支
- git branch -d 分支名：删除已合并分支，-D强制删除分支
- git branch -v：查看每一个分支的最后提交
- git branch 分支名 提交对象的hash值：创建一个新的分支指向对应的提交对象
- git log --online --decorate：查看项目分叉历史
- git reflog：查看项目完整操作历史
- git config --global alias.别名 "指令"：给指令设置别名
- git merge 分支名：合并其他分支到主分支上
  - 合并分之前确保分支上的文件都已提交
- git branch --merge：查看哪些分支已经合并到当前分支
- git branch --on-merge：查看为合并的分支列表
- git stash：将当前分支存储到栈当中
- git stash：查看存储
- git stash pop：应用储存并立即删掉栈中元素
- git checkout --文件名：撤销文件修改
  - git reset --hard 提交对象Hash：用指定的提交对象内容重置HEAD 重置暂存区 重置工作目录
- git reset HEAD 文件名：撤销暂存区
  - git reset [--mixed] 提交对象Hash：重置HEAD内容 重置暂存区
- git commit --amend：修改提交时的注释
  - git reset --soft 提交对象Hash：重置HEAD内容
- git tag：列出标签
- git  tag 标签名：创建标签
- git tag 标签名 提交对象Hash：给指定的提交对象设置标签
- git tag -d 标签名：删除指定标签
- git show 标签名：查看指定标签
- git checkout 标签名：将HEAD检出到指定标签，但会造成头部分离，需要在指定标签上创建分支

### 7、eslint

- js代码的检查工具

- 下载：npm i eslint -D

- 设置package.json文件

  - ```js
    "scripts" {
        "lint": "eslint ./src",
        "lint:create": "eslint --init"
    }
    ```

    

- 运行npm run lint:create，生成.eslintrc.js文件，提供编码规则

- eslint ./src：检查src目录下所有指定文件的编码规则是否正确

- 安装哈士奇：npm i husky --save-dev，安装前需要创建git库

- 配置package.json文件，如果编码规则不符合规范则不允许提交

  - ```js
    "husk": {
        "hooks": {
            "pre-commit": "npm run lint",
        }
    }
    ```


### 8、远程仓库（团队协作）

- 项目经理初始化远程仓库
- 项目经理创建本地仓库
  - git remote 别名 仓库地址
  - git init：创建git库，将源码复制进来
  - 修改用户名 修改邮箱
  - git add
  - git commit
  - 项目经理推送本地仓库到远程仓库
  - 清理windows凭据
  - git push 别名 分支 （输入用户名 密码；推完之后会附带生成远程跟踪分支）
- 项目邀请成员
- 成员克隆远程仓库
  - git clone 仓库地址
- 成员做出贡献
  - 修改代码
  - git add
  - git commit
  - git push 别名 分支
- 项目经理更新修改
  - git fetch 别名 （将修改同步到远程跟踪分支上）
  - git merge 远程跟踪分支
  - git pull == git fetch + git merge

### 9、远程分支

- git push 仓库地址 分支名：将分支推送到远程仓库
- git pull 仓库地址 分支名：合并远程仓库分支
- git push 仓库地址 --delete 分支名：删除远程仓库分支