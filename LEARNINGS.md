# 制作・検証記録 — 2026-09-18

## 成果
3D探索からターン制戦闘、祠の取得、竜討伐、エンディングまでを実装。

## Evidence
`tests/smoke.cjs` の Chromium 自動検証：PASS、pageerror 0。
確認項目：3D表示、キー移動、村の回復、祠３つ、魔法MP消費、ボス勝利、エンディング、保存再開、敗北復帰、390×844の画面幅での横はみ出しなし。
画面画像：`/tmp/dq3d-title.png`、`/tmp/dq3d-field.png`、`/tmp/dq3d-battle.png`、`/tmp/dq3d-ending.png`、`/tmp/dq3d-mobile.png`。

## 検証の限界
遭遇地点への位置設定をテスト内で行っている。全経路の手動踏破やiPhone実機／Safari検証は未実施。モバイルはChromiumのビューポート確認。公開は未実施。

## 学習
- 戦闘の非同期演出は固定秒数で待つと、勝利直前に次コマンドを送る誤判定が起きる。状態遷移とbusy解除で待つ。
- ソフトウェアWebGLでは高解像度の影と多数のメッシュが自動検証を遅くする。画面確認後にテスト側だけ解像度を下げ、ロジック検証を進めた。
- 依存ライブラリをローカル同梱し、オフライン起動と静的配布を可能にした。

## セキュリティ確認
本作コードに外部通信、認証情報、HTML文字列へのユーザー入力埋め込みはない。保存はlocalStorageのみ。重大度Criticalの指摘なし。Evidenceはgame.jsの実装とブラウザエラー検証。人間承認を要する外部公開は行っていない。

## 2026-09-19 フォルダ改名・ハーネス操作盤
- フォルダ名を `244-day068` から `244-hajimari-no-shima` へ変更。
- ハーネス契約（`#game-shell` / `#game-stage` / `#screen-wrap` / `#control-deck`、上75%下25%）を入れ、仮想スティックと調べる／薬草／ミュート／ポーズを操作盤へ移した。
- `setPointerCapture`、touchend 300ms、safe-area、`tg.244.mute`、ループBGM、タブ非表示ポーズを追加。冒険セーブキー `dq3d-island-v1` は維持。
- WebGLは `antialias:false`、pixelRatio上限1。描画先は `#screen-wrap` の実寸。
- 操作盤をDOM先頭に置き、CSS `order` で上段ステージ／下段操作に戻した。ハーネスの `button, [role=button], canvas` first がボタンを掴む。
- harness PASS: `docs/harness-reports/244-hajimari-no-shima-2026-09-19T07-13-38-005Z.md`（RAF 53、操作盤 25.0%、タップ成功）。iPhoneシミュレータは未実施。

## 2026-09-19 公開（GitHub Pages）
- URL: https://titan11111.github.io/244-hajimari-no-shima/ （HTTP 200・Pages status=built を実測）
- publish.sh が OGP タグを index.html へ挿入したため、**公開実体で harness を取り直した**: `docs/harness-reports/244-hajimari-no-shima-2026-09-19T07-20-23-845Z.md` → 14項目すべて PASS
- 学び: publish.sh の OGP 挿入は harness の後に走る。公開後の実体で1回取り直さないと、証跡が公開物と一致しない
- 未検証: iPhone実機（harness は Playwright/WebKit 390px のみ）
