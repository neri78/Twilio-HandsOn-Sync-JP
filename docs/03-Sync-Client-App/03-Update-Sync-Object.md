#  手順3: Syncオブジェクトの情報を更新

この手順ではクライアントアプリケーションからSyncオブジェクトを更新する処理を実装します。この処理により同じオブジェクトの購読を実施しているアプリケーションに同じ情報を送信できるようになります。

## 3-1. メッセージ送信の仕組みを実装

続けて`sync.js`ファイルを開き、`alertForm.addEventListener('submit', async (event) => { });`の中身を実装します。

このイベントリスナーでは、HTML要素から入力された値を取得し、Syncオブジェクトを更新します。

```js
alertForm.addEventListener('submit', async (event) => {
    event.preventDefault();

    // 情報の種類ならびにメッセージ内容を取得
    const submitId = event.submitter.id;
    const message = messageField.value;

    // Syncクライアントを使用し、同期するデータを更新
    syncClinet.document('Message')
        .then((document) => {
            document.update({
                messageType: submitId,
                message: message
            });
        });
});
```

## 3-2. 最終デプロイを実施し、アプリケーションの動作を確認

最終デプロイを実行し、複数タブでアプリケーションを起動します。1つのクライアントアプリケーションから発行したメッセージが他のアプリケーションにも反映されていることを確認してください。

## 次のステップ

これで基本的なSyncの処理を実装できました。このようにSyncを利用し複数の端末で同じ情報を共有できるようになります。

実開発においては、下記のリソースも参考にしてください。
- [Syncオブジェクトの生存期間（英語）](https://jp.twilio.com/docs/sync/objects-ttl)
- [Syncの制限（英語）](https://jp.twilio.com/docs/sync/limits)
- [Syncのセキュリティ（英語）](https://jp.twilio.com/docs/sync/permissions-and-access-control)