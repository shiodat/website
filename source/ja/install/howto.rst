インストールガイド
=================


Jubatus のインストール
----------------------

Red Hat Enterprise Linux (RHEL) 6.2 以降 (64-bit) と Ubuntu Server 12.04 LTS / 14.04  (64-bit) を公式にサポートしています。
これらのシステムでは、Jubatus のすべてのコンポーネントをバイナリパッケージでインストールすることができます。

また、その他の Linux 環境 (32-bit を含む) と Mac OS X が試験的にサポートされています。

Red Hat Enterprise Linux 6.2 以降 (64-bit)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

以下のコマンドを実行して、Jubatus の Yum リポジトリをシステムに登録します。

::

  // RHEL 6 の場合
  $ sudo rpm -Uvh http://download.jubat.us/yum/rhel/6/stable/x86_64/jubatus-release-6-2.el6.x86_64.rpm

  // RHEL 7 の場合
  $ sudo rpm -Uvh http://download.jubat.us/yum/rhel/7/stable/x86_64/jubatus-release-7-2.el7.x86_64.rpm

``jubatus`` と ``jubatus-client`` のパッケージをインストールします。

::

  $ sudo yum install jubatus jubatus-client

RHEL 6 では、依存パッケージ (``oniguruma``) のインストールに ``rhel-6-server-optional-rpms`` または ``jubatus-optional`` リポジトリを使用します。
上記の手順を実行した際、 ``oniguruma`` パッケージが存在しないエラーが表示された場合は、以下のコマンドのいずれかを実行してください。

::

  // RHEL 6 で、oniguruma パッケージが存在しない場合
  $ sudo yum --enablerepo=rhel-6-server-optional-rpms install jubatus jubatus-client

  // RHEL 6 で、oniguruma パッケージが存在しない場合 (rhel-6-server-optional-rpms が利用できない場合)
  $ sudo yum --enablerepo=jubatus-optional install jubatus jubatus-client

Ubuntu Server (64-bit)
~~~~~~~~~~~~~~~~~~~~~~

以下の行を ``/etc/apt/sources.list.d/jubatus.list`` に記述して、Jubatus の Apt リポジトリをシステムに登録します。

::

  // Ubuntu 12.04 (Precise) の場合
  deb http://download.jubat.us/apt/ubuntu/precise binary/

  // Ubuntu 14.04 (Trusty) の場合
  deb http://download.jubat.us/apt/ubuntu/trusty binary/

``jubatus`` のパッケージをインストールします。

::

  $ sudo apt-get update
  $ sudo apt-get install jubatus

現在、パッケージには GPG 署名が行われていません。
以下の警告メッセージが表示された場合は、 ``y`` を入力してください。

::

  Install these packages without verification [y/N]? y

これで、Jubatus が ``/opt/jubatus`` にインストールされました。

Jubatus を使う前に、毎回 ``profile`` スクリプトから環境変数を読み込む必要があります (``~/.bash_profile`` に追記しておくと便利です)。

::

  $ source /opt/jubatus/profile

csh または tcsh をお使いの場合は、こちらを使用してください。

::

  $ source /opt/jubatus/profile.csh

その他の Linux 環境 (32-bit を含む)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`jubatus-installer <https://github.com/jubatus/jubatus-installer>`_ を使用するか、 :doc:`build` を参照してソースからビルドしてください。

Mac OS X
~~~~~~~~~

Homebrew をお使いの場合は、 `tap リポジトリ <https://github.com/jubatus/homebrew-jubatus>`_ を使用すると簡単にインストールが行えます。

それ以外の場合は、 `jubatus-installer`_ を使用するか、 :doc:`build` を参照してソースからビルドしてください。

Jubatus クライアントのインストール
-----------------------------------

Jubatus を使ったクライアントアプリケーションは C++, Python, Ruby または Java で記述することができます。
クライアントアプリケーションから Jubatus を使うには、各言語のクライアントライブラリをインストールする必要があります。
クライアントライブラリは MIT License の下で配布されています。

:doc:`tutorial` を試す場合は、Python クライアントだけをインストールすれば十分です。

Jubatus と Jubatus クライアントのバージョンは異なることがあります。これは、Jubatus の API が変更されない場合はクライアント側のアップデートが不要なためです。

C++
~~~

クライアントは Jubatus フレームワークに含まれている (``$PREFIX/include/jubatus/client/*_client.hpp``) ため、インストールは不要です。

コンパイラや開発用のヘッダがインストールされていない場合は、以下の手順でセットアップを行ってください。
RHEL では、以下のコマンドを実行します。

::

  $ sudo yum groupinstall "Development tools" "Additional Development"

Ubuntu では、以下のコマンドを実行します。

::

  $ sudo apt-get install build-essential

Python
~~~~~~

クライアント (Python 2.6, 2.7 または 3.x が必要) は `PyPI <http://pypi.python.org/pypi/jubatus>`_ で配布されています。

::

  $ sudo pip install jubatus

``pip`` コマンドがインストールされていない場合は、以下の手順でインストールしてください。

::

  $ wget http://peak.telecommunity.com/dist/ez_setup.py
  $ sudo python ez_setup.py
  $ sudo easy_install pip

Ubuntu では ``pip`` のインストールに ``python-pip`` パッケージを利用することもできます。

Ruby
~~~~

クライアント (Ruby 1.9 以降が必要) は `RubyGems <http://rubygems.org/gems/jubatus>`_ で配布されています。

::

  $ sudo gem install jubatus

Java
~~~~

クライアントは Jubatus の Maven リポジトリで配布されています。
以下の記述をあなたのプロジェクトの ``pom.xml`` に追加してください。

.. code-block:: xml

   <repositories>
     <repository>
       <id>jubat.us</id>
       <name>Jubatus Repository for Maven</name>
       <url>http://download.jubat.us/maven</url>
     </repository>
   </repositories>

   <dependencies>
     <dependency>
       <groupId>us.jubat</groupId>
       <artifactId>jubatus</artifactId>
       <version>[0.9,)</version>
     </dependency>
   </dependencies>


Jubatus をソースからビルドする
-----------------------------------

Jubatus をソースからビルドすることは可能ですが、できる限りバイナリパッケージ (:doc:`quickstart` 参照) を使用することを推奨します。
ソースからビルドする場合は、 `jubatus-installer <https://github.com/jubatus/jubatus-installer>`_ が参考になるでしょう。

.. _requirements:

要件
~~~~

Jubatus をソースからビルドするには、 ``gcc`` (バージョン 4.4 以降), ``pkg-config`` (バージョン 0.26 以降) および ``python`` (バージョン 2.4 以降,  ``waf`` で使用される) が必要です。
加えて、以下のライブラリも必要になります。
サポートされているライブラリのバージョンについては `Jubatus Wiki <https://github.com/jubatus/jubatus/wiki/Supported-Library-Versions>`_ をご覧ください。

=================== ============== ========= ======================================================
ソフトウェア        バージョン     必須      備考
=================== ============== ========= ======================================================
jubatus_core        master         ✔
oniguruma           >= 5.9         [1]_      jubatus_core に必要。
re2                 master         [1]_      jubatus_core に必要 (``--regexp-library=re2`` ありでビルドする場合のみ)
msgpack             >= 0.5.7 [2]_  ✔         jubatus_core および jubatus に必要。
jubatus-mpio        0.4.5          ✔
jubatus-msgpack-rpc 0.4.4          ✔         C++ クライアントライブラリが必要である。
log4cxx             >= 0.10.0      ✔
mecab               >= 0.99                  ``--enable-mecab`` ありでビルドする場合のみ。
ux-trie             master                   ``--enable-ux`` ありでビルドする場合のみ。
zookeeper           >= 3.3                   ``--enable-zookeeper`` ありでビルドする場合のみ。
                                             C クライアントライブラリが必要である。
=================== ============== ========= ======================================================

.. [1] デフォルトでは oniguruma が jubatus_core の正規表現ライブラリとして使用されます (``--regexp-library=oniguruma``)。
       jubatus_core のビルド時に ``--regexp-library=none`` を指定することで正規表現機能を完全に無効にすることができます。
.. [2] MessagePack 1.x 系はサポートされていません。

お使いのディストリビューションによっては、一部のライブラリがバイナリパッケージとして提供されている場合もあります。
バイナリパッケージが利用できない場合は、これらのライブラリもソースからビルドする必要があります。以下の各サイトからダウンロードできます (
`oniguruma <https://github.com/kkos/oniguruma>`_,
`re2 <https://github.com/google/re2>`_,
`msgpack <http://msgpack.org/>`_,
`jubatus-mpio <https://github.com/jubatus/jubatus-mpio>`_,
`jubatus-msgpack-rpc <https://github.com/jubatus/jubatus-msgpack-rpc>`_,
`log4cxx <http://logging.apache.org/log4cxx/>`_,
`mecab <https://github.com/taku910/mecab>`_,
`ux-trie <https://github.com/hillbig/ux-trie>`_,
`zookeeper <http://zookeeper.apache.org/>`_
)。

Ubuntu 12.04
~~~~~~~~~~~~

Ubuntu 12.04 でのビルドを行う例です。

::

  $ sudo apt-get install build-essential git-core pkg-config

  $ sudo apt-get install libmsgpack-dev libonig-dev liblog4cxx10-dev

  $ wget http://download.jubat.us/files/source/jubatus_mpio/jubatus_mpio-0.4.1.tar.gz
  $ tar xzf jubatus_mpio-0.4.1.tar.gz
  $ cd jubatus_mpio-0.4.1
  $ ./configure
  $ make
  $ sudo make install
  $ cd ..

  $ wget http://download.jubat.us/files/source/jubatus_msgpack-rpc/jubatus_msgpack-rpc-0.4.1.tar.gz
  $ tar xzf jubatus_msgpack-rpc-0.4.1.tar.gz
  $ cd jubatus_msgpack-rpc-0.4.1
  $ ./configure
  $ make
  $ sudo make install
  $ cd ..

Jubatus のビルドを行います。

::

  $ wget -O jubatus_core.tar.gz https://github.com/jubatus/jubatus_core/archive/master.tar.gz
  $ tar xzf jubatus_core.tar.gz
  $ cd jubatus_core-master
  $ ./waf configure
  $ ./waf build
  $ sudo ./waf install
  $ sudo ldconfig

  $ wget -O jubatus-master.tar.gz https://github.com/jubatus/jubatus/archive/master.tar.gz
  $ tar xzf jubatus-master.tar.gz
  $ cd jubatus-master
  $ ./waf configure
  $ ./waf build
  $ sudo ./waf install
  $ sudo ldconfig

この例は最小限の設定でビルドしているため (どのようなオプションが利用可能かは ``./waf configure --help`` をご覧ください)、分散モードや特徴抽出プラグインなど一部の機能は利用できません。

Mac OS X
~~~~~~~~

Mac OS X では、スタンドアロンモードのビルドと実行が試験的にサポートされています。

`Homebrew tap リポジトリ <https://github.com/jubatus/homebrew-jubatus>`_ を使用すると簡単にインストールすることができます。

その他の環境
~~~~~~~~~~~~~~~~~~

- Debian GNU/Linux では動作しています。
- Arch Linux ではスタンドアローンモードで動作しています。
- 他の \*BSD systems や Solarisでの動作報告をお待ちしています。