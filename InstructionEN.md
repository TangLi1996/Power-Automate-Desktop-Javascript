# Power Automate Desktop (PAD) + JavaScript Web Automation Guide

---

## 📖 Introduction

This document is designed for a **special environment where only Power Automate Desktop (PAD) and Chrome are available**.  
(Under normal circumstances, it would be more advisable to use tools like **Selenium IDE** or **Tampermonkey** for automation.)

---

## 🎯 Scenario Overview

Suppose you have an Excel file with the following structure:

| Column A | Management Number |
|---|---|
| A2 | 154615656 |
| A3 | 586156156 |
| A4 | 45454564 |
| A5 | 564564564 |

The goal is to **automatically input these management numbers into a web form and submit them**.

---

## 🧠 Challenges

- PAD often **fails to accurately recognize UI elements** in WebApps (especially dynamic sites using frameworks like React/Next.js).
- Dynamic changes to the DOM structure can cause **instability in PAD's element targeting**.

---

## 🛠 Solution Overview

We will **open Chrome's Console using F12 and execute JavaScript scripts directly** to automate interactions with web elements.

- Particularly effective for **soft-refresh pages** (i.e., pages that update via JavaScript without a full page reload).

---

## 🔄 Automation Flow Diagram

```
start
: Open Excel;
: Open Chrome;
: Press F12 to open Console;
loop (iterate over each row)
    : Generate jsScript content;
    : Copy to clipboard;
    : Wait 1 second;
    : Send Ctrl+V to paste;
    : Press Enter to execute;
end loop
: Close Excel;
: Close Chrome;
stop
```

---

## 🖼 Example Flow Screenshots

Please refer to the following images for a visual understanding:

![img](picture\Instruction-Screenshot.png)
![img](picture\Instruction-Screenshot2.png)
---

## ⚡ Important Notes

- When opening the Console for the first time, you may encounter a "Welcome" tab or pop-up message.  
  **Please manually close any pop-ups before running the automation**.  
  (Otherwise, the script might fail to focus on the Console input area.)

- Before running, it is recommended to manually test:
  - After opening Console, **without clicking anywhere, try pasting (Ctrl+V) or typing directly** to check if input is possible.

---

## 🧩 Writing JavaScript (Basic)

1. Open the web page and press F12 to open the Console.
2. Click the target input field and inspect its HTML structure. Example:

```html
<input type="text" id="fname" name="fname" placeholder="Management Number">
```

3. Based on the element, write JavaScript like:

```javascript
document.querySelector('input[placeholder="Management Number"]').value = '%CurrentItem["Management Number"]%';
```

> 💡 Tip: You can adjust the CSS selector as needed depending on the target page structure.

---

## 🧩 Writing JavaScript (Advanced)

If you have multiple input fields (e.g., Management Number, Company Name, Address), you can extend the script like this:

```javascript
document.querySelector('input[placeholder="Company Name"]').value = 'Test Company';
document.querySelector('input[placeholder="Address"]').value = 'Your address';
document.querySelector('input[placeholder="Management Number"]').value = '%CurrentItem["Management Number"]%';
document.querySelector('button[type="submit"]').click();
```

You can also dynamically pull Company Name and Address values from Excel instead of hardcoding them!

---

# ✨ Conclusion

By mastering this method,  
**you'll be able to automate web form entries stably even if the web system updates or changes in the future**.

Don't worry if it seems a little complicated at first —  
**step by step, you'll definitely get the hang of it!** 😊

---
