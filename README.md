# js-plugin


<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>3D轮播</title>
	<meta charset="UTF-8" />
	<meta name="format-detection" content="telephone=no">
	<meta name="x5-orientation" content="portrait">
	<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1, maximum-scale=1, user-scalable=no">
	<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
	<meta name="apple-mobile-web-app-capable" content="yes">
	<meta name="apple-mobile-web-app-status-bar-style" content="black">
	<style>
		*{margin: 0;padding: 0;}
		html,body{width:100%;height: 100%;}
		ul,li{list-style: none}
		.special{width:100%;overflow: hidden;background: #cb1919 url("special_bg.jpg") no-repeat center top;background-size:7.5rem 6.55rem;height: 6.55rem;}
		#specialBanner{width:100%;height:4.7rem;margin-top: 1.55rem;position: relative;}
		.special-img{transition: all .5s linear;position: absolute;display: block;}
		.special-img:nth-of-type(1){background: url("special_0.png") no-repeat center top;background-size:100% 100%;}
		.special-img:nth-of-type(2){background: url("special_1.png") no-repeat center top;background-size:100% 100%;}
		.special-img:nth-of-type(3){background: url("special_2.png") no-repeat center top;background-size:100% 100%;}
		.special-img:nth-of-type(4){background: url("special_3.png") no-repeat center top;background-size:100% 100%;}
		.special-before{width:3.47rem;height:3.95rem;left:50%;top:0;transform:translateX(-50%);z-index: 2}
		.special-left,.special-right{width:1.6rem;height:1.82rem;top:.86rem;z-index: 1}
		.special-left{left:0;}
		.special-right{left:79%;}
		.special-after{width:.8rem;height:.91rem;left:50%;top:1.4rem;transform:translateX(-50%);z-index: 0}
		ul{position: absolute;bottom:0;left:50%;transform:translateX(-50%);width:1.96rem;height: .18rem;overflow: hidden;}
		li{float: left;margin:0 .15rem;width:.18rem;height:.18rem;border-radius: 50%;background: #970d0d}
	</style>
	<script type="text/javascript" src="zepto.min.js"></script>
</head>
<body>
	<section class="special">
	    <section id="specialBanner">
	        <a href="javascript:;"  class="special-img special-before"></a>
	        <a href="javascript:;"  class="special-img"></a>
	        <a href="javascript:;"  class="special-img"></a>
	        <a href="javascript:;"  class="special-img"></a>
	        <ul id="specialDot">
	            <li></li>
	            <li></li>
	            <li></li>
	            <li></li>
	        </ul>
	    </section>
	</section>
	<script>
		$("html").css("font-size",window.screen.width/7.5+"px");

		function getMoveAngle(sX,sY,eX,eY){
	        var xSpan = eX - sX;
	        var ySpan = eY - sY;
	        return (Math.atan2(-ySpan,xSpan))*180/Math.PI;
	    }
	    function changeStyle(){
	        for(var i=0;i<4;i++){
	            $('.special-img')[i].className="special-img "+classArr[i];
	            $('#specialBanner>a')[i].setAttribute('href','javascript:;');
	        }
	        var thisDot = classArr.indexOf('special-before');
	        $('#specialDot>li').css("background","#970d0d");
	        $('#specialDot>li').eq(thisDot).css("background","#fff");
	        $('#specialBanner>a')[thisDot].setAttribute('href',urlArr[thisDot]);
	    }
	    function moveResult(){
	        angle = getMoveAngle(startX,startY,endX,endY);
	        if(angle<45&&angle>-45){
	            //"right";
	            classArr.push(classArr.shift());
	            changeStyle();
	        }else if(angle>=45&&angle<135){
	            //"top";
	        }else if(angle>=135||angle<-135){
	            //"left";
	            classArr.unshift(classArr.pop());
	            changeStyle();
	        }else{
	            //"bottom";
	        }
	    }
	    var [startX,startY,moveX,moveY,endX,endY,angle] = [0,0,0,0,0,0,0];
	    var classArr = ['special-before','special-right','special-after','special-left'];
	    var urlArr = ['https://www.baidu.com/','http://www.hao123.com/','https://www.taobao.com/','https://www.jd.com/'];
	    for(var i=0;i<4;i++){
	        $('.special-img').eq(i).addClass(classArr[i]);
	        $('#specialBanner>a')[i].setAttribute('href','javascript:;');
	    }
	    $('#specialBanner>a')[0].setAttribute('href',urlArr[0]);
	    $('#specialDot>li').eq(0).css("background","#fff");

	    $('#specialBanner').on('touchstart',function (e) {
	        startX = endX = e.touches[0].clientX;
	        startY = endY = e.touches[0].clientY;
	    });
	    $('#specialBanner').on('touchmove',function (e) {
	        endX = e.touches[0].clientX;
	        endY = e.touches[0].clientY;
	    })
	    $('#specialBanner').on('touchend',function (e) {
	        startX==endX&&startY==endY ? '' : moveResult();
	        [startX,startY,moveX,moveY,endX,endY,angle] = [0,0,0,0,0,0,0];
	    })
	</script>
</body>
</html>
