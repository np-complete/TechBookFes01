# プロジェクトを作る

少し順番がキモになってきます。

## Re:VIEWのプロジェクト作成

まずRe:VIEWのプロジェクトを作ります。

    $ review-init MyBook

`MyBook`ディレクトリといくつかのファイルが作られます。
もうこの段階で、`MyBook`ディレクトリに入り

    $ rake pdf

と叩くと`book.pdf`が作られるはずです。
上手く作られない場合はTeXのインストールが失敗している可能性が高いでしょう。

出力されたPDFにフォントが埋め込まれているか確認します。

    $ pdffonts book.pdf

`emb`の項目が`yes`になっていたらフォントが埋め込まれています。
フォント埋め込みがされていない場合、PDFを印刷する際に問題が起きる可能性があります。

## GitBook化する

`MyBook`ディレクトリで

    $ gitbook init

を実行します。`README.md`と`SUMMARY.md`が作られます。さっそく

    $ gitbook serve

でGitBookのローカルサーバを起動してみましょう。
ブラウザで`http://localhost:4000`にアクセスすると`README.md`の内容が表示されていると思います。

## gitbookからreviewの繋ぎこみをする

Re:VIEWが生成するRakefileを編集します。
具体的には[Pull Request](https://github.com/np-complete/TechBookFes01/pull/2)を見てください。

```ruby
rule '.re' => '.md' do |t|
   sh "md2review --render-link-in-footnote #{t.source} > #{t.name}
end
```

でmarkdownからreview形式[^1]に変換しています。

[^1]: 実際のPull Requestは bundle exec を使っています

もうひとつ`catalog.yml`を`SUMMARY.md`から作るタスクを追加しています。
あとがきと付録はそれぞれ`postdef-*.md`と`appendix-*.md`というファイル名を付ける前提にしています。
まえがきを`RADME.md`で代用しているのですが、場合によっては`predef-*.md`をキーワードにしてもいいでしょう。

## .gitignoreを設定する

GitBookで使うファイルは全てコミットしますが、
そこから生成されるファイルは`.gitignore`で無視するようにします。

```
_book
*.re
*.pdf
catalog.yml
```

他にもエディタの一時ファイルなども無視するようにします。

GitBook用の`.bookignore`ファイルにも同様の設定を書いておきます。

## config.yml を編集する

`config.yml`でRe:VIEWの設定を行います。
設定項目が詳しく書かれているので読みながら必要な部分を編集していきます。

必要なのは、

- `booktitle` タイトル
- `aut` 著者
- `pbl` サークル名
- `date` 発行日
- `prt` 印刷所

などです。
特に同人誌では、**出版社=サークル**ということだけはきちんと抑えておきましょう。

## GitBookに登録する

まずリポジトリをGithubにpushし、その後にGitBookのサイトで新しい本を作ります。
Github連携すると、GithubからGitBookに同期する設定ができます。
これでGithubにpushするだけで自動でGitBookで公開される本ができあがりました。

さあ準備は整いました!!
本文を書き始めましょう!!
