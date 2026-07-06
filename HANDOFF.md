# 整 totonou HP 引き継ぎ書（2026-07-05 更新）

整体サロン「整 totonou」のホームページ。`index.html` 1ファイルにHTML/CSS/JSがすべて入ったスタンドアロン形式。

技術的な詳細（画像一覧・デザイントークン・実装ルール）は [CLAUDE.md](CLAUDE.md) を参照。この文書は「今どこまでできているか」の記録。

---

## 公開場所

- **公開URL**: https://tamichanmomochan326-a11y.github.io/sei-hp/ （GitHub Pages）
- **リポジトリ**: https://github.com/tamichanmomochan326-a11y/sei-hp （※Public設定）
- 確認方法: ローカルでは `index.html` をブラウザで直接開く。画像差し替え後は **Cmd+Shift+R**（強制リロード）

## Git の使い方

- コミット時は必ず `git commit --no-gpg-sign -m "メッセージ"`（GPG署名エラー回避）
- 作業ブランチ: `claude/gallant-wozniak-ve83yy`（作業後に main へマージして公開に反映）

---

## できていること（2026-07-05 時点）

- 全13セクションのレイアウト完成（ヘッダー〜フッター）
- スライドショー（5枚・自動切替）
- お悩みカード 8枚（肩こり／腰痛／冷え／自律神経／食いしばり／小顔／ダイエット／料金）
- 施術者写真 2枚のクロスフェード表示（therapist-1.jpg / therapist-2.jpg）
- フッターロゴの表示修正（存在しない logo.png → logo-new.png に変更済み）

## 残っている作業

| 項目 | 状態 |
|---|---|
| BEFORE & AFTER 写真 | ダミーグラデーション（写真未入稿） |
| 施術者の氏名・経歴 | ダミーテキストのまま（要差し替え） |
| 「症例をもっと見る」「詳しいプロフィール」 | リンク先未作成（`href="#"`） |
| SNSボタン | リンク先URL未設定 |
| Googleマップ | 埋め込み未完了 |
| 営業時間・住所・料金 | ダミーデータの可能性あり（要確認） |
