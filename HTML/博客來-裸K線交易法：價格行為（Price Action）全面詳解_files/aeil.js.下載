var toHTML = {
    on: function(str) {
        var a = [],
        i = 0;
        for (; i < str.length;) a[i] = str.charCodeAt(i++);
        return "&#" + a.join(";&#") + ";"
    },
    un: function(str) {
        return str.replace(/&#(x)?([^&]{1,5});?/g,
        function(a, b, c) {
            return String.fromCharCode(parseInt(c, b ? 16 : 10))
        })
    }
};

$(document).ready(function () {    
   $("a[href^=http]:not([href*='facebook.com'],[href*='plurk.com'],[href*='twitter.com'],[href*='youtube.com'],[href*='google.com'],[href*='ireader.cc'],[href*='apple.com'])").live('click', function () {
        var re1 = /books.com.tw/;
        var re2 = /(books.com.tw|facebook.com|plurk.com|twitter.com|youtube.com|google.com|apple.com)/;
        var re3 = /(myaccount.books.com.tw)/;
        var a = this.href;
        if (re1.test(a)) {
           if (a.indexOf("ap.php") < 0) {
              return true;
           } else {
              var b = a.split("?")[1].split("&");
              var c = '';
              for (var i in b) {
                 if (b[i].split("=")[0] == 'url') {
                    c = b[i].split("=")[1];
                 }
              }
              if (c.substring(0, 4) != 'http') {
                 return true;
              }
              if (re2.test(c)) {
                 return true;
              }
           }
        }
        
        var msg = "您即將離開博客來前往其它網站。請確定是否繼續前往?\n若該網站要求輸入個人資料，請多加留意。 ";
        var msg2 = "&#x60a8;&#x5373;&#x5c07;&#x96e2;&#x958b;&#x535a;&#x5ba2;&#x4f86;&#x524d;&#x5f80;&#x5176;&#x5b83;&#x7db2;&#x7ad9;&#x3002;&#x8acb;&#x78ba;&#x5b9a;&#x662f;&#x5426;&#x7e7c;&#x7e8c;&#x524d;&#x5f80;&#x3f;&#x5c;&#x6e;&#x82e5;&#x8a72;&#x7db2;&#x7ad9;&#x8981;&#x6c42;&#x8f38;&#x5165;&#x500b;&#x4eba;&#x8cc7;&#x6599;&#xff0c;&#x8acb;&#x591a;&#x52a0;&#x7559;&#x610f;&#x3002;";
        if(re3.test(document.domain)){
            return confirm(msg);
        }else{
            var msg = toHTML.un(msg2);
            return confirm(msg.replace("\\n","\n"));        
        }
        
   });
});