---
layout: post
title: Difference between Socket and Port
author: juned
categories: [Networking]
tags: [Linux,Networking]
image: assets/images/aws.jpg
featured: false
hidden: true
comments: true
---
## Port
Imagine you computer as a House with many doors.
The address of your house would be equal to the the IP address of a computer.
Each door would be equal to a computer's port. 

## Socket 
A socket would sit at a door and listen and talk. 
A socket is an a a connection to another computer. It would sit at one of your doors and yell across the street to your neighbour's house. In order to do this, you need to know  what door your neighbour is listening at otherwise he can't answer. 

You call up your neighbour and he tells you that he is listening  on port 150. You pick a random door at your house with a number above  1024 and make sure it's empty. If it isn't, you find another one and  repeat.(This is usually handled by the socket and you don't need to  specify this.) Then you open this door and throw a rock to your  neighbour's house across the street and hit the door nunmbered 150. Your neighbour opens his door(#150) and you now  can talk to him and send him data.

More details at the [coderanch][1]
[1]: http://www.coderanch.com/t/206360/sockets/java/port-vs-socket
