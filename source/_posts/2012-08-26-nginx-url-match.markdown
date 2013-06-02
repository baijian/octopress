---
layout: post
title: "nginx-url-match"
date: 2012-08-26 22:07
comments: true
categories: 
---
nginx的location配置:<br/>
I recommend that you should learn the configuration from website: <a href="http://nginx.org/en/docs/http/ngx_core_module.html#location">nginx.org/en/docs/</a>,
  It is accurate and clear, of course It is in english.<br/>
If you do not want to read english doc, you can learn from my opinion below:
<!-- more -->
location的匹配方法主要分为两种,
    1.普通匹配
      一些列子(prefix locations)：
      location /echo {},
      location = /echo {},
      location ^~ /echo {}.
    2.正则匹配
      一些例子(regular expressions):
      location ~ \.php$ {},
      location ~* \.php$ {}.

location的匹配顺序解释：<br/>
nginx首先会进行普通匹配,会匹配到一个相对最相似的location(没有什么顺序而言),但是并不一定会选择这个location处理请求,而是继续正则匹配（按配置文件书写的顺序),第一个匹配到的location将会处理请求，如果没有匹配到,就选择普通匹配里面那个最相似的进行处理。

关于普通匹配的一些解释：<br/>
1.= /echo 普通匹配里面的=表示如果完全匹配到这个location,就将选择这个location处理请求,而不会再去测试正则匹配了.<br/>
2.^ ~ /echo 表示如果在普通匹配阶段匹配到这个location,就不会再去测试正则匹配了,和=比较类似,不过还是有一点区别的.<br/>
3.在nginx0.7.1到0.8.41版本里面如果一个请求完全匹配到一个location,但是没有=或者^ ~,也不进行正则匹配了.<br/>

ok,that's all~下面给一个server的配置实例:<br/>
{
    server{
        listen 8081;
        root /home/bj/web/app-demo1;
        location = /index.php {
            fastcgi_index index.php;
            fastcgi_pass 127.0.0.1:9000;
            include /usr/local/nginx/conf/fastcgi_params;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            fastcgi_param SCRIPT_NAME $fastcgi_script_name;
        }   
        location ^~ /web/app/ {
            rewrite . /index.php last;
        }   
        location ~* .* {
            echo 'hi~ the page is not exists,so 404~';
        }   
    }
}

