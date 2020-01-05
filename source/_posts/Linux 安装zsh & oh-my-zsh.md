### shell 概念

shell是一个命令行解释器，相当于机器外面的一层壳，用于人机交互，只要是人与电脑之间交互的借口，就可以称之为shell。表现为用户输入一条命令，shell就立即执行一条命令。不局限于系统、语言等概念、操作方式和表现方式等。 比如我们平时在黑框框里输入命令，叫 command-line interface (CLI)；在屏幕上点点点，叫graphical user interface (GUI)。

常见的shell种类有：Bsh、Csh、Ksh、Bash、Zsh

Bsh和Csh出现的较早，Ksh继承了它两的功能，Bash继承了Bsh和Ksh的升级版，而且是Linux系统中默认的shell，Zsh则兼具了各种shell的程序有点，交互式操作效率更高。很多人使用zsh而不是bash一大半原因是oh-my-zsh这个配置集。

### 安装 zsh

#### 第一步：查看系统中有无zsh及版本**

~~~bash
$ cat /etc/shells 或
$ zsh --version

$ echo $ZSH_VERSION
~~~

#### **第二步：若系统中不存在zsh，则需要安装：([更多安装方式](https://github.com/robbyrussell/oh-my-zsh/wiki/Installing-ZSH))**

~~~bash
$ sudo yum install zsh  (Fedora和RedHat以及SUSE中)
$ sudo apt-get install zsh  (Debian系列，Ubuntu，deepin)
~~~

#### **第三步：查看当前默认shell**

~~~bash
$ echo $SHELL

// 把zsh设为默认shell，如果shell列表中没有zsh或者你没有使用chsh权限的时候，不起作用
$ [sudo] chsh -s $(which zsh) 或
$ chsh -s /bin/zsh
~~~

退出重新登录后生效

#### **第四步：安装 oh-my-zsh**

安装 oh-my-zsh 之前必须安装zsh，否则会收到如下提示：Zsh is not installed! Please install zsh first!

~~~zsh
#方法一：wget方式自动化安装oh my zsh：
$ wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh

#方法二：
$ curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh 

#官网上的另外一种写法 
$ sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

#方法三：当然也可以通过git下载 
$ git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
~~~

#### **第五步：配置 oh-my-zsh**

- **查看可用主题**

  ```
  $ ls ~/.oh-my-zsh/themes
  ```

- **oh-my-zsh的默认配置文件在 ~/.zshrc,通过编辑它修改主题，更改其他配置**

  ```
  $ vim ~/.zshrc  // 修改其中的 ZSH_THEME=“主题名称”，本人使用是ys
  ```

- **退出后，应用重启终端或配置文件，配置生效**

  ```
  source ~/.zshrc
  ```

####  第六步：安装自动补齐插件（选用）

提示：补齐插件在使用git指令时会出现严重的卡顿现象，酌情使用。

- **下载插件**

  ```
  $ wget http://mimosa-pudica.net/src/incr-0.2.zsh
  ```

- **将插件移动到oh-my-zsh目录的插件库下 (~/.oh-my-zsh/plugins/incr/,如果没有incr就新建一个)**

  ```
  $ cd ~/.oh-my-zsh/plugins/incr/
  $ ls
  incr-0.2.zsh
  ```

- **在`~/.zshrc`配置文件末尾加入**

  ```
  source ~/.oh-my-zsh/plugins/incr/incr*.zsh
  ```

- **更新配置**

  ```
  $ source ~/.zshrc
  ```

- **vim冲突解决**

  使用自动补全插件可能会与vim的提示功能相冲突，如会报以下错误：

  ```
  $ vim t
  _arguments:451: _vim_files: function definition file not found
  ```

  解决方法：将`~/.zcompdump*`删除即可

  ```
  $ rm -rf ~/.zcompdump*
  $ exec zsh
  ```

> 参考文章：
>
> [Mac、Linux 安装zsh & ohmyzsh](https://www.jianshu.com/p/d194d29e488c)
>
> [你明白 shell、bash 和 zsh 等词的真正含义吗？](https://zhuanlan.zhihu.com/p/34197680)