--- title: ""

emoji: "😸" 

type: "tech" 

topics: ["",""] 

published: **false**  ---



[[_TOC_]]

# 使用しているライブラリ
【npm】
- eslint
- prettier
- eslint-plugin-prettier
- eslint-config-prettier

【vscodeの拡張機能】
- ESLint

# 静的チェックの流れ
eslintとprettierを連携させて、静的チェックを行っている。

各ライブラリの役割は下記の通り。
| ライブラリ             | 役割                                                         |
| ---------------------- | ------------------------------------------------------------ |
| eslint                 | 構文チェックを行い、ルールに違反したコードを検知して警告する。 |
| prettier               | コードを、設定したルールに基づいてフォーマット(自動成形)する。 |
| eslint-plugin-prettier | esllintとprettierを連携させる。                              |
| eslint-config-prettier | 競合するルールをオフする。                                   |
| ESLint(vscode)         | コーディング時に動的に静的チェック警告を出力する。ファイル保存時にフォーマットをかける。 |

eslintだけでもコード整形はできるが、prettierを利用すれば、手軽にeslintでは対応できないコードも整形できる。

また、prettierには構文チェックの機能はないため、そこを補うためにeslintと併用している。

参考
https://qiita.com/soarflat/items/06377f3b96964964a65d
https://blog.ojisan.io/eslint-prettier

# 設定ファイル
## .eslintrc.json
eslintの設定ファイル
```
{
    "env": {
        "browser": true,
        "es6": true,
        "node": true
    },
    "extends": [
        "eslint:recommended",
        "plugin:@typescript-eslint/recommended",
        "plugin:@typescript-eslint/eslint-recommended",
        "plugin:prettier/recommended",
        "prettier/@typescript-eslint",
        "plugin:react/recommended"
    ],
    "parser": "@typescript-eslint/parser",
    "parserOptions": {
        "sourceType": "module"
    },
    "plugins": [
        "@typescript-eslint"
    ],
    "rules": {
        "prettier/prettier": [
            "error",
            {
              "endOfLine": "auto"
            }
          ]
    }
}
```
### 設定値の意味
【env】
静的チェックの前提条件を明示する。

[es6]をtrueにする場合、ES Modules機能が有効にならないらしい。
そのため、
[parserOptions]に下記を指定することでES Modules機能を有効にしている。
```
"sourceType": "module"
```

【extends】
外部の推奨設定をrulesに拡張する。
今回は下記を指定している。
```
"eslint:recommended",                             //eslintの推奨設定
"plugin:@typescript-eslint/recommended",          //typescriptの推奨設定
"plugin:@typescript-eslint/eslint-recommended",   //typescriptの推奨設定
"plugin:prettier/recommended",                    //prettierの推奨設定
"prettier/@typescript-eslint",                    //typescriptの推奨設定
"plugin:react/recommended"                        //reactの推奨設定
```
(上位の記載がベースとなって、下位の記載で上書きしていく)
※typescriptの設定がこんなにいるのか要調査

【parser】
Praserを明示する。
(デフォルトはEspreeを使用する。)
Tyepsscriptでの開発のため、下記を指定している。
```
"@typescript-eslint/parser",
```

【plugins】
サードパーティ製のプラグインを指定する。
Tyepsscriptでの開発のため、下記を指定している。
```
"@typescript-eslint"
```

extendsとpluginの違い↓
https://blog.ojisan.io/eslint-plugin-and-extend

【rules】
静的チェックのルールを指定する。
(今回は基本的にrecommend使ってるのであんまりrulesが書いてないけど、本当はここにプロジェクト独自のルールが記載されていく。)

prettierのチェックで、改行コードがLFでないとエラーが発生していたため、下記を指定。
```
"prettier/prettier": [
            "error",
            {
              "endOfLine": "auto"
            }
          ]
```

参考
https://eslint.org/docs/user-guide/configuring

### prettierとの連携
下記部分で「eslint-plugin-prettier」を用いてprettierとの連携を行っている。
```
"plugin:prettier/recommended",
```
参考
https://github.com/prettier/ESLint-plugin-prettier

## package.json
lintコマンドを抜粋
```
    "lint": "eslint --max-warnings 0 --fix --ext .tsx ./src",
```
### オプションの意味
【--max-warnings】
警告をどのくらいの量まで許すかを明示する。
(0 だと一件でも警告が出ればエラーとする。)

【--fix】
コードの自動フォーマットを行う。

【--ext】
どのファイルに対してチェックを行うか明示する。(デフォルトは*.js)

参考
https://eslint.org/docs/user-guide/command-line-interface

## settings.json(補足)
vscodeの設定ファイル
```
{
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    }
}

```
このファイルに上記の記載をすることで、ファイル保存時にフォーマットを行うことができる。