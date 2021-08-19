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

## TypeScript導入
- tsconfig.jsonを作成
- typescriptパッケージインストール
```
npm install --save-dev @types/react
```
- npm run devで再度実行
- 拡張子を変更(jsx->tsx)

## その他準備
- components ディレクトリを作成
- 必要のないファイル削除
styles/homemoduels.css,
pages/api
は削除。

## メモ
pagesフォルダにファイルを入れることで自動的にルーティングを設定。

## お問い合わせフォーム作成(SendGrid)
- SendGridをインストール
```
npm install --save @sendgrid/mail
```
- send.tsを作成して以下を記入。
```
const handler = (req, res) => {
	if (req.method === 'POST') {
		const sgMail = require('@sendgrid/mail');
		sgMail.setApiKey("SG.[SendGeidのキー]");

		const msg = {
			to: req.body.email,
			from: '[メールアドレス]',
			subject: 'お問い合わせを受け付けました。' + req.body.message,
			text: 'お問い合わせを受け付けました。' + req.body.message,
			html: 'お問い合わせを受け付けました。' + req.body.message,
		};

		(async () => {
			try {
				await sgMail.send(msg);
			}
			catch(error) {
				console.error(error);
				if (error.response) {
					console.error(error.response.body)
				}
			}
		})();
	}
	req.status(200)
}

export default handler;
```

## Font Awesomeをcomponentsで読み込む
- 以下のコマンドを実行
```
npm i --save @fortawesome/fontawesome-svg-core
             @fortawesome/free-solid-svg-icons
             @fortawesome/free-brands-svg-icons
             @fortawesome/react-fontawesome
```
- Font Awesomeを使用したいcomponentsで読み込む
```
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome'
import { faRss } from '@fortawesome/free-solid-svg-icons'
import { faTwitter } from '@fortawesome/free-brands-svg-icons'
import { faInstagram } from '@fortawesome/free-brands-svg-icons'
```
- 使用する際は以下のやり方
```
<FontAwesomeIcon icon={faTwitter} />
```

## GoogleAnalytics
- .env.productionを作成後以下を記入
```
NEXT_PUBLIC_GA_ID=[GoogleAnalyticsのトラッキングID]
```
- lib/gtag.tsに以下を記入
```
export const GA_TRACKING_ID = process.env.NEXT_PUBLIC_GA_ID || '';
export const pageview = (url: string): void => {
  if (!GA_TRACKING_ID) return;
  window.gtag('config', GA_TRACKING_ID, {
    page_path: url,
  });
};
```
- gtagにエラーが出るのでgtagをインストール
```
npm install -D @types/gtag.js
```
- pages/_document.tsxを作成しスクリプト埋め込み
```
import { GA_TRACKING_ID } from 'lib/gtag';
import Document, { Html, Head, Main, NextScript } from 'next/document';

export default class MyDocument extends Document {
  render(): JSX.Element {
    return (
      <Html lang="ja">
        <Head>
          // GA_TRACKING_ID が設定されていない場合は、なし
          {GA_TRACKING_ID && (
            <>
              <script async src={`https://www.googletagmanager.com/gtag/js?id=${GA_TRACKING_ID}`} />
              <script
                dangerouslySetInnerHTML={{
                  __html: `
            window.dataLayer = window.dataLayer || [];
            function gtag(){dataLayer.push(arguments);}
            gtag('js', new Date());
            gtag('config', '${GA_TRACKING_ID}', {
              page_path: window.location.pathname,
            });
        `,
                }}
              />
            </>
          )}
        </Head>
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
    );
  }
}
```
- Next.jsのサイトはページ遷移をする際にJavaScriptでURLを変更する為、Next.jsのRouter機能を用いて、URLが変更した際にPVをカウントアップ(pages/_app.tsxに記載)
```
import { GA_TRACKING_ID, pageview } from 'lib/gtag';
import { AppProps } from 'next/app';
import { useRouter } from 'next/router';
import { useEffect } from 'react';

export default function App({ Component, pageProps }: AppProps): JSX.Element {
  const router = useRouter();
  useEffect(() => {
    // GA_TRACKING_ID が設定されていない場合は、処理終了
    if (!GA_TRACKING_ID) return;

    const handleRouteChange = (url: string) => {
      pageview(url);
    };
    router.events.on('routeChangeComplete', handleRouteChange);
    return () => {
      router.events.off('routeChangeComplete', handleRouteChange);
    };
  }, [router.events]);

  return <Component {...pageProps} />;
}
```
- スクリプト内のコメントを削除。