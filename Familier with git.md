## Attention：Git报错： Failed to connect to github.com port 443 解决方案

**两种情况**：
**第一种情况**自己有vpn，网页可以打开github。说明命令行在拉取/推送代码时并没有使用vpn进行代理

**第二种情况**没有vpn，这时可以去某些网站上找一些代理ip+port

**解决办法**：配置http代理Windows、Linux、Mac OS 中 git 命令相同：
配置socks5代理

git config --global http.proxy socks5 127.0.0.1:7890
git config --global https.proxy socks5 127.0.0.1:7890
**配置http代理**

git config --global http.proxy 127.0.0.1:7890
git config --global https.proxy 127.0.0.1:7890

注意：

命令中的主机号（127.0.0.1）是使用的代理的主机号(自己电脑有vpn那么本机可看做访问github的代理主机)，即填入127.0.0.1即可，否则填入代理主机 ip(就是网上找的那个ip)
命令中的端口号（7890）为代理软件(代理软件不显示端口的话，就去Windows中的代理服务器设置中查看)或代理主机的监听IP，可以从代理服务器配置中获得，否则填入网上找的那个端口port 

![img](https://img-blog.csdnimg.cn/8e6fdc89ebe64cdfbb768d42ec203b3a.png)

socks5和http两种协议由使用的代理软件决定，不同软件对这两种协议的支持有差异，如果不确定可以都尝试一下
主机号和端口号可在代理的位置查看(自己有vpn的需要查看)



 ![img](https://img-blog.csdnimg.cn/9ee56b335ab7471ca882a58f4b0ec963.png)

**查看代理命令**

git config --global --get http.proxy
git config --global --get https.proxy

**取消代理命令**

git config --global --unset http.proxy
git config --global --unset https.proxy

## 1.**创建GitHub账户和仓库**:

GitHub是一个基于Git的版本控制系统，允许用户创建仓库（repository）来存储和管理项目。在这个步骤中，你会创建一个GitHub账户，然后创建一个新的仓库来托管你的项目。

1. 如果你还没有GitHub账户，首先需要在[GitHub官网](https://github.com/)注册一个账户。
2. 登录后，点击右上角的"+"按钮，选择"New repository"创建一个新的仓库。
3. 填写仓库名称，描述，选择仓库类型为公开，并可以选择初始化README，.gitignore和License。

## 2. **克隆仓库到本地**:

克隆（Clone）操作会创建仓库的一个本地副本。这样，你可以在本地机器上编辑文件，然后将更改推送（push）回GitHub。

1. 安装[Git](https://git-scm.com/downloads)。

2. 打开命令行，运行以下命令，将GitHub仓库克隆到本地：

   ```bash
   git clone https://github.com/your-username/your-repository.git
   ```

## 3. **配置Git**:

在提交更改时，Git需要知道你是谁。通过配置用户名和邮箱，你的每个提交都会包含这些信息，以便其他人知道谁做了哪些更改。

1. 在命令行中，运行以下命令，配置你的用户名和邮箱：

   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   ```

2. 在配置了Git后，你可以使用以下几种方法来查看当前的配置设置：

   1. **查看所有配置**: 你可以使用`git config --list`命令来查看所有的配置设置。这会显示所有的配置，包括全局配置、系统配置和当前仓库的局部配置：

      ```bash
      
      git config --list
      ```

   2. **查看特定配置**: 如果你想查看特定的配置项，你可以使用`git config`命令，后跟配置项的名称。例如，要查看你配置的用户名称和邮箱，你可以运行：

      ```bash
      git config user.name
      git config user.email
      ```

   3. **查看配置文件**: Git的配置存储在几个配置文件中。你可以直接打开并查看这些文件以了解当前的配置设置：

      - **全局配置**通常位于你的用户目录下的`.gitconfig`文件中，路径通常是`~/.gitconfig`。
      - **系统配置**通常位于`/etc/gitconfig`文件中。
      - **局部配置**（针对当前仓库的配置）位于仓库目录下的`.git/config`文件中。

      你可以使用文本编辑器打开这些文件并查看其中的配置。

   4. **使用图形化界面**: 你也可以使用图形化的Git客户端来查看和编辑配置。许多Git客户端，如SourceTree或GitHub Desktop，都提供了友好的界面来查看和管理Git配置。

## 4. **创建和切换到一个新的分支**:

分支（Branch）是Git中的核心概念之一，允许你在不影响主线（通常称为`main`或`master`）的情况下工作。创建一个新分支可以帮助你组织你的工作，并保持主线的稳定。

> 在Git版本控制系统中，分支（branch）是一个核心的概念，它有许多重要的作用：
>
> 1. **并行开发**: 分支允许多个开发人员或团队同时在同一项目上进行工作，而不会相互干扰。每个人可以在自己的分支上进行开发，然后通过合并（merge）操作将更改集成到主分支中。
> 2. **功能隔离**: 分支提供了一个隔离的环境，让你可以安全地开发和测试新功能或修复。通过创建一个新分支，你可以在不影响项目的主线的情况下进行实验和探索。
> 3. **代码审查**: 在GitHub或其他基于Git的版本控制平台上，分支通常用于创建Pull Requests（PRs），这是一个代码审查的过程。通过PRs，团队成员可以评审、讨论和批准分支中的更改，然后再将其合并到主分支中。
> 4. **版本控制和回溯**: 通过为每个新功能或修复创建一个新分支，你可以清晰地记录项目的历史。如果在将来需要回溯到某个特定点，你可以轻松地找到并检出（checkout）相应的分支。
> 5. **易于合并和解决冲突**: 分支提供了一个框架，使得合并更改和解决合并冲突变得更为容易。在合并分支时，Git会尝试自动合并更改，如果出现冲突，它会提供工具来手动解决。
> 6. **持续集成/持续部署（CI/CD）**: 在持续集成和持续部署的环境中，分支是非常重要的。通常，每个分支的更改都会通过自动测试，只有在测试成功后，更改才会被合并到主分支，并可能会自动部署到生产环境。
> 7. **灵活的工作流管理**: 分支提供了创建和管理多种工作流的可能。例如，你可以有一个开发分支（develop），用于日常开发，一个阶段分支（staging），用于预发布测试，以及一个主分支（main或master），用于生产发布。

1. 运行以下命令，创建并切换到一个新的分支，例如`develop`

   ```bash
   git checkout -b develop
   ```

2. **一次只能对一个分支提交修改**: 是的，你一次只能在一个分支上做修改和提交。每次你做修改并提交时，这些修改都会保存到你当前所在的分支。如果你想在另一个分支上做修改，你需要先切换到那个分支。

3. **未提交的修改**: 如果你在一个分支上做了一些修改，但还没有提交，然后你切换到另一个分支，Git默认不会让你切换，因为这样可能会丢失未提交的修改。但如果你仍然想切换分支，你有以下几个选择：

   - **提交修改**：你可以提交你当前分支上的修改，然后安全地切换到另一个分支。
   - **暂存修改**：使用`git stash`命令可以暂存你的修改，让工作目录变得干净，然后你可以切换到另一个分支。稍后，你可以使用`git stash apply`命令来恢复暂存的修改。
   - **放弃修改**：如果你不想保留当前的修改，你可以使用`git reset --hard`命令来重置你的工作目录，并放弃所有未提交的修改。

4. **修改记录的可见性**: 在Git中，只有当你执行`git commit`命令并创建一个新的提交时，你的修改才会被记录下来。如果你没有提交你的修改，那么Git不会保存这些修改的历史记录。每次你做出新的修改并提交时，一个新的提交会被创建，包含你在该时刻的所有修改。前一次未提交的修改不会被单独记录下来，除非你在做出这些修改后执行了`git commit`命令。

5. 总的来说，`git commit`是保存你修改历史的关键步骤。如果你想保留你的修改历史，你需要确保在切换分支或做其他操作之前提交你的修改。

> 分支的一些操作
>
> 在Git中，你可以通过多种方式查看和操作分支。以下是一些常用的命令和操作：
>
> ### 查看分支:
>
> 1. **列出所有分支**:
>
>    ```bash
>    git branch
>    ```
>
>    这个命令会显示所有的本地分支。当前活动分支会以一个星号 (*) 标记。
>
> 2. **列出远程分支**:
>
>    ```bash
>    git branch -r
>    ```
>
>    这个命令会显示所有的远程分支。
>
> 3. **列出所有本地和远程分支**:
>
>    ```bash
>    git branch -a
>    ```
>
>    这个命令会显示所有的本地和远程分支。
>
> ### 创建分支:
>
> 1. **创建新分支**:
>
>    ```bash
>    git branch branch-name
>    ```
>
>    这个命令会创建一个新的本地分支，但不会切换到这个分支。
>
> 2. **创建并切换到新分支**:
>
>    ```bash
>    git checkout -b branch-name
>    ```
>
>    这个命令会创建一个新的本地分支，并立即切换到这个分支。
>
> ### 切换分支:
>
> 1. 切换到一个已存在的分支
>
>    ```bash
>    git checkout branch-name
>    ```
>
> ### 删除分支:
>
> 1. **删除本地分支**:
>
>    ```bash
>    git branch -d branch-name
>    ```
>
>    如果分支上的更改已经被合并，使用上述命令删除本地分支。如果分支上的更改尚未合并，你需要使用`-D`选项来强制删除分支：
>
>    ```bash
>    git branch -D branch-name
>    ```
>
> 2. **删除远程分支**:
>
>    ```bash
>    git push origin --delete branch-name
>    ```
>
> ### 重命名分支:
>
> 1. 重命名本地分支
>
>    ```bash
>    git branch -m old-branch-name new-branch-name
>    ```
>
> ### 查看分支历史:
>
> 1. 查看特定分支的提交历史
>
>    ```bash
>    git log branch-name
>    ```
>
> ### 合并分支:
>
> 1. 将一个分支合并到当前分支
>
>    ```bash
>    git merge branch-name
>    ```
>
> 这些基本的分支操作能帮助你管理项目的不同开发阶段和功能。通过有效使用分支，你可以保持代码的组织性，隔离开发过程中的不同部分，并确保主分支的稳定性。

## 5. **提交修改**:

当你对项目做出更改时，你需要提交（commit）这些更改。每个提交都是项目历史的一个快照，记录了在该点上的文件状态。

1. 对项目进行修改，然后运行以下命令，查看你做了哪些修改：

   ```bash
   git status
   ```

2. 添加你想要提交的修改：

   ```bash
   git add .
   ```

3. 提交你的修改，并写一个清晰的提交消息：

   ```bash
   git commit -m "Describe your changes here"
   ```

## 6. **推送修改到GitHub**:

推送操作会将你的本地更改发送到GitHub仓库。这样，其他人可以看到你的更改，而你也可以在其他设备上访问这些更改。

1. 运行以下命令，将你的修改推送到GitHub仓库的

   `bash`

   分支：

   ```bash
   git push origin develop
   ```

## 7. **生成修改日志**:

Git记录了所有的提交，包括谁做了更改，何时做了更改，以及做了什么更改。通过查看提交历史，你可以生成一个修改日志，了解项目的发展过程。

1. 在本地，你可以使用

   `git log`

   命令来查看提交历史：

   ```bash
   git log
   ```

2. 或者，你可以使用一些图形化的工具，如[SourceTree](https://www.sourcetreeapp.com/)，或者在GitHub网站上直接查看提交历史。

```bash
$ git log
commit 2ec5dd512db501f0555db0ab133994f9c189836b (HEAD -> add_declaration_file, origin/add_declaration_file)
Author: StuckedCat <529853411@qq.com>
Date:   Fri Oct 6 09:50:08 2023 +0800

    Add a file describe how to use git

commit 5943a98b74feaff18d5be2555f6d2027e92462a3 (origin/main, origin/HEAD, main)
Author: thestuckedcat <46860100+thestuckedcat@users.noreply.github.com>
Date:   Thu Oct 5 19:33:18 2023 +0800

    Initial commit

```

输出的信息是`git log`命令的结果，它显示了仓库的提交历史。每个“commit”条目都代表了一个单独的提交。让我们逐行解读输出的信息：

1. **第一个提交**:

   - ```bash
     commit 2ec5dd512db501f0555db0ab133994f9c189836b (HEAD -> add_declaration_file, origin/add_declaration_file)
     ```

     - `commit 2ec5dd512db501f0555db0ab133994f9c189836b`: 这是提交的哈希值，它是一个唯一的标识符，用于标识这个特定的提交。
     - `(HEAD -> add_declaration_file, origin/add_declaration_file)`: 这表示当前的`HEAD`指针指向`add_declaration_file`分支，而这个分支在本地和远程仓库（`origin`）上都有。

   - `Author: StuckedCat <529853411@qq.com>`: 这是提交的作者信息，包括作者的名字和邮箱地址。

   - `Date: Fri Oct 6 09:50:08 2023 +0800`: 这是提交的日期和时间。

   - `Add a file describe how to use git`: 这是提交的消息，它描述了此次提交的内容或目的。

2. **第二个提交**:

   - ```bash
     commit 5943a98b74feaff18d5be2555f6d2027e92462a3 (origin/main, origin/HEAD, main)
     ```

     - `commit 5943a98b74feaff18d5be2555f6d2027e92462a3`: 这是另一个唯一的提交哈希值。
     - `(origin/main, origin/HEAD, main)`: 这表示该提交是`main`分支的一部分，同时也是远程仓库（`origin`）的`main`分支和`HEAD`指针的位置。

   - `Author: thestuckedcat <46860100+thestuckedcat@users.noreply.github.com>`: 这是第二个提交的作者信息。

   - `Date: Thu Oct 5 19:33:18 2023 +0800`: 这是第二个提交的日期和时间。

   - `Initial commit`: 这是第二个提交的消息，通常“Initial commit”表示这是仓库的第一个提交。

## 8. **创建Pull Request**:

Pull Request（PR）是GitHub中的一个功能，允许你请求将一个分支的更改合并到另一个分支。通过PR，你可以让其他人审查你的代码，并在代码合并前讨论更改。

1. 回到GitHub仓库页面，点击"Pull requests"，然后点击"New pull request"。
2. 选择你想要合并的分支，例如从`develop`到`main`，然后点击"Create pull request"。

## 9. **合并修改**:

合并操作将你的分支中的更改应用到目标分支（例如，`main`）。这是将你的工作集成到项目的主要方法。

1. 在Pull Request页面，点击"Merge pull request"，然后点击"Confirm merge"来合并你的修改到`main`分支。

## 10. **同步最新的更改**:

当你的更改被合并后，你需要同步这些更改到你的本地`main`分支，以确保你拥有最新的代码。

1. 在本地，切换回

   `main`

   分支，并拉取最新的更改：

   ```bash
   git checkout main
   git pull origin main
   ```

这样，你就创建了一个基本的GitHub项目工作流，并成功地进行了一次修改和合并。在实践中，你可能还会需要学习更多关于Git和GitHub的知识，以便更有效地管理你的项目。

# 例子

好的，让我们通过一个简单的项目来模拟GitHub工作流程。假设你正在创建一个网站，现在想要添加一个新功能，比如一个“联系我们”页面。以下是你可能会遵循的步骤：

1. **创建GitHub仓库**:

   - 首先，在GitHub上创建一个新的仓库，例如名为`my-website`的仓库。

2. **克隆仓库到本地**:

   ```bash
   git clone https://github.com/your-username/my-website.git
   cd my-website
   ```

3. **配置Git**:

   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   ```

4. **创建并切换到一个新分支**: 为“联系我们”页面创建一个新分支：

   ```bash
   git checkout -b add-contact-page
   ```

5. **添加新功能**:

   - 在你的项目中创建一个新的文件，比如`contact.html`，并添加一些内容，例如表单和联系信息。

6. **查看和提交修改**:

   ```bash
   git status  # 查看你做了哪些修改
   git add contact.html  # 添加新文件到暂存区
   git commit -m "Add contact page"  # 提交你的修改
   ```

7. **推送修改到GitHub**:

   ```bash
   git push origin add-contact-page
   ```

8. **创建Pull Request**:

   - 回到GitHub仓库页面，点击"Pull requests"，然后点击"New pull request"。
   - 选择你想要合并的分支，即从`add-contact-page`到`main`，然后点击"Create pull request"。

9. **代码审查**:

   - 你或你的团队成员现在可以在Pull Request页面上审查代码，讨论更改，并提出建议。

10. **合并修改**:

    - 一旦代码审查完成，并且所有人都满意，点击"Merge pull request"，然后点击"Confirm merge"来合并你的修改到`main`分支。

11. **同步最新的更改**:

    ```bash
    git checkout main
    git pull origin main
    ```

12. **查看修改日志**:

    ```bash
    git log
    ```

现在，你已经成功地通过一个新的分支添加了一个新功能，并通过Pull Request和合并流程将其集成到了项目的主分支中。在这个过程中，你可以看到分支如何帮助你隔离更改，同时保持主分支的稳定性，以及如何通过GitHub的Pull Request流程来审查和讨论代码。