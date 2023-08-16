---
title: "Amazon Pinpointのハンズオンをやってみた（その１）"
emoji: "⛳"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Pinpoint", "Handson"]
published: true
---

## はじめに

今回は、Amazon Pinpointのハンズオンをやっていきたいと思います。
Pinpoint、Amplifyでも使えるのですが、まだよくわかってない（汗）
とにかく手を動かして体で覚えていきましょう！
やれば、できる！！

## ハンズオンのURL
https://catalog.workshops.aws/amazon-pinpoint-customer-experience/ja-JP/prerequisites/create-a-project


## Amazon Pinpoint のプロジェクトの作成

![](/images/aws-pinpoint-handson-01/2023-08-11-20-50-36.png)

ハンズオンに指示のある通り、`clothes_store`というプロジェクトを作ってみましょう。
`Project name`に`clothes_store`を入力して、`Create a project`ボタンをクリックします。

![](/images/aws-pinpoint-handson-01/2023-08-11-20-53-02.png)

プロジェクトの作成が完了しましたね。

![](/images/aws-pinpoint-handson-01/2023-08-11-20-53-29.png)

## Eメールチャネルの設定

顧客にEメールを送信するためのメールアドレスの確認を行います。

![](/images/aws-pinpoint-handson-01/2023-08-11-20-59-02.png)


`を 編集`←（なんだこれは笑）ボタンをクリックします。

![](/images/aws-pinpoint-handson-01/2023-08-11-21-07-52.png)

`このプロジェクトの E メールチャネルを有効にする`にチェックします。

![](/images/aws-pinpoint-handson-01/2023-08-11-21-09-36.png)

Eメールを送信するために使用するメールアドレスを入力します。
入力したら`保存`ボタンをクリックします。

![](/images/aws-pinpoint-handson-01/2023-08-11-21-11-59.png)

と思ったら、怒られた。。

![](/images/aws-pinpoint-handson-01/2023-08-11-21-15-53.png)

`E メールアドレスを確認`ボタンをクリックするようです。
クリックすると下記のようになります。

![](/images/aws-pinpoint-handson-01/2023-08-11-21-16-50.png)

入力したメールアドレス宛に、`Amazon Web Services – Email Address Verification Request in region Asia Pacific`というタイトルのメッセージが送られてくるので、そのメールの中にあるリンクをクリックして、認証します。

![](/images/aws-pinpoint-handson-01/2023-08-11-21-20-32.png)

これでメールアドレスが認証されました。
今度こそ`保存`ボタンをクリックします。

![](/images/aws-pinpoint-handson-01/2023-08-11-22-21-30.png)

これでEメールチャネルの設定が完了です。

## E メールの送信
次に先ほど確認したメールアドレスにテストメールを送信してみることにします。

左メニューから、`分析 > メッセージングをテスト`をクリックします。

![](/images/aws-pinpoint-handson-01/2023-08-11-22-56-13.png)

![](/images/aws-pinpoint-handson-01/2023-08-11-22-57-45.png)

![](/images/aws-pinpoint-handson-01/2023-08-11-22-58-05.png)

設定はそのまま`E メール`でいきましょ。

メッセージの`件名`は`Sample Email`で。
メッセージについては、下記をコピーして使います。
→ハンズオンではダウンロードするようです。

```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xmlns:o="urn:schemas-microsoft-com:office:office" style="width:100%;font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';-webkit-text-size-adjust:100%;-ms-text-size-adjust:100%;padding:0;Margin:0">
 <head>
  <meta charset="UTF-8">
  <meta content="width=device-width, initial-scale=1" name="viewport">
  <meta name="x-apple-disable-message-reformatting">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta content="telephone=no" name="format-detection">
  <title>Welcome to Amazon Pinpoint</title>
  <!--[if (mso 16)]>
    <style type="text/css">
    a {text-decoration: none;}
    </style>
    <![endif]-->
  <!--[if gte mso 9]><style>sup { font-size: 100% !important; }</style><![endif]-->
  <!--[if gte mso 9]>
<xml>
    <o:OfficeDocumentSettings>
    <o:AllowPNG></o:AllowPNG>
    <o:PixelsPerInch>96</o:PixelsPerInch>
    </o:OfficeDocumentSettings>
</xml>
<![endif]-->
  <style type="text/css">
.section-title {
	padding:5px 10px;
	background-color:#f6f6f6;
	border:1px solid #dfdfdf;
	outline:0;
}
#outlook a {
	padding:0;
}
.ExternalClass {
	width:100%;
}
.ExternalClass,
.ExternalClass p,
.ExternalClass span,
.ExternalClass font,
.ExternalClass td,
.ExternalClass div {
	line-height:100%;
}
.es-button {
	mso-style-priority:100!important;
	text-decoration:none!important;
}
a[x-apple-data-detectors] {
	color:inherit!important;
	text-decoration:none!important;
	font-size:inherit!important;
	font-family:inherit!important;
	font-weight:inherit!important;
	line-height:inherit!important;
}
.es-desk-hidden {
	display:none;
	float:left;
	overflow:hidden;
	width:0;
	max-height:0;
	line-height:0;
	mso-hide:all;
}
[data-ogsb] .es-button {
	border-width:0!important;
	padding:10px 35px 10px 35px!important;
}
[data-ogsb] .es-button.es-button-1 {
	padding:10px 35px!important;
}
@media only screen and (max-width:600px), screen and (max-device-width:600px) {p, ul li, ol li, a { line-height:150%!important } h1, h2, h3, h1 a, h2 a, h3 a { line-height:120% } h1 { font-size:30px!important; text-align:center } h2 { font-size:26px!important; text-align:center } h3 { font-size:20px!important; text-align:center } .es-header-body h1 a, .es-content-body h1 a, .es-footer-body h1 a { font-size:30px!important } .es-header-body h2 a, .es-content-body h2 a, .es-footer-body h2 a { font-size:26px!important } .es-header-body h3 a, .es-content-body h3 a, .es-footer-body h3 a { font-size:20px!important } .es-menu td a { font-size:16px!important } .es-header-body p, .es-header-body ul li, .es-header-body ol li, .es-header-body a { font-size:16px!important } .es-content-body p, .es-content-body ul li, .es-content-body ol li, .es-content-body a { font-size:16px!important } .es-footer-body p, .es-footer-body ul li, .es-footer-body ol li, .es-footer-body a { font-size:16px!important } .es-infoblock p, .es-infoblock ul li, .es-infoblock ol li, .es-infoblock a { font-size:12px!important } *[class="gmail-fix"] { display:none!important } .es-m-txt-c, .es-m-txt-c h1, .es-m-txt-c h2, .es-m-txt-c h3 { text-align:center!important } .es-m-txt-r, .es-m-txt-r h1, .es-m-txt-r h2, .es-m-txt-r h3 { text-align:right!important } .es-m-txt-l, .es-m-txt-l h1, .es-m-txt-l h2, .es-m-txt-l h3 { text-align:left!important } .es-m-txt-r img, .es-m-txt-c img, .es-m-txt-l img { display:inline!important } .es-button-border { display:block!important } .es-btn-fw { border-width:10px 0px!important; text-align:center!important } .es-adaptive table, .es-btn-fw, .es-btn-fw-brdr, .es-left, .es-right { width:100%!important } .es-content table, .es-header table, .es-footer table, .es-content, .es-footer, .es-header { width:100%!important; max-width:600px!important } .es-adapt-td { display:block!important; width:100%!important } .adapt-img { width:100%!important; height:auto!important } .es-m-p0 { padding:0!important } .es-m-p0r { padding-right:0!important } .es-m-p0l { padding-left:0!important } .es-m-p0t { padding-top:0!important } .es-m-p0b { padding-bottom:0!important } .es-m-p20b { padding-bottom:20px!important } .es-mobile-hidden, .es-hidden { display:none!important } tr.es-desk-hidden, td.es-desk-hidden, table.es-desk-hidden { width:auto!important; overflow:visible!important; float:none!important; max-height:inherit!important; line-height:inherit!important } tr.es-desk-hidden { display:table-row!important } table.es-desk-hidden { display:table!important } td.es-desk-menu-hidden { display:table-cell!important } .es-menu td { width:1%!important } table.es-table-not-adapt, .esd-block-html table { width:auto!important } table.es-social { display:inline-block!important } table.es-social td { display:inline-block!important } a.es-button, button.es-button { font-size:20px!important; display:block!important; border-left-width:0px!important; border-right-width:0px!important } .es-m-p5 { padding:5px!important } .es-m-p5t { padding-top:5px!important } .es-m-p5b { padding-bottom:5px!important } .es-m-p5r { padding-right:5px!important } .es-m-p5l { padding-left:5px!important } .es-m-p10 { padding:10px!important } .es-m-p10t { padding-top:10px!important } .es-m-p10b { padding-bottom:10px!important } .es-m-p10r { padding-right:10px!important } .es-m-p10l { padding-left:10px!important } .es-m-p15 { padding:15px!important } .es-m-p15t { padding-top:15px!important } .es-m-p15b { padding-bottom:15px!important } .es-m-p15r { padding-right:15px!important } .es-m-p15l { padding-left:15px!important } .es-m-p20 { padding:20px!important } .es-m-p20t { padding-top:20px!important } .es-m-p20r { padding-right:20px!important } .es-m-p20l { padding-left:20px!important } .es-m-p25 { padding:25px!important } .es-m-p25t { padding-top:25px!important } .es-m-p25b { padding-bottom:25px!important } .es-m-p25r { padding-right:25px!important } .es-m-p25l { padding-left:25px!important } .es-m-p30 { padding:30px!important } .es-m-p30t { padding-top:30px!important } .es-m-p30b { padding-bottom:30px!important } .es-m-p30r { padding-right:30px!important } .es-m-p30l { padding-left:30px!important } .es-m-p35 { padding:35px!important } .es-m-p35t { padding-top:35px!important } .es-m-p35b { padding-bottom:35px!important } .es-m-p35r { padding-right:35px!important } .es-m-p35l { padding-left:35px!important } .es-m-p40 { padding:40px!important } .es-m-p40t { padding-top:40px!important } .es-m-p40b { padding-bottom:40px!important } .es-m-p40r { padding-right:40px!important } .es-m-p40l { padding-left:40px!important } }
</style>
 </head>
 <body style="width:100%;font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';-webkit-text-size-adjust:100%;-ms-text-size-adjust:100%;padding:0;Margin:0">
  <div class="es-wrapper-color" style="background-color:#F6F6F6">
   <!--[if gte mso 9]>
			<v:background xmlns:v="urn:schemas-microsoft-com:vml" fill="t">
				<v:fill type="tile" color="#f6f6f6"></v:fill>
			</v:background>
		<![endif]-->
   <table class="es-wrapper" width="100%" cellspacing="0" cellpadding="0" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px;padding:0;Margin:0;width:100%;height:100%;background-repeat:repeat;background-position:center top">
     <tr style="border-collapse:collapse">
      <td valign="top" style="padding:0;Margin:0">
       <table cellpadding="0" cellspacing="0" class="es-header" align="center" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px;table-layout:fixed !important;width:100%;background-color:transparent;background-repeat:repeat;background-position:center top">
         <tr style="border-collapse:collapse">
          <td align="center" style="padding:0;Margin:0">
           <table bgcolor="#ffffff" class="es-header-body" align="center" cellpadding="0" cellspacing="0" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px;background-color:#FFFFFF;width:600px">
             <tr style="border-collapse:collapse">
              <td align="left" style="Margin:0;padding-bottom:10px;padding-top:20px;padding-left:20px;padding-right:20px">
               <table cellpadding="0" cellspacing="0" width="100%" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px">
                 <tr style="border-collapse:collapse">
                  <td class="es-m-p0r" valign="top" align="center" style="padding:0;Margin:0;width:560px">
                   <table cellpadding="0" cellspacing="0" width="100%" role="presentation" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px">
                     <tr style="border-collapse:collapse">
                      <td align="center" style="padding:0;Margin:0;font-size:0px"><a target="_blank" href="https://viewstripo.email" style="-webkit-text-size-adjust:none;-ms-text-size-adjust:none;mso-line-height-rule:exactly;text-decoration:underline;color:#134F5C;font-size:14px"><img src="https://lpvxgg.stripocdn.email/content/guids/CABINET_cf24f191d128a6f1c601418ab4345dc5/images/78051628855364647.png" alt="Logo" style="display:block;border:0;outline:none;text-decoration:none;-ms-interpolation-mode:bicubic" width="150" title="Logo"></a></td>
                     </tr>
                   </table></td>
                 </tr>
               </table></td>
             </tr>
           </table></td>
         </tr>
       </table>
       <table class="es-content" cellspacing="0" cellpadding="0" align="center" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px;table-layout:fixed !important;width:100%">
         <tr style="border-collapse:collapse">
          <td align="center" style="padding:0;Margin:0">
           <table class="es-content-body" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px;background-color:#dee2e6;width:600px" cellspacing="0" cellpadding="0" align="center" bgcolor="#dee2e6">
             <tr style="border-collapse:collapse">
              <td align="left" style="padding:0;Margin:0">
               <table cellpadding="0" cellspacing="0" width="100%" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px">
                 <tr style="border-collapse:collapse">
                  <td align="center" valign="top" style="padding:0;Margin:0;width:600px">
                   <table cellpadding="0" cellspacing="0" width="100%" role="presentation" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px">
                     <tr style="border-collapse:collapse">
                      <td align="center" style="padding:0;Margin:0;font-size:0px"><img class="adapt-img" src="https://lpvxgg.stripocdn.email/content/guids/CABINET_40cd21c53de7b0c0f5da0e20308d4feb/images/32991610120251547.png" alt style="display:block;border:0;outline:none;text-decoration:none;-ms-interpolation-mode:bicubic" width="600"></td>
                     </tr>
                   </table></td>
                 </tr>
               </table></td>
             </tr>
             <tr style="border-collapse:collapse">
              <td align="left" style="padding:5px;Margin:0">
               <table cellpadding="0" cellspacing="0" width="100%" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px">
                 <tr style="border-collapse:collapse">
                  <td align="left" style="padding:0;Margin:0;width:590px">
                   <table cellpadding="0" cellspacing="0" width="100%" role="presentation" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px">
                     <tr style="border-collapse:collapse">
                      <td align="left" class="es-m-p20l es-m-txt-l" style="padding:0;Margin:0;padding-top:10px"><h1 style="Margin:0;line-height:30px;mso-line-height-rule:exactly;font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';font-size:30px;font-style:normal;font-weight:normal;color:#333333" class="b_title">Hello,</h1></td>
                     </tr>
                     <tr style="border-collapse:collapse">
                      <td align="left" class="es-m-p20l" style="padding:0;Margin:0;padding-top:10px;padding-bottom:10px"><p style="Margin:0;-webkit-text-size-adjust:none;-ms-text-size-adjust:none;mso-line-height-rule:exactly;font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';line-height:17px;color:#333333;font-size:14px" class="b_description"><br>Welcome to Amazon Pinpoint, this is your first email!</p></td>
                     </tr>
                     <tr style="border-collapse:collapse">
                      <td align="center" class="es-m-p20l" style="padding:15px;Margin:0"><span class="es-button-border" style="border-style:solid;border-color:#ff9900;background:#ff9900;border-width:2px;display:inline-block;border-radius:0px;width:auto"><a href="https://aws.amazon.com/pinpoint/" class="es-button es-button-1" target="_blank" style="mso-style-priority:100 !important;text-decoration:none;-webkit-text-size-adjust:none;-ms-text-size-adjust:none;mso-line-height-rule:exactly;color:#0f0e0e;font-size:18px;border-style:solid;border-color:#ff9900;border-width:10px 35px;display:inline-block;background:#ff9900;border-radius:0px;font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';font-weight:normal;font-style:normal;line-height:22px;width:auto;text-align:center">Visit us</a></span></td>
                     </tr>
                   </table></td>
                 </tr>
               </table></td>
             </tr>
             <tr style="border-collapse:collapse">
              <td align="left" style="padding:0;Margin:0">
               <table cellpadding="0" cellspacing="0" width="100%" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px">
                 <tr style="border-collapse:collapse">
                  <td align="center" valign="top" style="padding:0;Margin:0;width:600px">
                   <table cellpadding="0" cellspacing="0" width="100%" role="presentation" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px">
                     <tr style="border-collapse:collapse">
                      <td align="center" style="padding:0;Margin:0;font-size:0px"><img class="adapt-img" src="https://lpvxgg.stripocdn.email/content/guids/CABINET_40cd21c53de7b0c0f5da0e20308d4feb/images/46751610120197559.png" alt style="display:block;border:0;outline:none;text-decoration:none;-ms-interpolation-mode:bicubic" width="600"></td>
                     </tr>
                     <tr style="border-collapse:collapse">
                      <td align="center" style="padding:20px;Margin:0;font-size:0" bgcolor="#ffffff">
                       <table border="0" width="100%" height="100%" cellpadding="0" cellspacing="0" role="presentation" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px">
                         <tr style="border-collapse:collapse">
                          <td style="padding:0;Margin:0;border-bottom:0px solid #cccccc;background:none;height:1px;width:100%;margin:0px"></td>
                         </tr>
                       </table></td>
                     </tr>
                   </table></td>
                 </tr>
               </table></td>
             </tr>
           </table></td>
         </tr>
       </table>
       <table cellpadding="0" cellspacing="0" class="es-footer" align="center" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px;table-layout:fixed !important;width:100%;background-color:transparent;background-repeat:repeat;background-position:center top">
         <tr style="border-collapse:collapse">
          <td align="center" style="padding:0;Margin:0">
           <table bgcolor="#ffffff" class="es-footer-body" align="center" cellpadding="0" cellspacing="0" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px;background-color:#FFFFFF;width:600px">
             <tr style="border-collapse:collapse">
              <td align="left" bgcolor="#dee2e6" style="padding:10px;Margin:0;background-color:#dee2e6">
               <table cellpadding="0" cellspacing="0" width="100%" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px">
                 <tr style="border-collapse:collapse">
                  <td align="left" style="padding:0;Margin:0;width:580px">
                   <table cellpadding="0" cellspacing="0" width="100%" role="presentation" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px">
                     <tr style="border-collapse:collapse">
                      <td align="center" style="padding:0;Margin:0;font-size:0">
                       <table cellpadding="0" cellspacing="0" class="es-table-not-adapt es-social" role="presentation" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px">
                         <tr style="border-collapse:collapse">
                          <td align="center" valign="top" style="padding:0;Margin:0;padding-right:10px"><img title="Facebook" src="https://lpvxgg.stripocdn.email/content/assets/img/social-icons/square-black-bordered/facebook-square-black-bordered.png" alt="Fb" width="32" style="display:block;border:0;outline:none;text-decoration:none;-ms-interpolation-mode:bicubic;font-size:12px"></td>
                          <td align="center" valign="top" style="padding:0;Margin:0;padding-right:10px"><img title="Twitter" src="https://lpvxgg.stripocdn.email/content/assets/img/social-icons/square-black-bordered/twitter-square-black-bordered.png" alt="Tw" width="32" style="display:block;border:0;outline:none;text-decoration:none;-ms-interpolation-mode:bicubic;font-size:12px"></td>
                          <td align="center" valign="top" style="padding:0;Margin:0;padding-right:10px"><img title="Instagram" src="https://lpvxgg.stripocdn.email/content/assets/img/social-icons/square-black-bordered/instagram-square-black-bordered.png" alt="Inst" width="32" style="display:block;border:0;outline:none;text-decoration:none;-ms-interpolation-mode:bicubic;font-size:12px"></td>
                          <td align="center" valign="top" style="padding:0;Margin:0"><img title="Youtube" src="https://lpvxgg.stripocdn.email/content/assets/img/social-icons/square-black-bordered/youtube-square-black-bordered.png" alt="Yt" width="32" style="display:block;border:0;outline:none;text-decoration:none;-ms-interpolation-mode:bicubic;font-size:12px"></td>
                         </tr>
                       </table></td>
                     </tr>
                   </table></td>
                 </tr>
               </table></td>
             </tr>
           </table></td>
         </tr>
       </table>
       <table cellpadding="0" cellspacing="0" class="es-content" align="center" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px;table-layout:fixed !important;width:100%">
         <tr style="border-collapse:collapse">
          <td class="es-info-area" align="center" style="padding:0;Margin:0">
           <table class="es-content-body" align="center" cellpadding="0" cellspacing="0" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px;background-color:transparent;width:600px" bgcolor="#FFFFFF">
             <tr style="border-collapse:collapse">
              <td align="left" style="Margin:0;padding-left:20px;padding-right:20px;padding-top:25px;padding-bottom:25px">
               <table cellpadding="0" cellspacing="0" width="100%" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px">
                 <tr style="border-collapse:collapse">
                  <td align="center" valign="top" style="padding:0;Margin:0;width:560px">
                   <table cellpadding="0" cellspacing="0" width="100%" role="presentation" style="mso-table-lspace:0pt;mso-table-rspace:0pt;border-collapse:collapse;border-spacing:0px">
                     <tr style="border-collapse:collapse">
                      <td align="center" class="es-infoblock" style="padding:0;Margin:0;line-height:14px;font-size:12px;color:#CCCCCC"><p style="Margin:0;-webkit-text-size-adjust:none;-ms-text-size-adjust:none;mso-line-height-rule:exactly;font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';line-height:14px;color:#CCCCCC;font-size:12px">Amazon Web Services, Inc. is a subsidiary of Amazon.com, Inc. Amazon.com is a registered trademark of Amazon.com. This message was produced and distributed by Amazon Web Services, Inc. and its affiliates, 410 Terry Ave. North, Seattle, WA 98109.<br><br><a target="_blank" href="" style="-webkit-text-size-adjust:none;-ms-text-size-adjust:none;mso-line-height-rule:exactly;text-decoration:underline;color:#CCCCCC;font-size:12px">Privacy police</a> |<a target="_blank" href="" style="-webkit-text-size-adjust:none;-ms-text-size-adjust:none;mso-line-height-rule:exactly;text-decoration:underline;color:#CCCCCC;font-size:12px">Unsubscribe</a></p></td>
                     </tr>
                   </table></td>
                 </tr>
               </table></td>
             </tr>
           </table></td>
         </tr>
       </table></td>
     </tr>
   </table>
  </div>
 </body>
</html>
```

では、ここまでできたので、メール送信してみましょう。
`メッセージを送信`ボタンをクリックします。

![](/images/aws-pinpoint-handson-01/2023-08-11-23-03-29.png)

![](/images/aws-pinpoint-handson-01/2023-08-11-23-04-55.png)

ありゃ、また怒られた。。
送信先のメールアドレスを入れ忘れてましたね。
テストなので、先ほど登録したメールアドレスに`+test`とかつけてやってみますか。

![](/images/aws-pinpoint-handson-01/2023-08-11-23-08-13.png)

・・・なんと、エラーになってしまった。
最初の時点ではSandboxモードになっていて、送信先が制限されていることが原因のようです。
とりあえず、今回はハンズオンなので、認証したメールアドレスにして送信してみます。

![](/images/aws-pinpoint-handson-01/2023-08-11-23-13-46.png)

お、どうやらうまく行ったようです。
やっぱり制限されてるということなんですね。

![](/images/aws-pinpoint-handson-01/2023-08-11-23-14-57.png)

無事にメール受信していることを確認しました！

長くなりそうなので、今回はここまでにしたいと思います。
また次回！

