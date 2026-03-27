# asterisk-quickstart

Provisioning Asterisk Private Branch Exchange

## 構築手順

1. このリポジトリを git clone します
    ```
    $ git clone https://github.com/tkytel/asterisk-quickstart
    ```
2. 内線番号を 1 つ以上設定します
    * 次のファイルを参考にしてください:
        * `config/pjsip/internal/` 配下の例示ファイル
        * `config/extensions/telephones` 配下の例示ファイル
3. (任意) 外部プロバイダを 1 つ以上設定します
    * 次のファイルを参考にしてください:
        * `config/pjsip/external/example-tel.conf.example`
        * `config/extensions/external/example-tel.conf.example`

## Appendix

* 外接
    * 他局を受け付けるための inbound trunk は設定済みです。 \
        @ `config/pjsip/internal/trunk-inbound.conf`
        * Trunk name: `SIP-TRUNK-INBOUND`
        * パスワード: `SIP-TRUNK-INBOUND`
    * host 向けに SIP や RTP 周りのポートを開けます。
        * 他のアプリケーションで当該ポートを占有しないでください。
    * 局間ホップに対応済みです。
* アプリケーション
    * デフォルトでいくつかのアプリケーションが設定されています。 \
        @ `config/extensions/applications/*.conf`
        * my117: 内線番号 117 にコールすると、時報が再生されます。
        * hello-world: 内線番号 123 にコールすると、Hello world! と話します。
        * milliwatt: 1000 Hz tone を再生します。回線品質の劣化等を確認できます。
        * reads-back-number: 数秒間ダイヤルトーンを受け付け、聞き取った番号を読み上げます。
        * receive-fax: Fax を受信して、サーバに保存します。
        * echo-test: オウム返しします。
        * conference: 会議室を提供します。
* アップデート
    * このリポジトリの更新を取り入れるには、以下のようにしてください。
        ```
        $ git stash # ローカルの変更を、一旦棚に上げる
        $ git pull
        $ git stash pop # 棚上げした変更を戻す
        $ docker compose pull && docker compose up -d --remove-orphans # 最新のイメージで再起動する
        ```
