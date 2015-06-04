# 開発環境の使い方（Gulp Expert）
全てコマンドプロンプトから実行します。

## 初期設定
１．node.jsのインストール
インストールされていれば不要です。
コマンドプロンプトを開いて node -v と入力・実行し、バージョン表記が表示されればインストールされています。
インストールされていない場合は node.js 公式サイトからダウンロードしてインストールしてください。

２．gulpのインストール
コマンドプロンプトで npm install gulp -g と入力・実行してください。

## モジュールのインストール
package.json があるフォルダで[Shift+右クリック]→[コマンドウィンドウでここを開く]を選択してコマンドプロンプトを開き、
npm install と入力・実行してください。node_modules というフォルダが作成され、その中にインストールされます。
この操作は案件が変わり別のディレクトリなった場合にはもう一度必要になります。

## コマンド
gulp clean      : httpdocs を削除する。

gulp sass       : src/assets/sass/ の中にある .sassファイルをcssファイルにコンパイルして httpdocs に書き出す。

gulp ejs        : src/ の中にある.ejsファイルをhtmlファイルにコンパイルして httpdocs に書き出す。

gulp imagemin   : src/assets/img/ の中にある画像ファイルを圧縮して httpdocs に書き出す。
                  デフォルトでは無効にしているので、使用する際は setting.imagemin.disable を false にする。

gulp cssminify  : httpdocs/assets/css/ の中にある .css ファイルをミニファイして上書きする。
                  デフォルトでは無効にしているので、使用する際はsetting.minify.cssを true にする。

gulp jsminify   : httpdocs/assets/js/ の中にある .js ファイルをミニファイして上書きする。
                  デフォルトでは無効にしているので、使用する際はsetting.minify.jsを true にする。

gulp cssbeautify: httpdocs/assets/css/ の中にある .css ファイルのコードを整形して上書きする。
                  デフォルトでは無効にしているので、使用する際は setting.cssbeautify.disabled を false にする。
                  cssminify が有効な場合は使用できない。

gulp csscomb    : httpdocs/assets/css/ の中にある .css ファイルのCSSプロパティをソートして上書きする。
                  デフォルトでは無効にしているので、使用する際は setting.csscomb.disabled を false にする。
                  cssminify が有効な場合は使用できない。

gulp build      : src フォルダを元にコンパイルしたファイルを httpdocs フォルダに出力する。
                  すでに httpdocs がある場合は一度削除するため、httpdocs に直接ファイルを置かないように気をつける。
                  上記で紹介しているコマンドを一括で実行する。

gulp            : httpdocsフォルダをルートにWebサーバを立ち上げる。
                  ローカルとイントラネット内で確認できるAccess URLsを発行してくれる。
                  PHPを使用する場合は、setting.browserSync.server をコメントアウトし、
                  setting.browserSync.proxyにxamppで作成したローカルテスト環境のドメインを指定する。

## 主な機能
gulp-browserSync : gulpコマンドで立ち上げたWebサーバへのAccess URLにアクセスしているブラウザの挙動（スクロールやリロードなど）を同期する。
                   xxx:3001 にアクセスすることで同期する挙動の制御などができる。
gulp-sass        : scssファイルのコンパイル
gulp-imagemin    : 画像ファイルの圧縮（デフォルトでは無効）
gulp-autoprefixer: ベンダープレフィックスの付与
gulp-minify-css  : CSSコードのミニファイ（デフォルトでは無効）
gulp-uglify      : JSコードのミニファイ（デフォルトでは無効）
gulp-csscomb     : CSSプロパティのソート（デフォルトでは無効）
gulp-cssbeautify : CSSコードの整形（デフォルトでは無効）
gulp-ejs         : HTMLのテンプレートエンジン

##ディレクトリルール
src     : 開発用のデータを入れるフォルダ。このフォルダに全てのデータを格納するようにする。
httpdocs: 開発用のデータをコンパイルしたデータを出力するフォルダ。Webサーバで確認するときのルートフォルダになる。

----------------------------------
src
┣assets
┃┠img     - jpg|png|gif|svg
┃┠sass    - scss
┃┠js      - js
┃┠lib     - js単体ファイルでは済まずcssやimgをが含まれているjQuery Pluginなど
┃┠include - includeするファイル
┃┗etc     - 上記に含まれないもの全て
┠sitemap.xml
┗index.html|.php|.ejs
----------------------------------
※外部ファイルは全てassetsフォルダに入れる。
※上記のフォルダ以外のフォルダに入ったファイルは全てコピーされます。

## その他
・gulpfile.js で何を行っているのか、package.json にあるモジュールは何かを事前に把握して使用してください。
・gulpfile.js の中にある setting 変数で各種設定の変更ができます。
