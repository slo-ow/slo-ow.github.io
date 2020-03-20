---
title:  "[ERROR] The path attribute with value... has been ignored"
categories: Error
tags:
  - Spring Error Web Server Tomcat
toc: true
toc_label: "On this Page"
toc_icon: "cog"
header:
  overlay_image: "/assets/images/Spring/springcover.png"
  overlay_filter: 0.5
  image_description: "header cover image"
---


Spring 프로젝트를 진행하면서 Tomcat 서버를 돌리다가 아래와 같은 경고 메시지 받았다 <br />

<a href="{{ site.error_img }}/spring_error2.JPG" data-lightbox="falcon9-large" data-title="Check out the image">
  <img src="{{ site.error_img }}/spring_error2.JPG" title="Check out the image">
</a>

<br />

``` java
경고: The path attribute with value [/myspring] in deployment descriptor[C:\spring-tool-suite-4-4.1.2.RELEASE-e4.10.0-win32.win32.x86_64\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp2\conf\Catalina\localhost\myspring.xml] has been ignored
```
<br />

해결 방법은 아래의 오류를 해결하니 동시에 잡혔다 <br />

<a href="https://doorisopen.github.io/error/2019/08/20/Error-(SetContextPropertiesRule).html">Error-(SetContextPropertiesRule)<a>

<hr />

### References
> * From by [doorisopen](https://doorisopen.github.io/)
