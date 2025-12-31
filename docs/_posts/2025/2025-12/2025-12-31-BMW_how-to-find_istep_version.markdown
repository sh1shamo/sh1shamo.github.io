---
layout: post
title: "【BMW】 i-Step のバージョンを確かめる"
date:   2025-12-31 00:00:00 +0900
categories: car
background: ''
---

## やりたいこと<br>
i-Step のバージョンを確認したい。<br>
<br>
<font size="2"><font color="green">// 背景<br>
E-Sys と BimmerUtility で見たときとで i-Step のバージョンが違うため、一旦別の方法でどちらが正しいバージョンかを確かめたかった。</font></font><br>
<br>
▼ BimmerUtility<br>
<br>
![BimmerUtility で見たときの i-Step バージョン](\img\img4articles\2025\2025-12\2025-12-31-BMW_how-to-find_istep_version\i-Step_BU.png){: .img-fluid}<br>
<br>  
▼ E-Sys<br>
<br>
![E-Sys で見たときの i-Step バージョン](\img\img4articles\2025\2025-12\2025-12-31-BMW_how-to-find_istep_version\i-Step_E-Sys.png){: .img-fluid}<br>
<br>
## 解決策<br>
iDrive のメニューから個人設定を USB メモリにエクスポートすると、エクスポートされたファイル内に i-Step のバージョンが記録されるため、そこから確認することができました。<br>
<br>
<font size="2"><font color="green">// 出力ファイル<br>
[(ドライブレター):\BMWData\MobileProfile\(プロファイル名).mpd]　として出力されます。</font></font><br>
<br>
任意のテキスト エディターなどで開くことで内容が確認できます。ちなみに以下のとおり、 BimmerUtility が正しかったです。 (`F020-16-03-502`)<br>
<br>
▼ ファイル内容<br>
```
<?xml version="1.0" encoding="utf-8"?>
<bmwExportData>
<signedContent>
<header>
  <date>2025-12-31T15:43:44</date>
  <version>1</version>
  <username><プロファイル名></username>
  <vin><車台番号末尾 7 桁></vin>
  <i-step>F020-16-03-502</i-step>
</header>
(以下略)
```
<br>
## 参考情報<br> 
<br>
以下のコミュニティ投稿を参考にしました。<br>
<br>
タイトル: How-to: Find out your ISTEP version (guide)<br>
URL: [https://f87.bimmerpost.com/forums/showthread.php?t=1638904](https://f87.bimmerpost.com/forums/showthread.php?t=1638904)<br>