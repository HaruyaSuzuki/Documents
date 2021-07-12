# @content
> @includeでmixinを呼び出す際、@include hoge {}で呼び出し、mixin内で@content;を使うと@include hoge {}の{}内のスタイルが適用される。

# 辞書型変数
## 定義
> $[変数名]: ('[キー]': [値]);
## 値呼び出し
> map-get($[変数名], '[キー名]');

# 変数の値をテキストとして表示
## #{} インターポーテーションを使用
> #{[変数名]}

# !default
> 
## 使用例
> $my-black: #333 !default;