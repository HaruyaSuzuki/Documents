# Next.js
## インストール
npmが入っている状態で、npx create-next-app . --use-npm

## サーバー起動
npm run dev

## Tailwind cssの導入(Next.js)
- インストール
```
	npm i tailwindcss
	npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
```
- 設定ファイルの作成
```
	npx tailwindcss init -p
```
- purge書き換え
tailwind.config.jsが作成されているので下記へ変更
```
	purge: ['./pages/**/*.{js,ts,jsx,tsx}', './components/**/*.{js,ts,jsx,tsx}'],
```
- _app.jsに下記を追加
```
	import 'tailwindcss/tailwind.css'
```
- GrobalCSSの書き換え
styles内のgrobals.cssを以下に書き換え
```
	@tailwind base;
	@tailwind components;
	@tailwind utilities;
```

## その他準備
- components ディレクトリを作成
- 必要のないファイル削除
styles/homemoduels.css,
pages/api
は削除。

## メモ
pagesフォルダにファイルを入れることで自動的にルーティングを設定。