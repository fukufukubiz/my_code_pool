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
