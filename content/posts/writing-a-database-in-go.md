---
title: "Writing A Simple Database: Part 1"
date: 2019-07-12T19:58:53+02:00
description: "Writing a simple database in Go: The beginning"
tags:
    - Code
    - go
    - database
    - go-db
categories:
    - Dev
images:
    - https://www.instagram.com/p/BrQX5EMn6le/
    - /images/posts/moodb_initial.png
keywords: "Go, Golang, Database, Databases"
summary: "This post is an intro about writing database. Part-1 of the series on writing a db in Golang"
---

<img style="border-radius:0px;height:440px;width:100%;" src="https://instagram.fcpt7-1.fna.fbcdn.net/vp/fd2cc646f3f39f808dcd53c24e28031e/5DEEAE91/t51.2885-15/e35/46228023_318887132168061_95887248700416063_n.jpg?_nc_ht=instagram.fcpt7-1.fna.fbcdn.net">
<center>
<a href="https://www.instagram.com/p/BrQX5EMn6le/" rel="nofollow" style="color:#757575;font-size:80%;">Source: Instagram</a>
</center>

As part of <a href="https://en.wikipedia.org/wiki/Learning-by-doing" rel="nofollow">learning by doing</a>, I am trying to implement a simple database in Go. I got this project idea from <a href="http://nikhilism.com/post/2016/writing-simple-database-in-rust-part-1/" rel="nofollow">Nikhil's blog</a> about implementing a DB in Rust. The basic concept for implementation is based on [A Simple and Efficient Implementation for Small Databases](http://birrell.org/andrew/papers/024-DatabasesPaper-SOSP.pdf) paper. The paper describes the theoretical details of implementing a simple but fully functional DB.

Implementing a database as a side project looked fascinating to me as, till now, I have majorly worked with web technologies. Writing a DB will also expose me to a lot of new systems concepts and logic behind writing a reliable(hopefully distributed) system. It's also a good fit for using a static language, Go in this case. **By the end of this ["Writing a Simple Database" series](/tags/go-db/) we will have a working key-value database with persistence and fault-tolerance**

In the past, I have casually programmed in Go and I quite like it. But I forget the syntax over time as I don't get to use it much. Working on a side project will help me to learn it with a purpose this time. What I like about Go is that it's readable, compiled and language behind a lot fo distributed reliable systems like Kubernetes, etcd, docker, etc.

## High-Level Overview

**Functional requirements**

- The DB will have a client and server architecture
- It will store key-value data
- DB will be completely in-memory
- Backed by Write-ahead logs(WAL)
- Fault tolerance and restore in case of failure using WAL
- The latest snapshot of the in-memory DB will be backed up time-to-time in the file system

**Non-functional requirements**

- Should be fast(somewhat comparable to key-value stores like etcd/rockdb)
- Should be highly reliable
- Should always follow ACID properties

**Extension**

- Distributed database
- If DB is too big to fit in memory, overflow to disk
- Log compaction

Some of the requirements are likely to change as I start implementing the individual components.


## Progress

Source code: https://github.com/amitt001/moodb

**DB Name**: "MooDB" or "Mdb". I got this name idea from Friend's "[Moo point](https://www.youtube.com/watch?v=62necDwQb5E)" scene :) and it sounded like a funny but mildly apt name for a DB which won't be used in production.

I have already started the implementation. Till now I have a working command line with an in-memory key-value store. It supports 4 operations: `GET, SET, UPDATE, DELETE`.

</br>
![MooDB cli](/images/posts/moodb_initial.png)
<center style="color:#757575;font-size:80%;">DB cli with commands</center>


Currently, the client and server runs in the same process. In its current state like it's like an embedded DB library(like SQLite). As each run starts a new memory DB instance.


## What's next?

Next, I plan to implement the following features:

- Separate client and server: to support multi-client and one datastore
- Write-ahead log: to make DB fault-tolerant against power loss or crashes.


<small>
*I have decided to blog as I go to log my learnings. I am enjoying writing the code and learning a lot of new things. For implementing each part I am learning both the language and the underlying concept behind the DB component. Fun!*
</small>
