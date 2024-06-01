# この記事は何か

エンジニアをやっていると何かしらのエラーに遭遇することは避けられないでしょう。この記事では

- エンジニアになって日が浅い
- エラーに対して忌避感がある

といった方々に向けてエラーへの向き合い方のヒントを提示します。この記事を読んで少しでもエラーに対しての苦手意識が薄まったり、エラーを通じて自己成長につながれば嬉しく思います。

# エラーを解決するための行動(基礎編)

ここではエラーを解決するための具体的な行動についていくつか紹介します。これらの行動は必ずしも順番通りに取ることを意図していません。ただし「エラーメッセージを特定する」に関してはまず最初に行うのが普通です。何が起きているか分からなければ意味について考えることも、適切な方法で調べることもできないでしょう。これらの行動は手札としてストックしておき、状況や自身の好みに合わせて使ってみましょう。

## エラーメッセージを特定する

例えばJavaScriptで書かれたプログラムについて考えてみましょう。

※このプログラムはChatGPTが生成しました

```index.js
const axios = require('axios');

// 取得したいURLを指定
const url = 'https://jsonplaceholder.typicode.com/posts/1';

axios.get(url)
  .then(response => {
    // レスポンスデータをコンソールに表示
    console.log('データを取得しました:', response.data);
  })
  .catch(error => {
    // エラーメッセージをコンソールに表示
    console.error('エラーが発生しました:', error);
  });
```

プログラムを実行してみましょう。

```sh
$ node index.js
node:internal/modules/cjs/loader:1145
  throw err;
  ^

Error: Cannot find module 'axios'
Require stack:
- /home/***/work/tmp/index.js
    at Module._resolveFilename (node:internal/modules/cjs/loader:1142:15)
    at Module._load (node:internal/modules/cjs/loader:983:27)
    at Module.require (node:internal/modules/cjs/loader:1230:19)
    at require (node:internal/modules/helpers:179:18)
    at Object.<anonymous> (/home/***/work/tmp/index.js:1:15)
    at Module._compile (node:internal/modules/cjs/loader:1368:14)
    at Module._extensions..js (node:internal/modules/cjs/loader:1426:10)
    at Module.load (node:internal/modules/cjs/loader:1205:32)
    at Module._load (node:internal/modules/cjs/loader:1021:12)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:142:12) {
  code: 'MODULE_NOT_FOUND',
  requireStack: [ '/home/***/work/tmp/index.js' ]
}

Node.js v21.7.3
```

エラーが出ましたね。たくさん文字が書いていますが、それぞれが何を表しているのかコメントを追加してみました。

※ここでのコメントはNode.jsのコードを読んで調べながら書きましたが、厳密性を欠いている可能性があります

```sh
# エラーが出た箇所
node:internal/modules/cjs/loader:1145
  throw err;
  ^

# エラーメッセージ(!)
# 最も重要な部分の一つです
Error: Cannot find module 'axios'
# スタックトレース
# プログラムが実行されてからどこを辿ってエラーに帰着したか
Require stack:
- /home/***/work/tmp/index.js
    at Module._resolveFilename (node:internal/modules/cjs/loader:1142:15)
    at Module._load (node:internal/modules/cjs/loader:983:27)
    at Module.require (node:internal/modules/cjs/loader:1230:19)
    at require (node:internal/modules/helpers:179:18)
    at Object.<anonymous> (/home/***/work/tmp/index.js:1:15)
    at Module._compile (node:internal/modules/cjs/loader:1368:14)
    at Module._extensions..js (node:internal/modules/cjs/loader:1426:10)
    at Module.load (node:internal/modules/cjs/loader:1205:32)
    at Module._load (node:internal/modules/cjs/loader:1021:12)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:142:12) {
  # エラーコード
  code: 'MODULE_NOT_FOUND',
  # エラーが出たファイルに至った経路
  # 配列中の一番最初の要素が犯人
  requireStack: [ '/home/***/work/tmp/index.js' ]
}

Node.js vXX.X.X
```

少し解像度が上がったでしょうか？このようにエラーは多くの場合、

- サマリ（何が起きたかを端的に表す文章や識別子）
- 補足情報

を含んでいます。このうち最も注目すべきは何が起こったかを端的に表す**エラーメッセージ**や**エラーコード**です。多くの補足情報や英語に圧倒されて混乱してしまうかもしれませんが、要点を抑えておけば読み解けるエラーはかなり増えるでしょう。ここではNode.jsの `MODULE_NOT_FOUND` を例に紹介しましたが、経験則では大方のプログラムはだいたい前述の「サマリ&補足情報」のパターンに該当します。

## 意味について考える

## インターネットで調べる

## デバッグする

## 助けを求める

# エラーを解決するための行動(発展編)

## 報告する

https://github.com/carrierwaveuploader/carrierwave/issues/2608

## 自分で直す

https://github.com/carrierwaveuploader/carrierwave/pull/2613

# 最後に

これまで紹介してきた通りエラーを通じて、自身のスキルアップやコミュニティへの貢献に繋げられる可能性があります。エンジニアである以上エラーは避けて通れないため、学びの機会と前向きに捉えた方が豊かな時間を過ごせると私は考えます。この記事を読んだ皆さんがエラーに対して少しでも前向きな気持ちで向き合えるようになることを切に願っています。

# おまけ

## エラー解決フローチャートを作る

今回紹介した方法を実際に使いながらフローチャートを作って（あるいは意識して）みることもオススメです。エラーに未だ苦手意識がある人にとっては特に良いかもしれません。エラーに特化した話題ではありませんが、以下の記事が参考になるでしょう。私は以下で紹介されている「不安の決定木」に近い意識を常日頃持っています。エラーに限らない人生の広い問題に役立つテクニックです。

https://note.com/xtakayasux/n/n7c72a8842a36

## AIの活用について

エラー解決に際して私自身がほとんどと言ってよいほどAIを活用することが無いため書きませんでした。こんなプロンプトを書くと良い感じに教えてくれる、などありましたらむしろ私に教えてください！

## OSSへの貢献について

今回はエラーにフォーカスしたためあまり詳しく紹介しませんでしたが、このテーマだけでまた一つ記事が書けてしまいます。貢献の手段や作法、心構えなど大事なことは多いです。もし詳しく知りたければ自分で調べるなり、私に聞くなりしてみてください！もしリクエストがあれば今回のような記事を書くことがあるかもしれません。
