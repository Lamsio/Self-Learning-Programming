## Servlet
类似于Node.js中的Express框架。

**切记：Tomcat 10以上请使用依赖jakarta.servlet-api！**

#### 生命周期
![[Pasted image 20220610005814.png]]

#### UrlPattern匹配规则
UrlPattern支持几种匹配：
1. 多匹配
2. 精确匹配
3. 目录匹配
4. 扩展名匹配
5. 任意匹配

匹配顺序是按代码顺序从上往下的，如果匹配到`/sleep`就不会匹配`/*`，因此通常`/*`建议放在末尾

###### 多匹配
`@WebServlet(urlPatterns = {"/demo2","/demo3"})`
用花括号包裹可以包含多个匹配路径

###### 精确匹配
`@WebServlet(urlPatterns = {"/demo2","/demo3"})`
指明匹配路径

###### 目录匹配
`@WebServlet(urlPatterns = "/*")`
`/*`优先级高于`/`

###### 扩展名匹配
`@WebServlet(urlPatterns = "*.hello")`
任何以`.hello`结尾的，都会被匹配到
不支持以`/`开头的路径，必须是末尾路径