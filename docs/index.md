---
title: Home Page
description: Charles Chi Le — backend and AI agent engineer, Duke M.Eng. graduate, and open-source contributor.
hide:
  - navigation
  - toc
---

<div class="home-profile">
  <section class="home-hero" aria-labelledby="home-name">
    <div class="home-intro">
      <p class="home-eyebrow">BACKEND SYSTEMS &amp; AI AGENTS</p>
      <h1 id="home-name">Charles Chi Le <span class="home-name-cn" lang="zh">乐驰</span></h1>
      <p class="home-role">Backend &amp; AI Agent Engineer</p>
      <p class="home-lead">I build reliable cloud platforms and practical AI agents. My work spans Elasticsearch infrastructure, agent development, and backend systems at Alibaba Cloud, ByteDance, and Meituan.</p>
      <p class="home-lead">A Duke University M.Eng. graduate and open-source contributor, I enjoy turning complex systems into useful, dependable software.</p>
      <div class="home-actions">
        <a class="home-button home-button-primary" href="乐驰中文简历.pdf">View résumé <span lang="zh">· 中文</span></a>
        <a class="home-button" href="mailto:charles.chi.le@outlook.com">Get in touch <span aria-hidden="true">↗</span></a>
      </div>
      <div class="home-social" aria-label="Social profiles">
        <a href="https://github.com/charleschile">GitHub <span aria-hidden="true">↗</span></a>
        <a href="https://www.linkedin.com/in/chi-charles-le/">LinkedIn <span aria-hidden="true">↗</span></a>
        <a href="https://blog.charleschile.com/">Blog <span aria-hidden="true">↗</span></a>
      </div>
    </div>
    <figure class="home-portrait">
      <img src="About/me001.jpg" alt="Charles Chi Le in graduation attire" width="180" height="300">
      <figcaption>Duke M.Eng.<br>Zhejiang B.Sc.</figcaption>
    </figure>
  </section>

  <nav class="home-jump-links" aria-label="On this page">
    <a href="#experience">Experience</a>
    <a href="#education">Education</a>
    <a href="#opensource">Open source</a>
    <a href="#skills">Skills</a>
    <a href="#notebook">Notebook</a>
  </nav>

  <div class="home-metrics" aria-label="Selected engineering results">
    <div class="home-metric"><strong>16,000+</strong><span>Cloud instances inspected</span><small>Alibaba Cloud · ~99.9% success rate</small></div>
    <div class="home-metric"><strong>20M+</strong><span>Orders monitored daily</span><small>ByteDance · billing accuracy</small></div>
    <div class="home-metric"><strong>2,000 QPS</strong><span>Retrieval API capacity</span><small>Meituan · increased from 500 QPS</small></div>
  </div>

  <section id="experience" class="home-section" aria-labelledby="experience-title">
    <div class="home-section-heading"><span class="home-section-number" aria-hidden="true">01</span><h2 id="experience-title">Experience</h2></div>
    <div class="home-experience">
      <article class="home-entry home-entry-featured">
        <div class="home-entry-heading">
          <div><h3>Alibaba Cloud <span lang="zh">阿里云</span></h3><p class="home-entry-role">Java Backend &amp; Agent Engineer</p></div>
          <p class="home-entry-date">Feb–Nov 2026 <span>Hangzhou, China</span></p>
        </div>
        <p class="home-entry-team">Computing Platform Division · AI Search Cloud Platform</p>
        <ul class="home-highlights">
          <li><strong>Elasticsearch PaaS &amp; health events.</strong> Built control-plane capabilities across events, monitoring, inspections, and agents. Connected monitoring, log ingestion, and anomaly detection to generate about 1,500 health events per week across 400+ instances.</li>
          <li><strong>ES Agent.</strong> Integrated authorization, tools, knowledge bases, and Skills for diagnostics, data insights, and instance management. Serves <strong>150+ users</strong> and answers <strong>2,000+ questions</strong> monthly.</li>
          <li><strong>Intelligent inspections.</strong> Built Agent-first inspections with rule-based fallback, covering <strong>16,000+ instances</strong> at approximately <strong>99.9% success</strong>, with scheduled execution and structured reports.</li>
          <li><strong>Skill evaluation &amp; improvement.</strong> Built evaluation and iteration workflows across 12 fault scenarios, raising scores from about 40% to nearly 90%. Distilled 19 reusable Skill lessons from 541 cases, with human review before release.</li>
        </ul>
      </article>
      <article class="home-entry">
        <div class="home-entry-heading">
          <div><h3>ByteDance <span lang="zh">字节跳动</span></h3><p class="home-entry-role">Backend Engineering Intern · Go</p></div>
          <p class="home-entry-date">May–Aug 2025 <span>Hangzhou, China</span></p>
        </div>
        <p class="home-entry-team">Global E-commerce · Funds Center</p>
        <ul class="home-highlights">
          <li>Built configurable billing workflows, reducing development time for standard requests from <strong>4 to 0.5 person-days</strong>. Developed Elasticsearch and Hive dashboards to monitor more than <strong>20 million orders daily</strong>.</li>
          <li>Used RocketMQ and EaseJob to retry failed settlement tasks, improving billing–settlement consistency within SLA from <strong>80% to 99.99%+</strong>. Developed MySQL–Elasticsearch consistency checks.</li>
        </ul>
      </article>
      <article class="home-entry">
        <div class="home-entry-heading">
          <div><h3>Meituan <span lang="zh">美团</span></h3><p class="home-entry-role">Backend Engineering Intern · Java</p></div>
          <p class="home-entry-date">May–Aug 2024 <span>Beijing, China</span></p>
        </div>
        <p class="home-entry-team">Core Local Commerce · Search Advertising</p>
        <ul class="home-highlights">
          <li>Developed search-ad serving logic for pharmaceutical brands, including CPT/CPM sales logic and merchant/brand billing.</li>
          <li>Optimized an inverted-index retrieval API from <strong>500 to 2,000 QPS</strong>, reducing tail latency from <strong>181.9 ms to 24.7 ms</strong>. Compared traffic allocation and significance reporting across <a href="https://blog.charleschile.com/posts/abtest/">A/B experiment platforms</a>.</li>
        </ul>
      </article>
    </div>
  </section>

  <section id="education" class="home-section" aria-labelledby="education-title">
    <div class="home-section-heading"><span class="home-section-number" aria-hidden="true">02</span><h2 id="education-title">Education</h2></div>
    <div class="home-education-grid">
      <article class="home-education">
        <h3>Duke University</h3>
        <p>M.Eng. in Electrical and Computer Engineering<br>Software Development</p>
        <div class="home-education-meta"><span>Aug 2023–Dec 2025</span><strong>GPA 4.0 / 4.0</strong></div>
      </article>
      <article class="home-education">
        <h3>Zhejiang University</h3>
        <p>B.Sc. in Biomedical Sciences<br>Bioinformatics</p>
        <div class="home-education-meta"><span>Aug 2019–Jun 2023</span><strong>GPA 3.82 / 4.0</strong></div>
      </article>
    </div>
  </section>

  <section id="opensource" class="home-section" aria-labelledby="opensource-title">
    <div class="home-section-heading"><span class="home-section-number" aria-hidden="true">03</span><h2 id="opensource-title">Open source</h2></div>
    <div class="home-project-grid">
      <article class="home-project">
        <div class="home-project-top"><h3>MatrixOne</h3><a href="https://github.com/charleschile/matrixone" aria-label="MatrixOne development repository">Repository <span aria-hidden="true">↗</span></a></div>
        <p class="home-project-date">Go database development · Aug–Dec 2024</p>
        <p>Developed an LLM-based secondary index supporting document chunking, embeddings, and vector-based RAG through dynamically created SQL tables.</p>
        <a class="home-text-link" href="https://github.com/matrixorigin/matrixone/pull/18809">Read pull request #18809 <span aria-hidden="true">↗</span></a>
      </article>
      <article class="home-project">
        <div class="home-project-top"><h3>ModelCache</h3><a href="https://github.com/charleschile/ModelCache" aria-label="ModelCache development repository">Repository <span aria-hidden="true">↗</span></a></div>
        <p class="home-project-date">LLM backend components · Oct–Dec 2024</p>
        <p>Contributed a reranker module, additional embedding models, and migration to the FastAPI framework.</p>
        <a class="home-text-link" href="https://github.com/codefuse-ai/ModelCache">Explore the project <span aria-hidden="true">↗</span></a>
      </article>
    </div>
  </section>

  <section id="skills" class="home-section" aria-labelledby="skills-title">
    <div class="home-section-heading"><span class="home-section-number" aria-hidden="true">04</span><h2 id="skills-title">Tools I work with</h2></div>
    <div class="home-skill-groups">
      <div class="home-skill-group"><h3>Languages</h3><p>Java · Go · Python · C/C++ · SQL</p></div>
      <div class="home-skill-group"><h3>Backend &amp; infrastructure</h3><p>Elasticsearch · MySQL · Redis · Spring · Linux · Git · Kubernetes</p></div>
      <div class="home-skill-group"><h3>AI &amp; development</h3><p>Agent development · RAG · PyTorch · GDB</p></div>
    </div>
  </section>

  <section id="notebook" class="home-section home-notebook" aria-labelledby="notebook-title">
    <h2 id="notebook-title">Always learning, always building.</h2>
    <p>This notebook is where I keep my computer science course notes, programming practice, and engineering discoveries.</p>
    <div class="home-notebook-links"><a href="Course/">Course notes <span aria-hidden="true">↗</span></a><a href="Problem/">Programming practice <span aria-hidden="true">↗</span></a><a href="Tool/">Tools &amp; workflows <span aria-hidden="true">↗</span></a></div>
  </section>
</div>
