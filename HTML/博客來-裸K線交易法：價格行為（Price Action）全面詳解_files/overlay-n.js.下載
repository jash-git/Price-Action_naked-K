function Overlay(opt_module_id){
    var module_id = "";//模組編碼參數
    var self = this;
    
    //開始遮罩時執行的方法
    var loadInIframeModal = function(hash){
        var trigger = $(hash.t);
        var url = trigger.attr('href');
        if ($('#jqmContent').attr('src') != url){
            $('#jqmContent').html('').attr('src', url);
            $('#jqmTitleText').text(trigger.attr('title'));
        }
        $('.jqmWindow').css('height','660px');
        $('.jqmWindow').css('width','847px');
        $('.jqmWindow').css('left',($(document).width()/2-450)+'px');
        hash.w.fadeIn().show();
        //將header的順序往下壓
        $('#header_id').css( "zIndex", 3 );
    };

    //關閉遮罩時，執行的方法
    var closeModal = function(hash){
        hash.w.fadeOut(function(){
            hash.o.remove();
            //重新load iframe關閉影片
            if($('#jqmContent')[0].contentWindow){ // 多數瀏覽器支援
                $('#jqmContent')[0].contentWindow.location.reload();
            }else{
                $('#jqmContent')[0].contentDocument.location.reload();
            }
            //將header的順序提到最上面
            $('#header_id').removeAttr('style');
        });
    };
    
    if ($('#modalWindow').length == 0){
        var modal = '<div class="jqmWindow" id="modalWindow"><button type="button" class="btn closePop jqmClose" title="關閉視窗"><span class="hide">關閉視窗</span></button><iframe id="jqmContent" src="" scrolling="no" frameborder="0"></iframe></div>';
        $('body').append(modal);
    }//end if

    //初始化 jqModal
    $('#modalWindow').jqm({    
        modal: true,
        trigger: 'a.thickbox',
        target: '#jqmContent',
        onHide: closeModal,
        onShow: loadInIframeModal
    });
    
    var jqmWindowTop = 15;//置頂
    //if (jqmWindowTop<0){jqmWindowTop=0;}
    if (!$.browser.msie) {
        $('#modalWindow').css('top',jqmWindowTop+'px');
    }
    

    
    //啟動縮圖轉動
    this.scroll = function(){
        $('.'+module_id+'_scroll').scrollable({
        });
        return;
    }
    //加入縮圖click事件
    this.bindEvent = function(){
        $('ul.'+module_id+'_item>li').click(function() {
            $('ul.'+module_id+'_item>li').removeClass('here');
            $(this).addClass('here');
            var url = $(this).find('img').attr('src');
            var img = new Image();
            img.onload = function() {
                $('.'+module_id+'_image_wrap').attr('src', url);
            };
            img.src = url;
        }).filter(':first').click();
        return;
    } 

    //主程式
    this.main = function(opt_module_id){
        module_id = opt_module_id;//取得參數
        self.bindEvent();
        self.scroll();
    }
    //執行主程式
    this.main(opt_module_id);

}
