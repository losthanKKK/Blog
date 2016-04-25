---
layout: post
title:  "Node process!"
date:   2016-04-25 22:52:36 +0800
---
process是一个全局内置对象，可以在代码中的任何位置访问此对象，这个对象代表我们的node.js代码宿主的操作系统进程对象。


使用process对象可以截获进程的异常、退出等事件，也可以获取进程的当前目录、环境变量、内存占用等信息，还可以执行进程退出、工作目录切换等操作。


当我们想要查看应用程序当前目录时，可以使用cwd函数，使用语法如下：


process.cwd();
如果需要改变应用程序目录，就要使用chdir函数了，它的用法如下：
process.chdir("目录");




stdout的基本用法
stdout是标准输出流
console.log = function(d){
    process.stdout.write(d+'\n');
}
console.log就是封装了它。




stderr的基本用法
stderr是标准错误流，和stdout的作用差不多，不同的是它是用来打印错误信息的，我们可以通过它来捕获错误信息，基本使用方法如下：
process.stderr.write(输入内容);




stdin的基本用法
stdin是进程的输入流,我们可以通过注册事件的方式来获取输入的内容，如下：
process.stdin.on('readable', function() {
  var chunk = process.stdin.read();
  if (chunk !== null) {
    process.stdout.write('data: ' + chunk);
  }
});
exit函数的基本用法
如果你需要在程序内杀死进程，退出程序，可以使用exit函数，示例如下：


process.exit(code);




process.stdout.on('data',function(data){
   console.log(data);
});
在我们的输入输出的内容中有中文的时候，可能会乱码的问题，这是因为编码不同造成的，所以在这种情况下需要为流设置编码，如下示例：


process.stdin.setEncoding(编码);
 
process.stdout.setEncoding(编码);
 
process.stderr.setEncoding(编码);