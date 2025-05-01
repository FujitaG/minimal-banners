# Minimal Banners – Cloudflare Pages

2 枚のバナーだけで構成された抑制的ミニマル遷移ページ。  
**画像仕様**: 644 × 180 px、JPEG、各ファイルは `img/` 配下。  

| バナー | ファイル名 | リンク先 |
|--------|------------|----------|
| 水色 (JKA Social Action) | `banner-jka.jpg` | https://www.jka-cycle.jp/ |
| 白色 (KEIRIN.JP) | `banner-keirin.jpg` | https://keirin.jp/ |

## デプロイ手順

1. 本リポジトリを fork / clone。  
2. `img/` に 2 枚の JPG を入れ、必要なら差し替え。  
3. `index.html` の `<a href="…">` を編集して別 URL にも対応可。  
4. GitHub へ push。  
5. Cloudflare ダッシュボード → **Workers & Pages** → **Create project** でこの repo を選択。  
   * **Build command** : _(空欄)_  
   * **Output directory** : `/`  
   Cloudflare が push ごとに自動ビルド & 配信。 ([Build configuration · Cloudflare Pages docs](https://developers.cloudflare.com/pages/configuration/build-configuration/?utm_source=chatgpt.com))  
6. 独自ドメインを付ける場合は **Custom domains** で CNAME 追加。 ([Custom domains · Cloudflare Pages docs](https://developers.cloudflare.com/pages/configuration/custom-domains/?utm_source=chatgpt.com))  
7. `<link rel="preload">` を記述済みなので、Early Hints が自動で発行され LCP が向上。 ([Early Hints - Cache / CDN - Cloudflare Docs](https://developers.cloudflare.com/cache/advanced-configuration/early-hints/?utm_source=chatgpt.com))  

## 技術メモ

* `alt` 属性でリンク先の機能を簡潔に表記し、スクリーンリーダー互換を確保。 ([HTMLImageElement: alt property - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/alt?utm_source=chatgpt.com))  
* Flexbox 中央配置・折り返しでレスポンシブ。 ([Aligning items in a flex container - CSS: Cascading Style Sheets](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_flexible_box_layout/Aligning_items_in_a_flex_container?utm_source=chatgpt.com))  
* Transform/opacity を使った hover アニメはレイアウトを再計算しないため CLS を発生させない。 ([scale() - CSS: Cascading Style Sheets - MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/scale?utm_source=chatgpt.com))  
* Cloudflare Images/CDN を使えば URL パラメータで自動リサイズも可能。 ([Use image CDNs to optimize images | Articles - web.dev](https://web.dev/articles/image-cdns?utm_source=chatgpt.com))  

---

### これで完了です
Git push だけで更新が全世界 PoP に複製されます。画像を後で差し替えるだけなら `img/` フォルダのファイルを置き換え、再 push すれば自動展開されます。  

> *補足*: JPG は WebP より平均サイズが大きい傾向ですが、Quality 80 前後なら視覚と容量のバランスは良好とされています。 ([Image performance | web.dev](https://web.dev/learn/performance/image-performance?utm_source=chatgpt.com), [What Is a WEBP File?](https://www.lifewire.com/what-is-a-webp-file-5186388?utm_source=chatgpt.com))
