# PROJECT_SCHEDULE.md
# Dark Matter Halos in Spiral Galaxies: NFW vs Einasto
## Project Schedule (Sept 2026 – Jan 5, 2027)

**Team Roles**
- **Nathan (Lead):** Calculus derivations, fitting logic, physics interpretation, code verification
- **Drake (Coder):** Python implementation, numerical integration, plotting, fitting loops
- **Corbin (Secondary Math + Writing):** Algebraic computations, unit conversions, residuals, dark matter fraction, trapezoidal rule spot-checks, paper writing, slides

**Classroom Context:** Astronomy 35 – no dedicated classroom, self-directed research room, teacher available but not present most of the time.

---

## Phase 1: Foundation (Sept 1 – Oct 15)

### Week 1 (Sept 1–5)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Read SPARC paper (Lelli+2016) | Set up Python (Jupyter, numpy, scipy, matplotlib) | Download SPARC data for 4 galaxies (NGC 3198, NGC 2403, NGC 2903, NGC 6503) |
| Choose 4 galaxies based on data quality | Create shared GitHub or Google Drive folder | Open each data file, identify columns ($r$, $v_{\text{obs}}$, $v_{\text{err}}$) |
| Write down visible mass formula: <br> $v_{\text{vis}}(r) = \sqrt{GM_{\text{vis}}(r)/r}$ | Write script to load one galaxy's data and print first 5 rows | Create master spreadsheet (Google Sheets) with tabs per galaxy |

### Week 2 (Sept 8–12)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Derive NFW enclosed mass formula: <br> $M(r) = 4\pi \rho_0 r_s^3 \left[\ln(1+x) - \frac{x}{1+x}\right], \quad x = r/r_s$ | Write function to load SPARC data ($r$, $v_{\text{obs}}$, $v_{\text{err}}$) | **Unit conversions:** <br> $1\text{ kpc}=3.086\times10^{19}\text{ m}$ <br> $1 M_\odot=1.989\times10^{30}\text{ kg}$ <br> $G=6.674\times10^{-11}\text{ m}^3/\text{kg}/\text{s}^2$ <br> $G=4.3009\times10^{-3}\text{ (km/s)}^2\cdot\text{kpc}/M_\odot$ |
| | Plot raw $v_{\text{obs}}$ vs $r$ for one galaxy | |

### Week 3 (Sept 15–19)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Derive Einasto integral setup: <br> $M(r) = 4\pi \rho_e \int_0^r r'^2 \exp\left(-d_n\left[(r'/r_e)^{1/n}-1\right]\right) dr'$ | Write function for visible mass rotation curve: <br> $v_{\text{vis}}(r) = \sqrt{G M_{\text{vis}}(r)/r}$ | **Compute $v_{\text{vis}}(r)$ table for each galaxy** <br> For each $r_i$: $v_{\text{vis}} = \sqrt{G M_{\text{vis}} / r}$ |
| Write out trapezoidal rule for numerical integration: <br> $\int_a^b f(x) dx \approx \frac{\Delta x}{2} \left[ f(x_0) + 2f(x_1) + 2f(x_2) + \dots + f(x_n) \right]$ | Test on one galaxy, plot $v_{\text{vis}}$ vs $v_{\text{obs}}$ | Create table: $r$, $v_{\text{obs}}$, $v_{\text{vis}}$, $v_{\text{err}}$ |
| Note: $d_n \approx 3n - 1/3 + 0.0079/n$ | | **Compute fractional discrepancy:** <br> $\frac{v_{\text{obs}} - v_{\text{vis}}}{v_{\text{vis}}} \times 100\%$ |

### Week 4 (Sept 22–26)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Choose initial NFW parameters for NGC 3198 from literature: <br> $\rho_0 \sim 10^7 M_\odot/\text{kpc}^3$, $r_s \sim 5-15\text{ kpc}$ | Write NFW rotation curve function given $\rho_0, r_s$ | **Compute NFW $x$ and $f(x)$ tables for all galaxies** |
| Write $\chi^2$ definition: <br> $\chi^2 = \sum \frac{(v_{\text{model}} - v_{\text{obs}})^2}{\sigma^2}$ | Test on single radius against Nathan's hand calculation | For each $r$, given $r_s$: $x = r/r_s$, $f(x) = \ln(1+x) - x/(1+x)$ |
| | | Create table: $r$, $x$, $f(x)$ |

### Week 5 (Sept 29 – Oct 3)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Derive NFW rotation curve shape limits: <br> Small $r$: $v(r) \propto r$ (rising) <br> Large $r$: $v(r) \propto \sqrt{\ln r / r}$ (flat) | Implement $\chi^2$ error function for NFW | **Create discrepancy plots (Google Sheets/Excel):** <br> - $r$ vs $v_{\text{obs}}$ (dots with error bars) <br> - $r$ vs $v_{\text{vis}}$ (line) <br> - $r$ vs fractional discrepancy (bar chart) |
| | Write grid search over $\rho_0$ ($10^6$ to $10^9$) and $r_s$ (1 to 20 kpc) | |

### Week 6 (Oct 6–10)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Run NFW grid search for NGC 3198 with Drake | Execute grid search, find best-fit $\rho_0, r_s$ minimizing $\chi^2$ | **Compute final NFW rotation curve using best-fit parameters** <br> For each $r$: <br> $M(r) = 4\pi \rho_0 r_s^3 \cdot f(x)$, then $v_{\text{NFW}} = \sqrt{GM(r)/r}$ |
| Verify best-fit parameters are physically plausible | Generate plot: $v_{\text{obs}}$, $v_{\text{vis}}$, $v_{\text{NFW(best fit)}}$ | Create table: $r$, $v_{\text{obs}}$, $v_{\text{vis}}$, $v_{\text{NFW}}$, $v_{\text{err}}$ |

### Week 7 (Oct 13–15 — short week)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Review NFW results for NGC 3198 | Debug any remaining issues | **Write first draft of Data section** <br> - Describe SPARC database (citation) <br> - List galaxies chosen and why <br> - State units used <br> - Explain $v_{\text{vis}}$ computation <br> - Explain NFW table generation |
| Write Methods section (NFW part) for paper | Prepare code for remaining 3 galaxies | |
| Include derivation (condensed) and fitting procedure | | |

**Phase 1 Checkpoint (Oct 15):** One galaxy (NGC 3198) has working NFW fit. Tables for all galaxies. Draft Data section.

---

## Phase 2: Core Modeling (Oct 16 – Nov 30)

### Week 8 (Oct 16–19)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Write Einasto numerical integration plan (pseudocode) | Implement Einasto mass integral using `scipy.integrate.quad` | **Compute visible mass tables from SPARC photometry files (cross-check)** |
| Specify Simpson's rule or quad method | Test on single radius against known value | Algebra: summation, volume of spheres, density calculations |
| Choose initial $n$ values to try ($n = 4, 6, 8$) | | |

### Week 9 (Oct 20–24)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Determine reasonable Einasto parameter ranges from literature: <br> $\rho_e: 10^6\text{ to }10^9$, $r_e: 1\text{ to }20$, $n: 2\text{ to }10$ | Fit Einasto to NGC 3198 | **Compute Einasto $\chi^2$ contributions per radius (algebra version)** <br> For each $r$: $\frac{(v_{\text{obs}} - v_{\text{Einasto}})^2}{\sigma^2}$ |
| Compare $\chi^2$ to NFW fit | | Sum to get total $\chi^2$, compare to Drake's result |
| Which fits better for this galaxy? | | |

### Week 10 (Oct 27–31)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Debug Einasto integration issues (convergence at small/large $r$) | Run NFW and Einasto on all 4 galaxies | **Create master parameter table:** <br> Columns: Galaxy, Profile, $\rho_0$ or $\rho_e$, scale radius, $n$ (Einasto), $\chi^2$, reduced $\chi^2$ |
| Check numerical integration stability | Save best-fit parameters for each galaxy, each profile | Compute BIC: <br> $\text{BIC} = \chi^2 + k\ln(N)$ ($k$ = parameters, $N$ = data points) |

### Week 11 (Nov 3–7)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Analyze results: Which profile fits better? Does it vary by galaxy? | Produce final rotation curve plots: one per galaxy with all curves overlaid | **Write first draft of Results section:** <br> - NFW fits (table) <br> - Einasto fits (table) <br> - Which profile had lower $\chi^2$ per galaxy <br> - Reference to plots |
| Look for core-cusp tension (dwarf galaxies favor Einasto/cored profiles) | Ensure all plots have: legend, axis labels, error bars, title | |
| Note any galaxies where both profiles fit equally well | | |

### Week 12 (Nov 10–14)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Write Discussion section draft: <br> - Core-cusp problem (cusps or cores in your galaxies?) <br> - Limitations (small sample, simple fitting method) <br> - Comparison to literature | Add error bars to all plots (from SPARC $v_{\text{err}}$) | **Compute error propagation for derived quantities** <br> For each galaxy, uncertainty in $v_{\text{NFW}}$ and $v_{\text{Einasto}}$ using finite differences: <br> Vary each parameter by $\pm10\%$, see how $v$ changes |

### Week 13 (Nov 17–21)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Write Conclusion section: <br> - Summary of findings <br> - Future work (more galaxies, MCMC, baryonic feedback, alternative DM models) | Prepare code for final submission (clean notebooks, comments, README) | **Merge all paper sections into one document** <br> Check consistent formatting (fonts, section numbering, figure references) <br> Ensure all figures labeled correctly (Figure 1, Figure 2, etc.) |

### Week 14 (Nov 24–28)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Full physics review of entire paper | Final checks: all plots reproducible? Any off-by-one errors? | **Full grammar and style review** <br> Ensure references complete and correctly formatted (AAS journal style) <br> Create table of contents |
| Check every equation, unit, citation | | |
| Verify conclusions follow from results | | |

**Phase 2 Checkpoint (Nov 30):** All 4 galaxies fitted with both profiles. All plots generated. Full paper draft complete.

---

## Phase 3: Paper & Presentation (Dec 1 – Jan 5)

### Week 15 (Dec 1–5)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Revise Methods section, add derivation details in Appendix | Generate high-resolution figures (PNG/PDF, 300 dpi) for paper and slides | **Build presentation slides (15 slides max)** <br> Use Google Slides or PowerPoint template |
| Ensure calculus steps clearly explained for RASC audience | | |

### Week 16 (Dec 8–12)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Practice explaining derivations out loud to team | Help Corbin understand plots for their presentation portion | **Write speaker notes for each slide** <br> Practice your portion <br> Prepare Q&A cheat sheet (possible questions and answers) |
| Time yourself, cut anything over 15 minutes | | |

### Week 17 (Dec 15–19)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Full team mock presentation (time it) | Same | Same |
| Give feedback: clarity? timing? transitions? | | |

### Week 18 (Dec 22–26 — holidays, light work)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Final paper edits (physics) | Final code cleanup | Final reference check |
| Check all figures in paper match final versions | Upload code to GitHub | Submit final paper |
| | | Format title page, acknowledgments |

### Week 19 (Dec 29 – Jan 5)

| Nathan (Lead) | Drake (Coder) | Corbin (Secondary Math + Writing) |
| :--- | :--- | :--- |
| Final presentation rehearsal (twice) | Same | Same |
| Prepare 1-minute summary (elevator pitch) | | Print or save presentation to USB (backup) |

**Final Deadline: January 5, 2027** – Paper submitted. Presentation ready. Code archived.

---

## Presentation Slide Structure (15 slides)

| Slide | Content | Speaker |
| :--- | :--- | :--- |
| 1 | Title, team names, date | Corbin |
| 2 | The dark matter problem (why rotation curves are flat) | Corbin |
| 3 | How rotation curves work (diagram: galaxy, Doppler shift, flat curve) | Corbin |
| 4 | SPARC database and our galaxies | Corbin |
| 5 | Visible matter prediction ($v_{\text{vis}}$ formula) | Corbin |
| 6 | NFW profile (derivation sketch, formula, intuition) | Nathan |
| 7 | Einasto profile (extra parameter $n$, numerical integration) | Nathan |
| 8 | Fitting method (grid search, $\chi^2$) | Drake |
| 9 | Results — example galaxy (NGC 3198 rotation curve plot) | Drake |
| 10 | Results table (NFW vs Einasto parameters and $\chi^2$ for all galaxies) | Drake |
| 11 | Which profile wins? (core-cusp discussion) | Nathan |
| 12 | Limitations (small sample, simple fitting, no MCMC) | Nathan |
| 13 | Conclusion (summary, dark matter confirmed, both profiles work) | Nathan |
| 14 | Future work (more galaxies, better statistics, baryonic feedback) | Nathan |
| 15 | Acknowledgments + Questions | Corbin |

---

## Deliverables Summary

1. Research paper (8–12 pages): Introduction, Data, Methods, Results, Discussion, Conclusion, References, Appendices
2. Rotation curve plots (one per galaxy, 3–4 galaxies): $v_{\text{obs}}$, $v_{\text{vis}}$, $v_{\text{NFW(best fit)}}$, $v_{\text{Einasto(best fit)}}$
3. Parameter table per galaxy: $\rho_0, r_s$ (NFW); $\rho_e, r_e, n$ (Einasto) with uncertainties
4. Residuals table per galaxy: $v_{\text{obs}} - v_{\text{vis}}$, $v_{\text{obs}} - v_{\text{NFW}}$, $v_{\text{obs}} - v_{\text{Einasto}}$
5. Dark matter fraction table per galaxy: $f_{\text{DM}}(r) = M_{\text{DM}}(r) / [M_{\text{vis}}(r) + M_{\text{DM}}(r)]$
6. 15-minute presentation for RASC

---

**Total Hours:** 110 per person (330 total)  
**Weekly schedule:** 1 hour/day (5 days/week) + 45 min Thursday + ~20 min weekends/breaks
