# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

整体サロン「整 totonou」のホームページ。スタンドアロンHTML形式 — `index.html` 1ファイル（約980行）にHTML/CSS/JSがすべて収まっている。サーバー不要、ブラウザで直接開いて確認。

## ⚠️ セッション開始時に必ず伝えること

**新しいセッションが始まったら、最初にユーザーへ以下を伝える：**

> 「このセッションの変更は `claude/（ブランチ名）` というブランチに保存されます。作業が終わったら『公開して』と言ってもらえれば、mainへのマージ → Push → 公開反映の確認まで、こちらですべて行います。」

## ⚠️ 会話の圧縮が近づいたら必ず伝えること

会話が長くなり、そろそろ圧縮（コンテキストの切り捨て）が始まりそうなタイミングで、ユーザーへ以下を伝える：

> 「そろそろ会話が長くなってきました！次の3つをお願いします：
> 1. CLAUDE.md に今回の作業内容を追記します
> 2. main にマージします
> 3. 新しいセッションを立ち上げてください」

## 確認方法

`index.html` をブラウザで開く。編集後は **Cmd+Shift+R**（強制リロード）で画像キャッシュをクリア。

## Git コミット

```bash
git commit --no-gpg-sign -m "メッセージ"
```
`--no-gpg-sign` を必ず付けること（GPG署名エラー回避）。

## 公開の流れ（2026-07-06 更新：Pushまで自動化）

ユーザーが「公開して」「mainにマージして」と言ったら、**以下を一括で実行する（ユーザーのPush操作は不要）**：

1. 作業ブランチをコミット → `git checkout main` → `git merge` → `git push origin main`
2. mainへのPushで GitHub Actions が Cloudflare Pages へ自動デプロイする（`.github/workflows/deploy.yml`）
3. 1〜2分待って公開URLを curl で確認し、反映されたことをユーザーに報告する

- 公開URL: https://totonou-hp.pages.dev/ （Cloudflare Pages・mainへのPushで自動更新。2026-07-07 に sei-hp から改名）
- 旧URL: https://sei-hp.pages.dev/ （旧Cloudflareプロジェクト・更新されず残存）、https://tamichanmomochan326-a11y.github.io/sei-hp/ （GitHub Pages・稼働中）
- ⚠️ mainへのPush＝**本番公開**。ユーザーの依頼（「公開して」等）があったときだけ行い、勝手にPushしない
- Cloudflare の APIトークンは GitHub の Secrets（`CLOUDFLARE_API_TOKEN`）にあり、コードには書かない

## 写真の追加・差し替えフロー（2026-07-06 確定：一言で全自動）

ユーザーが**デスクトップ（`~/Desktop`）に写真を置いて「写真反映して」等と言ったら**、以下を一括で実行する：

1. `~/Desktop` 直下の新しい画像ファイル（jpg/png/heic、追加された時刻が新しいもの）を探す
2. **どこに使う写真か確認する**（ユーザーが「施術者の写真や」等と言っていればそれに従う。不明なときだけ質問する）
3. 用途に合わせてリネームし、このフォルダへ移動する
   - 既存の差し替え → 既存と同じファイル名にする（HTML修正不要）
   - 新規の場所 → 下の命名ルールで名前を付け、`index.html` の該当箇所も更新する
   - HEIC形式は `sips -s format jpeg` でJPEGに変換してから使う
4. commit（`--no-gpg-sign`）→ mainへマージ → push → 1〜2分後に公開URLで反映確認 → 報告

命名ルール（新規のとき）: 英数字とハイフンのみ。セクション名-連番（例: `ba-1-before.jpg` / `ba-1-after.jpg`、`slide-6.jpg`、`therapist-3.jpg`）

⚠️ 注意（実行前に必ず守る）:
- **写真反映の依頼はそのまま本番公開の依頼**とみなしてPushまで行ってよい（2026-07-06 ユーザー指示）
- **お客様など本人が特定できる人が写っている写真**は、公開前に「本人の同意は取れてるか」を一言確認する
- 元の写真ファイルはデスクトップから移動する（消さない）。同名ファイルを上書きする場合は旧ファイルがGit履歴に残るので復元可能

## 画像ファイルのルール

- **base64埋め込み禁止** — 必ず外部ファイル参照（`index.html` と同じフォルダに置く）
- アイコンを画像ファイルに差し替える場合：

```html
<div class="ricon" style="border:none;width:78px;height:78px">
  <img src="icon-xxx.png" style="width:78px;height:78px;object-fit:contain">
</div>
```
`border:none` 必須（画像自体の枠とCSSの枠が二重になるのを防ぐため）

## 画像ファイル一覧（index.html が実際に参照しているもの）

| ファイル名 | 用途 |
|---|---|
| `logo-new.png` | ヘッダーロゴ・ヒーロー左下ロゴ・フッターロゴ |
| `image-1779934233633.jpg` | スライドショー1枚目 |
| `image-1779934228345.jpg` | スライドショー2枚目 |
| `image-1779934231618.jpg` | スライドショー3枚目 |
| `image-1779934223142.jpg` | スライドショー4枚目 |
| `image-1779934235594.jpg` | スライドショー5枚目 |
| `concept.png` | CONCEPTセクション写真 |
| `about-1.jpg` | 当院ができること：カウンセリング（左上） |
| `about-2.jpg` | 当院ができること：体のおはなし（右上） |
| `about-3-new.jpg` | 当院ができること：セルフケア指導（左下） |
| `about-4-new.jpg` | 当院ができること：体質改善指導（右下） |
| `icons-about.png` | 当院ができることセクションのアイコン（骨・関節・筋肉・神経） |
| `icon-shoulder.png` | お悩みカード：肩こり・首こり |
| `icon-back.png` | お悩みカード：腰の張り・腰痛 |
| `icon-cold.png` | お悩みカード：冷え・むくみ |
| `icon-nerve.png` | お悩みカード：自律神経の乱れ |
| `icon-jaw.png` | お悩みカード：夜間の食いしばり |
| `icon-face.png` | お悩みカード：顔の大きさ・左右差 |
| `icon-diet.png` | お悩みカード：ダイエット＆体質改善 |
| `icon-price.png` | お悩みカード：料金について |
| `therapist-1.jpg` / `therapist-2.jpg` | 施術者写真（2枚クロスフェード表示） |

※ `logo.png` は削除済み（フッターも `logo-new.png` を使用）。`about-3.jpg`・`about-4.jpg`・`sejutsudai1.jpg` はフォルダに残っているが未使用。

## デザイントークン

```css
--teal: #48B4E0        /* メインカラー */
--teal-deep: #2E8FB8
--teal-soft: #E6F4FA
--beige: #EFEAD8
--warm: #FAF8F2        /* セクション背景 */
--ink: #2A2A2A         /* 本文テキスト */
--ink-soft: #5C5C5C
--line: #E5E5E0        /* 区切り線 */
```

フォント: `Noto Serif JP`（見出し）、`Noto Sans JP`（本文）、`Cormorant Garamond`（英字装飾）

## ページセクション構成

1. HEADER（固定） — logo-new.png、TEL: 070-9111-8430
2. HERO — 5枚スライドショー（5.5秒間隔自動切替）＋縦書きキャッチ
3. CONCEPT — concept.png + テキスト
4. ABOUT TILES — about-1 / about-2 / about-3-new / about-4-new の4枚グリッド
5. CONCERN（お悩みカード）— icon-*.png の8枚カード
6. BEFORE & AFTER — ※写真未入稿（グラデーションダミー）
7. MENU & PRICE
8. VOICE（お客様の声）
9. THERAPIST — 写真は therapist-1.jpg / therapist-2.jpg のクロスフェード入稿済み ※氏名・経歴はダミーのまま
10. INFO + SNS
11. ACCESS（Googleマップ未埋め込み）
12. CTA（予約バナー）
13. FOOTER

## ヘッダーブランドロゴ構成

```html
<a href="#" class="brand">
  <img src="logo-new.png">  <!-- 72px -->
  <div class="brand-text">
    <span class="ja">整体サロン</span>
    <div class="bottom-row">
      <span class="kanji">整</span>   <!-- 28px Noto Serif JP -->
      <span class="en">totonou</span> <!-- 22px Cormorant Garamond -->
    </div>
  </div>
</a>
```

## ヒーロー左下ブランド構成

```html
<div class="hero-brand">
  <div class="logo-circle">
    <img src="logo-new.png">  <!-- 130px -->
  </div>
  <div class="name">
    <span class="tag">整体サロン</span>  <!-- 18px、margin-bottom:-20px -->
    <div class="bottom-row">
      <span class="ja-name">整</span>       <!-- 78px Noto Serif JP -->
      <span class="en-name">totonou</span>  <!-- 34px Cormorant Garamond -->
    </div>
  </div>
</div>
```

## JS構成（index.html末尾 `<script>` タグ内）

- `header.scrolled` クラスのトグル（スクロール検知）
- ハンバーガーメニュー開閉
- スライドショー: `setInterval` 5500ms、`.slide.active` クラス切替
- スクロールフェードイン: `IntersectionObserver`、`.fade` → `.in` クラス付与

## 未完了の作業（2026-07-05 時点）

| 項目 | 状態 |
|---|---|
| BEFORE & AFTER 写真 | ダミーグラデーション（写真未入稿） |
| 施術者 氏名・経歴 | ダミーテキストのまま（「施術者名」「Therapist Name」を要差し替え） |
| 「症例をもっと見る」リンク | `href="#"` のまま |
| 「詳しいプロフィール」リンク | `href="#"` のまま |
| SNSボタンのリンク先 | `href="#"` のまま（Instagram等のURL未設定） |
| Googleマップ | `.access-map` に埋め込み未完了 |
| 営業時間・住所・料金 | ダミーデータの可能性あり（要確認） |
