# 環境構築

## anyenvをインストール

```
brew install anyenv
anyenv init
# follow the instruction

# reopen terminal

anyenv install --init
anyenv install nodenv
```

## anyenvのプラグインをインストール

```
# anyenv-update
mkdir -p $(anyenv root)/plugins
git clone https://github.com/znz/anyenv-update.git $(anyenv root)/plugins/anyenv-update

# nodenv-default-packages
brew install nodenv/nodenv/nodenv-default-packages
echo << __EOF__ > $(anyenv root)/default-packages
yarn
typescript
ts-node
typesync
__EOF__
```

## node.jsをインストール

```
nodenv install -l
nodenv install 14.15.0
nodenv global 14.15.0
```

## VSCodeのプラグインをインストール

```
ESLint
stylelint
Prettier
Visual Studio IntelliCode
Bracket Pair Colorizer 2
indent-rainbow
vscode-icons
Import Cost
Get History
VSCodeVim
Remote - WSL
Live Share
```

# サンプルアプリを起動してみる

```
npx create-react-app hello-world --template=typescript
cd hello-world
yarn start
```

* public/index.html -> src/index.tsxへの対応付けは、npx create-react-appでインストールされるreact-scriptsがbabelやwebpackを使って行っている
* パッケージをインストール: `yarn install` or `yarn`
* 依存関係はyarn.lockに保存される
* package.jsonのscriptsエントリは`yarn ○○`で実行
* scriptsの予約ワード(start): 開発用アプリケーションサーバの起動コマンド登録用
* scriptsの予約ワード(restart): 開発用アプリケーションサーバの再起動コマンド登録用
* scriptsの予約ワード(stop): 開発用アプリケーションサーバの停止コマンド登録用
* scriptsの予約ワード(test): テスト開始コマンド登録用
* フックコマンドの予約ワード(preinstall / postinstall): パッケージがインストールされる前後に実行
* フックコマンドの予約ワード(preuninstall / postuninstall): パッケージがアンインストールされる前後に実行
* フックコマンドの予約ワード(prestart / poststart): startスクリプトが走る前後に実行
* フックコマンドの予約ワード(pretest, posttest): testスクリプトが走る前後に実行
* フックコマンドの予約ワード(prepare): npm installコマンド実行時にインストール系の処理が終わった一番最後に実行

# ES6について
