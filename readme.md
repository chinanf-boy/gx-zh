![gx logo](logo.jpeg)

# gx [![translate-svg]][translate-list]

> 与语言无关的通用包管理器

[![](https://img.shields.io/badge/made%20by-Protocol%20Labs-blue.svg?style=flat-square)](http://protocol.ai) [![](https://img.shields.io/badge/freenode-%23gx-blue.svg?style=flat-square)](http://webchat.freenode.net/?channels=%23ipfs,%23gx)

[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list


---

## 校对✔

欢迎 \`Issue\` 和 \`Pull\` ❤️, 最好 \`Pull\` 👏

|翻译的原文|与日期|原文更新|更多
---|---|---|---
[commit]|2018 7.25|![last commit][last]|[中文翻译][more]

[commit]:  https://github.com/whyrusleeping/gx/tree/2e7e5abddb8321709666be9161e09aae16b2a0d8
[last]: https://img.shields.io/github/last-commit/whyrusleeping/gx.svg
[more]: https://github.com/chinanf-boy/chinese-translate-list

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---


gx是围绕[IPFS](//github.com/ipfs/ipfs) - 分布式内容寻址{*星际*}文件系统 构建的打包工具. 它旨在灵活,强大和简单. 

gx是**阿尔法质量**. 它还不完美,但它已被证明足以管理[go-ipfs](https://github.com/ipfs/go-ipfs/)的依赖关系,并准备 开拓开发人员和早期用户尝试和探索. 

> 如果你想了解ipfs - [ipfs 旅行](https://github.com/chinanf-boy/ipfs-tour) | [ipfs/ipfs 中文](https://github.com/chinanf-boy/ipfs-zh) |  [中文白皮书](https://gguoss.github.io/2017/05/28/ipfs/)

## 目录

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [背景](#%E8%83%8C%E6%99%AF)
- [要求](#%E8%A6%81%E6%B1%82)
- [安装](#%E5%AE%89%E8%A3%85)
- [用法](#%E7%94%A8%E6%B3%95)
  - [package.json](#packagejson)
- [安装gx包](#%E5%AE%89%E8%A3%85gx%E5%8C%85)
- [依赖](#%E4%BE%9D%E8%B5%96)
  - [gx依赖关系图宣言](#gx%E4%BE%9D%E8%B5%96%E5%85%B3%E7%B3%BB%E5%9B%BE%E5%AE%A3%E8%A8%80)
    - [1.依赖树的深度最小化.](#1%E4%BE%9D%E8%B5%96%E6%A0%91%E7%9A%84%E6%B7%B1%E5%BA%A6%E6%9C%80%E5%B0%8F%E5%8C%96)
    - [2.树的宽度最小化,但不以增加深度为代价.](#2%E6%A0%91%E7%9A%84%E5%AE%BD%E5%BA%A6%E6%9C%80%E5%B0%8F%E5%8C%96%E4%BD%86%E4%B8%8D%E4%BB%A5%E5%A2%9E%E5%8A%A0%E6%B7%B1%E5%BA%A6%E4%B8%BA%E4%BB%A3%E4%BB%B7)
- [这看你的](#%E8%BF%99%E7%9C%8B%E4%BD%A0%E7%9A%84)
- [为了解决这个问题,你可以通过](#%E4%B8%BA%E4%BA%86%E8%A7%A3%E5%86%B3%E8%BF%99%E4%B8%AA%E9%97%AE%E9%A2%98%E4%BD%A0%E5%8F%AF%E4%BB%A5%E9%80%9A%E8%BF%87)
  - [忽略发布中的文件](#%E5%BF%BD%E7%95%A5%E5%8F%91%E5%B8%83%E4%B8%AD%E7%9A%84%E6%96%87%E4%BB%B6)
- [存储库]](#%E5%9B%9E%E8%B4%AD)
  - [用法](#%E7%94%A8%E6%B3%95-1)
- [钩子](#%E9%92%A9%E5%AD%90)
- [包目录](#%E5%8C%85%E7%9B%AE%E5%BD%95)
- [使用gx作为Go包管理器](#%E4%BD%BF%E7%94%A8gx%E4%BD%9C%E4%B8%BAgo%E5%8C%85%E7%AE%A1%E7%90%86%E5%99%A8)
- [使用gx作为Javascript包管理器](#%E4%BD%BF%E7%94%A8gx%E4%BD%9C%E4%B8%BAjavascript%E5%8C%85%E7%AE%A1%E7%90%86%E5%99%A8)
- [使用gx作为语言/环境X的包管理器](#%E4%BD%BF%E7%94%A8gx%E4%BD%9C%E4%B8%BA%E8%AF%AD%E8%A8%80%E7%8E%AF%E5%A2%83x%E7%9A%84%E5%8C%85%E7%AE%A1%E7%90%86%E5%99%A8)
- [为什么叫gx?](#%E4%B8%BA%E4%BB%80%E4%B9%88%E5%8F%ABgx)
- [加入](#%E5%8A%A0%E5%85%A5)
- [执照](#%E6%89%A7%E7%85%A7)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## 背景

gx最初设计用于以分布式方式处理Go项目中的依赖项,并从其他 心爱的包管理器 中提取想法 (如[npm](http://npmjs.org/)) . 

gx的设计考虑了以下主要目标: 

1.  对于 语言/生态系统 可能通过 提供[git-like 钩子](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)来添加[新的生态系统](https://github.com/whyrusleeping/gx-go). 
2.  通过 内容寻址(ipfs 特性) 提供 完全一样的包. 
3.  使用[灵活的分布式存储后端-ipfs](http://ipfs.io/). 


## 要求

鼓励用户运行[IPFS 守护程序](//github.com/ipfs/go-ipfs)在他们的机器上,且至少0.4.2版本. 如果不存在,gx将使用公共网关. 但如果您希望发布包,则本地运行守护程序是一项硬性要求. 

## 安装

    $ go get -u github.com/whyrusleeping/gx

这将把 源项目 下载到`$GOPATH/src/github.com/whyrusleeping/gx`并构建和安装二进制文件到`$GOPATH/bin`. 要修改gx,只需更改该目录中的源项目,然后运行即可`go build`. 

## 用法

创建和发布 新的通用包: 

```bash
$ gx init
$ gx publish
```

这将输出一个'package-hash',它对于发布时 包的确切内容 是唯一的. 如果有人要下载你的软件包并重新发布它,它就会产生*准确*相同的哈希. 

### package.json

应该注意的是,gx意味着*与现有`package.json`文件合作*. 如果你添加一个包给gx,且你在其根目录会有`package.json`文件,gx将尝试与它一起工作. 任何共享字段都具有相同的类型,并且gx独有的任何字段将保持独立. 

例如. 单个`package.json`文件可用于同时为gx和另一个打包工具提供服务,例如npm. 因为gx是**阿尔法质量**,正如上述陈述可能有一些例外,如果您注意到,请提出问题. 

## 安装gx包

如果你已复制了gx包-`package.json`,只需运行即可`gx install`要么`gx i`安装它 (及其依赖项) . 

## 依赖

要将另一个包的依赖项添加到包中,只需通过其哈希导入它: 

```bash
$ gx import QmaDFJvcHAnxpnMwcEh6VStYN4v4PB4S16j4pAuC2KSHVr
```

这会将指定的哈希包下载到工作区中`vendor`目录. 它还添加了一个引用该包的字段到本地`package.json`. 

Gx有一些很好的工具来查看和分析依赖项. 首先,简单列出: 

```bash
$ gx deps
go-log              QmSpJByNKFX1sCsHBEp3R73FL4NF6FnQTEGyNAXHm2GS52 1.2.0
go-libp2p-peer      QmWXjJo15p4pzT7cayEwZi2sWgJqLnGDof6ZGMh9xBgU1p 2.0.4
go-libp2p-peerstore QmYkwVGkwoPbMVQEbf6LonZg4SsCxGP3H7PBEtdNCNRyxD 1.2.5
go-testutil         QmYpVUnnedgGrp6cX2pBii5HRQgcSr778FiKVe7o7nF5Z3 1.0.2
go-ipfs-util        QmZNVWh8LLjAavuQ2JXuFmuYH3C11xo988vSgp7UQrTRj1 1.0.0
```

这列出了这个包的直接依赖性. 要查看依赖项的依赖项,请使用`-r`选项:(和可选的`-s`选项来排序他们) 

```bash
$ gx deps -r -s
go-base58           QmT8rehPR3F6bmwL6zjUN8XpiDBFFpMP2myPdC6ApsWfJf 0.0.0
go-crypto           Qme1boxspcQWR8FBzMxeppqug2fYgYc15diNWmqgDVnvn2 0.0.0
go-datastore        QmbzuUusHqaLLoNTDEVLcSF6vZDHZDLPC7p4bztRvvkXxU 1.0.0
go-ipfs-util        QmZNVWh8LLjAavuQ2JXuFmuYH3C11xo988vSgp7UQrTRj1 1.0.0
go-keyspace         QmUusaX99BZoELh7dmPgirqRQ1FAmMnmnBn3oiqDFGBUSc 1.0.0
go-libp2p-crypto    QmVoi5es8D5fNHZDqoW6DgDAEPEV5hQp8GBz161vZXiwpQ 1.0.4
go-libp2p-peer      QmWXjJo15p4pzT7cayEwZi2sWgJqLnGDof6ZGMh9xBgU1p 2.0.4
go-libp2p-peerstore QmYkwVGkwoPbMVQEbf6LonZg4SsCxGP3H7PBEtdNCNRyxD 1.2.5
go-log              QmSpJByNKFX1sCsHBEp3R73FL4NF6FnQTEGyNAXHm2GS52 1.2.0
go-logging          QmQvJiADDe7JR4m968MwXobTCCzUqQkP87aRHe29MEBGHV 0.0.0
go-multiaddr        QmYzDkkgAEmrcNzFCiYo6L1dTX4EAG1gZkbtdbd9trL4vd 0.0.0
go-multiaddr-net    QmY83KqqnQ286ZWbV2x7ixpeemH3cBpk8R54egS619WYff 1.3.0
go-multihash        QmYf7ng2hG5XBtJA3tN34DQ2GUN5HNksEw1rLDkmr6vGku 0.0.0
go-net              QmZy2y8t9zQH2a1b8q2ZSLKp17ATuJoCNxxyMFG5qFExpt 0.0.0
go-testutil         QmYpVUnnedgGrp6cX2pBii5HRQgcSr778FiKVe7o7nF5Z3 1.0.2
go-text             Qmaau1d1WjnQdTYfRYfFVsCS97cgD8ATyrKuNoEfexL7JZ 0.0.0
go.uuid             QmcyaFHbyiZfoX5GTpcqqCPYmbjYNAhRDekXSJPFHdYNSV 1.0.0
gogo-protobuf       QmZ4Qi3GaRbjcx28Sme5eMH7RQjGkt8wHxt2a65oLaeFEV 0.0.0
goprocess           QmSF8fPo3jgVBAy8fpdjjYqgG87dkJgUprRBHRd2tmfgpP 1.0.0
mafmt               QmeLQ13LftT9XhNn22piZc3GP56fGqhijuL5Y8KdUaRn1g 1.1.1
```

这非常有用,我现在知道我的全套软件包的依赖. 但现在困难的是能够分辨出来自哪里. 为了解决这个问题,gx有一个`--tree`选项: 

```bash
$ gx deps --tree
├─ go-base58          QmT8rehPR3F6bmwL6zjUN8XpiDBFFpMP2myPdC6ApsWfJf 0.0.0
├─ go-multihash       QmYf7ng2hG5XBtJA3tN34DQ2GUN5HNksEw1rLDkmr6vGku 0.0.0
│  ├─ go-base58       QmT8rehPR3F6bmwL6zjUN8XpiDBFFpMP2myPdC6ApsWfJf 0.0.0
│  └─ go-crypto       Qme1boxspcQWR8FBzMxeppqug2fYgYc15diNWmqgDVnvn2 0.0.0
├─ go-ipfs-util       QmZNVWh8LLjAavuQ2JXuFmuYH3C11xo988vSgp7UQrTRj1 1.0.0
│  ├─ go-base58       QmT8rehPR3F6bmwL6zjUN8XpiDBFFpMP2myPdC6ApsWfJf 0.0.0
│  └─ go-multihash    QmYf7ng2hG5XBtJA3tN34DQ2GUN5HNksEw1rLDkmr6vGku 0.0.0
│     ├─ go-base58    QmT8rehPR3F6bmwL6zjUN8XpiDBFFpMP2myPdC6ApsWfJf 0.0.0
│     └─ go-crypto    Qme1boxspcQWR8FBzMxeppqug2fYgYc15diNWmqgDVnvn2 0.0.0
├─ go-log             QmNQynaz7qfriSUJkiEZUrm2Wen1u3Kj9goZzWtrPyu7XR 1.1.2
│  ├─ randbo          QmYvsG72GsfLgUeSojXArjnU6L4Wmwk7wuAxtNLuyXcc1T 0.0.0
│  ├─ go-net          QmZy2y8t9zQH2a1b8q2ZSLKp17ATuJoCNxxyMFG5qFExpt 0.0.0
│  │  ├─ go-text      Qmaau1d1WjnQdTYfRYfFVsCS97cgD8ATyrKuNoEfexL7JZ 0.0.0
│  │  └─ go-crypto    Qme1boxspcQWR8FBzMxeppqug2fYgYc15diNWmqgDVnvn2 0.0.0
│  └─ go-logging      QmQvJiADDe7JR4m968MwXobTCCzUqQkP87aRHe29MEBGHV 0.0.0
└─ go-libp2p-crypto   QmUEUu1CM8bxBJxc3ZLojAi8evhTr4byQogWstABet79oY 1.0.2
   ├─ gogo-protobuf   QmZ4Qi3GaRbjcx28Sme5eMH7RQjGkt8wHxt2a65oLaeFEV 0.0.0
   ├─ go-log          Qmazh5oNUVsDZTs2g59rq8aYQqwpss8tcUWQzor5sCCEuH 0.0.0
   │  ├─ go.uuid      QmPC2dW6jyNzzBKYuHLBhxzfWaUSkyC9qaGMz7ciytRSFM 0.0.0
   │  ├─ go-logging   QmQvJiADDe7JR4m968MwXobTCCzUqQkP87aRHe29MEBGHV 0.0.0
   │  ├─ go-net       QmZy2y8t9zQH2a1b8q2ZSLKp17ATuJoCNxxyMFG5qFExpt 0.0.0
   │  │  ├─ go-text   Qmaau1d1WjnQdTYfRYfFVsCS97cgD8ATyrKuNoEfexL7JZ 0.0.0
   │  │  └─ go-crypto Qme1boxspcQWR8FBzMxeppqug2fYgYc15diNWmqgDVnvn2 0.0.0
   │  └─ randbo       QmYvsG72GsfLgUeSojXArjnU6L4Wmwk7wuAxtNLuyXcc1T 0.0.0
   ├─ go-ipfs-util    QmZNVWh8LLjAavuQ2JXuFmuYH3C11xo988vSgp7UQrTRj1 1.0.0
   │  ├─ go-base58    QmT8rehPR3F6bmwL6zjUN8XpiDBFFpMP2myPdC6ApsWfJf 0.0.0
   │  └─ go-multihash QmYf7ng2hG5XBtJA3tN34DQ2GUN5HNksEw1rLDkmr6vGku 0.0.0
   │     ├─ go-base58 QmT8rehPR3F6bmwL6zjUN8XpiDBFFpMP2myPdC6ApsWfJf 0.0.0
   │     └─ go-crypto Qme1boxspcQWR8FBzMxeppqug2fYgYc15diNWmqgDVnvn2 0.0.0
   └─ go-msgio        QmRQhVisS8dmPbjBUthVkenn81pBxrx1GxE281csJhm2vL 0.0.0
      └─ go-randbuf   QmYNGtJHgaGZkpzq8yG6Wxqm6EQTKqgpBfnyyGBKbZeDUi 0.0.0
```

现在你可以看到了*整个*该项目的依赖树. 虽然,对于较大的项目,这将变得混乱. 如果您只对单个包的依赖树感兴趣,可以使用`--highlight`过滤`-tree`打印的选项: 

```bash
$ gx deps --tree --highlight=go-crypto
├─ go-multihash       QmYf7ng2hG5XBtJA3tN34DQ2GUN5HNksEw1rLDkmr6vGku 0.0.0
│  └─ go-crypto       Qme1boxspcQWR8FBzMxeppqug2fYgYc15diNWmqgDVnvn2 0.0.0
├─ go-ipfs-util       QmZNVWh8LLjAavuQ2JXuFmuYH3C11xo988vSgp7UQrTRj1 1.0.0
│  └─ go-multihash    QmYf7ng2hG5XBtJA3tN34DQ2GUN5HNksEw1rLDkmr6vGku 0.0.0
│     └─ go-crypto    Qme1boxspcQWR8FBzMxeppqug2fYgYc15diNWmqgDVnvn2 0.0.0
├─ go-log             QmNQynaz7qfriSUJkiEZUrm2Wen1u3Kj9goZzWtrPyu7XR 1.1.2
│  └─ go-net          QmZy2y8t9zQH2a1b8q2ZSLKp17ATuJoCNxxyMFG5qFExpt 0.0.0
│     └─ go-crypto    Qme1boxspcQWR8FBzMxeppqug2fYgYc15diNWmqgDVnvn2 0.0.0
└─ go-libp2p-crypto   QmUEUu1CM8bxBJxc3ZLojAi8evhTr4byQogWstABet79oY 1.0.2
   ├─ go-log          Qmazh5oNUVsDZTs2g59rq8aYQqwpss8tcUWQzor5sCCEuH 0.0.0
   │  └─ go-net       QmZy2y8t9zQH2a1b8q2ZSLKp17ATuJoCNxxyMFG5qFExpt 0.0.0
   │     └─ go-crypto Qme1boxspcQWR8FBzMxeppqug2fYgYc15diNWmqgDVnvn2 0.0.0
   └─ go-ipfs-util    QmZNVWh8LLjAavuQ2JXuFmuYH3C11xo988vSgp7UQrTRj1 1.0.0
      └─ go-multihash QmYf7ng2hG5XBtJA3tN34DQ2GUN5HNksEw1rLDkmr6vGku 0.0.0
         └─ go-crypto Qme1boxspcQWR8FBzMxeppqug2fYgYc15diNWmqgDVnvn2 0.0.0
```

此树是前一个树的子集,过滤仅显示到 所选包结束 的叶. 

`gx deps`命令还有另外两个较小的子命令,`dupes`和`stats`. `gx deps dupes`将打印出多个使用 相同名称 但 不同哈希 导入的包. 这可以用于查看在依赖关系树中的不同位置 是否已导入相同包的不同版本. 允许用户更轻松地解决差异. `gx deps stats`将输出导入的包的总数 (总数和唯一数) 以及 树中的平均导入深度. 这可以用来大致了解包的复杂性. 

### gx依赖关系图宣言

我坚信包会更好,在以下情况下: 

#### 1.依赖树的深度最小化. 

这意味着重构代码的方式使树变平 (并可能因此而扩大) . 
例如,在Go中,这通常意味着将 接口 作成 独立包,并将 实现 也放入它们自己的独立包中. 这里的好处是更平坦的树,更容易更新. 对于每个包的深度依赖,您必须更新,测试,提交,审查和合并另一个包. 这有很多工作,也有很多额外的空间可以让他们研究问题. 

#### 2.树的宽度最小化,但不以增加深度为代价. 

这应该是相当常识的,但只在实际需要的地方努力去,导入包有助于提高代码质量. 想象一下在一个包中有一个辅助函数,只是因为它很方便,它却在 树中其他地方的一堆导入. 

当然它很好,并没有实际增加你所依赖的'总'数量的包. 但当你随时更新时, 你会做了额外的工作,现在你也强迫 任何想要用你的帮助函数包的人,也导入所有其他依赖项. 

遵守上述两条规则应该 (我非常愿意对此进行讨论) 提高整体代码质量,并使您的代码库更容易导航和工作. 

## 更新

在gx中更新包很简单: 

```bash
$ gx update mypkg QmbH7fpAV1FgMp6J7GZXUV6rj6Lck5tDix9JJGBSjFPgUd
```

这会查找你的`package.json`中`mypkg`
并用给定的哈希引用替换它的哈希引用. 

或者,您只需指定要更新的哈希:

```bash
$ gx update QmbH7fpAV1FgMp6J7GZXUV6rj6Lck5tDix9JJGBSjFPgUd
```

这样做将拉取这个哈希包,检查其名称,然后更新该依赖项. 

请注意,默认情况下,这根本不会触及您的代码,因此您需要更新代码中 对 该哈希的任何引用. 
如果您有语言工具 (例如`gx-go`) ,它有一个`post-update`钩子,应该正确更新给定包的引用.如果没有,您可能必须在包上运行 查询 来更新所有内容. 好的一面是,你不太可能因为任何其他原因而坐在那里,所以全局查找替换应该没问题.  

## 出版和发布

如果您尚未更新其版本,则默认情况下Gx不允许您发布包两次.

要解决这个问题，你可以传递`-f`标志。 虽然不
推荐，它仍然是完美做到的。

要轻松更新版本，请使用`gx version`子命令。 您可以手动设置版本：

```bash
$ gx version 5.11.4
```

或者只是做一个'版本颠簸': 

```bash
$ gx version patch
updated version to: 5.11.5
$ gx version minor
updated version to: 5.12.0
$ gx version major
updated version to: 6.0.0
```

大多数情况下,您的流程将类似于: 

```bash
$ gx version minor
updated version to: 6.1.0
$ gx publish
package whys-awesome-package published with hash: QmaoaEi6uNMuuXKeYcXM3gGUEQLzbDWGcFUdd3y49crtZK
$ git commit -a -m "gx publish 6.1.0"
[master 5c4d36c] gx publish 6.1.0
 2 files changed, 3 insertions(+), 2 deletions(-)
```

要自动执行此操作,您可以使用`release`子命令. `gx release <version>`将自动进行版本更新 

- (使用与正常相同的输入) `version`命令)
- 运行一个`gx publish`,然后
- 执行你的`package.json`中的`releaseCmd`. 

要获得上面的git提交流程,您可以将其设置为: `git commit -a -m \"gx publish $VERSION\"`和`$VERSION`会被gx取代成,新更改的版本. 

### 忽略发布中的文件

你可以用一个`.gxignore`文件,使gx在发布期间忽略某些文件. 这与`.gitignore`具有相同的行为.

> *注意*:是 `.gx``ignroe`,当然

Gx也遵守`.gitignore`文件 (如果存在) ,并且不会发布它排除的任何文件. 

## 存储库

gx支持自定义包命名通过用户配置存储库. 存储库只是一个ipfs对象,其链接包名称为`哈希`. 您可以将 存储库 添加为`ipns或ipfs`路径. 

### 用法

添加一个新的存储库

```bash
$ gx repo add myrepo /ipns/QmPupmUqXHBxikXxuptYECKaq8tpGNDSetx1Ed44irmew3
```

列出配置的存储库

```bash
$ gx repo list
myrepo       /ipns/QmPupmUqXHBxikXxuptYECKaq8tpGNDSetx1Ed44irmew3
```

列出给定仓库中的包裹

```bash
$ gx repo list myrepo
events      QmeJjwRaGJfx7j6LkPLjyPfzcD2UHHkKehDPkmizqSpcHT
smalltree   QmRgTZA6jGi49ipQxorkmC75d3pLe69N6MZBKfQaN6grGY
stump       QmebiJS1saSNEPAfr9AWoExvpfGoEK4QCtdLKCK4z6Qw7U
```

从repo导入包: 

```bash
$ gx repo import events
```

## 钩子

gx可以通过根据您所处的场景,具有可扩展的智能默认值 来 支持各种用例. 为此,gx具有在某些操作期间调用的钩子. 

这些钩子是特定于语言的,并且gx将尝试调用与您的语言匹配的辅助二进制文件以执行钩子,例如,当使用go,gx用过`gx-go hook <hookname> <args>`的命令行使用钩子. 

目前可用的钩子是: 

-   `post-import`
    -   在导入新包并将其信息写入package.json之后调用. 
    -   将新导入的包的哈希值作为参数. 
-   `post-init`
    -   在初始化新包之后调用. 
    -   获取新初始化包的目录的可选参数. 
-   `pre-publish`
    -   在`gx publish`捆绑包并添加到ipfs之前. 
    -   目前没有参数. 
-   `post-publish`
    -   在`gx publish`将包添加到ipfs后. 
    -   将新发布的包的哈希值作为参数. 
-   `post-update`
    -   在`gx update`依赖关系更新之后. 
    -   将旧包引用 和 新哈希 作为参数. 
-   `post-install`
    -   在安装和导入下载新包后调用. 
    -   将新包的路径作为参数. 
-   `install-path`
    -   在程序包安装和导入调用. 
    -   设置gx的位置以安装包. 

## 包目录

默认情况下,Gx将会"全局"安装包,如果你给定了全局包类型. 全局gx包 在依赖于它们的所有包 中共享. 此目录的位置不是一成不变的,如果您想在特定的环境中使用它,只需在您的环境扩展工具中添加一个钩子`install-path` (见上文) ,那么gx将使用该路径. 如果您的语言未设置全局安装路径,则gx将作为默认值回退到本地安装. 这意味着它将在当前目录中创建一个名为`vendor`的文件夹并安装它. 

运行`gx install`在包的目录中,gx将递归地获取在`package.json`中指定的所有依赖项,并将它们保存到指定的安装路径. 

Gx支持本地和全局安装路径. 由于默认为全局,因此要在本地安装,请使用`--local`要么`--global=false`. 全局标志 传递给`install-path`钩子, 让您的扩展代码使用它的逻辑. 

## 使用gx作为Go包管理器

如果你想 (像我一样) 使用gx作为go的包经理,这很容易. 在开始项目之前,您将需要`gx go`扩展: 

    $ go get -u github.com/whyrusleeping/gx-go

安装完成后,使用gx像正常导入依赖项一样. 您可以使用以下方法从 供应商目录 导入代码: 

```go
import "gx/ipfs/<hash>/packagename"
```

例如,如果我有一个包`foobar`,你可以gx导入,像这样: 

```bash
$ gx import QmR5FHS9TpLbL9oYY8ZDR3A7UWcHTBawU1FJ6pu9SvTcPa
```

然后在你的go代码中,你可以使用它: 

```go
import "gx/ipfs/QmR5FHS9TpLbL9oYY8ZDR3A7UWcHTBawU1FJ6pu9SvTcPa/foobar"
```

然后只需设置环境变量`GO15VENDOREXPERIMENT`到`1`,并像往常一样运行`go build`要么`go install`. 或者,全局安装依赖项 (`gx install --global`) 你可以省去环境变量部分. 

看到[gx-go repo](https://github.com/whyrusleeping/gx-go)更多细节. 

## 使用gx作为Javascript包管理器

请看一下[gx-js](https://github.com/sterpe/gx-js). 

## 使用gx作为语言/环境X的包管理器

如果您想将gx 与 大量存储库/软件包 一起使用,请查看[GX-工作区](https://github.com/ipfs/gx-workspace). 

如果要扩展gx以使用任何其他语言或环境,可以在名为`gx-X`的二进制文件中实现相关的挂钩, 其中'X'是您环境的名称. 之后,在正常情况下 编程语言对应"X"名字的包 将调用该工具 挂钩`gx`操作. 例如,'go'包能运行`gx-go hook pre-publish`,命令会在`gx publish`实际发布包之前被调用. 有关挂钩的更多信息,请查看上面的挂钩部分. 

另见`examples`目录. 

## 为什么叫gx?

没有理由. "gx"代表什么都不是. 

## 加入

如果您对gx感兴趣,请在 freenode irc 上 #gx和#ipfs!

## 执照

麻省理工学院. 杰罗米约翰逊 Jeromy Johnson. 
