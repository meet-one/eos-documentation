# 白话 EOS 构思

## POS 链

话说地球上有个神奇的国度叫米国，它由 50 个州组成，国家事务都由这些州组成的管理会决策。

每个州的人口、经济和风俗各有差异，所有米国人民都可以为自己喜欢的州投票。

国家根据人民的投票高低从 50 个州里选出头 30 个，他们能优先获得资源。

其中的前 21 个还有决策权，能参与各项法律、政策的制定——21 个 BP。

所以每个州都会努力提高自己的各项实力来吸引更多的投票。

但是这些州在发展过程中，都会试图消灭对自己不利的因素，从而“骗取”更多投票。

比如某位旅游爱好者 P1，来到 A 州，发现这儿的旅馆质量太差，P1 到 A 州工商局投诉，工商局客服热情地听完了投诉，然后并没有记录在案。P1 到一些旅游交流论坛发帖吐槽，也可能很快遭到公关删帖。

再比如一些老赖、不良企业名单的管理，如果没有可靠的记录、公开，很容易被买通修改。

后来 21 个决策州在国家中央机构号召下召开会议探讨这个问题。

国家中央机构提出几项原则，所有州都必须实行，包括：

1. 每个州都发一个神奇印章，任何一个印章盖出来的印，其它州都认得，可以验证是哪个州盖的，但无法伪造别的印章。（类比签名）

2. 任何政策条款，不管由哪个决策州提出，只要盖了 15 个或以上州的印就能生效。（拜占庭将军问题，共识算法）

3. 所有生效的条款都会记录在档案库里，每个档案上可以记录多个条款，一个个档案按顺序存放。50 个州都要加到一个电报群，彼此可以同步档案库，以保证所有档案都一模一样。

那么问题来了：怎么防止某些州的档案管理员被收买而篡改档案呢？

引入一个术语：

散列摘要：给一段很长的文字用很短的文字概要表示。比如现代人写一大片旅游日记，古人四行五言总结了。可以理解为有损压缩，其压缩率很大，可以把任何文字压缩到固定的大小。比如 SHA256 可以把任何数据压缩到 256bit（32 字节）。散列摘要的特征是：不同数据的摘要一般是不同的；不同的摘要一定代表不同的原文。一个类比：我们身份证上的大头照，其实就是一个人脸的摘要，虽然尺寸很小，但都可以认清是谁。

规定：

4. 第一个档案的内容是所有人都知道的，比如“米国头号档案”。

5. 每个档案都可以计算一个摘要，不同内容的档案，其摘要一定不同，摘要可以验证内容是不是被改过。然后要把每个档案的摘要记录到下一个档案里。

这样我们要比较两个州的档案是不是完全一样就很简单了，只要比较最后一个档案的摘要是否一样，就可以知道这两个州的档案库是不是都一样了。

假设 A 州档案管理员把第 100 号档案改了，那么第 101 号档案里有第 100 号档案的摘要，于是为了使修改神不知鬼不觉，A 州管理员又要把第 101 号档案里的第 100 号档案的摘要给改成对应修改后的摘要，但是改动 101 号之后，101 号的摘要又变了，还得改 102 号里的 101 号的摘要，这样要一直改下去，直到改到最后一号档案。

但是 A 州档案管理员累死累活改完，却发现 A 州的最后一号档案和别的州不一样，不会被其它州承认。

这就是【不可篡改性】。

区块：一个档案袋，档案头部都有编号、记录时间等信息，而且里面的每个文件是一个合约。

每个档案的按编号严格递增、排序，并将每个档案的摘要记录在下一号档案内。比如第二号档案里就包含了第一号档案的摘要。这样在计算第二号档案的摘要时，是用到第二号档案的全部内容，其中就包含了第一号档案的摘要。以此类推。这些档案的组合就是一条链。

每个州都保存一份，这是【分布式存储】。

这个档案库系统建立完毕后，米国各州又开放了很多查询窗口给民众，民众可以查询任何档案。比如某民想知道某企业是不是曾经有过不良行为遭到过处罚，他可以通过查询窗口的搜索功能查到若干个记录这一企业的档案。这是【公开性】。

后来，米国管理会发现这套档案库，不仅可以用于信息记录、公开、查询，还可以服务金融业和商业。

因为档案库有公信力和容灾能力，用它记录账本和商业合约都很可靠。

【本文没有提到匿名性。】