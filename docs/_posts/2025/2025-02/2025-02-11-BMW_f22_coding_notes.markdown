---
layout: post
title: "【BMW M235i (F22)】コーディング備忘録"
date:   2025-02-11 00:00:00 +0900
categories: car
background: ''
---
備忘録がてら現在のコーディング内容を紹介します。  
  
<font size="2"><font color="green">// いくつかのコーディングは個別記事にしています。</font></font>  
  
▼ ASD (Active Sound Design; スピーカー出力の疑似排気音) 関連  
[【BMW M235i (F22)】 ASD のコーディングについて](https://sh1shamo.github.io/car/2025/07/12/BMW_f22_ASD_notes.html)  
  
▼ イージー エントリー関連  
[【BMW M235i (F22)】 イージー エントリー (Easy Entry) 機能をコーディングで有効化する](https://sh1shamo.github.io/car/2025/12/31/BMW_F22_Coding-EasyEntry.html)  
  
## 車体  
BMW M235i (F22)  
VIN からデコードした限り、 2015/9 製造らしい。  
  
## i-Step バージョン  
F020-16-03-502  
  
## コーディング内容
  
#### [GPS 時刻同期]  
```
<コーディング項目>  
1: HU_NBT2 / 3000 HMI / CLOCK_CHANGE_AUTOMATIC
2: HU_NBT2 / 3000 HMI / SETTINGS_TIME_AUTOMATIC

<設定値>  
1: aktiv
2: navigation
```
  
#### [iDrive 起動ロゴ M Performance 化]  
```
<コーディング項目>
HU_NBT2 / 3001 EXBOX / STARTUP_EMBLEM

<設定値>
variant_01
```
  
#### [US サイドマーカー]  
```
<コーディング項目>
1: FEM_BODY / 3063 LceLampMapping2 / MAPPING_SIDEMARKER_L_OUTPUT
2: FEM_BODY / 3063 LceLampMapping2 / MAPPING_SIDEMARKER_R_OUTPUT
3: FEM_BODY / 3063 LceLampMapping2 / MAPPING_SIDEMARKER_L_PWM_LEVEL_STANDARD
4: FEM_BODY / 3063 LceLampMapping2 / MAPPING_SIDEMARKER_R_PWM_LEVEL_STANDARD

<設定値>
1: fra_v_l
2: fra_v_r
3: 8.2V
4: 8.2V

<備考>
1 ～ 2 が機能の有効化、 3 ～ 4 は減光のための電圧設定。
電圧について、ウインカーバルブが電球のままの場合は最低でも 8.2 V ～ 9.0 V が必要? (そのあたりの電圧にしている設定例がよく見られた。)
LED バルブであれば最低の 6.0 V にするくらいが明るさ的にはちょうどいい。
```
  
#### [アイドリング ストップ デフォルト無効化]  
```
<コーディング項目>
FEM_BODY / 3023 TcMaster2 / TCM_MSA_DEFAULT_OFF

<設定値>
aktiv
```
  
#### [イージーエントリー (運転席側)]  
```
<コーディング項目>
1: SM2 / 3000 SM_GLOBAL / EINAUSSTIEGSHILFE
2: SM2 / 3012 EAH / EAH_SCHUTZFREIRAUM_HINTEN_SLV_PHYS
3: SM2 / 3012 EAH / EAH_VERFAHRWEG_SLV_PHYS

<設定値>
1: Modus_FA_SLV
2: 0x0, 0x32
3: 0x0, 0xFF

<備考>
詳細は個別記事参照。
```
  
#### [ウェルカムライト (フロント; 徐々に点灯, 眉毛消灯)]  
```
<コーディング項目>
1: FEM_BODY / 3062 LceLampMapping1 / MAPPING_STANDL_V_L_PART_OF_WL
2: FEM_BODY / 3062 LceLampMapping1 / MAPPING_STANDL_V_R_PART_OF_WL
3: FEM_BODY / 3062 LceLampMapping1 / MAPPING_DESIGNL_L_PART_OF_WL
4: FEM_BODY / 3062 LceLampMapping1 / MAPPING_DESIGNL_R_PART_OF_WL

<設定値>
1: soft_on
2: soft_on
3: not_active
4: not_active

<備考>
それぞれ 1 ～ 2 がリング部分、 3 ～ 4 が眉毛部分。
前者は 'hard_on' (普通の点灯) から 'soft_on' (徐々に明るくなる点灯) に変更。後者は not_active で非点灯に変更。
```
  
#### [ウェルカムライト (リア; 徐々に点灯)]  
```
<コーディング項目>
1: REM / 3062 LceLampMapping1 / MAPPING_KENNZEICHENL_PART_OF_WL
2: REM / 3062 LceLampMapping1 / MAPPING_STANDL_H1_L_PART_OF_WL
3: REM / 3062 LceLampMapping1 / MAPPING_STANDL_H1_R_PART_OF_WL
4: REM / 3062 LceLampMapping1 / MAPPING_STANDL_H2_L_PART_OF_WL
5: REM / 3062 LceLampMapping1 / MAPPING_STANDL_H2_R_PART_OF_WL
6: REM / 3062 LceLampMapping1 / MAPPING_UNIVERSAL_1_PART_OF_WL

<設定値>
1: soft_on
2: soft_on
3: soft_on
4: soft_on
5: soft_on
6: soft_on

<備考>
2 ～ 5 がリアライト。
1 は項目名的にナンバープレート灯だが実際はナンバープレート灯の制御は 6 の設定で変化する。
(そのため、最低限 2 ～ 6 の設定で事足りるが 1 も念のため設定している。)
いずれも 'soft_on' で徐々に点灯。
```
  
#### [クルーズ・コントロール 最低速度]  
```
<コーディング項目>
ICM / 3000 Daten / C_Wunschgeschw_min_kmh

<設定値>
0x05
```
  
#### [スポーツ表示 M 化]  
```
<コーディング項目>
HU_NBT2 / 3000 HMI / M_VEHICLE

<設定値>
aktiv
```
  
#### [スモールライト / ヘッドライト (眉毛消灯)]  
```
<コーディング項目>
1: FEM_BODY / 3063 LceLampMapping2 / MAPPING_DESIGNL_L_FUNCTION
2: FEM_BODY / 3063 LceLampMapping2 / MAPPING_DESIGNL_R_FUNCTION

<設定値>
1: 00
2: 00

<備考>
'01' → '00' で消灯
```
  
#### [デイライト (フロント; 眉毛消灯)]  
```
<コーディング項目>
1: FEM_BODY / 3060 LceMaster / TFL_MODUS
2: FEM_BODY / 3063 LceLampMapping2 / MAPPING_UNIVERSAL_1_OUTPUT
3: FEM_BODY / 3063 LceLampMapping2 / MAPPING_UNIVERSAL_2_OUTPUT

<設定値>
1: tfl_s
2: off
3: off

<備考>
1 だけだと眉毛も点灯。
```
  
#### [デイライト (リア)]  
```
<コーディング項目>
1: REM / 3062 LceLampMapping1 / MAPPING_TAGFAHRL_H_L_OUTPUT
2: REM / 3062 LceLampMapping1 / MAPPING_TAGFAHRL_H_R_OUTPUT

<設定値>
1: sl_l
2: sl_r
```
  
#### [デイライト メニュー追加]  
```
<コーディング項目>
HU_NBT2 / 3000 HMI / DAYDRIVING_LIGHT

<設定値>
standard

<備考>
iDrive にデイライトのオンオフの項目を追加。
```
  
#### [デジタル スピード メーター (BC)]  
```
<コーディング項目>
KOMBI / 3000 Anzeige_Konfiguration / BC_DIGITAL_V

<設定値>
aktiv
```
  
#### [ドアオープン時 iDrive オフ]  
```
<コーディング項目>
FEM_BODY / 3020 TcMaster / TCM_LOGIC_R_OFF_DOOR

<設定値>
aktiv
```
  
#### [レーン・ディパーチャー・ウォーニング 検知対象拡張]  
```
<コーディング項目>
KAFAS2 / 3020 TLC_CODING / ROAD_EDGE_WARNING_ENABLED

<設定値>
detection_for_grass_edge_and_curb_stone

<備考>
白線以外に草や縁石にも反応するようになるらしい。
```
  
#### [レーン・ディパーチャー・ウォーニング 有効化速度]  
```
<コーディング項目>
1: KAFAS2 / 3020 TLC_CODING / THRV_AVAI_TLC_HIGH
2: KAFAS2 / 3020 TLC_CODING / THRV_AVAI_TLC_LOW

<設定値>
1: 0x0A
2: 0x05

<備考>
1 を超えると有効になり、 2 を下回ると無効になる。
値はそれぞれ 16 進数表記。 (それぞれ '10' と '5' )
```
  
#### [ロック時ドアミラー格納]  
```
<コーディング項目>
FEM_BODY / 3053 PwMaster / KOMFORT_SCHLIESSEN

<設定値>
0x05

<備考>
ドアミラー格納までのホールド時間。リモコン キーとコンフォート アクセスとで若干挙動が異なる。

【リモコン キーによるロック】
'00' (= 0.0 秒) のときホールド不要でドアミラー格納。 '05' (= 0.5 秒) のときは要 0.5 秒ホールド。

【コンフォート アクセスによるロック】
'00' のときも気持ち要ホールド。 '05' のときはリモコン キーと同様。
```
  
#### [後退時ドアハンドル点灯]  
```
<コーディング項目>
FEM_BODY / 3070 LciMaster / OVT_BEI_RUECKFAHRLICHT

<設定値>
aktiv

<備考>
正直見やすくなるとかはない。
```
  
▼ 今はやっていない設定  
  
#### [ASD オフ]
```
1: ASD / 3000 ASD-Configuration / Engine
2: ASD / 3000 ASD-Configuration / Model Range

<設定値>
1: N74B66
2: F001

<備考>
1, 2 は実車と異なる設定であれば何でも良い。
```
  
#### [オーディオ設定変更]
```
<コーディング項目>
HU_NBT2 / 3002 AUDIO_TUNER_TRAFFIC / AUDIO_SYSTEM

<設定値>
individual_sound

<備考>
ここはお好み。
individual_sound > highpremium > hifi_system_harmankardon の順でドンシャリ度が高いらしく、だいたいこの 3 つのどれかにしている人が多い印象。
```
  
## 更新履歴  
  
2025/02/11: 記事作成  
2026/01/02: 再整形、追記