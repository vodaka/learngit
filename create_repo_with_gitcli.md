# 1 Create a local repository
## 1.1创建本地git仓库
- $ mkdir ~/Document/git_learn
- $ cd ~/Document/git_learn
- $ git init

   Initialized empty Git repository in /home/tux/Documents/git_learn/.git/
## 1.2向仓库添加文件并提交到本地
- $ vim test.md
- $ git add test.md
- $ git status

     On branch master

     Initial commit

    Changes to be committed:

         (use "git rm --cached <file>..." to unstage)

	      new file:   test.md
- $ git commit -m "add test.md"

    [master (root-commit) 2f5cb45] add test.md

    1 file changed, 1 insertion(+)

    create mode 100644 test.md

# 2 将远程仓库与本地仓库关联，并将本地仓库推送到远程仓库
## 2.1 关联
- $ git remote add origin https://github.com/vodaka/learngit.git
> NOTE:如果在远程github上不存在learngit仓库，上面的操作是没意义的。所以上面的操作必须建立在github已存在learngit仓库。
## 2.2 推送到远程仓库
- $ git push -u origin master

    Username for 'https://github.com': vodaka
    Password for 'https://vodaka@github.com':
    Counting objects: 3, done.
    Writing objects: 100% (3/3), 222 bytes | 0 bytes/s, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To https://github.com/vodaka/learngit.git
    \* [new branch]      master -> master
    Branch master set up to track remote branch master from origin.
# 3 Extension
You can create a GitHub repo via the command line using the GitHub API. Check out the repository API. If you scroll down about a third of the way, you'll see a section entitled "Create" that explains how to create a repo via the API (right above that is a section that explains how to fork a repo with the API, too). Obviously you can't use git to do this, but you can do it via the command line with a tool like curl.
Outside of the API, there's no way to create a repo on GitHub via the command line. As you noted, GitHub doesn't allow shell access, etc., so aside from the GitHub API, the only way to create a repo is through GitHub's web interface.
## 3.1  create repo which does not exist on remote github using git api
curl -u 'nyeates' https://api.github.com/user/repos -d '{"name":"projectname","description":"This project is a test"}'
> explanation:
> - curl is a unix command (above works on mac too) that retrieves and interacts with URLs. It is commonly already installed.
> - "-u" is a curl parameter that specifies the user name and password to use for server authentication.
>    - If you just give the user name (as shown in example above) curl will prompt for a password.
>    - If you do not want to have to type in the password, see githubs api documentation on Authentication
> - "-d" is a curl parameter that allows you to send POST data with the request
>    - You are sending POST data in githubs defined API format
> - "name" is the only POST data required; I like to also include "description"
> - I found that it was good to quote all POST data with single quotes ' '
## 3.2 Define where to push to
 $ git remote add origin git@github.com:nyeates/projectname.git
 > explanation:
 > - add definition for location and existance of connected (remote) repo on github
 > - "origin" is a default name used by git for where the source came from
 >    - technically didnt come from github, but now the github repo will be the source of record
 > - "git@github.com:nyeates" is a ssh connection that assumes you have already setup a trusted ssh keypair with github.
 ## 3.3 Push local repo to github
 $ git push origin master

> explanation:
>  - push to the origin remote (github) from the master local branch
