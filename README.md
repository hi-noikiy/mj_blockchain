# mj_blockchain
基于laravel来做的一个区块链demo

区块链只是由一个个的数据块串联起来。当前块根据上一个块的某个值相关联。每次验证的时候循环整个区块链，依次验证当前块跟上一个块关联关系是否一致，来验证数据完整性。

最近我花了大约一周时间来试图摸懂区块链的作用。中间查过很多资料，也走过很多弯路。这中间最大的问题可能就是对于区块链这项技术，我们总有很多的误解。写这篇文章呢，其实是为了做一个总结，然后在写文章的基础上通过php代码来解释区块链，顺便让自己理解的更透彻一些。中间也借鉴了很多人的代码还有理论。事实证明当你真的了解这个东西的本质的时候，才会发现他的本质并没有多么高深，只是有点别扭。

当区块链带上比特币，这里面的东西可能就相对比较复杂了。这里只是简单的理解一下区块链的一些原理和性质。至于比特币，至少到现在，我只能靠猜。

理论上讲，一篇好的文章应该主次分明，条理清晰。可惜碰上了我，这注定不是一篇好文章，只是记录一下我从不懂区块链到最后似懂非懂的一个摸索的过程。

还有一点需要提到，别因为他的神化觉得这个东西很难，他只是比较绕而已。

很多人都容易犯这个错误，当然我也是这种思维的受害者之一。我不会告诉你在我彻底想搞清楚区块链之前我至少看过二十篇微信公众号推送的关于区块链的文章。说实话，相当于没看，不仅仅是浪费时间那么可怕，可怕的是没弄懂之前就退缩了。

事实证明很多东西其实本质上并不是那么困难。但是很多东西就是难在你不想去了解他。可能你也看过很多关于他的文章，但是从来没有真正理解他。这个是最致命的。

我想先在这里说下区块链最基本的原理，当然是自己的理解。区块链只是由一个个的数据块串联起来。当前块根据上一个块的某个值相关联。每次验证的时候循环整个区块链，依次验证当前块跟上一个块关联关系是否一致，来验证数据完整性。

有个插曲，2018年4月10日早上，我给我最爱的人讲了一遍我理解的比特币和区块链。最终结果是跟我扛了一个早上。最后跟我说，不就是一个循环吗，讲的那么牛逼。。，我就想知道这玩意能干啥。讲了这么多也没看出来他有什么用。我：。。。

其实说对了，事实上抛开其他乱七八糟的，他就是一个循环，循环验证，循环计算，再加一个追加。只不过里面加了很多限制，限制你追加的频率，限制写入区块的大小(我觉得区块的大小应该是比特币限制的，只不过这种方式能有效控制垃圾数据量)。不能轻易得到，也不能轻易修改。

区块链不是比特币。区块链只是这样一种链接式存储数据的方式。只能说比特币是基于区块链来存储的。如果不做任何限制，他其实就是计算当前与上一个的关系，串联起来的数据而已。当然如果没有限制，这种链条实际上也没有任何意义。因为我完全可以在修改了数据以后重新计算链条上的所有哈希，所以说，这种限制是必然的。

我之所以说区块链有误解是因为我之前没接触过比特币。下意识错误的把比特币当成了区块链。所以弯路走了不少。接下来我就来介绍下我的理解和思路
>区块链的本质是什么
- 区块链只是一个分布式数据库。我觉得可以把它理解为保存数据的一种方式。因为他的数据是一块一块的链接到一起的，所以叫做区块链。这个在接下来项目例子里会着重分析。也就是说，这个链条上有很多个块，每个块里存储了一部分数据。整个链条就是所有的数据。可以想象成多个表关联，每个表里都有一部分数据。但是只要其中一个表被断开了，他后面的所有关联的表的链条就都断开。整个数据就要作废。
>区块链和比特币的区别和关系在哪？
- 我发现这个东西对于我这种不怎么关心他的人来说简直是致命伤。简单来讲，区块链只是比特币作为核心存储的一项技术。。其实这不是什么新技术点，任何语言都可以实现这个逻辑。
- 比特币其实不只是有区块链。区块链在我看来最大的作用就是存储数据。所以我觉得只能说他在数据层依托了区块链的数据结构。

我在看这个的时候就一直有个弯路，我在看了区块链的介绍的时候我不知道他的具体用途在哪。因为很难跟比特币关联起来。特别刚开始我还在想这种多节点是怎么来的。如果我是一个php的区块链程序，是不是每个节点都需要安装一套php环境。然后就是全网广播怎么实现。事实证明，想多了，多节点和全网广播，那其实是为了保证分布式数据同步来用的，如果只是用来研究原理，单个节点就可以，如果要运行到实际上，这个才是要考虑周全的。

就像我上面说的。我根本不知道区块链的直接用途。所以很难凭借猜想去想到他实际的用途。事实上我现在都没想通他能用来干啥。举一个最典型的例子，网易有个星球基地，当我每天去领取钻的时候，我就在想，难道我没领取一次你就给我生成一个区块去存放我的钻？而且这东西怎么都感觉就是个积分系统。后来我发现区块链有三种类型。我才猜想，星球基地有可能只是个私链，只不过数据存储可能确实用了区块链，多个私链节点统一广播复制。保证数据完整性。这跟分布式数据库有啥区别，好吧，区块链本质上就是来做分布式数据库的。唯一的本质不同可能就是他必须每个区块相关联吧。
>区块链的三种类型（公有链，联盟链，专有链）
- 公有链，听名字就知道，谁都能成为节点的这种。最著名的例子，比特币。谁都可以加入，谁都可以退出。只要节点够多，退出一个两个都没有问题。
- 联盟链。相当于合伙，我有一个节点群，你要加入，必须经过我的授权。授权了以后共同监督
- 专有链。私链。一家独大，所有节点都是自己的。已经生成的数据是不可逆。也符合区块链的数据结构，只不过如果我想改什么规则，想给谁加东西，理论上都是可以加的。
>php实现一个区块链

写这个呢？主要是加深我对区块链的理解。也能让我的朋友们能认识到区块链跟比特币的关系。其实区块链最大的作用就是一旦写入无法修改。这样可以保证一些人不会人为的去篡改数据。这里用php来实现一个区块链程序。一条条的来分析他是怎么来验证，存储，为啥他写入了以后就不能修改了。

先来整理下PHP实现区块链的思路。
- 区块链本质上是数据存储。所以首先要把所有的数据存储拿出来。取出最后一个区块，用来做写入区块验证
- 生成新的区块。取出最后一个区块的hash值，将最新区块的数据加上前一个区块的hash值一起hash运算出一个新的hash。这个意思是将当前区块与上一个区块相关联。为了以后循环验证做准备。
- 程序运行开始要有一个创世区块，他不关联上一个区块，下一个区块生成的hash要跟上一个区块关联
- 当有新的交易记录时候，将交易记录保存起来，当写入区块时候一起写入到数据中。因为比特币中每个区块最多有2M，所以矿工可以选择剔除部分交易，一般金额越小越容易剔除。因为他可以获得手续费。
- 当写入新的区块的时候，引用工作量证明来解决频繁写入。
- 还要有一个共识算法来解决冲突问题，单个节点这个就没啥用了
- 接收数据的时候验证区块链是否被篡改过，这里涉及到的就是循环整个链条，通过上一个区块的hash值来确定下一个链条是否被篡改过。
- 当区块生成的时候，给生成区块的人奖励，这是促使矿工争抢生成区块的最终动力，巅峰时期比特币达到接近两万美元一个，运气好十分钟挖到一个区块。
- 循环整个区块，计算当前人的剩余金额

这个只是简单的大体思路。真正的比特币会更加复杂，包括用户交易信息的非对称加密。工作量证明的难度。这些我统统没有考虑到系统里。等我过后完善吧。

其实这也证明了区块链最基本的原理并不是太复杂。只是刚开始想象不到他的验证是通过整个数据循环验证。反正就是一切都是循环。

真正落实到代码了就比较啰嗦了，刚看前面自己写的就觉得是真的啰嗦。抓不住重点。所以我偷了个懒，尽量给每行核心代码加上注释。然后更新到github上。




 



