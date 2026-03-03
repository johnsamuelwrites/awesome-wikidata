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
    --accent-2: #4cffb2;
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

  h2 {
    font-size: 1.1rem;
    margin: 0 0 0.65rem;
    color: var(--accent);
  }

  ul {
    margin: 0;
    padding-left: 1.1rem;
  }

  li + li {
    margin-top: 0.35rem;
  }

  a {
    color: #b1ecff;
    text-decoration-color: rgba(177, 236, 255, 0.45);
  }

  a:hover {
    color: white;
    text-decoration-color: white;
  }

  .tag {
    display: inline-block;
    margin-left: 0.35rem;
    padding: 0.08rem 0.38rem;
    font-size: 0.73rem;
    border-radius: 999px;
    border: 1px solid rgba(76, 255, 178, 0.45);
    color: var(--accent-2);
    vertical-align: middle;
  }
</style>

<main class="shell">
  <section class="hero">
    <h1>Awesome Wikidata Apps</h1>
    <p class="subtitle">A modern, platform-first catalog of tools for desktop, web, and mobile workflows.</p>
  </section>

  <section class="grid">
    <article class="card">
      <h2>Web Applications</h2>
      <ul>
        <li><a href="https://pltools.toolforge.org/harvesttemplates">Harvest Templates</a> <span class="tag">Desktop</span></li>
        <li><a href="https://mix-n-match.toolforge.org/#/">Mix-n-match</a> <span class="tag">Desktop</span></li>
        <li><a href="https://github.com/OpenRefine/OpenRefine">OpenRefine</a> <span class="tag">Desktop</span></li>
        <li><a href="https://tools.wmflabs.org/ordia/">Ordia</a> <span class="tag">Desktop</span> <span class="tag">Mobile</span></li>
        <li><a href="https://tools.wmflabs.org/quickstatements">QuickStatements</a> <span class="tag">Desktop</span></li>
        <li><a href="https://scholia.toolforge.org/">Scholia</a> <span class="tag">Desktop</span> <span class="tag">Mobile</span></li>
        <li><a href="https://lexeme-forms.toolforge.org/">Wikidata Lexeme Forms</a> <span class="tag">Desktop</span> <span class="tag">Mobile</span></li>
        <li><a href="https://hay.toolforge.org/propbrowse/">Propbrowse</a> <span class="tag">Desktop</span></li>
        <li><a href="https://www.wikidata.org/wiki/Wikidata:Tools/inteGraality">inteGraality</a> <span class="tag">Desktop</span></li>
        <li><a href="https://sqid.toolforge.org/#/">SQID</a> <span class="tag">Desktop</span></li>
        <li><a href="https://wdprop.toolforge.org/">WDProp</a> <span class="tag">Desktop</span> <span class="tag">Mobile</span></li>
        <li><a href="https://petscan.wmflabs.org/">PetScan</a> <span class="tag">Desktop</span></li>
        <li><a href="https://wd-image-positions.toolforge.org/">Wikidata Image Positions</a> <span class="tag">Desktop</span></li>
        <li><a href="https://machtsinn.toolforge.org/">Makesense</a> <span class="tag">Desktop</span></li>
        <li><a href="https://pageviews.wmcloud.org/massviews/">Massviews Analysis</a> <span class="tag">Desktop</span> <span class="tag">Mobile</span></li>
        <li><a href="https://fist.toolforge.org/file_candidates/#/">Wikidata file candidates</a> <span class="tag">Desktop</span> <span class="tag">Mobile</span></li>
        <li><a href="https://fist.toolforge.org/fist.php">Free Image Search Tool</a> <span class="tag">Desktop</span></li>
        <li><a href="https://fist.toolforge.org/wdfist/">Wikidata Free Image Search Tool</a> <span class="tag">Desktop</span></li>
        <li><a href="https://cradle.toolforge.org/#/">Cradle</a> <span class="tag">Desktop</span></li>
        <li><a href="https://hay.toolforge.org/sdsearch/">Structured Search</a> <span class="tag">Desktop</span> <span class="tag">Mobile</span></li>
        <li><a href="https://github.com/ad-freiburg/qlever">QLever</a> <span class="tag">Desktop</span></li>
        <li><a href="https://graphpedia.org/">Graphpedia</a> <span class="tag">Desktop</span></li>
      </ul>
    </article>

    <article class="card">
      <h2>Desktop / CLI Applications</h2>
      <ul>
        <li><a href="https://github.com/maxlath/wikibase-cli">wikibase-cli</a></li>
        <li><a href="https://www.weso.es/YASHE/">YASHE (Yet Another ShEx Editor)</a></li>
        <li><a href="https://wd-shex-infer.toolforge.org/">Wikidata Shape Expressions Inference</a></li>
        <li><a href="https://tools-static.wmflabs.org/entityschema-generator/">EntitySchema Generator</a></li>
        <li><a href="https://shexstatements.toolforge.org/">ShExStatements</a></li>
        <li><a href="https://huggingface.co/spaces/b289zhan/ESGen">ESGen</a></li>
      </ul>
    </article>

    <article class="card">
      <h2>Mobile-Friendly Apps</h2>
      <ul>
        <li><a href="https://tools.wmflabs.org/ordia/">Ordia</a></li>
        <li><a href="https://scholia.toolforge.org/">Scholia</a></li>
        <li><a href="https://lexeme-forms.toolforge.org/">Wikidata Lexeme Forms</a></li>
        <li><a href="https://wdprop.toolforge.org/">WDProp</a></li>
        <li><a href="https://pageviews.wmcloud.org/massviews/">Massviews Analysis</a></li>
        <li><a href="https://fist.toolforge.org/file_candidates/#/">Wikidata file candidates</a></li>
        <li><a href="https://hay.toolforge.org/sdsearch/">Structured Search</a></li>
      </ul>
    </article>
  </section>
</main>
