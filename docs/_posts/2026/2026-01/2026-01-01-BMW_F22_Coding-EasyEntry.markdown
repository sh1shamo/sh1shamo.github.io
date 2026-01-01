---
layout: post
title: "【BMW M235i (F22)】 イージー エントリー (Easy Entry) 機能をコーディングで有効化する"
date:   2026-01-01 00:00:00 +0900
categories: car
background: ''
---

## やりたいこと<br>
<br>
F22 型の M235i でイージーエントリー (Easy Entry) 機能をコーディングで有効化する。<br>
<br>
<font size="2"><font color="green">// イージーエントリー (Easy Entry) 機能 = 乗り降りしやすいように IG OFF でドアを開けるとシートが後退する機能</font></font><br>
<br>
## コーディングする項目<br>
<br>
以下の 3 箇所<br>
<br>
※ SM2 は運転席と助手席の 2 つありますが、今回は運転席の方です。<br>
(NCD ファイル名だと `CAFD_000000B5_012_004_029.ncd` の方。)<br>
<br>
▼ コーディング箇所・説明など<br>
```
[コーディング箇所]
1: SM2 / 3000 SM_GLOBAL / EINAUSSTIEGSHILFE
2: SM2 / 3012 EAH / EAH_SCHUTZFREIRAUM_HINTEN_SLV_PHYS
3: SM2 / 3012 EAH / EAH_VERFAHRWEG_SLV_PHYS

[項目の意味]
1: 機能の有効 / 無効 (初期値: nicht_aktiv)
2: 後退限度として設定するシートレール後端からの距離 (初期値: 0x64 = 100 mm)
3: 後退距離 (初期値: 0x3C = 60 mm)

[設定した値]
1: Modus_FA_SLV
2: 0x32
3: 0xFF
```
<br>
## 備考<br>
<br>
2 と 3 の値は 2 が優先される様子。なので、 3 に適当にデタラメな大きい値を入れて、 2 で後部座席用に確保するスペースを調整するのが良さそう。<br>
<br>
## 設定後の動作<br>
IG ON の状態で運転時のポジションに設定しておくと、 IG OFF してドアを開けたタイミングで設定した値までシートが後退する。<br>
キーが車外にあるとドアを閉めても後退した位置のまま。キーが車内にあるとドアを閉めると再度運転時のポジションに戻る。<br>
一度シートが元の運転時のポジションまで戻ると、再度後退動作が有効になるには、一度 IG ON → IG OFF を行わないといけなさそう。<br>
<br>
## 参考元<br>
<br>
以下のサイトを参考にしました。<br>
<br>
[https://minkara.carview.co.jp/userid/1004397/car/2941070/5904420/note.aspx](https://minkara.carview.co.jp/userid/1004397/car/2941070/5904420/note.aspx)<br>
[https://minkara.carview.co.jp/userid/458038/blog/43135497/](https://minkara.carview.co.jp/userid/458038/blog/43135497/)
[https://minkara.carview.co.jp/userid/2454953/car/2925166/5839981/note.aspx](https://minkara.carview.co.jp/userid/2454953/car/2925166/5839981/note.aspx)