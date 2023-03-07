# smart-contract-development
Hands-On Smart Contract Development With Solidity and Ethereum: From Fundamentals to Deployment

## 開発環境

truffleインストール
```
$ sudo npm install -g truffle
```

バージョン一覧
```
➜  greeter git:(main) truffle -v  
Truffle v5.7.9 (core: 5.7.9)
Ganache v7.7.5
Solidity - 0.8.19 (solc-js)
Node v16.16.0
Web3.js v1.8.2
```

## Greeterプロジェクト
### プロジェクト初期化
```
$ truffle init
```

### テストを実施
```
$ truffle test
```

### コントラクトのコンパイル
```
$ truffle compile
```
デフォルトの出力はbuildとなっている。

出力先を変更するには、`truffle-config.js`の`contracts_build_directory`に定義値を修正する。
```
module.exports = {
  ...
  contracts_build_directory: './client/src/contracts',
};
```

### デプロイ
`truffle-config.js`にデプロイ先を定義する。

#### ローカル環境のデプロイ
ニモニックを自動生成する場合は、パラメータなしでローカルサーバーを起動する
```
$ ganache
```
ニモニックが既にある場合は、以下のコマンドでローカルサーバーを起動する
```
$ export MNEMONIC=<YOUR MNEMONIC>
$ ganache -m $MNEMONIC
```

`truffle-config.js`の定義内容：
```
module.exports = {
    ...
    development: {
      host: '127.0.0.1', // Localhost (default: none)
      port: 8545, // Standard Ethereum port (default: none)
      network_id: '*', // Any network (default: none)
    },
    ...
};
```

ローカル環境にコントラクトをデプロイする
```
$ truffle migrate --network development
```

#### Testnetのデプロイ
`truffle-config.js`の定義内容：
```
module.exports = {
    ...
    sepolia: {
      provider: () =>
        new HDWalletProvider(
          MNEMONIC,
          `https://eth-sepolia.g.alchemy.com/v2/${PROJECT_ID}`
        ),
      network_id: '11155111',
    },
    ...
};
```

テストネットワーク環境にデプロイするには、ETHが必要となるため、
以下のサイトから少しETHをもらったからデプロイする必要がある。
https://sepolia-faucet.pk910.de/

テストネットワークにコントラクトをデプロイする
```
$ truffle migrate --network sepolia
```

### 画面で動作確認
```
$ cd client
$ npm install
$ npm start
```
