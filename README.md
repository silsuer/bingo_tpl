# bingo_tpl

Go语言实现的模版引擎


执行过程
------

在配置文件中指定界限符（左界限符和右界限符）

从输入流中读取

取出界限符中间的数据作为语法内容，一对界限符生成一个词法节点

节点结构为

```go
// 词法分析链包含大量节点
type LexicalChain struct {
	Nodes   []*LexicalNode
	current int // 当前指针
}

type LexicalNode struct {
	T       int    // 类型（词法节点还是文本节点）
	Content []byte // 内容，生成模版的时候要使用内容进行输出
}
```

以 `;` 号将语法内容分割为语句

整个文件的词法节点构成一条词法链并缓存到内存中

节点的 `Content` 是一个字符数组，对于每一个模版，文本节点和词法节点共同构成了一条词法链

而针对所有词法节点，将共同构成`Token`流，其中的每个`token`都是一种语法数据,
`token`的最小单位是表达式

----------


当http请求时，
遍历链上所有节点，
按照顺序解析语句，
构成语法树，
将变量映射到语法树中，
得到每个节点的返回值


解析节点流程：

对节点内容按照字符读取，遇到保留字 对当前行的保留字的内容进行解析


## Change Log

#### 20180827 更新

  初步构建模版引擎环境变量，解析文本流为词法链