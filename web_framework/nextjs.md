> next.jsのインストール
	npmが入っている状態で、npx create-next-app . --use-npm

> サーバー起動
	npm run dev

> Tailwind cssの導入(Next.js)
	npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
> 設定ファイルの作成
	npx tailwindcss init -p
> purge書き換え
	tailwind.config.jsが作成されているのでpurge: ['./pages/**/*.{js,ts,jsx,tsx}', './components/**/*.{js,ts,jsx,tsx}'],に変更。
> GrobalCSSの書き換え
	styles内のgrobals.cssを以下に書き換え
	@tailwind base;
	@tailwind components;
	@tailwind utilities;
> 必要のないファイル削除
	styles/homemoduels.css,
	pages/api
	は削除。

> index.js の準備
	index.js内の
	import styles from '../styles/Home.module.css'、
	return の中身を削除する。

# メモ
	pagesフォルダにファイルを入れることで自動的にルーティングを設定。