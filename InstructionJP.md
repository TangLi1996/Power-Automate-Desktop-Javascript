# Power Automate Desktop（PAD）＋ JavaScriptによるWeb自動化ガイド

---

## 📖 はじめに

本ドキュメントは、**特別な制約（PADとChromeのみ使用可能）** のもとで実施した自動化手法をまとめたものです。

※通常であれば、**Selenium IDE** や **Tampermonkey** を使用したスクリプト自動化をおすすめします。

---

## 🎯 想定ケース

Excelファイルに1列のデータが存在する場合を想定します：

| A列 | 管理番号 |
|---|---|
| A2 | 154615656 |
| A3 | 586156156 |
| A4 | 45454564 |
| A5 | 564564564 |

この管理番号を、Webフォームに自動入力して送信することを目指します。

---

## 🧠 難点

- PADでは**WebAppのUI要素（CSSセレクター）を正確に認識できない**ケースが多い
- DOM構造が動的に変わるため、**UI要素認識に失敗しやすい**

---

## 🛠 解決方法

**F12キーでConsoleを開き、JavaScriptを直接入力・実行して自動化**します。

- （サイトが「ソフトリロード」（画面遷移せずDOMだけ更新される）タイプの場合に特に有効）

---

## 🔄 自動化フロー図

```
start
: Excelを開く;
: Chromeを起動する;
: F12キーでConsoleを開く;
loop (各データを処理)
    : JavaScriptスクリプトをセット;
    : クリップボードにコピー;
    : 1秒待機;
    : Ctrl+Vで貼り付け;
    : Enterキーで実行;
end loop
: Excelを閉じる;
: Chromeを閉じる;
stop
```

---

## 🖼 フロー画面例

以下のスクリーンショットも参考にしてください：

![img](picture\InstructionScreenshot.png)
![img](picture\InstructionScreenshot2.png)
---

## ⚡ 注意事項

- **初めてConsoleを開くときや、長期間未使用だった場合、**  
  "Welcome" タブなどのポップアップが表示されることがあります。  
  ⇒ 必ず手動で閉じてから自動化をスタートしてください。

- テストとして、F12を押した後、**何もクリックせずにControl+Vや直接入力できるか**を事前に確認してください。

---

## 🧩 JavaScriptの書き方（基本編）

1. F12でConsoleを開き、マウスで入力欄をクリックします
2. HTMLコードを確認します（例）：

```html
<input type="text" id="fname" name="fname" placeholder="管理番号">
```

3. それに合わせて、以下のようなJavaScriptを書きます：

```javascript
document.querySelector('input[placeholder="管理番号"]').value = '%CurrentItem["管理番号"]%';
```

※ CSSセレクターは他にも多くの指定方法がありますので、状況に合わせて自由に選べます。

---

## 🧩 JavaScriptの書き方（応用編）

もし複数の入力フィールドがある場合（例：管理番号、会社名、住所など）、  
それぞれ以下のように記述します：

```javascript
document.querySelector('input[placeholder="会社名"]').value = 'Test Company';
document.querySelector('input[placeholder="住所"]').value = 'Your address';
document.querySelector('input[placeholder="管理番号"]').value = '%CurrentItem["管理番号"]%';
document.querySelector('button[type="submit"]').click();
```

※ もちろん、会社名や住所もExcelから読み込んで動的に入力するよう拡張できます！

---

# ✨ まとめ

この方法をマスターすれば、  
**どんなにWebシステムが進化しても、自動入力を安定して実現できる** ようになります！

焦らず、一歩ずつ一緒に練習していきましょう😊
