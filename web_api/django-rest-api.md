# Django REST api 作成

> pipモジュールのインストール
	pip install django
	pip install djangorestframework

> アプリの作成
	python manage.py startapp [アプリ名]
	settings.pyにもアプリ名を追加しておく。

> モデルの定義
	アプリ内のmodels.pyを入力。

> DB作成
	python3 manage.py makemigrations
	python3 manage.py migrate

> 管理者作成
	python3 manage.py createsuperuser

> admin.pyへモデルの登録
	from django.contrib import admin
	from .models import [モデル名]

	@admin.register([モデル名])
	class [モデル名](admin.ModelAdmin):
			pass

> Django REST api の取り込み
	settings.pyのinstalled_appsに 'rest_framework', を追加。

> Serializerの定義
	作成したアプリディレクトリの中に、serializer.pyを作成する。
	作成したpyファイルの中に、
	from rest_framework import serializers
	from .models import [モデル名]

	class [モデル名]Serializer(serializers.ModelSerializer):
		class Meta:
			model = [モデル名]
			fields = (
				'[モデル要素名]',
			)

> ViewSetの定義
	アプリ内のviews.pyに以下を記述。
	from rest_framework import generics
	from .models import [モデル名]
	from .serializer import [モデル名]Serializer

	class [モデル名]View(generics.ListAPIView):
		queryset = [モデル名].objects.all()
		serializer_class = [モデル名]Serializer

	class [モデル名]DetailView(generics.ListAPIView):
		queryset = [モデル名].objects.all()
		serializer_class = [モデル名]Serializer

> URL patternの定義
	プロジェクト内のurls.pyに以下を記述。
	from django.urls import path, include
	from django.contrib import admin


	urlpatterns = [
			path('admin/', admin.site.urls),
			path('api/', include('app.urls')),
	]

	アプリ内にurls.pyを作成し、以下の内容を記述。
	from django.urls import path
	from . import views

	urlpatterns = [
		path('hoge/', views.HogeView.as_view(), name='hoge_list'),
		path('hoge/<str:pk>/', views.HogeDetailView.as_view(), name='hoge'),
	]
> PAGINATIONの活用
	一度に取得するデータの数を制限する。
	REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.LimitOffsetPagination',
    'PAGE_SIZE': 3
	}

# フロントエンドとバックエンドの接続

> django-cors-headersのインストール
	pip3 install django-cors-headers

> corsheadersの設定
	> corsheaderの登録
		settings.pyのINSTALLED_APPSに
		'corsheaders'
		settings.pyのMIDDLEWAREに
		'corsheaders.middleware.CorsMiddleware',
	> ローカルホスト3000番ポートからの接続を許可。
		CORS_ORIGIN_WHITELIST = [ "http://localhost:3000", ]


# [番外編]画像を使う
> Pillowのインストール
	pip3 install pillow

> MEDIA_URL, MEDIA_ROOTの設定
	import os
	MEDIA_URL = '/media/'
	MEDIA_ROOT = os.path.join(BASE_DIR, 'media')

> urlの設定
	プロジェクトのurls.pyに以下を追加。
	from django.conf import settings
	from django.conf.urls.static import static

	if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)


# メモ
REST apiを作成するには、Serializer, ViewSet, URL patternの最低3つが必要になる。
 - Serializerはソフトウェア内部で扱っているデータをそのまま、保存したり送受信することができるように変換すること
 - ViewSetは「APIのクエリーをどう解釈するかを決めるためのもの」
 - URL Patternは「DjangoにURLのパターンを教えるためのもの」