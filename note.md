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
