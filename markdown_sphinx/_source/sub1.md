# その他の拡張機能

## Jupyter notebook 連携

- <https://nbsphinx.readthedocs.io/en/0.6.1/>
- <https://www1.gifu-u.ac.jp/~fujilab/sphinx_html/install.html>

- インストールコマンド
  
``` bash
sudo apt-get install pandoc
pip install nbsphinx
```

- config(conf.py)の書き方

``` python
# for jupyter-notebook

from recommonmark.parser import CommonMarkParser

source_parsers = {
    '.md': CommonMarkParser,
}

from recommonmark.transform import AutoStructify

github_doc_root = 'https://github.com/rtfd/recommonmark/tree/master/doc/'
def setup(app):
    app.add_config_value('recommonmark_config', {
            'url_resolver': lambda url: github_doc_root + url,
            'auto_toc_tree_section': 'Contents',
            }, True)
    app.add_transform(AutoStructify)
```

- index.tocに「jupyter-notbook のファイル名」を入れておく

# その他のテーマ

「sphinx_rtd_theme」より使いやすいテーマがあるのか...

## edx-sphinx-theme

- <https://sphinx-themes.org/html/edx-sphinx-theme/edx_theme/basic.html>
  - 使い勝手は「sphinx_rtd_theme」と同様
  - オススメ

- インストールコマンド

``` bash
pip install edx-sphinx-theme
```

- conf.pyの書き方

``` python
import edx_theme

extensions += ['edx_theme']

copyright = '{year}, edX Inc.'.format(year=datetime.datetime.now().year)
author = edx_theme.AUTHOR

html_theme = 'edx_theme'
html_theme_path = [edx_theme.get_html_theme_path()]
html_favicon = os.path.join(html_theme_path[0], 'edx_theme', 'static', 'css', 'favicon.ico')

master_doc = 'index'
latex_documents = [
    (master_doc, 'edx-sphinx-theme.tex', 'edx-sphinx-theme Documentation',
     author, 'manual'),
]
```

## groundwork-sphinx-theme

- <https://sphinx-themes.org/html/groundwork-sphinx-theme/groundwork/index.html>
  - ダークなテーマ
  - コードブロック内の文字の色が、シンタックスハイライトによっては真っ暗になり見づらくなる。
  - かっこいいが、使い方を選ぶ
  - あまりオススメではない

- インストールコマンド

``` bash
pip install groundwork-sphinx-theme
```

- conf.pyの書き方

``` python
html_theme = 'groundwork'

html_theme_options = {
    "sidebar_width": '240px',
    "stickysidebar": True,
    "stickysidebarscrollable": True,
    "contribute": True,
    "github_fork": "useblocks/groundwork",
    "github_user": "useblocks",
}
```

## mozilla-sphinx-theme

- <https://sphinx-themes.org/html/mozilla-sphinx-theme/mozilla/index.html>
  - シンプルでいい配色ではあるが...
  - サイドバーの目次一覧の表記がおかしい
    - ネストが深くなると縦文字になってしまう
  - あまりオススメではない

- インストールコマンド

``` bash
pip install mozilla-sphinx-theme
```

- conf.pyの書き方

``` python
import mozilla_sphinx_theme
import os

html_theme_path = [os.path.dirname(mozilla_sphinx_theme.__file__)]

html_theme = 'mozilla'
```

## msmb_theme

- <https://sphinx-themes.org/html/msmb_theme/msmb_theme/index.html>
  - 使い勝手は「sphinx_rtd_theme」と同様
  - 白黒のためややシンプル過ぎる印象
  - オススメ？

- インストールコマンド

``` bash
pip install msmb_theme
```

- conf.pyの書き方

``` python
html_theme = 'msmb_theme'
import msmb_theme
html_theme_path = [msmb_theme.get_html_theme_path()]
```

## rtcat-sphinx-theme

- <https://sphinx-themes.org/html/rtcat-sphinx-theme/rtcat_sphinx_theme/index.html>
  - 使い勝手は「sphinx_rtd_theme」と同様
  - 「sphinx_rtd_theme」をちょっとかっこ良くした感じの配色
  - オススメ

- インストールコマンド

``` bash
pip install rtcat-sphinx-theme
```

- conf.pyの書き方

``` python
import rtcat_sphinx_theme

html_theme = "rtcat_sphinx_theme"

html_theme_path = [rtcat_sphinx_theme.get_html_theme_path()]
```

## sphinx-ustack-theme

- <https://sphinx-themes.org/html/sphinx-ustack-theme/sphinx_ustack_theme/index.html>
  - 青緑な感じの色
  - 配色はいいが、章番号の数字表記が小さくなってしまう...
  - 色合いが良いだけに、惜しい

- インストールコマンド

``` bash
pip install sphinx-ustack-theme
```

- conf.pyの書き方

``` python
html_theme = 'sphinx_ustack_theme'
```

## PSphinxTheme

- <https://sphinx-themes.org/html/PSphinxTheme/p-greenblue/index.html>
  - 割と良い
  - 3色の使い分けができる
    - 赤、緑、青
  - サイドバーを隠すことができる
  - サイドバーの伸縮ができる
  - 割と良いが... 検索ボタンの「検索」の文字が見切れている
  - 非常に惜しい...

- インストールコマンド

``` bash
pip install PSphinxTheme
```

- conf.pyの書き方

``` python
html_theme = 'p-greenblue'
import os
from PSphinxTheme import utils

p, html_theme, needs_sphinx = utils.set_psphinxtheme(html_theme)
html_theme_path = p
```

- 色を変えたい場合はここを変える
  - `html_theme = 'p-main_theme'`
  - `html_theme = 'p-red'`

## sphinx_theme_pd

- <https://sphinx-themes.org/html/sphinx_theme_pd/sphinx_theme_pd/index.html>
  - 配色はいい
  - インデックスが右に表示される
  - インデックス欄が短く、改行がやや見づらい
  - ちょっとオススメ

- インストールコマンド

``` bash
pip install sphinx_theme_pd
```

- conf.pyの書き方

``` python
html_theme = 'sphinx_theme_pd'
import sphinx_theme_pd
html_theme_path = [sphinx_theme_pd.get_html_theme_path()]
```
