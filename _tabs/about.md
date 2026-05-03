---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
---

<style>
/* Developer Luxury Styling for Chirpy Theme */
:root {
  --lx-primary: #3b82f6;
  --lx-surface: rgba(255, 255, 255, 0.03);
  --lx-border: rgba(120, 120, 120, 0.2);
  --lx-shadow: 0 10px 40px -10px rgba(0,0,0,0.1);
}

html[data-mode="light"] {
  --lx-surface: rgba(0, 0, 0, 0.02);
  --lx-border: rgba(0, 0, 0, 0.08);
}

.luxury-header {
  text-align: center;
  padding: 3rem 1rem;
  margin-bottom: 3rem;
  background: var(--lx-surface);
  border-radius: 16px;
  border: 1px solid var(--lx-border);
  box-shadow: var(--lx-shadow);
  backdrop-filter: blur(10px);
}

.luxury-header img {
  width: 140px;
  height: 140px;
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 1.5rem;
  box-shadow: 0 8px 24px rgba(0,0,0,0.15);
  border: 4px solid var(--lx-primary);
}

.luxury-header h1 {
  font-size: 2.2rem;
  margin-bottom: 0.5rem;
  font-weight: 700;
  letter-spacing: -0.5px;
}

.luxury-header p {
  color: var(--text-muted-color);
  font-size: 1.1rem;
  max-width: 600px;
  margin: 0 auto;
}

.luxury-card {
  background: var(--lx-surface);
  border-radius: 12px;
  padding: 2rem;
  margin-bottom: 2rem;
  border: 1px solid var(--lx-border);
  box-shadow: var(--lx-shadow);
  transition: transform 0.3s ease;
}

.luxury-card:hover {
  transform: translateY(-3px);
}

.resume-item {
  margin-bottom: 2rem;
  padding-bottom: 1.5rem;
  border-bottom: 1px dashed var(--lx-border);
}

.resume-item:last-child {
  border-bottom: none;
  padding-bottom: 0;
}

.resume-meta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.resume-meta h5 {
  margin: 0;
  font-size: 1.15rem;
  font-weight: 600;
}

.resume-meta .date-location {
  font-size: 0.9rem;
  color: var(--text-muted-color);
  font-weight: 500;
}

.tag-pill {
  display: inline-block;
  padding: 0.3rem 0.8rem;
  background: rgba(59, 130, 246, 0.1);
  color: var(--lx-primary);
  border-radius: 99px;
  font-size: 0.8rem;
  font-weight: 600;
  margin: 0.2rem;
  border: 1px solid rgba(59, 130, 246, 0.2);
}

.skill-category {
  margin-bottom: 1rem;
}

.skill-category strong {
  display: block;
  margin-bottom: 0.4rem;
  color: var(--text-color);
}
</style>

<div class="luxury-header">
  <img src="/assets/img/unnamed.png" alt="Kishan Singh" />
  <h1>Kishan Singh</h1>
  <p>Software Engineer | Open Source Contributor</p>
</div>

## 👨‍💻 About Me : 

<div class="luxury-card">
  <h3>Education</h3>
  <div class="resume-item">
    <div class="resume-meta">
      <h5>ABES Engineering College</h5>
      <span class="date-location">Jun 2023 — Jun 2027 | Ghaziabad, UP</span>
    </div>
    <p>B.Tech in Information Technology</p>
  </div>
  <div class="resume-item">
    <div class="resume-meta">
      <h5>Acharya Ambalal V Patel Junior College</h5>
      <span class="date-location">Jun 2021 — Mar 2022 | Mumbai, MH</span>
    </div>
    <p>Senior Secondary (Science)</p>
  </div>
</div>

<div class="luxury-card">
  <h3>Technical Skills</h3>
  <div class="skill-category">
    <strong>Languages</strong>
    <span class="tag-pill">Java</span> <span class="tag-pill">C++</span> <span class="tag-pill">Python</span> <span class="tag-pill">JavaScript</span> <span class="tag-pill">TypeScript</span> <span class="tag-pill">SQL</span>
  </div>
  <div class="skill-category">
    <strong>Backend</strong>
    <span class="tag-pill">Node.js</span> <span class="tag-pill">Express.js</span> <span class="tag-pill">Fastify</span> <span class="tag-pill">SpringBoot</span> <span class="tag-pill">FastAPI</span> <span class="tag-pill">REST APIs</span> <span class="tag-pill">WebSockets</span> <span class="tag-pill">gRPC</span> <span class="tag-pill">tRPC</span>
  </div>
  <div class="skill-category">
    <strong>AI & Agents</strong>
    <span class="tag-pill">LangChain</span> <span class="tag-pill">LangGraph</span> <span class="tag-pill">RAG Pipelines</span> <span class="tag-pill">AI Agent Workflows</span>
  </div>
  <div class="skill-category">
    <strong>Databases & DevOps</strong>
    <span class="tag-pill">PostgreSQL</span> <span class="tag-pill">MongoDB</span> <span class="tag-pill">Redis</span> <span class="tag-pill">Docker</span> <span class="tag-pill">Kubernetes (K3s)</span> <span class="tag-pill">AWS</span> <span class="tag-pill">ArgoCD</span> <span class="tag-pill">CI/CD</span> <span class="tag-pill">NGINX</span>
  </div>
  <div class="skill-category">
    <strong>Frontend & Tools</strong>
    <span class="tag-pill">React.js</span> <span class="tag-pill">Next.js</span> <span class="tag-pill">Git</span> <span class="tag-pill">Linux</span> <span class="tag-pill">Prisma ORM</span> <span class="tag-pill">BullMQ</span>
  </div>
</div>

<div class="luxury-card">
  <h3>Experience</h3>
  <div class="resume-item">
    <div class="resume-meta">
      <h5>Oppia Foundation — Collaborator, CORE Team</h5>
      <span class="date-location">Jan 2026 — Present | Remote</span>
    </div>
    <ul>
      <li>Fixed a critical <strong>Story Viewer</strong> bug by aligning frontend and backend chapter-state logic, restoring content publishing reliability.</li>
      <li>Designed and shipped an <strong>Apache Beam audit + migration pipeline</strong> to backfill missing <code>BlogAuthorDetailsModel</code> entities, resolving large-scale datastore inconsistency.</li>
      <li>Eliminated <strong>CI flakiness</strong> by fixing race conditions via deterministic rendering and improved test synchronization.</li>
      <li>Authored technical <strong>root cause analysis docs</strong> covering datastore migration design and validation strategies.</li>
    </ul>
  </div>
</div>

<div class="luxury-card">
  <h3>Featured Projects</h3>
  
  <div class="resume-item">
    <div class="resume-meta">
      <h5>Code Submission Platform (Distributed Judge)</h5>
      <span class="date-location">Node.js, Redis, BullMQ, Docker, K3s, ArgoCD</span>
    </div>
    <ul>
      <li>Architected a microservices-based online judge with decoupled services for scalable code execution.</li>
      <li>Built an async evaluation pipeline with Redis + BullMQ, reducing submission latency by ~30% and improving throughput by ~40%.</li>
      <li>Implemented Docker sandboxed execution with CPU, memory, and network isolation for C++, Java, and Python.</li>
      <li>Deployed on K3s (Kubernetes) with ArgoCD GitOps, cutting deployment time by ~50%.</li>
    </ul>
  </div>

  <div class="resume-item">
    <div class="resume-meta">
      <h5>v0.dev Clone (AI Full-Stack App Generator)</h5>
      <span class="date-location">Next.js, tRPC, Prisma, E2B, Docker</span>
    </div>
    <ul>
      <li>Built an AI-powered platform that generates full-stack applications from natural language prompts using LLM-driven workflows.</li>
      <li>Enabled safe runtime execution via E2B sandboxed containers, isolating generated app environments per user.</li>
    </ul>
  </div>

  <div class="resume-item">
    <div class="resume-meta">
      <h5>Workflow Automation Platform (n8n Clone)</h5>
      <span class="date-location">Next.js, TypeScript, Inngest, Stripe</span>
    </div>
    <ul>
      <li>Built a node-based workflow automation platform for visually designing and executing multi-step automations.</li>
      <li>Designed an event-driven execution engine using Inngest for durable background jobs with step orchestration and retries.</li>
    </ul>
  </div>

  <div class="resume-item">
    <div class="resume-meta">
      <h5>MiniPostgres (Relational DB Engine from Scratch)</h5>
      <span class="date-location">Java 17, B+ Tree, Buffer Pool, SQL Engine</span>
    </div>
    <ul>
      <li>Built a relational database engine from scratch with schema management, disk-based storage, and SQL execution.</li>
      <li>Implemented a B+ Tree index for fast search and a buffer pool with LRU eviction to reduce disk I/O.</li>
    </ul>
  </div>
</div>

<div class="luxury-card">
  <h3>Achievements</h3>
  <div class="resume-item">
    <div class="resume-meta">
      <h5>Hacktoberfest 2025 — Global Super Contributor</h5>
    </div>
    <p>Ranked in the <strong>Top 10,000 contributors globally</strong> for open-source contributions during Hacktoberfest 2025.</p>
  </div>
  <div class="resume-item">
    <div class="resume-meta">
      <h5>DrawDB — Open Source Contributor</h5>
    </div>
    <p>Implemented <strong>PostgreSQL <code>INHERITS</code> support</strong> with 240+ lines of production code, enabling hierarchical table modeling.</p>
  </div>
  <div class="resume-item">
    <div class="resume-meta">
      <h5>Competitive Programming</h5>
    </div>
    <p>Solved <strong>500+ problems</strong> across data structures and algorithms with a peak LeetCode contest rating of <strong>1639</strong>.</p>
  </div>
</div>
