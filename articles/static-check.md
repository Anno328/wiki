---

title: ""

emoji: "ð¸" 

type: "tech" 

topics: ["",""] 

published: **false** 

 ---



[[_TOC_]]

# ä½¿ç¨ãã¦ããã©ã¤ãã©ãª
ãnpmã
- eslint
- prettier
- eslint-plugin-prettier
- eslint-config-prettier

ãvscodeã®æ¡å¼µæ©è½ã
- ESLint

# éçãã§ãã¯ã®æµã
eslintã¨prettierãé£æºããã¦ãéçãã§ãã¯ãè¡ã£ã¦ããã

åã©ã¤ãã©ãªã®å½¹å²ã¯ä¸è¨ã®éãã
| ã©ã¤ãã©ãª             | å½¹å²                                                         |
| ---------------------- | ------------------------------------------------------------ |
| eslint                 | æ§æãã§ãã¯ãè¡ããã«ã¼ã«ã«éåããã³ã¼ããæ¤ç¥ãã¦è­¦åããã |
| prettier               | ã³ã¼ãããè¨­å®ããã«ã¼ã«ã«åºã¥ãã¦ãã©ã¼ããã(èªåæå½¢)ããã |
| eslint-plugin-prettier | esllintã¨prettierãé£æºãããã                              |
| eslint-config-prettier | ç«¶åããã«ã¼ã«ããªãããã                                   |
| ESLint(vscode)         | ã³ã¼ãã£ã³ã°æã«åçã«éçãã§ãã¯è­¦åãåºåããããã¡ã¤ã«ä¿å­æã«ãã©ã¼ãããããããã |

eslintã ãã§ãã³ã¼ãæ´å½¢ã¯ã§ããããprettierãå©ç¨ããã°ãæè»½ã«eslintã§ã¯å¯¾å¿ã§ããªãã³ã¼ããæ´å½¢ã§ããã

ã¾ããprettierã«ã¯æ§æãã§ãã¯ã®æ©è½ã¯ãªãããããããè£ãããã«eslintã¨ä½µç¨ãã¦ããã

åè
https://qiita.com/soarflat/items/06377f3b96964964a65d
https://blog.ojisan.io/eslint-prettier

# è¨­å®ãã¡ã¤ã«
## .eslintrc.json
eslintã®è¨­å®ãã¡ã¤ã«
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
### è¨­å®å¤ã®æå³
ãenvã
éçãã§ãã¯ã®åææ¡ä»¶ãæç¤ºããã

[es6]ãtrueã«ããå ´åãES Modulesæ©è½ãæå¹ã«ãªããªããããã
ãã®ããã
[parserOptions]ã«ä¸è¨ãæå®ãããã¨ã§ES Modulesæ©è½ãæå¹ã«ãã¦ããã
```
"sourceType": "module"
```

ãextendsã
å¤é¨ã®æ¨å¥¨è¨­å®ãrulesã«æ¡å¼µããã
ä»åã¯ä¸è¨ãæå®ãã¦ããã
```
"eslint:recommended",                             //eslintã®æ¨å¥¨è¨­å®
"plugin:@typescript-eslint/recommended",          //typescriptã®æ¨å¥¨è¨­å®
"plugin:@typescript-eslint/eslint-recommended",   //typescriptã®æ¨å¥¨è¨­å®
"plugin:prettier/recommended",                    //prettierã®æ¨å¥¨è¨­å®
"prettier/@typescript-eslint",                    //typescriptã®æ¨å¥¨è¨­å®
"plugin:react/recommended"                        //reactã®æ¨å¥¨è¨­å®
```
(ä¸ä½ã®è¨è¼ããã¼ã¹ã¨ãªã£ã¦ãä¸ä½ã®è¨è¼ã§ä¸æ¸ããã¦ãã)
â»typescriptã®è¨­å®ããããªã«ããã®ãè¦èª¿æ»

ãparserã
Praserãæç¤ºããã
(ããã©ã«ãã¯Espreeãä½¿ç¨ããã)
Tyepsscriptã§ã®éçºã®ãããä¸è¨ãæå®ãã¦ããã
```
"@typescript-eslint/parser",
```

ãpluginsã
ãµã¼ããã¼ãã£è£½ã®ãã©ã°ã¤ã³ãæå®ããã
Tyepsscriptã§ã®éçºã®ãããä¸è¨ãæå®ãã¦ããã
```
"@typescript-eslint"
```

extendsã¨pluginã®éãâ
https://blog.ojisan.io/eslint-plugin-and-extend

ãrulesã
éçãã§ãã¯ã®ã«ã¼ã«ãæå®ããã
(ä»åã¯åºæ¬çã«recommendä½¿ã£ã¦ãã®ã§ããã¾ãrulesãæ¸ãã¦ãªããã©ãæ¬å½ã¯ããã«ãã­ã¸ã§ã¯ãç¬èªã®ã«ã¼ã«ãè¨è¼ããã¦ããã)

prettierã®ãã§ãã¯ã§ãæ¹è¡ã³ã¼ããLFã§ãªãã¨ã¨ã©ã¼ãçºçãã¦ãããããä¸è¨ãæå®ã
```
"prettier/prettier": [
            "error",
            {
              "endOfLine": "auto"
            }
          ]
```

åè
https://eslint.org/docs/user-guide/configuring

### prettierã¨ã®é£æº
ä¸è¨é¨åã§ãeslint-plugin-prettierããç¨ãã¦prettierã¨ã®é£æºãè¡ã£ã¦ããã
```
"plugin:prettier/recommended",
```
åè
https://github.com/prettier/ESLint-plugin-prettier

## package.json
lintã³ãã³ããæç²
```
    "lint": "eslint --max-warnings 0 --fix --ext .tsx ./src",
```
### ãªãã·ã§ã³ã®æå³
ã--max-warningsã
è­¦åãã©ã®ãããã®éã¾ã§è¨±ãããæç¤ºããã
(0 ã ã¨ä¸ä»¶ã§ãè­¦åãåºãã°ã¨ã©ã¼ã¨ããã)

ã--fixã
ã³ã¼ãã®èªåãã©ã¼ããããè¡ãã

ã--extã
ã©ã®ãã¡ã¤ã«ã«å¯¾ãã¦ãã§ãã¯ãè¡ããæç¤ºããã(ããã©ã«ãã¯*.js)

åè
https://eslint.org/docs/user-guide/command-line-interface

## settings.json(è£è¶³)
vscodeã®è¨­å®ãã¡ã¤ã«
```
{
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    }
}

```
ãã®ãã¡ã¤ã«ã«ä¸è¨ã®è¨è¼ããããã¨ã§ããã¡ã¤ã«ä¿å­æã«ãã©ã¼ããããè¡ããã¨ãã§ããã