# CodeUps_1cw_sk-Vite_01
- これは静的サイト用Vite環境です
- srcフォルダ内のpublicフォルダ(images, js)、htmlファイル、scssフォルダのみ扱うことを基本とします
    - カスタマイズ・改変は自己責任でお願いします。エラーが起こった場合、こちらでは対応いたしかねます
- 開発環境で起動する場合、ファイルは出力されません（ゆえに速度が速い）
- vite.config.jsのportで任意のポート番号を指定できます
    - 必要ない場合は削除してください

# コマンド
- 最初に`npm i`（gulpと同様にnode_modulesをインストール）
- `npm run dev`で開発環境起動
    - ターミナルに表示される`> Local: http://localhost:****/`をcommand押しながらクリックしてください（自動で開きません）
- `npm run build`でdistフォルダ作成（ファイル出力）
- ** package.jsonを参照すること **

# 注意点
- 開発フォルダはsrcです
- `<link rel="stylesheet" href="./scss/style.scss" />`のように直接scssを指定してください
- publicフォルダ内のファイルは変換されず、そのままdistフォルダにコピーされます
- `src/public/assets/js/`にjsファイルがない場合はpackage.json > scripts > build の`&& esbuild`以降を削除すること
    - 例：hoge.htmlを作成した場合 => `hoge: resolve(__dirname, './src/hoge.html'),`

# ファイル新規作成時の検知・更新について
- scssなどのファイル新規作成時は検知/更新されない
- 既存のファイルを修正して検知させる、もしくは再度`npm run dev`を実行する

# 画像に関して（imgタグ, backgroundプロパティ）
- scssでbackgroundを指定する場合
    - `background-image: url('../../assets/images/hoge.jpg');` のようにpublicは省略する
- imgタグで指定する場合
    - `<img src="./assets/images/hoge.jpg" alt="">` のようにpublicは省略する

# JSについて
- `<script type="module" src="./js/main.js"></script>`は必ず記載してください
- main.jsのtype="module"は外すことはできません
- main.jsは出力後head内に記載されるが問題ありません（type="module"はdeferと同様の処理がされます）
- main.jsの名称を変更した際は、必ずvita.config.jsで設定を変更してください
- publicフォルダ内のJSについて
    - type属性を書かずに通常の方法で記述してください
    - publicフォルダ内のJSを読み込む際は`<script src="./assets/js/script.js"></script>`のようにpublicは省略する

# ライブラリにスタイルが当たらない問題について
- swiperに対してscssで指定してもスタイルが反映しない
    - jsでスタイルを当てると、scssが有効になる（バグ？）
    - 例：`$('.swiper-pagination-progressbar .swiper-pagination-progressbar-fill').css('background', 'red');`
    - slick, splide等では未検証
    - ①postcss.config.jsのsafelistにクラス名を入れる、②他のCSSを先に読み込み、style.scssを最後に読み込む で対応可能
    - 他に関しても同様のことが起こった場合は上記を実行してみてください

# includeについて
- componentsフォルダ内のファイルから他のファイルをinclude出来ない
    - index.htmiからcomponentsフォルダ内のファイルをincludeすることは可能 

# 画像圧縮
- vite-plugin-imageminで実行させてます
- 不要な場合はvite.config.jsの「viteImagemin」の記述部分とプラグインvite-plugin-imageminを削除してください

# 変数の記述方法
- 基本的にhandlebarsの記述方法で行うこと 例：`{{hoge}}`
- includeとhtml内で定義した変数のみEJSが使用可能 例：`<%= hoge %>` `<%- include('./components/_c-btn.html') %>`
# -CodeUps_1cw_sk-Vite_01
