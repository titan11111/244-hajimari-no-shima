# はじまりの島 — 仕様

## 0. ドキュメント情報
- 対象ゲーム: 244-hajimari-no-shima
- 更新日: 2026-09-19
- ステータス: 公開
- 参照ファイル: index.html / style.css / game.js / three.min.js

## 1. ゲーム概要
- ジャンル: 短編3D探索RPG
- 一言説明: 3Dフィールドで３つの祠を巡り、北の古城の竜を倒す。
- 想定プレイ時間: 10〜20分
- 対象端末: iPhone Safari / GitHub Pages

## 2. 対象環境
- 配信先: GitHub Pages
- 最優先端末: iPhone Safari
- 対応画面幅: 320px〜430px
- 実装方式: 静的 HTML / CSS / JS。Three.js はローカル同梱

## 3. 操作 / 設定UI（必須）
- 入力: キーボード（WASD / 矢印 / E / Space / Q / R）＋ Pointer Events の仮想スティック
- `setPointerCapture` をスティックと操作ボタンに適用
- ポーズ: 操作盤のⅡ、Pキー、Escape、タブ非表示
- ミュート: 操作盤の音ボタン。`localStorage` キー `tg.244.mute`
- 冒険セーブ: 既存キー `dq3d-island-v1` を維持（移行なし）
- 画面構成: 上75% `#game-stage` / 下25% `#control-deck`（ハーネス契約）

## 4. コアループ
- 村で回復 → 祠で光を集める → 遭遇戦闘 → 古城の竜
- 戦闘: たたかう / 魔法 / 薬草 / ぼうぎょ / にげる
- 敗北: 所持金半減で村へ復帰

## 5. 音声
- 開始タップで AudioContext unlock
- WebAudio のループBGM（`.loop = true`）と効果音
- ミュート時はBGM停止

## 6. 未確定事項
- なし（公開ブロッカーなし）
