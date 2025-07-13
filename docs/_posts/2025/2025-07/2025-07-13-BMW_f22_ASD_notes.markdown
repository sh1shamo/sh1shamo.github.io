---
layout: post
title: "【BMW M235i (F22)】 ASD のコーディングについて"
date:   2025-07-13 00:00:00 +0900
categories: car
background: ''
---
いろいろあって ASD のコーディング内容を弄ろうと思ったので備忘録としてメモしておきます。  
というのも、 ASD については値を初期値から変更すると ASD 自体が動作しなくなる項目があり、どこが変更可能かというのが結構重要になります。  
  
こうなった経緯として、下記海外フォーラムのポストを見る限り、昔 (2014 ～ 2015 年頃)  は何でも変えられたらしく、 ASD の音だけ M3 / M4 にしたりと結構やりたい放題できたようです。  
ただ、それ以降にリリースされたファームウェアでは対策されたようで、今は例えば "Engine" という ASD が発生させるエンジン音に関わる設定項目の値を変えると ASD 自体が機能しなくなったりするので、今回どこかが変更可能か? というのを整理した次第です。  
    
> --- 抜粋 ---  
> you have to return ASD software to I-Level F020-14-11-502. If your ASD have HWEL_00000F94_003_003_000, you may copy appended (I-Level F020-14-11-502) files swfl_000021d4.bin.001_009_001 swfl_000021d4.bsw.001_009_001 swfl_000021d4.xml.001_009_001 to your "FULL !!!!" psdzdata\swe\swfl directory and use E-EYS with Tal_ASD.xml and Svt_soll_ASD.xml and program it. All coding options should be functional. You can compare size of your SWFL_00003846_xxx_xxx_xxx vs swfl_000021d4_001_009_001  
> --- 抜粋 ---  
   
URL: [https://www.2addicts.com/forums/showpost.php?p=20873743&postcount=2](https://www.2addicts.com/forums/showpost.php?p=20873743&postcount=2)  
   
## 車体  
BMW M235i (F22)  
VIN からデコードした限り、 2015/9 製造らしい。  
  
## i-Step バージョン / ASD モジュールのバージョン
・i-Step: `F020-16-03-502`  
・ASD: 色々あってよくわからないのでとりあえず BimmerUtility に表示されたものをべた張り。  
  
--- 抜粋 ---  
`BTLD-0000111C-002.000.001` - Bootloader ASD  
`CAFD-00000F9B-001.022.000` - CODIERDATEN  
`HWEL-00000F94-003.003.000` - Hardware ASD  
`SWFL-0000111D-002.007.006` - Applikation MC  
`SWFL-00003846-001.004.000` - Applikation Datenstand LK F2x  
--- 抜粋 ---  
  
## コーディング項目と変更可否 (+ コメント)

| 項目名                | 変更可能? (Changeable?) | 初期値 (Default value)  | 項目の概要                                                                | コメント                                                                                                                                                                                              |
|--------------------|---------------------|----------------------|----------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Audio Level        | yes                 | Stereo               | 音質のモードか何か。車載のオーディオ毎に初期値が異なる。例えばオプションの Harman / Kardon なら　"Brended Hifi" らしい (<span style="color: red;">*1</span>) | 純正 (Stock) のオーディオだとこの項目を変更すると音量が小さくなったので、あまり変えないほうが良さそう。                                                                                                                                          |
| Competition Paket  | no                  | No                   | Competition 仕様の車両向けの項目 ?                                             | 海外フォーラムでは排気音が大きい Competitition 仕様の車両向けに ASD の音量を抑えているように感じるというポストが見られたが、今回の検証では ASD が無効化された。 (<span style="color: red;">*2</span>)                                                                                                 |
| Construction Stage | yes                 | later or equal 07/13 | 車両の製造時期別の細かい調整 ?                                                     | 生産時期によって微妙に ASD を変えているらしい。選択肢が多すぎて未検証。 (<span style="color: red;">*3</span>)                                                                                                                                                       |
| Country Variant    | yes                 | ECE                  | 仕向け国向けごとに音を変えていると噂されているパラメーター。                                       | 差異の有無については要検証。                                                                                                                                                                                    |
| Engine             | no                  | N55B30               | ASD で発生させるエンジン音。 "Model Range" とセットでの設定が必要か?                         |                                                                                                                                                                                                   |
| Model Range        | no                  | F22 with N55         | 上に同じ                                                                 |                                                                                                                                                                                                   |
| Power Class        | yes                 | 0L                   | ASD の音量。　← [小] UL / KL / ML / OL / SL / TL [大] → らしい。                | 各項目の Werte (独: "値" の意) について、最も小さいとされる "UL" の '0' から最も大きい "TL" の '5' まで 1 ずつ値が大きくなっており、値は音量レベルを表している可能性がある。ただ、そうなるとこれら "*L" シリーズとは別で "Hybrid" という項目があり、こちらの Werte は '6' なのでこれが最も最大ということになるのか? 要検証。 |
  
[注釈]  
<span style="color: red;">*1</span>: [https://minkara.carview.co.jp/userid/2318519/blog/46580351/](https://minkara.carview.co.jp/userid/2318519/blog/46580351/)  
  
> --- 抜粋 ---  
> ところが、ハーマンカードン搭載車両の初期設定は  
> 以下の2項目が違います。  
> Audio Level　Branded HiFi  
> Power Class　最大  
> --- 抜粋 ---  
  
<span style="color: red;">*2</span>: [https://f30.bimmerpost.com/forums/showpost.php?p=24343598&postcount=2](https://f30.bimmerpost.com/forums/showpost.php?p=24343598&postcount=2)  
  
> --- 抜粋 ---  
> if you set "Competition Paket" to on the sound inside the cabin is less and a slightly different tone. I expect this is because the competition pack is louder on the outside so inside noise needs to be adjusted.  
> --- 抜粋 ---  
  
<span style="color: red;">*3</span>: [https://f10.m5post.com/forums/showpost.php?p=21131384&postcount=1](https://f10.m5post.com/forums/showpost.php?p=21131384&postcount=1)
    
> --- 抜粋 ---  
> Construction stage. Again there are quite a few dates to choose from and they all have differing sound, some subtle, some not. This is probably BMW making tweaks as the cars developed..  
> --- 抜粋 ---  