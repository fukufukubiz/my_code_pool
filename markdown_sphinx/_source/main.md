# Markdown to Sphinx(reST)

本書は、MarkdownでSphinxドキュメントを生成する方法についてまとめたものである。  

本来はreSTという独自の記述方式を用いる必要があるが、  
reSTを新たに覚えるのが面倒になる。  

そこで、広く普及しているMarkdownで記述できたら便利だろう、  
ということでその手法をまとめてみた。

## 参考サイト

- Sphinxを便利にして、みんなに使ってもらいたい (2017年03月06日)
  - <https://qiita.com/pashango2/items/d1b379b699af85b529ce>

- Sphinxでblockdiagを使って簡単にシーケンス図、ブロック図を含めたHTMLベースのドキュメントを生成する環境を整える (2016年03月02日)
  - <https://qiita.com/yamionp/items/8f8d52d6b41bf9d4d16d>

- 化学系のための Sphinx の文章作成マニュアル (2017)
  - <https://www1.gifu-u.ac.jp/~fujilab/sphinx_html/index.html>

- aSphinx から完全に reStructuredText を追い出した話 (2016-12-29)
  - <https://tk0miya.hatenablog.com/entry/2016/12/29/232900>

``` eval_rst
.. note:: Googleで検索して出てくるsphinx関係のまとめ記事が軒並み古いため、現時点(2020/4)でも通用するのかを確認して、最新情報を残す意味も込めてまとめてみた。
```

## インストール

### 前提

- python3.x系が入っている事

### Sphinx

- インストールコマンド

``` bash
pip install Sphinx commonmark recommonmark
```

### 拡張機能系

#### sphinxcontrib-toc

- <https://tk0miya.hatenablog.com/entry/2016/12/29/232900>
  - ドキュメント構造(toctree)を reST で書かなくても良くするプラグイン
  - これによって完全に reST を書かなくてもよい仕組みになる

- インストールコマンド
  
  ``` bash
  pip install sphinxcontrib-toc
  ```

- config(conf.py)の書き方
  - 後述

- 使い方
  - index.toc というファイルを新規作成する。
  - ドキュメントを構成するファイル(markdownファイル名)を列挙する。(拡張子は不要)

    ``` text
    chapter1
    chapter2
    chapter3
    ```

#### blockdiag

- <http://blockdiag.com/ja/blockdiag/index.html>
  - UMLを書くためのプラグイン

- インストールコマンド
  
    ``` bash
    pip install sphinxcontrib-actdiag sphinxcontrib-blockdiag sphinxcontrib-nwdiag sphinxcontrib-seqdiag
    ```

- config(conf.py)の書き方
  - 後述

    ``` python
    extensions = [
        'sphinxcontrib.blockdiag',
        'sphinxcontrib.seqdiag',
        'sphinxcontrib.actdiag',
        'sphinxcontrib.nwdiag',
        'sphinxcontrib.rackdiag',
        'sphinxcontrib.packetdiag',
    ]

    blockdiag_html_image_format = 'SVG'
    seqdiag_html_image_format = 'SVG'
    actdiag_html_image_format = 'SVG'
    nwdiag_html_image_format = 'SVG'
    rackiag_html_image_format = 'SVG'
    packetdiag_html_image_format = 'SVG'
    ```

### テーマ

- 定番のsphinxテーマ
  - sphinx_rtd_theme
    - <https://sphinx-themes.org/html/sphinx_rtd_theme/sphinx_rtd_theme/index.html>

- インストールコマンド
  
``` bash
pip install sphinx_rtd_theme
```

- config(conf.py)の書き方
  - 後述

## ドキュメント生成手順

``` eval_rst
.. note:: 以下の手順を踏む事で、必要なフォルダ構成、ファイル類が生成される。ここで生成される conf.py を後ほど編集して環境を整えていく。
```

- フォルダを作成する
- フォルダに移動する
- ターミナルを起動する
- 以下のコマンド実行する
  
    ``` bash
    sphinx-quickstart
    ```

- 以下の内容が対話式で聞かれる

    ``` text
    Sphinx X.X.X クイックスタートユーティリティへようこそ。

    以下の設定値を入力してください（Enter キーのみ押した場合、
    かっこで囲まれた値をデフォルト値として受け入れます）。

    選択されたルートパス: .

    Sphinx 出力用のビルドディレクトリを配置する方法は2つあります。
    ルートパス内にある "_build" ディレクトリを使うか、
    ルートパス内に "source" と "build" ディレクトリを分ける方法です。
    > ソースディレクトリとビルドディレクトリを分ける（y / n） [n]:

    プロジェクト名は、ビルドされたドキュメントのいくつかの場所にあります。
    > プロジェクト名:
    * 何か入力してください。
    > プロジェクト名: test_pj
    > 著者名（複数可）: me
    > プロジェクトのリリース []:

    If the documents are to be written in a language other than English,
    you can select a language here by its language code. Sphinx will then
    translate text that it generates into that language.

    For a list of supported codes, see
    https://www.sphinx-doc.org/en/master/usage/configuration.html#confval-language.
    > プロジェクトの言語 [en]: ja

    ファイル ./conf.py を作成しています。
    ファイル ./index.rst を作成しています。
    ファイル ./Makefile を作成しています。
    ファイル ./make.bat を作成しています。

    終了：初期レクトリ構造が作成されました。

    マスターファイル ./index.rst を作成して
    他のドキュメントソースファイルを作成します。次のように Makefile を使ってドキュメントを作成します。
    make builder
    "builder" はサポートされているビルダーの 1 つです。 例: html, latex, または linkcheck。
    ```

``` eval_rst
.. note:: プロジェクト名、著者名は必須入力。
```

- ディレクトリの中を確認する。

    ``` bash
    $ ls -ltra
    total 32
    drwxr-xr-x  7 user  group   224  4 22 00:06 ..
    drwxr-xr-x  2 user  group    64  4 22 00:11 _build
    drwxr-xr-x  2 user  group    64  4 22 00:11 _templates
    drwxr-xr-x  2 user  group    64  4 22 00:11 _static
    -rw-r--r--  1 user  group  2107  4 22 00:11 conf.py
    -rw-r--r--  1 user  group   437  4 22 00:11 index.rst
    -rw-r--r--  1 user  group   634  4 22 00:11 Makefile
    drwxr-xr-x  9 user  group   288  4 22 00:11 .
    -rw-r--r--  1 user  group   795  4 22 00:11 make.bat
    ```

- conf.pyを編集する。
  - 編集方法は後述。
- 文章を書きたいmarkdownファイルを生成する。
  - ex : main.md , sub.md
- index.toc ファイルを生成する。
  - 作成したmarkdownファイル名（拡張子なし）を列挙する。
    - ex :

        ``` text
        main
        sub
        ```

- markdownファイルを編集する。
- ビルドをする。

  ``` bash
  make html
  ```

- ビルド完了後、以下を参照する。
  - [現在のフォルダ]/_build/html/index.html

## ドキュメントの自動生成

- 上記の手順では、markdownを修正する度に手動で `make html` を実行する必要がある。
- そこで、次のプラグインを使用して自動ビルドできるようにする。

### sphinx-autobuild

- インストールコマンド

``` bash
pip install sphinx-autobuild
```

- ビルドコマンド

``` bash
sphinx-autobuild  <ソースディレクトリ> <ビルド成果物出力ディレクトリ>
```

- 例

``` bash
sphinx-autobuild ./ ./sq/_build/html/index.html
```

- 上記でも良いが、さらに楽するには、Makefileを編集する。
- Makefileの末尾に以下を追記する。

``` text
livehtml:
    sphinx-autobuild -b html $(ALLSPHINXOPTS) $(BUILDDIR)/html
```

- 以下のコマンドを入力する

``` bash
make livehtml
```

``` eval_rst
.. note:: 常時監視状態になるためターミナルがフォアグラウンド状態になる。抜けたい場合は手動で停止(control + c)すること。
```

## conf.py の編集

- 「ドキュメント生成手順」で生成された conf.py を開き、以下の記述を探して修正する。
  - before

    ``` text
    extensions = [
    ]
    ```

  - after

    ``` text
    extensions = [
    'sphinxcontrib.toc',
    'sphinxcontrib.blockdiag',
    'sphinxcontrib.seqdiag',
    'sphinxcontrib.actdiag',
    'sphinxcontrib.nwdiag',
    'sphinxcontrib.rackdiag',
    'sphinxcontrib.packetdiag',
    ]
    ```

  - before

    ``` text
    html_theme = 'alabaster'
    ```

  - after

    ``` text
    html_theme = "sphinx_rtd_theme"
    html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]
    ```

  - before

    ``` text
    copyright = '2020, XXXXX'
    ```

  - after

    ``` text
    copyright = '{year}, XXXXX.'.format(year=datetime.datetime.now().year)
    ```

- conf.py に以下の記述を冒頭に記述する。
  - 「# -- Path setup 」と書かれたコメントを探し、そのエリアに記述すると良い。
  - conf.py の冒頭に以下の記述がある。

      ``` python
      # -- Path setup

      ...

      # import os
      # import sys
      # sys.path.insert(0, os.path.abspath('.'))
      ```

  - この記述の直後に以下を追記する。

      ``` python
      from recommonmark.parser import CommonMarkParser
      from recommonmark.transform import AutoStructify
      import sphinx_rtd_theme
      import os
      import datetime
      ```

- conf.py の末尾に、以下の記述を追記する。

  ``` text
  source_suffix = ['.md']
  source_parsers = {
      '.md': CommonMarkParser,
  }

  blockdiag_html_image_format = 'SVG'
  seqdiag_html_image_format = 'SVG'
  actdiag_html_image_format = 'SVG'
  nwdiag_html_image_format = 'SVG'
  rackiag_html_image_format = 'SVG'
  packetdiag_html_image_format = 'SVG'

  copyright = '{year}, edX Inc.'.format(year=datetime.datetime.now().year)

  github_doc_root = 'https://github.com/rtfd/recommonmark/tree/master/doc/'
  def setup(app):
      app.add_config_value('recommonmark_config', {
              'url_resolver': lambda url: github_doc_root + url,
              'auto_toc_tree_section': 'Contents',
              }, True)
      app.add_transform(AutoStructify)
  ```

- 補足
  - AutoStructifyコンポーネント : マークダウンからreStructuredTextの様々な拡張が使えるようになる
    - できるようになること
      - toctree生成
      - 他文書のリンク
      - 数式 / インライン数式1
      - reStructuredTextの埋め込み

# Markdown to Sphinx 記述例

## toctree生成 / 他ドキュメントへのリンク

- [Title1](sub1.md)
- [Title2](sub2.md)

[Title1](sub1.md)

## math

- <https://www.sphinx-doc.org/ja/1.6/ext/math.html#math-support>

``` text
    ``` math
    E = m c^2
    ```
```

``` math
E = m c^2
```

``` text
    ``` math
    (a - b)^2 = a^2 - 2ab + b^2
    ```
```

``` math
(a - b)^2 = a^2 - 2ab + b^2
```

``` text
    ``` math
    e^{i\pi} + 1 = 0
    ```
```

``` math
e^{i\pi} + 1 = 0
```

``` text
    ``` eval_rst
    .. math::
        (a + b)^2 &= (a + b)(a + b) \\
                &= a^2 + 2ab + b^2
    ```
```

``` eval_rst
.. math::
    (a + b)^2 &= (a + b)(a + b) \\
              &= a^2 + 2ab + b^2
```

## 原子記号

``` text
    ``` eval_rst
    H
    :subscript:`2`
    O
    ```
```

``` eval_rst
H
:subscript:`2`
O
```

## Commonmarkの表

``` text
    ``` eval_rst
    =====  =====  =======
    A      B      A and B
    =====  =====  =======
    False  False  False
    True   False  False
    False  True   False
    True   True   True
    =====  =====  =======
    ```
```

``` eval_rst
=====  =====  =======
A      B      A and B
=====  =====  =======
False  False  False
True   False  False
False  True   False
True   True   True
=====  =====  =======
```

### 【参考】 markdown表記の場合

``` text
|A     | B     |A and B|
|------|-------|-------|
|False |False  |False  |
|True  |False  |False  |
|False |True   |False  |
|True  |True   |True   |
```

- ただし markdown -> sphinxの場合は、  
  従来のmarkdownの表が正しく出力さない。

|A     | B     |A and B|
|------|-------|-------|
|False |False  |False  |
|True  |False  |False  |
|False |True   |False  |
|True  |True   |True   |

- このように崩れてしまう...

## 注釈など

- markdownにはなく、reSTでしか表現できないもの

``` text
    ``` eval_rst
    .. seealso:: This is a simple **seealso** note  
    ```
```

``` eval_rst
.. seealso:: This is a simple **seealso** note  
```

``` text
    ``` eval_rst
    .. note:: note that ...
    ```
```

``` eval_rst
.. note:: note that ...
```

``` text
    ``` eval_rst
    .. warning:: be careful not to ...
    ```
```

``` eval_rst
.. warning:: be careful not to ...
```

``` text
    ``` important:: Its a note! in markdown!
    ```
```

``` important:: Its a note! in markdown!
```

## UML

- blockdiag

``` text
    ``` eval_rst
    .. blockdiag::

        blockdiag {
        A -> B -> C;
        A -> E -> F;
        }
    ```
```

``` eval_rst
.. blockdiag::

    blockdiag {
       A -> B -> C;
       A -> E -> F;
    }
```

### 【参考】 UML - mermaid.js

- mermaid.js
  - mermaid.jsを用いて図を作成、埋め込みたい場合は、別markdownで記載して画像などで出力してから
    画像として埋め込むことをお勧めする
  - markdownでmermaid.js
    - <https://qiita.com/t_o_d/items/ac5b04419252f768a535>

## 注意

以下の記述はエラーを招く

- インライン数式

``` text
`$ y=\sum_{i=1}^n g(x_i) $`
```

この記述を含んだ状態で make html を実行すると以下のようなエラーが出る

``` bash
例外が発生しました
  File "/XXXXXXX/lib/pythonX.X/site-packages/docutils/parsers/rst/roles.py", line 361, in math_role
    text = rawtext.split('`')[1]
IndexError: list index out of range
完全なトレースバックを/var/folders/n8/XXXXXXXXXX/T/sphinx-err-XXXXXX.logに保存しました。問題を開発者に報告するときに添付してください。
次期バージョンでのエラーメッセージ改善のために、ユーザーエラーの場合にも報告してください。
バグ報告はこちらにお願いします <https://github.com/sphinx-doc/sphinx/issues> 。ご協力ありがとうございます！
make: *** [html] Error 2
```

``` bash
cat /var/folders/n8/XXXXXXXXXX/T/sphinx-err-XXXXXX.log
```

``` text
Traceback (most recent call last):
 File "/XXXXXXX/lib/pythonX.X/site-packages/sphinx/cmd/build.py", line 276, in build_main

...

 File "/XXXXXXX/lib/pythonX.X/site-packages/docutils/parsers/rst/roles.py", line 361, in math_role
    text = rawtext.split('`')[1]
IndexError: list index out of range
```

- 原因
  - 詳細は不明だが、バージョンによる問題もありそう
  - 以下参考
    - <https://github.com/readthedocs/recommonmark/issues/120>
