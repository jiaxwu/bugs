# FAIL    command-line-arguments [build failed]
其实从看看上面的这段提示：build failed，构建失败，我们应该就能看出一下信息。go test与其他的指定源码文件进行编译或运行的命令程序一样（参考：go run和go build），会为指定的源码文件生成一个虚拟代码包——“command-line-arguments”，对于运行这次测试的命令程序来说，测试源码文件getinfo_test.go是属于代码包“command-line-arguments”的，可是它引用了其他包中的数据并不属于代码包“command-line-arguments”，编译不通过，错误自然发生了。

执行命令时加入这个测试文件需要引用的源码文件，在命令行后方的文件都会被加载到command-line-arguments中进行编译。

所以用go test . -test.bench=".*" 用.引入包下所有依赖就可以解决问题
