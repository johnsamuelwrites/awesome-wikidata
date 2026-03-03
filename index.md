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

  .hero-actions {
    margin-top: 0.85rem;
    display: flex;
    gap: 0.6rem;
    flex-wrap: wrap;
  }

  .edit-link {
    display: inline-block;
    padding: 0.42rem 0.7rem;
    border-radius: 999px;
    border: 1px solid var(--line);
    color: #c9f2ff;
    text-decoration: none;
    background: rgba(67, 224, 255, 0.08);
  }

  .edit-link:hover {
    color: #fff;
    border-color: rgba(93, 219, 255, 0.6);
  }

  .grid {
    margin-top: 1.2rem;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 0.9rem;
  }

  .menu {
    margin-top: 1rem;
    display: flex;
    gap: 0.6rem;
    flex-wrap: wrap;
  }

  .menu-link {
    display: inline-block;
    padding: 0.38rem 0.7rem;
    border-radius: 999px;
    border: 1px solid rgba(93, 219, 255, 0.35);
    color: #cbf4ff;
    text-decoration: none;
    background: rgba(67, 224, 255, 0.08);
  }

  .menu-link:hover {
    color: #fff;
    border-color: rgba(93, 219, 255, 0.65);
    background: rgba(67, 224, 255, 0.14);
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
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .icon {
    display: inline-flex;
    width: 1.35rem;
    height: 1.35rem;
    border-radius: 999px;
    border: 1px solid rgba(93, 219, 255, 0.45);
    background: rgba(67, 224, 255, 0.12);
    align-items: center;
    justify-content: center;
    font-size: 0.82rem;
    line-height: 1;
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
    <p class="subtitle">Curated list of Wikidata applications across web, desktop, and mobile.</p>
    <nav class="menu" aria-label="Platform menu">
      <a class="menu-link" href="#web-applications">Web</a>
      <a class="menu-link" href="#desktop-cli-applications">Desktop / CLI</a>
      <a class="menu-link" href="#mobile-friendly-applications">Mobile</a>
    </nav>
    <div class="hero-actions">
      <a id="improve-link" class="edit-link" href="#">Improve this list</a>
    </div>
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

    function slugify(text) {
      return (text || "")
        .toLowerCase()
        .replace(/[^a-z0-9]+/g, "-")
        .replace(/^-+|-+$/g, "");
    }

    function renderCard(root, iconHtml, title, items) {
      var article = document.createElement("article");
      article.className = "card";
      article.id = slugify(title);
      var h2 = document.createElement("h2");
      var iconSpan = document.createElement("span");
      iconSpan.className = "icon";
      iconSpan.innerHTML = iconHtml;
      h2.appendChild(iconSpan);
      h2.appendChild(document.createTextNode(title));
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
    var repoUrl = "{{ site.github.repository_url | default: '' }}";
    var defaultBranch = "{{ site.github.default_branch | default: 'main' }}";
    var readmeEditUrl = repoUrl ? repoUrl + "/edit/" + defaultBranch + "/README.md" : "";

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

    renderCard(grid, "&#x1F578;", "Web Applications", webApps);
    renderCard(grid, "&#x1F5A5;", "Desktop / CLI Applications", desktopApps);
    renderCard(grid, "&#x1F4F1;", "Mobile-Friendly Applications", mobileApps);

    var improve = document.getElementById("improve-link");
    if (improve && readmeEditUrl) improve.href = readmeEditUrl;

    var links = document.querySelectorAll("a");
    for (var n = 0; n < links.length; n += 1) {
      var label = normalize(links[n].textContent);
      var href = links[n].getAttribute("href") || "";
      var isImproveLabel = label.indexOf("improve this page") !== -1;
      var pointsToIndex = /\/(blob|edit|tree)\/[^/]+\/index\.md(?:$|[#?])/i.test(href);
      if ((isImproveLabel || pointsToIndex) && readmeEditUrl) {
        links[n].href = readmeEditUrl;
      } else if (pointsToIndex) {
        links[n].href = href.replace(/index\.md/i, "README.md");
      }
    }

    var legacyMap = {
      "#models": "#web-applications",
      "#tools": "#desktop-cli-applications",
      "#libraries": "#mobile-friendly-applications"
    };
    for (var p = 0; p < links.length; p += 1) {
      var current = (links[p].getAttribute("href") || "").toLowerCase();
      if (legacyMap[current]) links[p].setAttribute("href", legacyMap[current]);
    }
  })();
</script>
