# 動画眼Lite
ユーザーテストやインタビューの動画を効率的に見返すためのインデックスツール「[動画眼3](https://github.com/do-gugan/do-gagan_electron)」の簡易ビューワー動作を
HTML/JavaScriptのみで実現する。

動画ファイルと、動画眼でエキスポートしたデータファイルと一緒に、本HTMLファイルを同梱しておけば、動画眼のインストール無しで、ブラウザのみで頭出し再生が行えます。

## 暫定マニュアル
### 配布方法
動画「hoge.mp4」があるフォルダに、データファイル「hoge.json.js」と本ページからダウンロードしたindex.htmlを「hoge.mp4」にリネームして保存します（つまり、**3つのファイルが拡張子違いで同じフォルだに存在する状態**になります）。Webサーバーに置いても良し、PCのローカルストレージ（HDD/SSD）に置いても良しです。ローカルストレージの場合はhtmlファイルを開けば標準ブラウザで開かれると思います。
データファイルはWindowsアプリ「動画眼2」（v2.4以降）にて出力します。
### 操作方法
- スペースキーで再生と一時停止をトグルで切り替えます
- Wキーで指定秒数先へ進みます。
- Qキーで指定秒数前に戻ります。
  - 検索欄にフォーカスがあると、これらのキーは文字入力に使われショートカットは発動しません。代わりにAlt+S/W/Qが使えます。
- スキップする秒数は画面上のプルダウンメニューで指定します（進むと戻るで個別に指定可能）。
- 右サイドのリストから閲覧したいメモ／発話をクリックすると当該再生位置にジャンプします。
- 右上のテキストボックスに文字を入力するとそれを含む発話メモを検索できます。
  - 検索結果の表示方法として「抽出」と「強調」があります。
  - 「抽出」は、検索語を含まない発話メモを非表示にします（いわゆる絞り込み）。
  - 「強調」は、検索語を含む発話に色付けして目立たせます。
### 制限事項
- 主にChromium Edgeで開発、動作検証しています。Chromeは基本的に同じ結果が得られるはずです。FireFoxやSafariでも簡単にチェックはしていますが、もし不具合があればIssuesに報告いただければと思います。
- ビューワーであるため、メモの追加や編集はできません。

### データフォーマット
- サンプルは[こちら](sample.json.js)
- HTMLファイルに無操作で読み込むため、外部jsファイルの体をとり、内部でJSON形式のオブジェクトを生成しています。
- 先頭の「const scriptsJson = [」と最終行の「];」は変更しないでください。
- 1つのレコードは{}で囲み、最後の1つ以外は行末に,（半角カンマ）を打ちます。最後のレコードの後は,があるとエラーになります。
- inは開始点で、動画の先頭を0として秒数で表します。
- sctiptが発話内容。途中に改行を含むことはできません。
- speakerは話者コード。一人目が0、二人目が1、三人目が2...としておくと、画面上で色分け表示されます。
