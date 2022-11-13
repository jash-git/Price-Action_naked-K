function img_zoomer(opt_module_id){
    var mod = $('#'+opt_module_id), //模組容器 (=blk的容器)
        img = $('.cover',mod), //小圖
        mdw = $(mod).width(), //mod容器尺寸
        mdh = $(mod).height(),
        ie = $.browser.msie,
        iev = parseInt($.browser.version),
        ie8 = ie && (iev>=8),
        body = $('body')[0],
        min_size = 700, //啟動效果的最低尺寸
        img_waiting = '#fff url("https://db.books.com.tw/G/shopping_car_2007/images/waiting.gif") 50% 50% no-repeat',
        img_blk = 'url(/csss/images/img_drag_bg.gif)',
        blkCSS = {
            background: img_blk,
            position: 'absolute',
            cursor:'move'
        },
        preCSS = {
            width:440,
            height:440,
            overflow:'hidden',
            position: 'absolute',
            visibility: 'hidden',
            background: img_waiting
        },
        tempImgCSS = {
            position:'absolute',
            visibility:'hidden',
            top:'-9999px',
            display:'none'
        },
        obj = this; 
    obj.main = function(){
        $(mod).bind({
            'mouseenter':function(e){obj.open(e)},
            'mouseleave':function(){obj.close()}
        });
    };
    obj.open = function(e){       
        var src = $(img).attr('src'); //小圖路徑
        obj.setDOM().setImg(src,e);
    };
    obj.close = function(){       
        $('#img_drag_pre').remove();
        $('#img_drag_blk').remove();
        $('#img_drag_tempimg').remove();
        $(mod).unbind('mousemove');
    };
    obj.setDOM = function(e){
        //var pos = $('.prd001').offset(); //品名容器位置(H2)
        var pos = $('h1:eq(0)').offset(); //品名容器位置(H1)
        var blk = $('<div id="img_drag_blk"></div>');
        var pre = $('<div id="img_drag_pre"><img title="loading"></div>'); //預覽框
        $(pre).appendTo(body).css({
            left: pos.left-10,
            top: pos.top
        }).css(preCSS);
        $(blk).appendTo(mod)
            .css(blkCSS);
        return obj;
    };
    obj.setImg = function(s,e){
//        var psrc = s.substring(0,s.indexOf('&v=')).replace(/^http.*i=/,''); //原始圖路徑
//        var verno = s.substr(s.indexOf('&v=')+3,8); //取得版號        
        //var patt = /(https?:)?\/\/.*\?i=([\w\d\/\.:]+)&v=([\d\w]+)&.*/i;
        var patt = /(?:https?:)?\/\/.*\?i=([\w\d\/\.:]+)&v=([\d\w]+)&.*/i;
        var result_arr = patt.exec(s);  //取得 pattern 後的結果
        var psrc_org = result_arr[1];   //原始圖路徑
        var verno = result_arr[2];  //取得版號
        var psrc = '//im1.book.com.tw/image/getImage?i='+psrc_org+'?v='+verno; //取得帶縮圖程式的原圖
        if(!ie || ie8){
            var img1 = $('<img id="img_drag_tempimg">');
            $(img1).load(function(){
                $(img1).appendTo(body).css(tempImgCSS);
                var iw = $(img1).width(),
                    ih = $(img1).height(),
                    is = (iw>=ih)?iw:ih;
                if(is>=min_size){
                    var nsrc = '//im2.book.com.tw/image/getImage?i='+psrc_org+'&v='+verno+'&w='+is+'&h='+is,
                        pre = $('#img_drag_pre');
                    $(pre).css('visibility','visible');
                    var img2 = $('<img>');
                    $(img2).load(function(){
                        $('img',pre).attr('src',nsrc).css('position','absolute');
                        obj.setBlk($('img',pre)).move(e);
                    }).attr('src',nsrc);
                }
            }).attr('src',psrc);
        }
    };
    obj.setBlk = function(i){
        var pre = $('#img_drag_pre');
        $('#img_drag_blk').css({
            width:mdw*$(pre).width()/$(i).width(),
            height:mdh*$(pre).height()/$(i).height()
        });
        return obj;
    };
    obj.setPos = function(e){
        var msx = e.pageX, //滑鼠座標
            msy = e.pageY,
            mdx = $(mod).offset().left, //mod容器座標
            mdy = $(mod).offset().top,
            blk = $('#img_drag_blk'),
            pre = $('#img_drag_pre'),
            bw = $(blk).width(), //blk尺寸
            bh = $(blk).height(),
            bxx = (msx-mdx-0.5*bw<=0)?0:((msx-mdx>=mdw-0.5*bw)?mdw-bw:msx-mdx-0.5*bw), //滑鼠修正座標
            byy = (msy-mdy-0.5*bh<=0)?0:((msy-mdy>=mdh-0.5*bh)?mdh-bw:msy-mdy-0.5*bh),
            mrx = bxx/mdw, //滑鼠位移率
            mry = byy/mdh;
        $(blk).css({
            left: bxx,
            top:byy,
            'z-index':1
        });
        $('.looks',mod).css('z-index',2);
        $('img',pre).css({
            left: -1*mrx*$('img',pre).width(),
            top: -1*mry*$('img',pre).height()
        });
    };
    obj.move = function(e){ //e=event
        obj.setPos(e);
        $(mod).bind('mousemove',function(e){
            obj.setPos(e);
        });            
    };
    obj.main();
}