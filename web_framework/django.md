# Django動作環境作成手順

> pythonのバージョン確認
python -V または python3 -V

> virtualenvにてプロジェクトの開発環境作成
virtualenv -p python3 サービス名

> Djangoのインストール
pip3 install django

> Djangoのサービスツールを作成
django-admin startproject サービス名 .

> アプリ追加
python3 manage.py startapp アプリ名 -> settings.py にて作成したアプリの登録

> 使用言語, 時間帯の設定
settings.py内にあるLANGUAGE_CODEをjaに変更。 TIME_ZONEをAsia/Tokyoに変更。

> templatesフォルダの設定
templatesフォルダを作成。 -> 登録しているアプリのフォルダを中に作成。
settings.py内にあるTEMPLATES = [{'DIRS': []}]の[]の中に"os.path.normpath(os.path.join(BASE_DIR, 'templates')),"を記載。

> staticフォルダの設定 staticフォルダを作成 -> 中にjs, css, imagesなどのフォルダを作成。 
settings.py内にあるSTATIC_URLの下に以下のコードを貼り付け。(import os必須) 
STATICFILES_DIRS = ( os.path.join(BASE_DIR, "static"), )

MEDIA_ROOTの設定 pip3 install pillow # Python 3.x settings.pyに以下のコードを記載。(import os必須) MEDIA_URL = '/media/' MEDIA_ROOT = os.path.join(BASE_DIR, 'media/')

> サービス名ディレクトリにあるurls.pyに以下のコードを追加。 
from django.conf import settings from django.conf.urls.static import static
if settings.DEBUG: urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)