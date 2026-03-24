# asterisk-quickstart

Provisioning Asterisk Private Branch Exchange

## 設定

* 構築
    * Docker Compose を用いてプロビジョニングされることを想定しています。
        ```
        $ docker compose up -d
        ```
* 外接
    * 他局を受け付けるための inbound trunk は設定済みです。 \
        @ `config/pjsip/internal/trunk-inbound.conf`
        * Trunk name: `SIP-TRUNK-INBOUND`
        * パスワード: (適宜更新してください)
    * Tailscale を sidecar container としています。
        * `.env` 内で下記のように Tailscale の Auth key を指定してください。
            ```
            TS_AUTH_KEY=tskey-auth-...
            ```
    * host 向けに SIP や RTP 周りのポートを開けます。
        * 他のアプリケーションで当該ポートを占有しないでください。
* アプリケーション
    * デフォルトでいくつかのアプリケーションが設定されています。 \
        @ `config/extensions/applications/*.conf`
        * my117: 内線番号 117 にコールすると、時報が再生されます。
        * hello-world: 内線番号 123 にコールすると、Hello world! と話します。
* 内線
    * 基本的に 2 つのファイルを追加するだけで、局に収容する電話機を増設できます。
    * 次のファイルを参考にしてください:
        * `config/pjsip/internal/100.conf`
        * `config/extensions/telephones/100.conf`
