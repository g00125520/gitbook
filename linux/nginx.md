# understand and use configuration to solve problems

## proxy_redirect:修改从被代理服务器传来的应答头中的"Location"和"Refresh"字段。

语法：proxy_redirect [ default|off|redirect replacement ],proxy_redirect http:// https://,修改location中的协议。proxy_redirect ~^(.*)abc(.*) https://abc.com/$1

## rewrite:实现URL重定向的重要指令，根据regex来匹配内容跳转到replacement

rewrite ^(.*) https://$server_name$1 permanent;

## proxy_set_header:重新定义或者添加发往后端服务器的请求头

- proxy_set_header Host  $proxy_host;设置host为被代理服务器地址；
- proxy_set_header Host  $http_host;和源请求头一样；
- proxy_set_header Host  $host;如果源没有host，则为主机域名；
- proxy_set_header Host  $host:$proxy_port;

