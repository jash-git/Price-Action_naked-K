$( document ).ready(function() {
    var getLazyloadColumn = function(lazyclsname,nolazyclsname,callback){
        $("."+lazyclsname).each(function(i , el){
            var column = $(el).not(":has(."+lazyclsname+")");
            if(column.length){
                var imgs = column.find("img").not("."+nolazyclsname+" img");
                if(imgs.length){callback(imgs);}
            }else{
                var imgs = $(el).find("img").not("."+lazyclsname+" ."+lazyclsname+" img").not("."+nolazyclsname+" img");
                if(imgs.length){callback(imgs);}
            }
        });
    };
    getLazyloadColumn("lazyload","nolazyload_img",function(imgs){
        imgs.lazyload({
           effect : "fadeIn"
        });
    });
});