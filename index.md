---
title: Awesome Wikidata
---

<style>
  :root {
    --bg-1: #03111f;
    --bg-2: #071d2f;
    --panel: rgba(7, 23, 40, 0.72);
    --line: rgba(93, 219, 255, 0.24);
    --text: #e7f6ff;
    --muted: #9ec5db;
    --accent: #43e0ff;
  }

  body {
    margin: 0;
    color: var(--text);
    background:
      radial-gradient(circle at 10% 0%, #114063 0, transparent 45%),
      radial-gradient(circle at 90% 20%, #15485a 0, transparent 35%),
      linear-gradient(140deg, var(--bg-1), var(--bg-2) 60%, #061726);
    font-family: "Space Grotesk", "Segoe UI", sans-serif;
  }

  .shell {
    max-width: 1100px;
    margin: 0 auto;
    padding: 2.4rem 1rem 3rem;
  }

  .hero {
    padding: 1.2rem 1.1rem;
    border: 1px solid var(--line);
    border-radius: 18px;
    background: linear-gradient(165deg, rgba(67, 224, 255, 0.11), rgba(76, 255, 178, 0.06));
    box-shadow: 0 0 60px rgba(67, 224, 255, 0.1);
  }

  h1 {
    margin: 0;
    font-size: clamp(1.9rem, 5vw, 3rem);
    letter-spacing: 0.02em;
  }

  .subtitle {
    color: var(--muted);
    margin: 0.5rem 0 0;
  }

  .grid {
    margin-top: 1.2rem;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 0.9rem;
  }

  .card {
    border: 1px solid var(--line);
    border-radius: 16px;
    padding: 0.9rem;
    background: var(--panel);
    backdrop-filter: blur(4px);
  }

  .card h2 {
    margin: 0 0 0.65rem;
    font-size: 1.1rem;
    color: var(--accent);
  }

  .card ul {
    margin: 0;
    padding-left: 1.1rem;
  }

  .card li + li {
    margin-top: 0.35rem;
  }

  .card a {
    color: #b1ecff;
    text-decoration-color: rgba(177, 236, 255, 0.45);
  }

  .card a:hover {
    color: #fff;
    text-decoration-color: #fff;
  }

  #readme-source {
    display: none;
  }
</style>

<main class="shell">
  <section class="hero">
    <h1>Awesome Wikidata Apps</h1>
    <p class="subtitle">Generated from README.md. Single source of truth.</p>
  </section>
  <section id="app-grid" class="grid"></section>
</main>

<section id="readme-source">
  {% capture readme_content %}{% include_relative README.md %}{% endcapture %}
  {{ readme_content | markdownify }}
</section>

<script>
  (function () {
    function normalize(text) {
      return (text || "").replace(/\s+/g, " ").trim().toLowerCase();
    }

    function findHeading(container, tagName, text) {
      var headings = container.querySelectorAll(tagName);
      var target = normalize(text);
      for (var i = 0; i < headings.length; i += 1) {
        if (normalize(headings[i].textContent) === target) {
          return headings[i];
        }
      }
      return null;
    }

    function collectListsBetween(startHeading, endHeading) {
      var out = [];
      if (!startHeading) return out;
      var node = startHeading.nextElementSibling;
      while (node && node !== endHeading) {
        if (node.tagName === "UL") out.push(node);
        node = node.nextElementSibling;
      }
      return out;
    }

    function firstLinkItem(li) {
      var a = li.querySelector("a");
      if (!a) return null;
      return { name: a.textContent.trim(), href: a.href, raw: li.textContent || "" };
    }

    function hasDesktopMarker(raw) {
      return /🖥|desktop|ðŸ–¥/i.test(raw);
    }

    function hasMobileMarker(raw) {
      return /📱|mobile|ðŸ“±/i.test(raw);
    }

    function dedupePush(target, item, seen) {
      if (!item || !item.href || seen[item.href]) return;
      seen[item.href] = true;
      target.push(item);
    }

    function renderCard(root, title, items) {
      var article = document.createElement("article");
      article.className = "card";
      var h2 = document.createElement("h2");
      h2.textContent = title;
      article.appendChild(h2);

      var ul = document.createElement("ul");
      for (var i = 0; i < items.length; i += 1) {
        var li = document.createElement("li");
        var a = document.createElement("a");
        a.href = items[i].href;
        a.textContent = items[i].name;
        li.appendChild(a);
        ul.appendChild(li);
      }
      article.appendChild(ul);
      root.appendChild(article);
    }

    var source = document.getElementById("readme-source");
    var grid = document.getElementById("app-grid");
    if (!source || !grid) return;

    var webHeading = findHeading(source, "h3", "Web");
    var cliHeading = findHeading(source, "h3", "Command-line");
    var librariesHeading = findHeading(source, "h2", "Libraries");

    var webLists = collectListsBetween(webHeading, cliHeading);
    var cliLists = collectListsBetween(cliHeading, librariesHeading);

    var webApps = [];
    var desktopApps = [];
    var mobileApps = [];
    var seenWeb = {};
    var seenDesktop = {};
    var seenMobile = {};

    for (var i = 0; i < webLists.length; i += 1) {
      var lis = webLists[i].querySelectorAll("li");
      for (var j = 0; j < lis.length; j += 1) {
        var item = firstLinkItem(lis[j]);
        dedupePush(webApps, item, seenWeb);
        if (item && hasDesktopMarker(item.raw)) dedupePush(desktopApps, item, seenDesktop);
        if (item && hasMobileMarker(item.raw)) dedupePush(mobileApps, item, seenMobile);
      }
    }

    for (var k = 0; k < cliLists.length; k += 1) {
      var cliLis = cliLists[k].querySelectorAll("li");
      for (var m = 0; m < cliLis.length; m += 1) {
        var cliItem = firstLinkItem(cliLis[m]);
        dedupePush(desktopApps, cliItem, seenDesktop);
      }
    }

    renderCard(grid, "Web Applications", webApps);
    renderCard(grid, "Desktop / CLI Applications", desktopApps);
    renderCard(grid, "Mobile-Friendly Applications", mobileApps);
  })();
</script>
