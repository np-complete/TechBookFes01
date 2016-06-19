# セットアップ

必要なコンピュータの要件は、

- **Git**が動くこと
- **Node.js**が動くこと
- **Ruby**が動くこと
- **TeX**が動くこと
- **emacs**という素晴らしいエディタが動くこと

だけです。
基本的にはどのご家庭にもある**Linux**マシンを使えばよいのですが、
もしかしたら一部のゲーミングOS(windowsなど)でも動くかもしれません。

### gitbookのインストール

    $ npm install gitbook-cli

でgitbookコマンドをインストールします。

### reviewのインストール

    $ gem install review md2review

でRe:VIEW関連のコマンドをインストールします。

### texのインストール

ちょっとした地獄です。

    $ sudo apt-get install texlive texlive-lang-japanese texlive-latex-extra xzdec

でいろいろ入ります。

一番肝心な日本語フォントの設定をします。

    $ kanji-config-updmap auto

これでセットアップはできているはずです[^1]。

[^1]: 正直TeXのインストールに自信ない
