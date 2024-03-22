##### 一、另外生成一份SSH key

执行命令：

```bash
ssh-keygen -t rsa -f /c/Users/Administrator/.ssh/id_rsa_second -C "xxxxx@163.com" 
```

生成成功会在.ssh目录下看到多出两个文件：id_rsa_second和id_rsa_second.pub，同样我们把新生成的公钥添加到gitLab新账号上。

##### 二：添加密钥到 SSH Agent

执行命令：

```bash
ssh-agent bash
ssh-add /c/Users/Administrator/.ssh/id_rsa_second
```

##### 三、配置config文件

.ssh目录下默认是没有config文件的，我们手动在.ssh目录下创建一个config文件（不需要后缀）。然后用编辑器打开config文件，给新账号单独配置一个Host，Host要取一个别名，每个Host主要配置HostName和IdentityFile即可。如下：

```javascript
Host gitLab-second
HostName gitLab.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa_second
```

检查是否配置成功：

```sql
ssh -T git@gitLab-second
```

如果看到自己的昵称则表示配置成功，如：Hi (you name)! You've successfully authenticated, but GITEE.COM does not provide shell access.
 配置完成后，在连接非默认帐号的gitLab仓库时，远程库的地址要对应地做一些修改，比如现在克隆second帐号下的一个仓库xxxxx：

```bash
git clone git@gitLab-second:name/xxxxx.git
```

其实此时就可以使用了，但是网上还有其他配置

##### 四、取消全局的用户名和邮箱配置

因为一台电脑上配置了多个git账号，所以就不能再配置全局的用户名和邮箱了，而是在不同的仓库下，配置相应的局部用户名和邮箱即可。 打开 git bash，输入以下命令取消全局配置：

```css
css复制代码git config --global --unset user.name
git config --global --unset user.email
```

##### 五、为某个仓库配置用户名和邮箱

进入某个仓库根目录，打开 git bash,输入以下命令为其配置局部用户名和邮箱：

```lua
git config user.name "xx"
git config user.email "xx@xx.com"
git config --list   （查看配置）
```

https://juejin.cn/post/6992519940074897444
