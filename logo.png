#!/usr/bin/env python3
import shutil
import subprocess
from pathlib import Path

SITE_DIR = Path.home() / "Downloads" / "clarosmed-site"
SITE_DIR.mkdir(parents=True, exist_ok=True)
DL = Path.home() / "Downloads"

# Preserve existing logo.png or auto-copy if downloaded in ~/Downloads
logo_dest = SITE_DIR / "logo.png"
if not logo_dest.exists():
    for pat in ("logo.png", "logo.jpg", "*clarosmed*.*", "watermarked_img_*.*"):
        matches = [p for p in DL.glob(pat) if p.is_file()]
        if matches:
            shutil.copy2(matches[0], logo_dest)
            break

has_logo = logo_dest.exists()
nav_logo = '<img src="logo.png" alt="ClarosMed Emblem" class="nav-emblem" />' if has_logo else '<div class="nav-monogram">CM</div>'
hero_emblem = '<img src="logo.png" alt="ClarosMed Seal" class="hero-seal" />' if has_logo else ''

HTML = f"""<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>ClarosMed | Institutional AI Safety, Red-Teaming &amp; Healthcare Evaluation</title>
  <meta name="description" content="ClarosMed is an independent AI safety, adversarial red-teaming, and healthcare evaluation practice supporting AI labs and enterprise healthcare organizations." />
  <style>
    :root {{
      --obsidian: #0b111a;
      --obsidian-light: #131c2b;
      --gold: #c8a24d;
      --gold-soft: #e6cf93;
      --gold-border: rgba(200, 162, 77, 0.28);
      --bg: #f8fafc;
      --surface: #ffffff;
      --text: #0f172a;
      --muted: #475569;
      --border: #e2e8f0;
    }}
    * {{ box-sizing: border-box; margin: 0; padding: 0; }}
    html {{ scroll-behavior: smooth; }}
    body {{
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      background: var(--bg);
      color: var(--text);
      line-height: 1.65;
      -webkit-font-smoothing: antialiased;
    }}
    .container {{ max-width: 1120px; margin: 0 auto; padding: 0 24px; }}

    /* Top Navigation */
    nav {{
      position: sticky;
      top: 0;
      z-index: 100;
      background: rgba(11, 17, 26, 0.96);
      backdrop-filter: blur(8px);
      border-bottom: 1px solid var(--gold-border);
    }}
    .nav-inner {{
      display: flex;
      align-items: center;
      justify-content: space-between;
      height: 76px;
    }}
    .brand {{
      display: flex;
      align-items: center;
      gap: 14px;
      text-decoration: none;
    }}
    .nav-emblem {{
      height: 46px;
      width: auto;
      border-radius: 6px;
      border: 1px solid var(--gold-border);
    }}
    .nav-monogram {{
      width: 42px;
      height: 42px;
      border-radius: 6px;
      border: 1px solid var(--gold);
      color: var(--gold);
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 800;
      letter-spacing: 0.06em;
    }}
    .brand-text {{
      display: flex;
      flex-direction: column;
    }}
    .brand-name {{
      color: #ffffff;
      font-weight: 700;
      font-size: 1.1rem;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      line-height: 1.1;
    }}
    .brand-sub {{
      color: var(--gold-soft);
      font-size: 0.72rem;
      letter-spacing: 0.06em;
      text-transform: uppercase;
      margin-top: 2px;
    }}
    .nav-links {{
      display: flex;
      align-items: center;
      gap: 28px;
    }}
    .nav-links a {{
      color: #cbd5e1;
      text-decoration: none;
      font-size: 0.9rem;
      font-weight: 500;
      transition: color 0.2s;
    }}
    .nav-links a:hover {{ color: var(--gold-soft); }}
    .nav-cta {{
      background: var(--gold);
      color: var(--obsidian) !important;
      padding: 10px 18px;
      border-radius: 6px;
      font-weight: 700 !important;
      font-size: 0.86rem !important;
      letter-spacing: 0.02em;
    }}
    .nav-cta:hover {{ background: var(--gold-soft); }}

    /* Hero */
    .hero {{
      background: radial-gradient(circle at top right, #172336 0%, var(--obsidian) 65%);
      color: #ffffff;
      padding: 84px 0 72px;
      border-bottom: 1px solid var(--gold-border);
    }}
    .hero-grid {{
      display: grid;
      grid-template-columns: 1.35fr 0.65fr;
      gap: 48px;
      align-items: center;
    }}
    .eyebrow {{
      display: inline-block;
      color: var(--gold-soft);
      font-size: 0.78rem;
      font-weight: 700;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      margin-bottom: 16px;
      border: 1px solid var(--gold-border);
      padding: 5px 12px;
      border-radius: 4px;
      background: rgba(200, 162, 77, 0.08);
    }}
    .hero h1 {{
      font-size: 2.85rem;
      line-height: 1.15;
      font-weight: 700;
      letter-spacing: -0.02em;
      margin-bottom: 20px;
    }}
    .hero p {{
      color: #cbd5e1;
      font-size: 1.08rem;
      max-width: 620px;
      margin-bottom: 32px;
    }}
    .hero-actions {{
      display: flex;
      flex-wrap: wrap;
      gap: 14px;
    }}
    .btn-primary {{
      background: var(--gold);
      color: var(--obsidian);
      text-decoration: none;
      font-weight: 700;
      padding: 14px 26px;
      border-radius: 6px;
      font-size: 0.95rem;
    }}
    .btn-secondary {{
      border: 1px solid rgba(255, 255, 255, 0.25);
      color: #ffffff;
      text-decoration: none;
      font-weight: 600;
      padding: 14px 26px;
      border-radius: 6px;
      font-size: 0.95rem;
    }}
    .hero-visual {{
      display: flex;
      justify-content: center;
    }}
    .hero-seal {{
      width: 100%;
      max-width: 340px;
      border-radius: 12px;
      border: 1px solid var(--gold-border);
      box-shadow: 0 24px 60px rgba(0, 0, 0, 0.55);
    }}

    /* Institutional Trust Strip */
    .trust-strip {{
      background: var(--obsidian-light);
      border-bottom: 1px solid rgba(255, 255, 255, 0.08);
      padding: 26px 0;
    }}
    .trust-grid {{
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 20px;
    }}
    .trust-item {{
      border-left: 2px solid var(--gold);
      padding-left: 16px;
    }}
    .trust-val {{
      color: #ffffff;
      font-weight: 700;
      font-size: 1.05rem;
    }}
    .trust-label {{
      color: #94a3b8;
      font-size: 0.82rem;
      margin-top: 2px;
    }}

    /* Sections */
    section {{ padding: 76px 0; }}
    .section-head {{ margin-bottom: 42px; max-width: 720px; }}
    .section-kicker {{
      color: #947122;
      font-weight: 700;
      font-size: 0.78rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      margin-bottom: 8px;
    }}
    .section-head h2 {{
      font-size: 2rem;
      letter-spacing: -0.02em;
      margin-bottom: 12px;
      color: var(--text);
    }}
    .section-head p {{ color: var(--muted); font-size: 1.02rem; }}

    /* Practice Cards */
    .grid-3 {{
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 24px;
    }}
    .card {{
      background: var(--surface);
      border: 1px solid var(--border);
      border-top: 3px solid var(--obsidian);
      border-radius: 10px;
      padding: 28px;
      box-shadow: 0 4px 16px rgba(15, 23, 42, 0.03);
    }}
    .card h3 {{
      font-size: 1.12rem;
      margin-bottom: 12px;
      color: var(--text);
    }}
    .card p {{
      font-size: 0.94rem;
      color: var(--muted);
      margin-bottom: 16px;
    }}
    .card ul {{
      list-style: none;
      border-top: 1px solid var(--border);
      padding-top: 14px;
    }}
    .card li {{
      font-size: 0.88rem;
      color: #334155;
      padding: 4px 0 4px 16px;
      position: relative;
    }}
    .card li::before {{
      content: "▪";
      color: var(--gold);
      position: absolute;
      left: 0;
    }}

    /* Methodology */
    .method-bg {{ background: #ffffff; border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }}
    .grid-4 {{
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 20px;
    }}
    .step {{
      background: var(--bg);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 24px;
    }}
    .step-num {{
      font-size: 0.8rem;
      font-weight: 800;
      color: #947122;
      letter-spacing: 0.1em;
      margin-bottom: 10px;
    }}
    .step h3 {{ font-size: 1.02rem; margin-bottom: 8px; }}
    .step p {{ font-size: 0.9rem; color: var(--muted); }}

    /* Track Record & References */
    .record-grid {{
      display: grid;
      grid-template-columns: 1.2fr 0.8fr;
      gap: 28px;
      align-items: start;
    }}
    .record-list {{
      display: flex;
      flex-direction: column;
      gap: 16px;
    }}
    .record-item {{
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 22px 24px;
    }}
    .record-item h3 {{ font-size: 1.02rem; margin-bottom: 6px; }}
    .record-item p {{ font-size: 0.92rem; color: var(--muted); }}
    .ref-box {{
      background: var(--obsidian);
      color: #ffffff;
      border: 1px solid var(--gold-border);
      border-radius: 12px;
      padding: 32px;
    }}
    .ref-box h3 {{
      color: var(--gold-soft);
      font-size: 1.2rem;
      margin-bottom: 12px;
    }}
    .ref-box p {{
      color: #cbd5e1;
      font-size: 0.94rem;
      margin-bottom: 16px;
    }}
    .ref-tag {{
      display: inline-block;
      font-size: 0.8rem;
      font-weight: 600;
      color: var(--gold-soft);
      background: rgba(200, 162, 77, 0.12);
      border: 1px solid var(--gold-border);
      padding: 6px 12px;
      border-radius: 4px;
    }}

    /* Leadership */
    .leader-card {{
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 32px;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      gap: 24px;
      align-items: center;
    }}
    .leader-info {{ max-width: 720px; }}
    .leader-role {{
      color: #947122;
      font-weight: 700;
      font-size: 0.85rem;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      margin-bottom: 4px;
    }}
    .leader-info h3 {{ font-size: 1.4rem; margin-bottom: 10px; }}
    .leader-info p {{ color: var(--muted); font-size: 0.95rem; margin-bottom: 14px; }}
    .cred-pills {{ display: flex; flex-wrap: wrap; gap: 8px; }}
    .pill {{
      background: #f1f5f9;
      border: 1px solid var(--border);
      color: #334155;
      font-size: 0.82rem;
      font-weight: 600;
      padding: 5px 12px;
      border-radius: 999px;
    }}

    /* CTA & Footer */
    .cta-section {{
      background: var(--obsidian);
      color: #ffffff;
      padding: 68px 0;
      border-top: 1px solid var(--gold-border);
    }}
    .cta-box {{
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: 24px;
    }}
    .cta-box h2 {{ font-size: 1.85rem; margin-bottom: 8px; }}
    .cta-box p {{ color: #cbd5e1; max-width: 600px; }}
    footer {{
      background: #070b12;
      color: #94a3b8;
      padding: 28px 0;
      font-size: 0.84rem;
      border-top: 1px solid rgba(255, 255, 255, 0.06);
    }}
    .footer-inner {{
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      gap: 12px;
    }}

    @media (max-width: 900px) {{
      .hero-grid, .grid-3, .grid-4, .trust-grid, .record-grid {{ grid-template-columns: 1fr; }}
      .nav-links {{ display: none; }}
      .hero h1 {{ font-size: 2.15rem; }}
    }}
  </style>
</head>
<body>

  <nav>
    <div class="container nav-inner">
      <a href="#" class="brand">
        {nav_logo}
        <div class="brand-text">
          <span class="brand-name">ClarosMed</span>
          <span class="brand-sub">AI Safety &amp; Healthcare Evaluation</span>
        </div>
      </a>
      <div class="nav-links">
        <a href="#capabilities">Capabilities</a>
        <a href="#methodology">Methodology</a>
        <a href="#track-record">Track Record</a>
        <a href="#leadership">Leadership</a>
        <a href="#contact" class="nav-cta">Request Engagement</a>
      </div>
    </div>
  </nav>

  <header class="hero">
    <div class="container hero-grid">
      <div>
        <div class="eyebrow">Independent AI Governance &amp; Clinical-Workflow Advisory</div>
        <h1>Domain-Grounded AI Safety for Regulated Healthcare.</h1>
        <p>ClarosMed partners with frontier AI labs, health-tech platforms, and enterprise healthcare organizations to red-team behavioral models, audit clinical workflows, and enforce evidence-based safety rubrics before deployment.</p>
        <div class="hero-actions">
          <a href="#contact" class="btn-primary">Initiate a Consultation</a>
          <a href="#capabilities" class="btn-secondary">Explore Capabilities</a>
        </div>
      </div>
      <div class="hero-visual">
        {hero_emblem}
      </div>
    </div>
  </header>

  <div class="trust-strip">
    <div class="container trust-grid">
      <div class="trust-item">
        <div class="trust-val">Fortune 100</div>
        <div class="trust-label">Enterprise &amp; National Client Pedigree</div>
      </div>
      <div class="trust-item">
        <div class="trust-val">US-Based Practice</div>
        <div class="trust-label">New York Registered · Async &amp; Sprint Ready</div>
      </div>
      <div class="trust-item">
        <div class="trust-val">MPH &amp; Behavioral</div>
        <div class="trust-label">Multidisciplinary Clinical Milieu Depth</div>
      </div>
      <div class="trust-item">
        <div class="trust-val">Verified References</div>
        <div class="trust-label">Available Upon Request Under NDA</div>
      </div>
    </div>
  </div>

  <section id="capabilities">
    <div class="container">
      <div class="section-head">
        <div class="section-kicker">Core Practice Areas</div>
        <h2>Precision Evaluation Where Generalist Testing Fails</h2>
        <p>Healthcare AI failure modes are rarely obvious to non-specialist annotators. ClarosMed brings frontline behavioral health, public health, and enterprise payer experience directly into your evaluation loop.</p>
      </div>
      <div class="grid-3">
        <div class="card">
          <h3>Behavioral Health &amp; Psychological Harm Red-Teaming</h3>
          <p>Structured adversarial testing of conversational and decision-support models across high-vulnerability mental health and recovery scenarios.</p>
          <ul>
            <li>Crisis-escalation &amp; refusal boundary auditing</li>
            <li>Eating disorder &amp; recovery-enabling detection</li>
            <li>DBT, CBT &amp; ACT therapeutic alignment review</li>
            <li>Severity tagging against incident taxonomies</li>
          </ul>
        </div>
        <div class="card">
          <h3>Public Health &amp; Biomedical Rubric Evaluation</h3>
          <p>High-consistency grading, hallucination detection, and evidence-backed rationale authoring for regulated biomedical and public health datasets.</p>
          <ul>
            <li>Multi-page rubric execution &amp; drift auditing</li>
            <li>Inter-rater calibration &amp; dispute adjudication</li>
            <li>Pre-genetic &amp; population-health accuracy checks</li>
            <li>Structured remediation rationales for RLHF</li>
          </ul>
        </div>
        <div class="card">
          <h3>Enterprise Payer &amp; Healthcare Operations Audits</h3>
          <p>Real-world validation of AI outputs touching US health plan administration, coverage logic, hospital systems, and patient care transitions.</p>
          <ul>
            <li>ACA Marketplace, Medicare &amp; employer plan logic</li>
            <li>Care-transition &amp; patient navigation accuracy</li>
            <li>Hospital clinical communication workflow checks</li>
            <li>Policy-hallucination &amp; compliance screening</li>
          </ul>
        </div>
      </div>
    </div>
  </section>

  <section id="methodology" class="method-bg">
    <div class="container">
      <div class="section-head">
        <div class="section-kicker">Evaluation Architecture</div>
        <h2>Built for Inter-Rater Consistency at Scale</h2>
        <p>Every ClarosMed engagement follows a disciplined, auditable review workflow designed to integrate cleanly with frontier AI research teams and vendor evaluation portals.</p>
      </div>
      <div class="grid-4">
        <div class="step">
          <div class="step-num">01 / SCOPE</div>
          <h3>Failure-Mode Mapping</h3>
          <p>Align on target clinical, behavioral, or administrative risk surfaces and severity taxonomies prior to batch execution.</p>
        </div>
        <div class="step">
          <div class="step-num">02 / STRESS-TEST</div>
          <h3>Adversarial Execution</h3>
          <p>Deploy multi-turn edge-case prompts and real-world patient scenarios to expose subtle hallucinations and unsafe advice.</p>
        </div>
        <div class="step">
          <div class="step-num">03 / CALIBRATE</div>
          <h3>Rubric &amp; Drift Audit</h3>
          <p>Apply standardized scoring criteria across high-volume batches with rigorous quality checks and guideline citations.</p>
        </div>
        <div class="step">
          <div class="step-num">04 / REMEDIATE</div>
          <h3>Corrected Reasoning</h3>
          <p>Deliver clean, evidence-backed golden responses and structured failure reports ready for model training teams.</p>
        </div>
      </div>
    </div>
  </section>

  <section id="track-record">
    <div class="container">
      <div class="section-head">
        <div class="section-kicker">Institutional Pedigree</div>
        <h2>Enterprise Healthcare &amp; Clinical Operations Track Record</h2>
        <p>ClarosMed’s advisory methodology is grounded in over a decade of direct execution across Fortune 100 ecosystems, major multi-hospital health systems, and high-acuity clinical milieus.</p>
      </div>
      <div class="record-grid">
        <div class="record-list">
          <div class="record-item">
            <h3>Enterprise Health Systems &amp; Clinical Infrastructure</h3>
            <p>Leadership experience negotiating and structuring complex, multi-hospital clinical communication and nurse-call safety deployments—including $18M+ 10-year enterprise health-system agreements across clinical, IT, biomedical engineering, and executive stakeholders.</p>
          </div>
          <div class="record-item">
            <h3>Fortune 100, Financial Institution &amp; National Payer Accounts</h3>
            <p>Proven execution scaling digital healthcare exchange platforms across 60–80 national employer, bank, credit union, and association accounts, backed by deep familiarity with 48-state health plan compliance across employer, ACA Marketplace, and Medicare lines.</p>
          </div>
          <div class="record-item">
            <h3>High-Acuity Behavioral Health &amp; Multidisciplinary Milieus</h3>
            <p>Direct frontline collaboration with therapists and multidisciplinary care teams facilitating DBT, CBT, and ACT programming, crisis-risk identification, and protocol-compliant clinical documentation.</p>
          </div>
        </div>
        <div class="ref-box">
          <h3>Enterprise Vetting &amp; Verified References</h3>
          <p>ClarosMed operates as an independent New York advisory practice (a registered DBA of <strong>Do Better Consulting LLC</strong>). We maintain strict confidentiality across client engagements and model evaluations.</p>
          <p><strong>Verified professional, enterprise, and healthcare operations references are available upon request</strong> for AI research labs, enterprise procurement teams, and specialist evaluation cohorts.</p>
          <span class="ref-tag">NDA-Ready · W-9 / US LLC Entity</span>
        </div>
      </div>
    </div>
  </section>

  <section id="leadership" class="method-bg">
    <div class="container">
      <div class="section-head">
        <div class="section-kicker">Practice Leadership</div>
        <h2>Principal-Led Accountability</h2>
      </div>
      <div class="leader-card">
        <div class="leader-info">
          <div class="leader-role">Managing Principal · AI Safety &amp; Healthcare Evaluation</div>
          <h3>Khaleel Zughbieh, MPH</h3>
          <p>Khaleel leads ClarosMed’s evaluation methodology and client engagements, combining graduate public health training (MPH), postgraduate pre-genetic counseling coursework (SCUHS), frontline behavioral health facilitation (Eating Recovery Center, Helio Health), and enterprise healthcare systems leadership (Hillrom/Baxter, HealthPlan Services).</p>
          <div class="cred-pills">
            <span class="pill">Master of Public Health (MPH)</span>
            <span class="pill">SCUHS Pre-Genetic Counseling</span>
            <span class="pill">DBT / CBT / ACT Facilitation</span>
            <span class="pill">NYS Certified Provisional Peer Specialist</span>
            <span class="pill">Former 48-State Health Plan Licensure</span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section id="contact" class="cta-section">
    <div class="container cta-box">
      <div>
        <h2>Engage ClarosMed for Your Next Evaluation Sprint</h2>
        <p>Available for US-based remote AI safety red-teaming, rubric auditing, and healthcare evaluation cohorts. Direct inquiries, W-9 requests, and reference verifications answered promptly.</p>
      </div>
      <a class="btn-primary" href="mailto:YOUR_EMAIL@DOMAIN.COM?subject=ClarosMed%20Enterprise%20Evaluation%20%26%20Reference%20Inquiry">Request Credentials &amp; References</a>
    </div>
  </section>

  <footer>
    <div class="container footer-inner">
      <div>&copy; 2026 ClarosMed (ClarosMed.org), a DBA of Do Better Consulting LLC · New York. All rights reserved.</div>
      <div>Verified references available upon request.</div>
    </div>
  </footer>

</body>
</html>
"""

(SITE_DIR / "index.html").write_text(HTML, encoding="utf-8")
(SITE_DIR / "CNAME").write_text("clarosmed.org\n", encoding="utf-8")
print(f"[REBUILT] {SITE_DIR / 'index.html'}")
print(f"[LOGO] {'Found logo.png' if has_logo else 'No logo.png yet — drop your logo into ~/Downloads/clarosmed-site/logo.png'}")
subprocess.run(["open", str(SITE_DIR / "index.html")])
