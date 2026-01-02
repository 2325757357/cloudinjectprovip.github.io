<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>微信扫码自助充值</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Microsoft Yahei", sans-serif;
        }
        body {
            background-color: #f5f5f5;
        }
        .header {
            background-color: #128cff;
            color: #fff;
            padding: 15px 10px;
            text-align: center;
            font-size: 18px;
            font-weight: 500;
        }
        .container {
            width: 90%;
            margin: 20px auto;
            background-color: #fff;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }
        .title {
            text-align: center;
            font-size: 22px;
            font-weight: bold;
            margin-bottom: 10px;
        }
        .sub-title {
            text-align: center;
            color: #999;
            font-size: 14px;
            margin-bottom: 20px;
        }
        .progress-bar {
            height: 20px;
            background-color: #ddd;
            border-radius: 10px;
            margin-bottom: 30px;
        }
        .process-box {
            background-color: #fef9e7;
            padding: 15px;
            border-radius: 5px;
            margin-bottom: 30px;
        }
        .process-title {
            color: #d68910;
            font-size: 16px;
            font-weight: bold;
            margin-bottom: 10px;
        }
        .process-list {
            color: #666;
            font-size: 14px;
            line-height: 1.8;
            margin-bottom: 15px;
        }
        .tips-red {
            color: #e74c3c;
            font-size: 14px;
            line-height: 1.8;
            margin-bottom: 10px;
        }
        .tips-yellow {
            color: #d68910;
            font-size: 14px;
        }
        .qq-link {
            color: #2980b9;
            text-decoration: none;
        }
        .qrcode-box {
            text-align: center;
            margin-bottom: 20px;
        }
        .qrcode {
            width: 200px;
            height: 200px;
            border: 1px solid #eee;
            display: inline-block;
            object-fit: cover;
        }
        .link-box {
            text-align: center;
        }
        .wechat-link {
            color: #e74c3c;
            font-size: 16px;
            text-decoration: none;
            display: block;
            margin-bottom: 15px;
        }
        .admin-link {
            color: #2980b9;
            font-size: 14px;
            text-decoration: none;
        }
        .font-bold {
            font-weight: bold;
        }
        .font-red {
            color: #e74c3c;
        }
        /* 新增会员权益折叠面板样式 */
        .vip-benefits {
            margin: 30px 0;
        }
        .benefits-trigger {
            background-color: #e0e0e0;
            color: #333;
            padding: 12px 15px;
            border-radius: 5px;
            text-align: center;
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .benefits-trigger:hover {
            background-color: #d0d0d0;
        }
        .benefits-content {
            margin-top: 15px;
            padding: 15px;
            background-color: #f9f9f9;
            border-radius: 5px;
            display: none;
        }
        .benefits-content.active {
            display: block;
        }
        .benefits-title {
            color: #128cff;
            font-size: 16px;
            font-weight: bold;
            margin-bottom: 12px;
        }
        .benefits-list {
            color: #666;
            font-size: 14px;
            line-height: 2.0;
            list-style-position: inside;
        }
        .benefits-list li {
            margin-bottom: 5px;
        }
    </style>
</head>
<body>
    <div class="header">
        微信扫码自助充值
    </div>
    <div class="container">
        <h1 class="title">会员购买须知</h1>
        <p class="sub-title">请按照流程完成支付</p>
        <div class="progress-bar"></div>
        <div class="process-box">
            <h2 class="process-title">购买流程说明：</h2>
            <div class="process-list">
                1.微信扫描下方二维码进入支付页面<br>
                2.选择您需要充值的金额（会员 ¥15/月）<br>
                3.输入<span class="font-bold font-red">本平台登录账号</span>完成支付<br>
                4.自助充值<span class="font-bold font-red">1-3日内到账余额</span>，自行开通会员
            </div>
            <div class="tips-red">
                未到账处理：若超出3日仍未到账，请您立即 <a href="mqqapi://card/show_pslcard?src_type=internal&version=1&uin=2912409904&card_type=person&source=qrcode" class="qq-link">联系管理员 QQ2912409904</a>
            </div>
            <div class="tips-yellow font-bold">注意：<span class="font-red">因账号输入错误充至其他账户，责任自负、不予退款。</span></div>
        </div>

        <!-- 新增会员权益折叠面板 -->
        <div class="vip-benefits">
            <div class="benefits-trigger" onclick="toggleBenefits()">点击查看会员权益</div>
            <div class="benefits-content" id="benefitsContent">
                <h3 class="benefits-title">会员权益说明：</h3>
                <ul class="benefits-list">
                    <li>单文件最大上传 300M，再大就不支持了需要拆包进行注入。</li>
                    <li>会员期间内不会自动清理已上传的安装包。</li>
                    <li>单应用最多支持3000条未使用卡密。</li>
                    <li>累计2.5GB云储存空间。</li>
                    <li>支持应用实时在线用户管理。</li>
                    <li>支持实时用户踢下线。</li>
                    <li>使用平台加固功能。</li>
                    <li>单应用最多允许创建20个HTML弹窗。</li>
                    <li>专属VIP身份标识。</li>
                    <li>专属客服。</li>
                </ul>
            </div>
        </div>

        <div class="qrcode-box">
            <img src="https://i10.hoopchina.com.cn/editor/bf4caaf1374f72e9824671dc086ed935_w_500_h_500_.png" class="qrcode" alt="充值二维码" referrerpolicy="no-referrer">
        </div>
        <div class="link-box">
            <a href="javascript:window.location.href='weixin://'" class="wechat-link">点我立即打开微信扫一扫</a>
            <a href="mqqapi://card/show_pslcard?src_type=internal&version=1&uin=2912409904&card_type=person&source=qrcode" class="admin-link">点我联系管理员 QQ2912409904</a>
        </div>
    </div>

    <!-- 折叠面板切换脚本 -->
    <script>
        function toggleBenefits() {
            const content = document.getElementById('benefitsContent');
            content.classList.toggle('active');
        }
    </script>
</body>
</html>
