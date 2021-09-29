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

* ES6はJavaScriptの仕様のこと
* JavaScriptはプリミティブ型とオブジェクト型の2種類がある。プリミティブ型はオブジェクトではなくインスタンスメソッドを持たないデータのことを言う
* プリミティブ型は以下の通り
  * Boolean: trueかfalseの真偽値
  * Number: 少数も整数も同じ型
  * BigInt: Numberよりも大きな数値を扱う。Numberとは互換性がなく、相互に代入、計算、等価比較ができない
  * String: 文字列
  * Symbol: オブジェクトのプロパティキーとして使う
  * Null: 何もデータが存在しない状態
  * Undefined: 宣言のみが行われた変数や、オブジェクトの存在しないプロパティへのアクセスに割り当てられる
* falsy: false, 0, Nan, '', null, undefined
* truthy: falsy以外
* JavaScriptのオブジェクトはキーとそれに対応する値を持ったプロパティの集まり（連想配列）のことを言う
* 関数の定義は関数宣言文による定義と関数式による定義の2種類がある。再宣言ができるのと宣言の巻き上げができてしまうので基本的には関数式による定義が推移される
* JavaScriptの関数は第一級オブジェクト(変数に代入、オブジェクトのプロパティにしたり、他の関数に引数として渡したり戻り値としたりできる)となっており、第一級関数という性質を持つ
* JavaScriptのクラスはクラスベースではなくプロトタイプベース。
* オブジェクトのプロパティのキーや値を任意の変数から展開できる({ foo: 256, [key]: 512, bar: val }のように)
* オブジェクトの定義(プロパティ名のショートハンド): consst aaa = 256; const obj = { aaa };これでobjに{ aaa: 256}が代入される
* 分割代入1: const obj = { name: 'hoge', age: 111 }; const { name, age } = obj;
* 分割代入2: const response = { data: [ { name: 'aaa' }, { id: 'bbb' } ] }; const { data: users = [] } = response;
* スプレッド構文: const arr1 = ['a', 'b']; const arr2 = [ ...arr1, 'c'];
* 分割代入とスプレッド構文の組み合わせ: const user = { id: 1, name: 'aaa', email: 'aaa@bbb' }; const { id, ...userWithoutId } = user;
* オブジェクトのコピーはObject.assign()だと値の追加変更ができない。なので分割代入( const original = {a: 1}; const copy = {...original};)すると良い。
  * ただシャローコピーのためプロパティの値が配列やオブジェクトだった場合その値までコピーされないことに注意
  * nullやundefinedが含まれなければ、JSON.stringify()したのをJSON.parse()するとよい
* アロー関数式: const hoge = (n) => { return n; };
  * もしくは const hoge = n => n;
* JavaScriptのようなプロトタイプベースは抽象としてのクラスが存在しない
  * オブジェクトは直接他のオブジェクトを継承する
  * 継承元のオブジェクトをプロトタイプと呼ぶ
* Optional chaining: オブジェクトに対するプロパティアクセスにおいて指定したキーのプロパティが存在しなかった場合、1階層目ならundefined、２階層目ならタイプエラーとなる。`?.`演算子を使うと２階層目でプロパティが存在しなくてもundefinedを返してくれる。
* Null合体演算子: `??`で左辺がnullかundefinedのときだけ右辺が評価される。`||`でも代用できる場合があるが、0や空文字の場合を考えるとできる限りNull合体演算子を使った方がよい
