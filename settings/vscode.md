VSCode
======

## 全体の設定

* 設定（⌘ + ,） → ユーザー → 右上の設定ファイルアイコンをクリック

```
{
    "files.exclude": {
        "**/node_modules": true
    },
    "auto-close-tag.SublimeText3Mode": true,
    "editor.cursorStyle": "block",
    "editor.linkedEditing": true,
    "editor.minimap.enabled": false,
    "editor.stickyScroll.enabled": false,
    "workbench.startupEditor": "none",
    "php.validate.executablePath": "",
    "workbench.colorCustomizations": {
        "editor.lineHighlightBackground": "#00aa3922",
        "statusBar.background": "#0039aacc",
        "tab.activeBackground": "#0039aacc",
    },
    "editor.tabSize": 2,
    "git.openRepositoryInParentFolders": "never",
    // "workbench.editor.wrapTabs": true,
}
```


## エクスプローラーに表示しないファイルを指定する

* 設定（⌘ + ,） → ワークスペース → 右上の設定ファイルアイコンをクリック

@vscode-workspace-settings.json
```
{
	"folders": [
		{
			"path": "../MAMP/htdocs/sample/www"
		}
	],
	"settings": {
		"files.exclude": {
			".vscode": true,
			"node_modules": true,
			"httpdocs/.htaccess": true,
			"httpdocs/assets/css/": true,
			"httpdocs/assets/img/": true,
			"httpdocs/assets/js/": true,
			"httpdocs/assets/libs/": true,
			"httpdocs/wp-sample/.htaccess": true,
			"httpdocs/wp-sample/index.php": true,
			"httpdocs/wp-sample/wp-*.php": true,
			"httpdocs/wp-sample/readme.html": true,
			"httpdocs/wp-sample/license.txt": true,
			"httpdocs/wp-sample/xmlrpc.php": true,
			"httpdocs/wp-sample/wp-admin/": true,
			"httpdocs/wp-sample/wp-includes/": true,
			"httpdocs/wp-sample/wp-content/languages/": true,
			"httpdocs/wp-sample/wp-content/plugins/": true,
			"httpdocs/wp-sample/wp-content/upgrade/": true,
			"httpdocs/wp-sample/wp-content/uploads/": true,
			"httpdocs/wp-sample/wp-content/upgrade-temp-backup": true,
			"httpdocs/wp-sample/wp-content/index.php": true,
			"httpdocs/wp-sample/wp-content/themes/index.php": true,
			"httpdocs/wp-sample/wp-content/themes/*/screenshot.png": true,
			"httpdocs/wp-sample/wp-content/themes/sample/assets/img": true,
			"httpdocs/wp-sample/wp-content/themes/sample/index.php": true,
			"httpdocs/favicon.ico": true,
			"httpdocs/android-touch-icon.png": true,
			"httpdocs/apple-touch-icon.png": true,
			"src/compiled": true,
			".editorconfig": true,
			".gitignore": true,
			"babel.config.js": true,
			"bs-config.js": true,
			"package.json": true,
			"package-lock.json": true,
			"postcss.config.js": true
		}
	}
}
```

## カーソルの移動を vim 風にする

@vscode-keybindings.json
```
[
    { "key": "ctrl+l","command": "cursorRight","when":"textInputFocus" },
    { "key": "ctrl+h","command": "cursorLeft","when": "textInputFocus" },
    { "key": "ctrl+k","command": "cursorUp","when": "textInputFocus" },
    { "key": "ctrl+j","command": "cursorDown","when": "textInputFocus" }
]
```
