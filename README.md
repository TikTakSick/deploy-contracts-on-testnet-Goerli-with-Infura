# InfuraとTruffleを用いたスマートコントラクトのデプロイ
- 下記の本で紹介されていた，Infuradでのスマートコントラクトのデプロイ方法に補足説明をする．

- [SolidityとEthereumによる実践スマートコントラクト開発 ―Truffle Suiteを用いた開発の基礎からデプロイまで \| Kevin Solorio, Randall Kanna, David H\. Hoover, 中城 元臣, 株式会社クイープ \|本 \| 通販 \| Amazon](https://www.amazon.co.jp/Solidity%E3%81%A8Ethereum%E3%81%AB%E3%82%88%E3%82%8B%E5%AE%9F%E8%B7%B5%E3%82%B9%E3%83%9E%E3%83%BC%E3%83%88%E3%82%B3%E3%83%B3%E3%83%88%E3%83%A9%E3%82%AF%E3%83%88%E9%96%8B%E7%99%BA-%E2%80%95Truffle-Suite%E3%82%92%E7%94%A8%E3%81%84%E3%81%9F%E9%96%8B%E7%99%BA%E3%81%AE%E5%9F%BA%E7%A4%8E%E3%81%8B%E3%82%89%E3%83%87%E3%83%97%E3%83%AD%E3%82%A4%E3%81%BE%E3%81%A7-Kevin-Solorio/dp/4873119340/ref=sr_1_5?__mk_ja_JP=%E3%82%AB%E3%82%BF%E3%82%AB%E3%83%8A&crid=1CG6G7UW26U5O&keywords=hands+on+smart+contracts&qid=1707793937&sprefix=hands+on+smart+contract%2Caps%2C287&sr=8-5)

## 実際のデプロイ結果
- デプロイ先のネットワーク：Goerli
- [Greeter \| Address 0x482cb785f19d9ceb19cb325973c36f70eb9d0c2c \| Etherscan](https://goerli.etherscan.io/address/0x482cb785f19d9ceb19cb325973c36f70eb9d0c2c#code)

## 補足説明

### Node.jsのバージョンに伴うエラー
ローカルマシンにインストールしたnode.jsのバージョン次第では，下記のようなエラーを起こす場合がある．
```
Error: error:0308010C:digital envelope routines::unsupported
```
truffleを用いたスマートコントラクトのデプロイを行う際は，実行時のターミナルに下記の操作を行う．
```
$ export NODE_OPTIONS=--openssl-legacy-provider
```

しかし，上記の操作の適用範囲はこれを実行したターミナルのみであるため，ターミナルを閉じるとリセットされる．
他の方法を模索している場合は，**参考**の「Error: error:0308010C:digital envelope routines::unsupportedの解決法」等参考にしていただきたい．

### MNEMONICの設定
私が使っているMac環境では，下記のように行えばうまくいった．
```
$ export MNEMONIC="bus make ... hello"
```

### Infuraの設定
- InfuraサイトURL：([Ethereum API \| IPFS API & Gateway \| ETH Nodes as a Service \| Infura](https://app.infura.io/))

教科書に書かれている内容とは異なり，API Keyを手にする．API Keyの情報の中に，英数字からなる文字列が表示される．
これを```NFURA_PROJECT_ID```として使う．

その後，繋げたいネットワークにはチェックマークをつける必要がある．
![画像1](https://github.com/TikTakSick/deploy-contracts-on-testnet-Goerli-with-Infura/assets/117717470/48f70e2a-53c3-4ef2-ac80-f0e73a6345e4)

その後，教科書に書かれているように```$ export INFURA_PROJECT_ID="edfs13~"```のように行えば良い

その後，以下のようにtruffle-config.jsを書く．


```js
  networks: {
    development: {
     host: "127.0.0.1",     // Localhost (default: none)
     port: 8545,            // Standard Ethereum port (default: none)
     network_id: "*",       // Any network (default: none)
    },
    goerli: {
      provider: () => { 
        const mnemonic = process.env["MNEMONIC"];
        const project_id = process.env["INFURA_PROJECT_ID"];
        const goerli_infura_url = "https://goerli.infura.io/v3/" + project_id;
        return new HDWalletProvider(mnemonic, goerli_infura_url);
      },
      
      network_id: 5, 
      gas: 4500000,
      gasPrice: 10000000000,
    },
  },
```

その他
- mnemonicとproject_idの設定に関して，```export ~```ではなく，truffle-config.js内に直接代入する方法でも良い．
- デプロイする際は，MetaMask等のウォレットを通して，ブロックチェーン上にスマートコントラクトをデプロイすることになり,Goerli用のETH(Ether）が必要になる．
- 私の環境では，ウォレットにETHを用意したとしてもデプロイできずにエラーが出力されたため，truffle-config.jsに関してはgasの設定をしておくべきかもしれない．


## 参考
- [【Node\.js】Error: error:0308010C:digital envelope routines::unsupportedの解決法 \#Node\.js \- Qiita](https://qiita.com/kokogento/items/f5b176d05c621223670b)

- [「SolidityとEthereumによる実践スマートコントラクト開発」を読んではまったところメモ](https://zenn.dev/kuromoka/scraps/a8cf68d4ec033e)

- [Solidity勉強メモ｜Ichiro](https://note.com/ichirotech/n/nbfab4f80be3c)
