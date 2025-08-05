Mac Global Setup
================

Homebrew
----------------------------------------

### Install

* [https://brew.sh/ja/](https://brew.sh/ja/)

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

brew --version
brew list
brew update
```


Wget
----------------------------------------

### Install

```
brew install wget

wget --version
```


Node.js
------------------------------

### Install

```
brew install nodebrew

nodebrew --version
```

#### List remote versions
```
nodebrew ls-remote
```

#### Install stable version
```
mkdir -p ~/.nodebrew/src
nodebrew install-binary stable
nodebrew ls
```

#### Select version
```
nodebrew use vXX.XX.XX
nodebrew ls
```

#### PATH
```
echo 'export PATH=$HOME/.nodebrew/current/bin:$PATH' >> ~/.zprofile
source ~/.zprofile
```

#### Check
```
node --version
npm --version
npx --version
```

```
cd
cd xxxxx/xxxxx
npm init
npm install
```

## npm-check-updates

* check package.json
* update package.json
* update packages


```
npm install -g npm-check-updates
ncu

ncu -u
ncu -u xxxxx

npm update
```
