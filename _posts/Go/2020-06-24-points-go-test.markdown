---
layout: post
title:  "Go test命令要点简述"
comments: true
categories: Go
date:   2020-06-24 20:10:54
---

## 文件名
	与package名一致 + _test 
	
	例如 mycompress_test.go
	
## 包引入
	`import testing`

## 测试函数
	测试函数必须以 `Test` 开头
	
	例如 TestMyCompress

## 函数参数
	函数参数必须是 `t *testing.T` 或 b *testing.B

	
## 依赖关系
	go test命令 依赖于$GOPATH 环境变量，文件要在$GOPATH/src/下
	
## 综述
	综合以上描述，则定义的函数形如：
	`func TestMyCompress(t *testing.T)` 

## 使用方式
	go test + ‘package name’
	e.p. `go test mycompress`

## 参考代码 
&nbsp;&nbsp;详见[github](https://github.com/lbbxsxlz/gzCoredump/blob/master/src/mycompress/mycompress_test.go)上的test代码
	
