$(function(){
/*待接单*/ 
    var ifdetail = $('.J_toggle');
    ifdetail.click(function(){
        $(this).toggleClass('down').parents('.order-detail').toggleClass('active');
    });
/*弹出框*/
var popBox = $('.alert-layer');
    function showPop(obj){
        obj.removeClass('none');
    };
    function hidePop(obj){
        obj.addClass('none');
    };
    $('.J_addFare').click(function(){
        showPop(popBox);
    }) 
    $('.J_cancel,.J_confirm').click(function(){
        hidePop(popBox);
    });
    popBox.click(function(e){
        var objSrc = e.target.getAttribute('class');
        if(objSrc === 'alert-layer'){
            $(this).addClass('none');   
        } else{
            return false;
        }
    })        
//获取验证码 
    var t,
        timer,
        JgetCode=$('.J_GetCode'),
        bState=true;
    function getCode(){
        t=3;
        clearInterval(timer);
        timer=setInterval(function(){
            bState = false;
            JgetCode.html(t+"&nbsp;s").addClass('code_gray');
            if (t==0) {
                clearInterval(timer);
                JgetCode.html("获取验证码").removeClass('code_gray');
                bState = true;
            };
            t--;
        },1000);
    };
    JgetCode.click(function(){
        bState && getCode();
    });
// 维修工星级评价
    var gradeId = 4 
    var gradeItem = $('.J_grade').find('span');
    for (var i = 0; i < gradeItem.length; i++) {
        if(i < gradeId){
            gradeItem.eq(i).addClass('active');
        }
    }        
})