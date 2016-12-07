---
title: 预防xss攻击-前端篇
date: 2016-11-18 16:11:04
tags: [xss]
---
#### 什么事xss攻击
- xss攻击：跨站脚本攻击(Cross Site Scripting)，为不和层叠样式表(Cascading Style Sheets, CSS)的缩写混淆，故将跨站脚本攻击缩写为XSS。恶意攻击者往Web页面里插入恶意Script代码，当用户浏览该页之时，嵌入其中Web里面的Script代码会被执行，从而达到恶意攻击用户的特殊目的。（解释摘自百度百科）
- 通俗点讲，一般攻击者把网站中的输入框中填写类似："/><script>alert('xss')</script><input value=" ,其中alert可以是获得用户cookie等敏感信息。
- 尤其是在后端渲染的页面，危害比较大
#### 解决办法
- 主要是处理输入表单和url中的 '"<>字符
- 网上有许多讲解的办法，在此不赘述，可以自行google，本文主要讲表单提交时的处理。
- 用以下方法处理以下
~~~
       /**
     * 防止xss替换特殊字符
     * @param str 源字符串
     * @returns {*} 转换后的字符串
     */
    function xssFilterStr(str){
        return str.replace(/\<|\>|\"|\'/g,function(MatchStr) {
            switch (MatchStr) {
                case "<":
                    return "&lt;";
                    break;
                case ">":
                    return "&gt;";
                    break;
                case "\"":
                    return "&quot;";
                    break;
                case "'":
                    return "&apos;";
                    break;

                default:
                    return'';
                    break;
            }
        });
    }

    /**
     * 防止xss替换特殊字符,兼容多种输入
     * @param input 可以是对象\数组\字符串
     * @returns {{}} 分别对应对象\对象\字符串,如果input不是以上数据类型,返回空数组""
     */
    function xssFilter(input){

        var res = {};
        if(Object.prototype.toString.call(input) == "[object Object]"){
            for(var key in input){
                res[xssFilterStr(key)] = xssFilterStr(input[key]);
            }
        }else if(Object.prototype.toString.call(input) == "[object Array]"){
            $.each(input,function (index,cur){
                res[xssFilterStr(cur["name"])] = xssFilterStr(cur["value"]);
            })
        }
        else if(Object.prototype.toString.call(input) == "[object String]"){
            res = xssFilterStr(input);
        }else{
            res = '';
        }

        return res;
    }
~~~

- 提交表单时用jquery.serialize的弊端
1. 序列化时，自动调用了encodeURIComponent，把"<>转义
2. 如果通过class/id等获取input单独处理，攻击者也可以在浏览器中删除对应class/id等，再提交
3. 因此建议用jquery.serializeArray方法，然后调用xssFilter函数处理
如果想全面防护，可以看一下这个项目 [Github-js-xss](https://github.com/leizongmin/js-xss)

##预防二:
页面增加CSP(Content Security Policy - 网页安全政策)的配置


详细介绍参见: [阮一峰博客](http://www.ruanyifeng.com/blog/2016/09/csp.html?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)
