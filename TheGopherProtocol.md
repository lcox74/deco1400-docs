# The Gopher Protocol
> 8th March 2022

Gopher is a protocol created around 1991 but a team of people at the University of Minnesota. It's a very light internet protocol that was killed off swiftly after the release of the World Wide Web (www). It's light in the sense that it was mainly used for read-only documentation distribution and functioned/looked very much like a file system. This allowed Gopher to be compatiable with working in terminal based computers

This post is an introduction to the network protocol and trying to develop a client and server application as a challenge to myself to learn new things and see how things were done before my time. The spec I am following for this project is via the IETF datatracker; [RFC 1436](https://datatracker.ietf.org/doc/html/rfc1436). I'll be starting with a terminal based client application and test it with any servers that still actively use the protocol like: `gopher://gopher.floodgap.com/gopher` ([http proxy](http://gopher.floodgap.com/gopher/gw.lite)).

## How Does Gopher Work?

Unlike `http://` using port **80**, Gopher (`gopher://`) uses port **70** as its default port. But similarly still uses TCP for requests. The client and server interact as follows:

1. Client connects to server (i.e. `gopher.floodgap.com` ) on port **70**.
2. Server accepts.
3. Client sends a selector (i.e. `/gopher` ) or just an empty line to see what selectors the server has.
4. Server sends back a response and closes the connection.

The response the server gives back follows a strict format, with each item the in the response is on a new line ( `CRLF` ) and each element of an item is seperated by a tab ( `\t` ) except for the first and second item:

1. An Item Type; consisting of a single character (ie. `1` , `0` )
2. A Display String; Which is directly after the Item Type with no white space.
3. A Selector; which is the address selector for where the item is (ie. `/`,  `/gopher/file.txt`  )
4. A Hostname; the address hostname of what to add the selector onto.
5. A Port; the port of the item, quite typically **70**.

> **Note:** Even though the protocol is designed to run on port **70**, is has the ability to have items on different ports.

From this design the following are a couple examples of results given by a
Gopher server. For simplicity, tabs will be represented as `\t`.

```txt
1Root Page\t\\tgopher.lachlancox.dev\t70
0Sample Readme\t\readme.txt\tgopher.lachlancox.dev\t70
ISample Image\t\res\img.png\tgopher.lachlancox.dev\t70
9Sample Binary\t\a.out\tgopher.lachlancox.dev\t70
```

You can find all the Item Types for Gopher in section 3.8 of the [RFC 1436](https://datatracker.ietf.org/doc/html/rfc1436).