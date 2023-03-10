---
layout: post
title: "Povoでdアカウントのパスワードレス設定が解除できないときの対処法"
date:   2023-02-12 11:00:00 +0900
categories: note
background: '/img/img4articles/2023/2023-02/2023-02-12-d-account_how-to-disable_pwless_on_povo/d-account_titleback.png'
---
ある日突然 **[dアカウント設定]アプリ** の認証が通らなくなり、パスワードレス設定にしていたdアカウントにログインできず詰みかけたので、その際の対処法を備忘録として残しておきます。  
  
cf. 当該のエラー  
![認証エラー](\img\img4articles\2023\2023-02\2023-02-12-d-account_how-to-disable_pwless_on_povo\d-account_auth_error.png){: .img-fluid}  
`[D1100]`  
`エラーが発生しました。`  
`しばらく時間をおいてから、もう一度お試しください。`  
`もしくは、dアカウントを一旦解除し、再度設定をしてください。`  
<small>(※スクショを撮り忘れてしまいましたが、エラーコードが [D5900] のパターンもあった気がします。)</small>  
  
  
～～～～～～～～～～  
**【前提条件】**  
**・Povo2.0の音声通話SIMを使用している。**  
**・その音声通話SIMの電話番号とdアカウントとが紐づいている。**  
**・上記2つの条件下でdアカウント設定アプリの認証をしようとすると、エラーが発生して認証ができない状態。**  
  
先に結論から言ってしまうと、タイトルにも入れた通り **PovoのSIMが悪さ** をしているようでした。  
  
<small>ーーーーーーーーーー</small>  
<small>`"色々やってみて分かったこと。povoのSIMではエラーが出る。`</small>  
<small>`(中略)`</small>  
<small>`dアカウント設定アプリで認証が通らない（D5900送信できませんでした）"`</small>  
<small></small>  
<small>cf. 『povoではd払い（dアカウント）が使えない模様・・・orz | SKILLS OF LIFE 3』</small>  
<small>https://pandaignis.com/wp/66952.html </small>  
<small>ーーーーーーーーーー</small>  
<small>↑類似例</small>  
  
そのため、SIMを抜いてしまえば万事解決(のはず)ですが、認証フロー上SMSを受信する必要があるため、今から紹介する方法では **スマホがもう一台必要** となります。  
持ってない方は友達のスマホに一瞬PovoSIMを入れさせてもらうか、中古で適当な端末を漁るか、あるいは頑張ってSMSを受信してください。(ごめんね。)
  
手順としては、以下の通りとなります。  
<small>(※ワンタイムパスワードの発行手順やパスワードレス設定の解除手順については、共通手順につき割愛します。)</small>  
  
**①SIMを抜いたスマホ(以下、SIM抜きスマホ)とPovoのSIMの入ったスマホ(以下、Povoスマホ)を用意する。**  
**②SIM抜きスマホに [dアカウント設定]アプリ を入れて、当該のアカウントでログインする。**  
**③Povoスマホにワンタイムパスワードの書かれたSMSが届くので、そのパスワードを使ってSIM抜きスマホ側で認証を通す。**  
**④SIM抜きスマホ側で認証が通る<small>(はず)</small>ので、パスワードレス設定を解除する。**  
  
ちなみに手順完了後、認証の通った状態のSIM抜きスマホに改めてPovoのSIMを挿すと、SIMカードの変更を検知して認証が解除されるので、常用はできない様子でした。  
  
cf. 再認証を求められる様子  
![要再認証](\img\img4articles\2023\2023-02\2023-02-12-d-account_how-to-disable_pwless_on_povo\d-account_need-to-reauth.png){: .img-fluid}  
  
ただ、パスワードレス設定を使わないのであれば、 **[dアカウント設定]アプリ** は必要ないはずなので、このまま削除してしまえば完了です。  
  
以上、備忘録でした。  
  
～～～～～～～～～～  
【追伸】  
そもそもPovoユーザの私がなぜdアカウントを使っているかというと、それはドコモ時代に契約したドコモ光がまだ残っているからです。  
ただ、キャリアに依存すると今回のようにキャリアから出たときにドツボにハマる可能性が高いので、次の更新時期に別回線に乗り換えようかなぁ…と、ふとMy docomoからドコモ光の契約状況を確認しようとしたところ…。  
  
![パスワードレス設定の有効化が必要](\img\img4articles\2023\2023-02\2023-02-12-d-account_how-to-disable_pwless_on_povo\d-account_need-to-enable_pwless.png){: .img-fluid}  
<font color="red"><b>「セ　キ　ュ　リ　テ　ィ　強　化　の　た　め　、　現　在　の　ア　カ　ウ　ン　ト　設　定　で　は　本　サ　ー　ビ　ス　を　ご　利　用　い　た　だ　け　ま　せ　ん　。」</b></font>  
  
正体はコイツ。  
  
<small>ーーーーーーーーーー</small>  
<small>`"ドコモオンライン手続きでは、2022年8月10日（水曜）より、セキュリティ強化のためログイン方法が以下のとおり一部変更となります。お手続きの際にログインできない場合ご一読ください。`</small>  
<small>`「dアカウントとパスワードによるログイン」ではなくなり、「ネットワーク暗証番号を入力してログイン」または`</small><small>**`「パスワードレス認証によるログイン」`**</small><small>`が必須となります。※一部を除きます。詳細は下記をご覧ください。"`</small>  
<small></small>  
<small>cf. 『【重要】ドコモオンライン手続きにログインできない場合ご一読ください | My docomo | NTTドコモ』</small>  
<small>https://www.docomo.ne.jp/mydocomo/info/detail/221007_1.html</small>  
<small>ーーーーーーーーーー</small>  
  
端的に言うと、  
  
**「(非ドコモユーザが)My docomoからオンラインで手続きしたかったら、パスワードレス設定を有効にしてね。」**  
  
とのお達し。  
  
![寝言は寝てから言おう!](\img\img4articles\2023\2023-02\2023-02-12-d-account_how-to-disable_pwless_on_povo\d-account_are-you-kidding-me.png){: .img-fluid}  
だから、それができないというのが今回の話でして…。  
  
  
改めて、お古のスマホが生きているうちにさっさと違約金払ってでも解約しておこうかなと思った次第でした。  
<small>(ちなみに契約満了月までにはまだ1年ほどありました…。違約金分くらいのキャッシュバックやってるところないかなぁ…?)</small>
