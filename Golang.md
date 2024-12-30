## 用Go构建简单、安全、可扩展的系统
Go是一个开源项目，采用BSD风格的许可证分发。
Go有两个官方的编译器工具链。重点介绍gc Go编译器及其工具。如果你想了解如何使用gccgo（一个使用GCC后端的传统编译器）

Go 工具链是用 Go 编写的。因此，为了构建 Go 工具链，您需要先安装一个 Go 编译器（应该在环境变量里）。
Go 最后一个使用 C 编写的版本Go 1.4

克隆 Go 仓库并检出最新的分支
运行sr目录下的all.bash make.bash
Go 的编译环境可以通过环境变量进行定制。
可以在同一台机器上安装多个 Go 版本。需要确保已安装 Git。

Linux安装
```
$ sudo tar -C /usr/local -xzf go1.23.4.linux-amd64.tar.gz
$ export PATH=$PATH:/usr/local/go/bin
$ source $HOME/.profile
```

多版本Go
```
$ go install golang.org/dl/go1.10.7@latest
$ go1.10.7 download
$ go1.10.7 version
go version go1.10.7 linux/amd64
$ go1.10.7 env GOROOT
```

删除 Go
删除 Go 目录，通常是 /usr/local/go。
编辑 /etc/profile 或 $HOME/.profile环境变量中删除 Go 的 bin 目录。



### Get started

运行代码`go run hello.go`
查看3方包info`go list -m example.com/some/package`
安装`go get github.com/gorilla/mux`

# 问题1 go.mod ？与go run . go.sum
