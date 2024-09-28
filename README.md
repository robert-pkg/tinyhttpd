 
 tinyhttpd 是一个简易的 http 服务器，支持CGI。代码量少，非常容易阅读，十分适合网络编程初学者学习的项目。
 麻雀虽小，五脏俱全。在tinyhttpd中可以学到 linux 上进程的创建，管道的使用。linux 下 socket 编程基本方法和http 协议的最基本结构。

### 编译

修改了Makefile文件

### 阅读建议

每个函数的作用：

     accept_request:  处理从套接字上监听到的一个 HTTP 请求，在这里可以很大一部分地体现服务器处理请求流程。

     bad_request: 返回给客户端这是个错误请求，HTTP 状态吗 400 BAD REQUEST.

     cat: 读取服务器上某个文件写到 socket 套接字。

     cannot_execute: 主要处理发生在执行 cgi 程序时出现的错误。

     error_die: 把错误信息写到 perror 并退出。

     execute_cgi: 运行 cgi 程序的处理，也是个主要函数。

     get_line: 读取套接字的一行，把回车换行等情况都统一为换行符结束。

     headers: 把 HTTP 响应的头部写到套接字。

     not_found: 主要处理找不到请求的文件时的情况。

     sever_file: 调用 cat 把服务器文件返回给浏览器。

     startup: 初始化 httpd 服务，包括建立套接字，绑定端口，进行监听等。

     unimplemented: 返回给浏览器表明收到的 HTTP 请求所用的 method 不被支持。

建议源码阅读顺序： main -> startup -> accept_request -> execute_cgi, 通晓主要工作流程后再仔细把每个函数的源码看一看。

注意点： http解析一行。如果遇到\r，就必定是一行。\r或\r\n，都是当做一行
 
### 以下内容为原来 tinyhttpd 的 README 原版内容。

  This software is copyright 1999 by J. David Blackstone.  Permission
is granted to redistribute and modify this software under the terms of
the GNU General Public License, available at http://www.gnu.org/ .

  If you use this software or examine the code, I would appreciate
knowing and would be overjoyed to hear about it at
jdavidb@sourceforge.net .

  This software is not production quality.  It comes with no warranty
of any kind, not even an implied warranty of fitness for a particular
purpose.  I am not responsible for the damage that will likely result
if you use this software on your computer system.

  I wrote this webserver for an assignment in my networking class in
1999.  We were told that at a bare minimum the server had to serve
pages, and told that we would get extra credit for doing "extras."
Perl had introduced me to a whole lot of UNIX functionality (I learned
sockets and fork from Perl!), and O'Reilly's lion book on UNIX system
calls plus O'Reilly's books on CGI and writing web clients in Perl got
me thinking and I realized I could make my webserver support CGI with
little trouble.

  Now, if you're a member of the Apache core group, you might not be
impressed.  But my professor was blown over.  Try the color.cgi sample
script and type in "chartreuse."  Made me seem smarter than I am, at
any rate. :)

  Apache it's not.  But I do hope that this program is a good
educational tool for those interested in http/socket programming, as
well as UNIX system calls.  (There's some textbook uses of pipes,
environment variables, forks, and so on.)

  One last thing: if you look at my webserver or (are you out of
mind?!?) use it, I would just be overjoyed to hear about it.  Please
email me.  I probably won't really be releasing major updates, but if
I help you learn something, I'd love to know!

  Happy hacking!

                                   J. David Blackstone
