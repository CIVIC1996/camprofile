/** main.cpp
 * @file    main
 * @brief   ESP32dによるカムプロフィール測定プログラム
 * @author  yoshio ide(井出芳夫)
 * @date    2026-05-01
 * @Board   ESP32_DEV_Module 
 * @ボードマネージャ = esp32 by Esprssif Systems (3.04)
 *                    Arduino ESP32 Boards by Arduino (2.0.18)
 * @version 1.0.0
 * 
 * [概要]
 * カムプロフィール測定を行う。
 * 表示はi2c LCD およびWifi接続による。
 * 
 * [ハードウェア構成]
 * - Board: ESP32-WROOM-32E (DevKit V1)
 * - rotary encoder:メニュー設定用 (A:27, B:26番ピン）
 * - rotary encoder: 多摩川精機(FA-CODER 48-1000P6-L6-5V TS 5207 N577 SER.NoB17524) （A:13, B:14番ピン）
 * - dial gauge: 小野測器 GS-1730A （A:35, B:36番ピン）→（A:34, B:35番ピン）
 * - i2c LCD 5V 4行 × 20文字 （21,22 番ピン）
 *
 *
 * 1.main.ino               : UI状態遷移（UI状態管理、リアルタイム表示、設定操作、測定開始トリガー)
 *                              MAIN    : 測定データのリアルタイム表示モード。
 *                              MENU_SEL: 設定項目の選択モード。
 *                              OPT_SEL : 設定値の変更モード。
 * 2.CamAnalyzer.cpp        : 波形解析、データ記録、CSVダンプ、フィルタ処理
 * 3.Encoder_PCNT.cpp       : 角度・リニアゲージ・メニュー用エンコーダの PCNT 制御
 * 4.InterruptHandler.cpp   : ボタン割り込み（デバウンス付き）ボタンA/Bのチャタリング防止割り込み処理。
 * 5.Lcd_driver.cpp         : LCD描画（メイン画面・設定画面）スクロール表示、等号整列、動的ラベル描画。
 * 6.Profile.cpp            : 角度計算、RPM計算、リニアゲージ変換。
 * 7.setting.cpp            : 設定メニュー生成(0.01mm単位（151項目）の動的メニュー生成)、Preferences保存・復帰、初期化機能。
 * 8. Buzzer_Pi.cpp         : ブザー制御
 *
 * [作成履歴 / Update History]
 * 2026/07/01 - 新規作成 (v1.0.0)
 * 2026/07/02 - Calc計算方法追加 CAM CRANK ESP32CH340C_NEW_15_BTDC
 * 2026/07/03 - 720度 削除
 * 2026/07/04 - Calc計算方法削除 CAM CRANK  ESP32CH340C_NEW_16
 * 2026/07/05 - データダンプ（デバッグ用）修正ESP32CH340C_NEW_17_OK
 * 2026/07/05 - Intake / Exhaus測定順改善（どちらからでも測定可能とした）
 * 2026/07/21 - Wifi機能追加
 * 2026/08/01 - version 1.0.0
 *
 *
 *
 * Copyright (c) 2026 [yoshio ide]
 * All rights reserved.
 */

URL livedoor Blog

https://wave0505.blog.jp/archives/31364867.html


