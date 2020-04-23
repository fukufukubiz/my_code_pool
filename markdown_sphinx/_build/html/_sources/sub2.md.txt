# おまけ

## 導入検討中

- 以下のツールは便利そうだが残念...
  - Sphinxのドキュメント作成を便利にする「sphinx-quickstart-plus」を作りました (2017年03月10日)
    - <https://qiita.com/pashango2/items/512e567b328058d4107a>
      - 長らくメンテナンスされていない。最新のsphinxで試そうとすると動かない。
      - インストールコマンド実行時にエラーになる。

        ``` bash
        pip install sphinx-quickstart-plus
        ```

      - この直後にエラー発生。（エラー原因については後述）

  - markdown-preview-enhancedのマークダウンを取り込むSphinxフィルタ (2017年05月28)
    - <https://qiita.com/pashango2/items/cd78658bc16240ef23d8>
      - 長らくメンテナンスされていないようで、最新版sphinxや各種プラグインに対応できるか不明。過信はできない。

- sphinx-quickstart-plus のエラーについて
  - 動かない原因 : sphinxのディレクトリ構成が変わったため。
    - sphinx-quickstart-plus 配布先より。
      - <https://github.com/pashango2/sphinx-qsp/blob/master/sphinx_qsp/quickstart_plus.py>
      - この記述部分 : `from sphinx.quickstart import ask_user, generate, do_prompt, nonempty, boolean`
      - これが原因になっている。  
        最新のsphinxで動作させるためには  `from sphinx.cmd.quickstart ...` としないといけない。
      - エラーログの例:

          ``` bash
          $ pip install sphinx-quickstart-plus
          Collecting sphinx-quickstart-plus
          Using cached sphinx-quickstart-plus-0.6.tar.gz (5.9 kB)
              ERROR: Command errored out with exit status 1:
              ...
              File "<string>", line 1, in <module>
              File "/private/var/folders/XX/XXXXXXXXXX/T/pip-install-XXXXXX/sphinx-quickstart-plus/setup.py", line 9, in <module>
              import sphinx_qsp
              File "/private/var/folders/XX/XXXXXXXXXX/T/pip-install-XXXXXX/sphinx-quickstart-plus/sphinx_qsp/__init__.py", line 4, in <module>
              from .quickstart_plus import main, __version__
              File "/private/var/folders/XX/XXXXXXXXXX/T/pip-install-XXXXXX/sphinx-quickstart-plus/sphinx_qsp/quickstart_plus.py", line 31, 
              in <module>
              from sphinx import quickstart
              ImportError: cannot import name 'quickstart' from 'sphinx' (/XXXXXXXXXXXXXX/pythonX.X/site-packages/sphinx/__init__.py)
              ----------------------------------------
              ERROR: Command errored out with exit status 1: python setup.py egg_info Check the logs for full command output.
          ```

    - 一方、最新のsphinxでは...
      - <https://github.com/sphinx-doc/sphinx/blob/master/sphinx/cmd/quickstart.py>
        - このファイルを「sphinx-quickstart-plus」から参照しようとしているが、  
          ディレクトリ構成が`... /sphinx/cmd/quickstart.py`となっており、  
          importができない。
  - この問題について言及されているコメント。
    - <https://github.com/pashango2/sphinx-qsp/pull/14>
      - > As it's written in the code of quickstart.py.  
        > the package name has changed to sphinx.cmd.quickstart.  
        > So I just replaced the path from sphinx.quickstart to sphinx.cmd.quickstart.  

# テーマのカスタマイズ

- <http://kuttsun.blogspot.com/2016/11/sphinx-sphinxrtdtheme.html>
  - こちら参照
  - 注意点として、
    > _static/css/my_theme.css を作成します。
  - と書かれているディレクトリは、`_build/html/_static/css/my_theme.css` を指しているということ。
