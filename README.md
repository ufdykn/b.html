# b.html
<html lang="zh-cn">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1"/>
  <title>麦当劳雪碧领取.</title>
  <link href="//lib.baomitu.com/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet"/>
  <script src="//lib.baomitu.com/jquery/1.12.4/jquery.min.js"></script>
  <script src="//lib.baomitu.com/layer/3.1.1/layer.js"></script>
  <!--[if lt IE 9]>
    <script src="//lib.baomitu.com/html5shiv/3.7.3/html5shiv.min.js"></script>
    <script src="//lib.baomitu.com/respond.js/1.4.2/respond.min.js"></script>
  <![endif]-->
</head>
<body>
<div class="container">
<div class="col-xs-12 col-sm-10 col-md-8 col-lg-6 center-block" style="float: none;">
<br>
<div class="panel panel-primary">
<!-- background: linear-gradient(to right,#b221ff,#14b7ff,#8ae68a); -->
	<div class="panel-heading"><h3 class="panel-title">
	麦当劳雪碧领取. By: 网络达人.<br>作者QQ: 2829968806
	</div>
	<div class="panel-body" style="text-align: center;">
		<div class="list-group" id="PhoneInfo" style="display: block;">
			<div class="list-group-item">
			 	<img src="https://q4.qlogo.cn/headimg_dl?dst_uin=940055248&spec=100" width="80" style="border-radius: 50%;opacity: 0.80;" id="avatar">
			</div>
			<div class="list-group-item">
				<div class="input-group">
					<div class="input-group-addon">手机号: </div>
					<input type="text" id="phone" class="form-control" required="">
				</div>
			</div>
			<div class="list-group-item">
				<div class="input-group">
					<div class="input-group-addon">验证码: </div>
					<input type="text" id="code" class="form-control" required="">
				</div>
			</div>
			<!-- background: linear-gradient(to right,#b221ff,#14b7ff); -->
			<div class="list-group-item" id="Post"><a href="JavaScript:void(0)" onclick="sendCode()" class="btn btn-block btn-primary">发送验证码</a></div>
			<div class="list-group-item" id="Post"><a href="JavaScript:void(0)" onclick="getGift()" class="btn btn-block btn-primary">领取</a></div>
		</div>
	</div>
	<div class="panel-heading"><h3 class="panel-title">
		使用教程: <br>
		1: 发送验证码<br>
		2: 输入验证码进行领取<br>
		3: 截图二维码<br>
		4: 去麦当劳店里去领取兑换即可<br>
	</div>
</div>
</div>
</div>
<script type="text/javascript">
	function sendCode(){
		let phone = $('#phone').val();
		var regex = /^1[123456789]\d{9}$/;
		if(!regex.test(phone)) {
			layer.msg('手机号有误!');
			return;
		}
		let url = 'operate.php?do=sendCode&phone=' + phone
		$.ajax({
			url: url,
			type: 'get',
			success: function(res){
				if(res.code != 0) {
					layer.msg('验证码发送失败!');
				} else {
					layer.msg('验证码发送成功!');
				}
			}
		})
	}

	function getGift(){
		let phone = $('#phone').val();
		var regex = /^1[123456789]\d{9}$/;
		if(!regex.test(phone)) {
			layer.msg('手机号有误!');
			return;
		}

		let code = $('#code').val();
		if(code == '') {
			layer.msg('请输入验证码!');
			return;
		}

		let url = 'operate.php?do=getGift&phone=' + phone + '&code=' + code
		$.ajax({
			url: url,
			type: 'get',
			success: function(res){
				if(res.code == 0) {
					layer.msg('领取成功, 稍后即将展示二维码!');
					setTimeout(function(){
						var imgUrl = 'http://q.ppzzt.cn/qrcode/api.php?text=' + res.data.code;
						layer.open({
							type: 1
							,title: phone //不显示标题栏
							,closeBtn: false
							,shade: 0.8
							,id: 'LAY_layuipro' //设定一个id，防止重复弹出
							,btn: ['收到']
							,btnAlign: 'c'
							,moveType: 1 //拖拽模式，0或者1
							,content: '<div style=line-height: 22px; background-color: #393D49; color: #fff;"><p><img style="width: 270px;height: 270px" src="'+imgUrl+'" alt=""></p></div>'
						});
					}, 1000)
				} else {
					layer.msg('领取失败, 验证码错误或者其他!');
				}
			}
		})

	}
</script>
</body>
</html>
