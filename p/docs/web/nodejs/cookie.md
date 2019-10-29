## JS中对Cookie的操作详解

```
(function(){
 var cookieObj={
   'add':function(name, value, hours){ //修改或是添加cookie
    var expire = "";
    if(hours != null){
     expire = new Date((new Date()).getTime() + hours * 3600000);
     expire = "; expires=" + expire.toGMTString();
    }    
    document.cookie = name + "=" + escape(value) + expire + ";path=/";
    //如果指定域名可以使用如下
    //document.cookie = name + "=" + escape(value) + expire + ";path=/;domain=findme.wang";
   },
   'get':function(c_name){//读取cookie
    if (document.cookie.length>0){
      c_start=document.cookie.indexOf(c_name + "=")
      if (c_start!=-1){ 
      c_start=c_start + c_name.length+1 
      c_end=document.cookie.indexOf(";",c_start)
      if (c_end==-1){
       c_end=document.cookie.length
      }
      return unescape(document.cookie.substring(c_start,c_end))
      } 
      }
     return "";
   }
 };
 window.cookieObj=cookieObj;
}());
```