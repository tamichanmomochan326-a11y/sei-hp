# 整 totonou HP 引き継ぎ書

## プロジェクト概要
整体サロン「整 totonou」のホームページ（スタンドアロンHTML）。
デスクトップの「整HP作成」フォルダで管理。ブラウザで直接 `index.html` を開いて確認。

---

## ファイル構成（「整HP作成」フォルダ内）

### メインファイル
- `index.html` — すべてのHTML/CSS/JSが1ファイルに収まったスタンドアロンHP

### 画像ファイル（全て同フォルダに置く）
| ファイル名 | 用途 |
|---|---|
| `logo.png` | フッターロゴ |
| `logo-new.png` | ヘッダーロゴ・ヒーロー左下ロゴ |
| `image-1779934233633.jpg` | スライドショー1枚目 |
| `image-1779934228345.jpg` | スライドショー2枚目 |
| `image-1779934231618.jpg` | スライドショー3枚目 |
| `image-1779934223142.jpg` | スライドショー4枚目 |
| `image-1779934235594.jpg` | スライドショー5枚目 |
| `concept.png` | CONCEPTセクション写真 |
| `about-1.jpg` | 当院ができること：カウンセリング（左上） |
| `about-2.jpg` | 当院ができること：体のおはなし（右上） |
| `about-3.jpg` | 当院ができること：セルフケア指導（左下） |
| `about-4.jpg` | 当院ができること：体質改善指導（右下） |
| `icons-about.png` | 当院ができることセクションのアイコン4つ（骨・関節・筋肉・神経） |
| `icon-shoulder.png` | こんなお悩み：肩こり・首こり |
| `icon-back.png` | こんなお悩み：腰の張り・腰痛 |
| `icon-cold.png` | こんなお悩み：冷え・むくみ |
| `icon-nerve.png` | こんなお悩み：自律神経の乱れ |
| `icon-price.png` | こんなお悩み：料金について |

---

## デザイントークン（CSSカスタムプロパティ）

```css
--teal: #48B4E0
--teal-deep: #2E8FB8
--teal-soft: #E6F4FA
--beige: #EFEAD8
--warm: #FAF8F2
--ink: #2A2A2A
--ink-soft: (やや薄いインク色)
--line: (区切り線の色)
```

### フォント（Google Fonts CDN）
- 見出し：`Noto Serif JP`
- 本文：`Noto Sans JP`
- 英字装飾：`Cormorant Garamond`

---

## ページセクション構成（上から順）

1. **HEADER**（固定）— logo-new.png、整体サロン totonou、電話 070-9111-8430
2. **HERO** — 5枚スライドショー、縦書きキャッチコピー、左下ブランドロゴ
3. **CONCEPT** — concept.png + テキスト
4. **ABOUT TILES**（当院ができること）— 4枚グリッド写真
5. **CONCERN**（こんなお悩みはありませんか）— 5枚アイコンカード
6. **BEFORE & AFTER**（お客様の変化）— 3症例ダミー、「症例をもっと見る」ボタン ※写真未入稿
7. **MENU & PRICE**（施術内容・料金）
8. **VOICE**（お客様の声）
9. **THERAPIST**（施術者紹介）— ダミーテキスト ※写真・名前・経歴未入稿
10. **INFO + SNS**
11. **ACCESS**（アクセス）
12. **CTA**（予約バナー）
13. **FOOTER**

---

## 重要な実装ルール

### 画像ファイルの扱い
- **base64埋め込み禁止** — 必ず外部ファイル参照（トークン節約のため）
- 画像は全て `index.html` と同じフォルダに置く

### アイコンを画像ファイルに差し替える場合のルール
```html
<!-- 正しい書き方（一重枠・78px） -->
<div class="ricon" style="border:none;width:78px;height:78px">
  <img src="icon-xxx.png" style="width:78px;height:78px;object-fit:contain">
</div>
```
- `border:none` を必ず追加（画像自体に枠があるため、CSSの枠と二重になるのを防ぐ）
- サイズは78×78px固定

### ブラウザ更新
ファイル差し替え後は必ず **Cmd+Shift+R**（強制リロード）

---

## ヘッダーブランドロゴ構成

```html
<a href="#" class="brand">
  <img src="logo-new.png">  <!-- 72px円形ロゴ、背景透過 -->
  <div class="brand-text">
    <span class="ja">整体サロン</span>
    <div class="bottom-row">
      <span class="kanji">整</span>  <!-- 28px Noto Serif JP -->
      <span class="en">totonou</span>  <!-- 22px Cormorant Garamond -->
    </div>
  </div>
</a>
```

---

## ヒーロー左下ブランド構成

```html
<div class="hero-brand">
  <div class="logo-circle">
    <img src="logo-new.png">  <!-- 130px、白丸背景なし・透過 -->
  </div>
  <div class="name">
    <span class="tag">整体サロン</span>  <!-- 18px、margin-bottom:-20px -->
    <div class="bottom-row">
      <span class="ja-name">整</span>  <!-- 78px Noto Serif JP -->
      <span class="en-name">totonou</span>  <!-- 34px Cormorant Garamond -->
    </div>
  </div>
</div>
```

---

## 未完了・今後の作業

| 項目 | 状態 |
|---|---|
| BEFORE & AFTER 写真 | ダミーグラデーション（写真未入稿） |
| 施術者紹介 写真 | `photo-placeholder` ダミー表示 |
| 施術者紹介 氏名・経歴 | ダミーテキスト（要入力） |
| 施術者紹介 写真ファイル | ファイル名未定（決まったら `therapist.jpg` 推奨） |
| 「症例をもっと見る」リンク先 | `href="#"` のまま（詳細ページ未作成） |
| 「詳しいプロフィール」リンク先 | `href="#"` のまま |
| 営業時間・アクセス情報 | ダミーデータの可能性あり（要確認） |
| メニュー・料金 | ダミーデータの可能性あり（要確認） |

---

## Git情報
- リポジトリ: `/home/claude/repo/`
- ブランチ: `main`
- コミット時: `--no-gpg-sign` を必ず付ける（GPG署名エラー回避）
```bash
git commit --no-gpg-sign -m "メッセージ"
```
