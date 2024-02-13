# InfuraとTruffleを用いたスマートコントラクトのデプロイ
- 下記の本で紹介されていた，Infuradでのスマートコントラクトのデプロイ方法に補足説明をします．

- [SolidityとEthereumによる実践スマートコントラクト開発 ―Truffle Suiteを用いた開発の基礎からデプロイまで \| Kevin Solorio, Randall Kanna, David H\. Hoover, 中城 元臣, 株式会社クイープ \|本 \| 通販 \| Amazon](https://www.amazon.co.jp/Solidity%E3%81%A8Ethereum%E3%81%AB%E3%82%88%E3%82%8B%E5%AE%9F%E8%B7%B5%E3%82%B9%E3%83%9E%E3%83%BC%E3%83%88%E3%82%B3%E3%83%B3%E3%83%88%E3%83%A9%E3%82%AF%E3%83%88%E9%96%8B%E7%99%BA-%E2%80%95Truffle-Suite%E3%82%92%E7%94%A8%E3%81%84%E3%81%9F%E9%96%8B%E7%99%BA%E3%81%AE%E5%9F%BA%E7%A4%8E%E3%81%8B%E3%82%89%E3%83%87%E3%83%97%E3%83%AD%E3%82%A4%E3%81%BE%E3%81%A7-Kevin-Solorio/dp/4873119340/ref=sr_1_5?__mk_ja_JP=%E3%82%AB%E3%82%BF%E3%82%AB%E3%83%8A&crid=1CG6G7UW26U5O&keywords=hands+on+smart+contracts&qid=1707793937&sprefix=hands+on+smart+contract%2Caps%2C287&sr=8-5)

## 実際のデプロイ結果
- デプロイ先のネットワーク：Goerli
- [Greeter \| Address 0x482cb785f19d9ceb19cb325973c36f70eb9d0c2c \| Etherscan](https://goerli.etherscan.io/address/0x482cb785f19d9ceb19cb325973c36f70eb9d0c2c#code)

## 


## 補足説明

### Infuraの設定
- Infura([Ethereum API \| IPFS API & Gateway \| ETH Nodes as a Service \| Infura](https://app.infura.io/))

教科書に書かれている内容とは異なり，API Keyを手にすることで，各ネットワークと繋がるようになる．その際，繋げたいネットワークには，チェックマークをつける必要がある．

### MNEMONICの設定
```
MNEMONIC
```

### Node.jsのバージョンに伴うエラー
- ローカルマシンにインストールしたnode.jsのバージョン次第では，下記のようなエラーを起こす場合がある．
```
Error: error:0308010C:digital envelope routines::unsupported
```

そのため，truffleを用いたスマートコントラクトのデプロイを行う際は，実行時のターミナルに下記の操作を行う．
```
export NODE_OPTIONS=--openssl-legacy-provider
```

しかし，上記の操作の適用範囲はこれを実行したターミナルのみであるため，ターミナルを閉じるとリセットされる．
他の方法を模索している場合は，**参考資料**の「Error: error:0308010C:digital envelope routines::unsupportedの解決法」等参考にしていただきたい．

## 参考資料
[【Node\.js】Error: error:0308010C:digital envelope routines::unsupportedの解決法 \#Node\.js \- Qiita](https://qiita.com/kokogento/items/f5b176d05c621223670b)
