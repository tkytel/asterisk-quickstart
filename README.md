# asterisk-quickstart

Provisioning Asterisk Private Branch Exchange

## 構築手順

1. このリポジトリを git clone します
    ```
    $ git clone https://github.com/tkytel/asterisk-quickstart
    ```
2. Tailscale の Auth key を指定します
    ```
    $ cat .env
    TS_AUTH_KEY=tskey-auth-...
    ```
3. 内線番号を 1 つ以上設定します
    * 次のファイルを参考にしてください:
        * `config/pjsip/internal/100.conf`
        * `config/extensions/telephones/100.conf`

## Appendix

* 外接
    * 他局を受け付けるための inbound trunk は設定済みです。 \
        @ `config/pjsip/internal/trunk-inbound.conf`
        * Trunk name: `SIP-TRUNK-INBOUND`
        * パスワード: `SIP-TRUNK-INBOUND`
    * host 向けに SIP や RTP 周りのポートを開けます。
        * 他のアプリケーションで当該ポートを占有しないでください。
* アプリケーション
    * デフォルトでいくつかのアプリケーションが設定されています。 \
        @ `config/extensions/applications/*.conf`
        * my117: 内線番号 117 にコールすると、時報が再生されます。
        * hello-world: 内線番号 123 にコールすると、Hello world! と話します。
