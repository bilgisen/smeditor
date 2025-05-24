---
layout: page
title: Stylish Markdown Editor
permalink: /smeditor/
---

<div id="editor-wrapper">
  <textarea id="editor"></textarea>

  <div id="buttons" style="margin-top: 1em;">
    <button id="generate" onclick="convertText()">Generate Unicode</button>
    <button id="edit-again" onclick="editAgain()" style="display:none;">Edit Again</button>
    <button id="copy-btn" onclick="copyText()" style="display:none;">Copy Text</button>
  </div>
</div>

<link rel="stylesheet" href="https://unpkg.com/easymde/dist/easymde.min.css">
<script src="https://unpkg.com/easymde/dist/easymde.min.js"></script>

<style>
  #editor-wrapper {
    max-width: 100%;
    margin: auto;
  }
  @media(min-width: 768px) {
    #editor-wrapper {
      width: 80%;
    }
  }
</style>

<script>
  let easyMDE = new EasyMDE({ 
    element: document.getElementById("editor"),
    autofocus: true,
    placeholder: "Write your text using **bold** or *italic* formatting...",
    spellChecker: false
  });

  const toUnicode = (input) => {
    const map = {
      A:'𝐀',B:'𝐁',C:'𝐂',D:'𝐃',E:'𝐄',F:'𝐅',G:'𝐆',H:'𝐇',I:'𝐈',J:'𝐉',K:'𝐊',
      L:'𝐋',M:'𝐌',N:'𝐍',O:'𝐎',P:'𝐏',Q:'𝐐',R:'𝐑',S:'𝐒',T:'𝐓',U:'𝐔',V:'𝐕',
      W:'𝐖',X:'𝐗',Y:'𝐘',Z:'𝐙',a:'𝐚',b:'𝐛',c:'𝐜',d:'𝐝',e:'𝐞',f:'𝐟',g:'𝐠',
      h:'𝐡',i:'𝐢',j:'𝐣',k:'𝐤',l:'𝐥',m:'𝐦',n:'𝐧',o:'𝐨',p:'𝐩',q:'𝐪',r:'𝐫',
      s:'𝐬',t:'𝐭',u:'𝐮',v:'𝐯',w:'𝐰',x:'𝐱',y:'𝐲',z:'𝐳'
    };
    return input.replace(/[A-Za-z]/g, c => map[c] || c);
  };

  function convertText() {
    const inputText = easyMDE.value();
    const converted = toUnicode(inputText);
    easyMDE.value(converted);
    document.getElementById("generate").style.display = "none";
    document.getElementById("edit-again").style.display = "inline-block";
    document.getElementById("copy-btn").style.display = "inline-block";
  }

  function copyText() {
    navigator.clipboard.writeText(easyMDE.value()).then(() => {
      alert("Copied!");
    });
  }

  function editAgain() {
    document.getElementById("generate").style.display = "inline-block";
    document.getElementById("edit-again").style.display = "none";
    document.getElementById("copy-btn").style.display = "none";
  }
</script>
