### [Notes on structured concurrency, or: Go statement considered harmful — njs blog](https://vorpus.org/blog/notes-on-structured-concurrency-or-go-statement-considered-harmful/#id25)
为什么 goto 语句会让程序变得混乱呢？混乱具体指的又是什么呢？  
所谓的混乱指的是代码的书写顺序和执行顺序不一致。代码的书写顺序，代表的是我们的思维过程，如果思维的过程与代码执行的顺序不一致，那就会干扰我们对代码的理解。
在结构化程序设计中，可以使用三种基本控制结构来代替 goto，这三种基本的控制结构就是今天我们广泛使用的<strong>顺序结构</strong>、<strong>选择结构</strong>和<strong>循环结构</strong>，实际上if..else和while循环
底层页的确是用了goto。Golang中的go语句底层也是goto。
