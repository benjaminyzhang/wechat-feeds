# WeChat-Feeds

<div align=center><img src="img/wechat.png" height="160" width="160" /></div>

* [WeChat-Feeds](#wechat-feeds)
   * [声明](#声明)
   * [如何使用](#如何使用)
   * [如何添加/修改公众号](#如何添加修改公众号)
   * [FAQ](#faq)
      * [如何获取 bizid?](#如何获取-bizid)
      * [服务是否稳定?](#服务是否稳定)
      * [feeds 更新频率如何?](#feeds-更新频率如何)
      * [数量是否有上限?](#数量是否有上限)
      * [是否有隐私风险?](#是否有隐私风险)
      * [是如何爬取的?](#是如何爬取的)
      * [csv 转义方式](#csv-转义方式)
   * [结构](#结构)
      * [main](#main)
      * [feeds](#feeds)
      * [pages](#pages)
   * [TODO](#todo)
   * [捐赠](#捐赠)

---

> 给微信公众号生成 RSS 订阅源  

> 列表页 [https://wechat.privacyhide.com/](https://wechat.privacyhide.com/)  

众所周知, 微信公众号比较封闭, 爬取也有一定门槛, 对于 RSS 重度用户来说很不友好, 加上如今订阅号的推送也是乱序时间轴的, 作为在推荐算法的重重包围下做挣扎的一员, 希望在此借助 Github 为同好提供有限的订阅服务.

---
## 声明

收录的公众号均来自网友提交或者采集自公开榜单, 不代表任何立场; 所有内容均为手动抄录, 未进行任何逆向工程.

--- 
## 如何使用

1. 所有 feeds 将采用 [Atom](https://tools.ietf.org/html/rfc4287) 标准, 请确保你的 RSS 订阅工具支持这种标准  

2. 在 [列表页](https://wechat.privacyhide.com/) 中搜索你想要订阅的公众号, 点击复制链接

---
## 如何添加/修改公众号

> 本指南只针对不是很熟悉 github 的朋友, 方便大家直接在网页上提交 pr, 老手可忽略~

1. 首先要有一个 github 账户: [注册](https://github.com/join?source=login) | [登录](https://github.com/login)

2. 如果你不熟悉 GitHub 同步上游的操作, 就先在浏览器中打开 `https://github.com/<你的github用户名>/wechat-feeds/settings#danger-zone`, **如果能成功访问没有 404**, 说明你之前 fork 过, 则点击 `Delete this repository` 并按照提示操作来删除你 fork 后的仓库. **同时这也是接下来每一步操作遇到问题时的通用解决办法**.

![delete](img/how-to-pr/delete.png)

3. 在浏览器中打开 [list.csv](https://github.com/hellodword/wechat-feeds/blob/main/list.csv), 先搜索有没有你需要的公众号, 确定没有则点击箭头指示的编辑按钮, 开始编辑

![edit-01](img/how-to-pr/edit-01.png)

4. **注意事项**:
   1. 可以一次性添加多个, 但同一个pr里不建议超过20个, 可以多次提交pr.
   2. 请确认自己的输入法, 分隔的标点符号为半角符号, 而不是全角符号, 区别请自行搜索
   3. 直接在网页上拉到行尾添加, 以免破坏文件格式
   4. 获取 `bizid`, 参见 [如何获取 bizid](#如何获取-bizid)
   5. `name` 和 `bizid` 为必需, `description` 可留空, `description` 内如有半角双引号、换行、逗号时, 需要转义, 参见 [csv 转义方式](#csv-转义方式)


根据下图的箭头指示添加完成后, 点击 **`Propose changes`**

![edit-02](img/how-to-pr/edit-02.png)

5. 网页跳转后来到如下页面则说明修改成功了, 开始提交 pr

![pr-01](img/how-to-pr/pr-01.png)
![pr-02](img/how-to-pr/pr-02.png)


6. 接下来你就可以通过 github 或者 Email 查看这个 pr 是否被合并, 或者是否被要求更改

![email](img/how-to-pr/email.png)


---

## FAQ

### 如何获取 bizid?

#### 自动获取

1. 选择一篇文章复制链接

![](img/bizid-01.png)

2. 在 [这里](https://github.com/hellodword/wechat-feeds/issues/new) 新开一个 issue, 填上链接, github actions 会自动抓取和回复数据, 只需要等待几十秒然后复制就可以了. 参考 [#29](https://github.com/hellodword/wechat-feeds/issues/29). 如果失败, 请 [手动获取](#手动获取)

#### 手动获取

1. 选择一篇文章复制链接

2. 在浏览器中打开链接, 右键查看网页源代码, 搜索 `var biz`, 可以搜到 `var biz = ""||"MzI1NTQxODA4NA==";`, 那么 `MzI1NTQxODA4NA==` 也就是需要的 bizid

### 服务是否稳定?

完全不敢保证, 抱歉 (项目的特殊性决定了一切说绝对稳定的都是过度自信)

### feeds 更新频率如何?

~~暂定两个小时一次~~

发现太频繁了抓取到的信息达不到预期, 改为七个时间点:

01,07,11,13,16,20,23

如果有更好的时间点设计欢迎 issue 告诉我, 因为凌晨这段时间推送的更新很少, 抓取有点浪费


### 数量是否有上限?

鉴于账号限制, 暂时只打算提供10000个公众号的服务, 每个 feed 至多只保留20篇

### 是否有隐私风险?

feeds 托管在 github 上, 我无法获取订阅这些 feeds 的用户的任何信息

2020/10/5: 在列表页新增了 [GA](https://github.com/hellodword/wechat-feeds/blob/82c14ebd869fe11618142d9a04b487b53988dd3e/index.html#L22-L30), 只是为了统计一下列表页的使用情况, 如有介意, 可以使用 [list.csv](https://github.com/hellodword/wechat-feeds/blob/main/list.csv) 代替列表页.

### 是如何爬取的?

真实: 全部是我一条一条定时手动抄录的, 一个小时最多抄录两万个公众号的内容.

### csv 转义方式

**首先确保你的输入法切换到半角符号状态**


1. 如果内容中有**半角**双引号, 需要在每个**半角**双引号前面再加一个**半角**双引号来转义, 然后将内容用一对**半角**双引号包起来:

   假设需要转义的内容为: 

   ```
   它说:"你好"
   ```

   则改为: 

   ```
   "它说:""你好"""
   ```

2. 如果内容中有**半角**逗号, 将内容用一对**半角**双引号包起来:

   假设需要转义的内容为: 

   ```
   你好,世界
   ```

   则改为: 

   ```
   "你好,世界"
   ```

3. 如果内容中有换行, 要将整个内容都用一对**半角**双引号包起来:

   > 不建议包含换行

   假设需要转义的内容为: 

   ```
   它说:"你好世界"
   它说:"知道了"
   ```

   则改为: 

   ```
   "它说:""你好世界""
   它说:""知道了"""
   ```

---

## 结构


### main
主分支 `main`:

1. [list.csv](https://github.com/hellodword/wechat-feeds/blob/main/list.csv): 由 `name`, `bizid`, `description` 组成的无序公众号列表

### feeds

分支 `feeds` 储存更新的 feeds

### pages

分支 `pages` 是列表页的源码, 部署在 github pages 上, 其中的 [VERSION](https://github.com/hellodword/wechat-feeds/blob/pages/VERSION) 文件会随着 [feeds 分支](#feeds) 自动更新.

---
## TODO

- [x] 同步 gitee 提升访问体验
- [x] 根据 list.csv 生成列表页, 通过 pages 展示 (感谢 [Treblex](https://github.com/Treblex) 的 [Treblex/wechat-feeds-page](https://github.com/Treblex/wechat-feeds-page))
- [ ] 给 pr 和 commit 添加自动 checks
- [x] 给 issue 添加 actions, 来自动获取 bizid 等
- [ ] 考虑添加更多可供列表页搜索/过滤的属性, 例如微信号、 TAG 等
- [ ] 思考更简单的添加公众号的方式, 前提是继续控制成本
- [ ] 思考如何用低成本实现添加全文(格式处理/IP限制/静态资源限制等问题有点麻烦, 成本很难控制)
- [ ] 考虑 feeds 分支使用 force push, 以避免触及[仓库容量预警上限](https://docs.github.com/cn/github/managing-large-files/what-is-my-disk-quota#file-and-repository-size-limitations)

---

## 捐赠

本项目使用完全免费. 但有一定的维护成本, 故此处开放捐赠, 但不对捐赠者做任何关于本项目的额外的承诺, 亦不会在项目中主动公开捐赠者信息. 


<details>
<summary>展开查看捐赠方式</summary>

<h3>BTC</h3>
<img src="img/sponsor/btc.jpg" />

<h3>ETH (ERC20)</h3>
<img src="img/sponsor/eth-erc20.jpg" />

<h3>USDT (ERC20)</h3>
<img src="img/sponsor/usdt-erc20.jpg" />

<h3>XMR</h3>
<img src="img/sponsor/xmr.jpg" />

</details>
