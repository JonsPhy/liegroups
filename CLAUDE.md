# Lie Groups Lecture Notes — Transcription Reference

## Project
- **Course:** Lectures on Groups and Lie Algebras, SS 2026, LMU Munich, Prof. Dr. Lukas Müller
- **Author:** Jonas von Stein
- Compiled with `latexmk`; aux files in `aux/`, output in `pdf/`

## Where to Add Content
Content files (one per chapter) in `content/`:
| File | Chapter |
|---|---|
| `01_symmetries.tex` | Symmetries |
| `02_basic_group_theory.tex` | Basic group theory |
| `03_representation_theory.tex` | Representation theory |
| `04_lie_groups.tex` | Lie groups |
| `05_representations_sun.tex` | Representation theory of su(n) (complete) |
| `06_simple_lie_algebras.tex` | Simple Lie algebras |
| `07_representations_of_compact_lie_groups.tex` | Representations of compact Lie groups ← current |

New chapters: add file in `content/` and `\input{content/XX_name}` in `main.tex`.

## Structure Conventions
```latex
\chapter{Title}
\section{Title}
\subsection{Title}
```
**Heading casing: sentence case** project-wide (e.g. "Basic group theory", "The Killing form and structure constants"). Capitalize only the first word + proper nouns (Lie, Schur, Hamiltonian, Weyl, Cartan, Dynkin). Applies to chapter, section, and subsection titles.

**Sectioning discipline (enforced 2026-06-24):**
- Each chapter is either fully divided into `\section`s or has none (short intros like ch.1 may have none). Don't mix.
- **Never leave a lone subsection:** a section has either 0 subsections or ≥2. If a single subsection appears, drop the heading or give it a sibling.
- Keep granularity coarse — roughly one section per several PDF pages (ch.6 ≈ 15 pp → 5 sections). Promote/merge rather than over-splitting.
- Per-chapter section counts: ch.1 = 0 (intro); ch.2 = 5; ch.3 = 4 (two of them subdivided, 5 & 2 subsections); ch.4 = 2; ch.5 = 2 (flat); ch.6 = 5 (flat).
Quotes at chapter start (see ch. 4):
```latex
\begin{center}
    \vspace{-15pt}
    {\large\itshape "Quote text."\par}
    \vspace{-8pt}
    {\color{gray!70}\rule{0.32\textwidth}{0.5pt}\par}
\end{center}
```

## Theorem / Box Commands (`style/theorems.tex`)

| Command | Renders as | Color | Notes |
|---|---|---|---|
| `\defn{Title}{body}` | Definition | red | auto-indexes title |
| `\defnr{Title}{label}{body}` | Definition (referenceable) | red | `\cref{defn:label}` |
| `\defn[-]{Title}{body}` | Definition | red | suppresses index |
| `\thm{Title}{body}` | Theorem | purple | |
| `\thmr{Title}{label}{body}` | Theorem (referenceable) | purple | |
| `\thmp{Title}{body}{proof}` | Theorem + proof | purple | |
| `\thmpr{Title}{label}{body}{proof}` | Theorem + proof (referenceable) | purple | ref with `\ref{thm:label}` (number only) |
| `\lem{Title}{body}` | Lemma | violet | |
| `\lemp{Title}{body}{proof}` | Lemma + proof | violet | |
| `\cor{body}` | Corollary | orange | no title |
| `\corp{body}{proof}` | Corollary + proof | orange | third arg `{}` for empty ref |
| `\prop{body}` | Proposition | yellow | no title |
| `\propp{body}{proof}` | Proposition + proof | yellow | |
| `\clm{Title}{body}` | Claim | pink | |
| `\clmp{Title}{body}{proof}` | Claim + proof | pink | |
| `\fact{body}` | Fact | cyan side-rule | styled like `\rmkb` — not numbered, no title |
| `\pf{body}` | Proof block | — | standalone proof after \thm |
| `\ex{body}` | Example | cyan border | |
| `\rmk{text}` | Inline remark | blue italic | |
| `\rmkb{body}` | Remark block | cyan border | |

**Note on multi-arg commands:** body args use `+m` (verbatim), so `align*`, `itemize`, etc. work inside without bracing issues. Just wrap content in `{ }`.

## Packages Available
`amsmath`, `mathtools`, `amssymb`, `amsthm`, `physics`, `siunitx`, `ytableau`, `slashed`, `tikz` (with `arrows.meta`, `calc`, `cd`, `hobby`), `pgfplots`, `tcolorbox`, `xcolor`, `hyperref`, `cleveref`, `makeidx`, `biblatex`

## Common Math Patterns Seen
```latex
% Sets / groups
\mathrm{SU}(2),\ \mathrm{SO}(3),\ \mathrm{GL}(n,\mathbb{C})
\mathfrak{su}(2),\ \mathfrak{sl}(2,\mathbb{C}),\ \mathfrak{h}
\mathrm{End}(V),\ \mathrm{Mat}(2,\mathbb{C})

% Maps
\rho: \mathfrak{g} \to \mathrm{End}(V)
\twoheadrightarrow   % surjection
\hookrightarrow      % injection

% Algebra
A^\dagger            % adjoint/conjugate transpose
\operatorname{span}  % or \mathrm{span}
\ker, \dim, \mathrm{tr}, \mathrm{id}_V

% Tensor / symmetric
V \otimes W
\mathrm{Sym}^n(\mathbb{C}^2)
\bigoplus_{n\in\mathbb{Z}} V_{\lambda+2n}

% Index entry (manual, inside defn body)
\index{term}
\index{parent!child}   % e.g. \index{weight!highest weight}

% Citation
\citep{key}   % (Author)  — italic parens
\cite{key}    % Author    — italic
```

## TikZ Weight Diagrams (pattern from ch. 5)
```latex
\begin{center}
\begin{tikzpicture}[>=Stealth, baseline=(current bounding box.center)]
    \filldraw (0,0) circle (2pt);
    \node[below=6pt] at (0,0) {$V_0$};
    % arrows between nodes:
    \draw[->, bend left=25] (-2.35,0.08) to node[above] {\small$E$} (2.35,0.08);
    \draw[->, bend left=25] (2.35,-0.08) to node[below] {\small$F$} (-2.35,-0.08);
\end{tikzpicture}
\end{center}
```
Hexagon root diagram: see ch. 5 (`\coordinate`, `filldraw[fill=gray!15]`, vertices at `(60:1)` etc.)

## Transcription Workflow
1. User sends screenshot of 1–3 handwritten pages
2. Identify: section heading? theorem/def/example/remark/proof?
3. Pick the right command from the table above
4. Write math inline; use `align*` for multi-line derivations
5. Add `\index{term}` inside `\defn` body for new terms (or use `\defn[index key]{Title}{...}`)
6. Append to the appropriate `content/XX_*.tex` file

## Workflow notes (learned)
- **No trailing `%`** after opening braces of box commands (write `\rmkb{`, not `\rmkb{%`). User dislikes it; boxes trim leading whitespace anyway.
- Transcribe **faithfully**: minimal changes, make full sentences from keypoints, formalize sketched ideas into precise statements, but **add nothing not in the notes**. Flag (don't silently fix) likely physics/notation slips (e.g. Ξ⁰ vs Ξ⁺), and call out any clarifying additions you make.
- Default action when sent a screenshot: identify each item (def/thm/lemma/prop/cor/example/remark/proof/section heading), pick the matching box command, transcribe into the **current chapter file**, appending after the existing content. **Never compile** (`latexmk` etc.) unless the user explicitly asks — the user manages builds themselves.
- Lecturer-authored content only; the gauge-theory `\rmkb` at the end of ch.5 is explicitly marked "(Added by transcriber, not part of the lecture.)" — keep that disclaimer for any transcriber additions.
- Lemma without a title: use `\lem{}{...}` (empty first arg → renders just "Lemma").
- **tikzcd**: put diagrams in a `center` environment, NOT inside `\[ ... \]`. Do NOT use quoted edge labels at all when they contain macros/`^`/`?` (e.g. `\arrow[dr,"\exp(ixa)"]`, `"e^{ix}"`, `"\exists?"`, `"\text{x}"`) — they break tikz-cd's `\csname` node-naming → "Missing \endcsname / culprit is a tikzcd arrow". Leave arrows unlabeled and explain in prose. **Inside a box command** (`\ex`, `\defn`, `\rmkb`, … — bodies are `+m` verbatim), tikzcd's `&` gets the wrong catcode → "Single ampersand used with wrong catcode" (+ spurious "\mathrm allowed only in math mode"). Fix: `\begin{tikzcd}[ampersand replacement=\&]` and use `\&` between cells.
- Weight diagrams: keep root/E labels outside the hexagon stacked with `\shortstack`; reuse the ch.5 TikZ patterns (`>=Stealth`, `baseline=(current bounding box.center)`, vertices at `(60:1)` etc.).
- Coset/quotient notation: write classes explicitly as `x + \mathfrak{h}` (not `[x]`) to avoid clashing with Lie-bracket `[ , ]`.
- **Box command arg counts (verified):** `\corp{body}{proof}{ref}` needs the 3rd `{}` (empty ref) or it errors "File ended while scanning". `\thmp{title}{body}{proof}` for theorem-with-proof. `\lemp{title}{body}{proof}` — empty `{}` title renders just "Lemma".
- **TikZ libraries:** `decorations.pathreplacing` added to `style/project.sty` (for `brace` underbraces in the Dynkin classification figure). `enumitem` is loaded (so `[label=(\arabic*)]`, `[label=\Alph*)]` work).
- Root/Dynkin diagrams: reuse the rank-2 patterns — `A₂` 6 roots at `0,60,…`; `B₂` short at `0,90,…` (len 1) + long at `45,135,…` (len √2≈1.414); `g₂` short `0,60,…` (len 1) + long `30,90,…` (len √3≈1.732). Simple roots = violet `->` arrows; Dynkin multi-edges = parallel lines + a `>` chevron toward the shorter root.
- Citations go through a custom `\cite` (`style/project.sty`): `\cite[Chapter~5]{key}` = postnote; `\cite[pre][post]{key}`. Bröcker–tom Dieck entry `BrockerRepresentationsCompactLieGroups2010` added to `refs.bib` (GTM 98; date set to 2010 to match key, original is 1985).
- **Cross-refs to theorem/defn boxes:** all `tcbtheorem` boxes share the `mydefinition` counter (`use counter from=mydefinition`), so cleveref has no per-type name and `\cref{thm:label}` renders as "?? 3.2.12". Use plain `\ref{thm:label}` (→ just "3.2.12") and write the type word yourself (e.g. "Maschke's theorem, \ref{thm:maschke}"). Referenceable variants: `\defnr` (`defn:`), `\thmr` (`thm:`), `\thmpr` (`thm:`, added 2026-07-08). Maschke's theorem has label `thm:maschke`.

## Active Chapter Progress (ch. 7 — CURRENT)
**Current file: `content/07_representations_of_compact_lie_groups.tex`** (title "Representations of compact Lie groups"). Append new transcriptions here. Wired into `main.tex` (line 22).

Ch. 5 **complete** (su(n)). Ch. 6 transcribed through §7 (Weyl character/dimension formula, Example 7.34). Ch. 7 just started: chapter-intro (finite-group inner product → compact-group Haar measure), then `\section{Integration on manifolds}` with `\defn{Metric}` (Euclidean = pos. def.). Lecturer numbers items 7.xx (continuing from ch.6's numbering).

**Ch. 6 is split into flat `\section`s (no subsections — keep it that way; promote, don't orphan):**
1. `\section{Ideals, simple and semisimple Lie algebras}`
2. `\section{Cartan subalgebras and the root space decomposition}`
3. `\section{The Killing form and structure constants}`
4. `\section{Simple roots, Dynkin diagrams and the classification}`
5. `\section{Root strings and the Weyl group}`
6. `\section{Highest weight representations}` (weight decomposition, dominant weights/classification of fundamental reps, quadratic Casimir, Freudenthal recursion formula)
7. `\section{The Weyl character formula}` ← append new transcriptions at the end here

The numbered list below maps content to these sections (item → section): 1–9 → §1; 10–17 → §2; 18–21 → §3; 22–26 → §4; 27–29 → §5.

Ch. 6 content in order:
1. Motivation: finite-group `H ⊴ G → G/H` analogy → Lie algebra `h → g → g/h` (tikzcd, unlabeled dashed vertical arrow); normality differentiates to bracket condition.
2. `\defn` **Ideal** — subspace `h ⊆ g` with `[X,H] ∈ h ∀ X∈g, H∈h`.
3. `\rmkb` every ideal is a Lie subalgebra.
4. `\ex` ideal examples: `0`, `g`; `h = T_eH` from normal `H ⊴ G`; any subspace of abelian g; derived subalgebra `g' = [g,g]`.
5. `\propp` quotient Lie algebra `g/h` with bracket `[x+h, y+h] := [x,y]+h` (+ well-definedness proof).
6. `\rmkb` extension `0 → h → g → g/h → 0`.
7. `\defn` **Simple Lie algebra** — non-abelian, only ideals `0` and `g`.
8. `\lem{}` simple ⟹ `g = [g,g]` (**stated without proof — proof likely on a next page**).
9. `\rmkb` "Types of Lie algebras" TikZ diagram (simple → semisimple; abelian; both → reductive `A⊕g`).
10. `\defn` **Semi-simple element** — `[X,-]` diagonalizable.
11. `\defn` **Cartan subalgebra** — maximal abelian subalgebra of semisimple elements; dim = **rank**.
12. `\rmkb` Cartan not unique, choice won't matter.
13. `\ex` diagonal matrices form a Cartan subalgebra of `sl(N)`.
14. `\defn` **Root space decomposition** — `g = g_0 ⊕ ⊕_α g_α`, `g_0` Cartan, `α ∈ g_0^*`; defines **roots** and **root system** `Φ(g)`.
15. `\rmkb` **Facts about roots** (span `g_0^*`; root spaces 1-dim; only multiples ±α; integer basis `α(H_i)∈ℤ`).
16. `\defn` **Cartan–Weyl basis** `{H_i} ∪ {E^α}`.
17. `\ex` 3 rank-2 simple Lie algebras `sl(3)/A₂` (dim 8), `so(5)/B₂` (dim 10), `g₂` (dim 14) — TikZ root systems; `[H,[E^α,E^β]]=(α+β)(H)[E^α,E^β]` ⟹ weight of `[E^α,E^β]` is `α+β`.
18. `\defn` **Killing form** `κ(X,Y)=Tr_g(ad_X∘ad_Y)`.
19. `\rmkb` **Facts** (κ non-deg ⟹ `g≅g*`; restriction to `g_0` non-deg; diagrams respect it). Then: `\propp` orthogonality `g_α⊥g_β` (α+β≠0); `\defn` metric dual `t_α` (`κ(t_α,-)=α`); `\lemp` `[E^α,E^-α]=κ(E^α,E^-α)t_α`; `\defn` inner product on `g_0^*` `(α,β):=κ(t_α,t_β)=α(t_β)`; `\propp` `sl(2)`-triples `H^α:=2t_α/(α,α)`, `[E^α,E^-α]=H^α`, `[H^α,E^±α]=±2E^±α`; `\rmkb` constrains rep theory.
20. **Structure constants** (`\section`): `[T^a,T^b]=Σf^{ab}_c T^c`; `\defn` + identities; `\ex` `sl(2)` (`f^{ij}_l=2iε`), `gl(n)`.
21. `\propp` structure constants of Cartan–Weyl basis (`f^{iα}_β=α^iδ`, `f^{αβ}_i=α̃_iδ_{α,-β}`, `f^{αβ}_γ=e_{α,β}δ`); Killing form `(*)` (cites Exercise 1, Sheet 10); `\corp` `(λ,μ)=Σ_α(α,λ)(α,μ)`.
22. `\defn` **Root space** (real span of roots, `(·,·)` pos. def.); `\rmkb` two meanings of "root space"; `\defn` **Positive/negative roots** via hyperplane `ℍ` (= `\mathbb{H}`, through origin), `Φ_±`.
23. `\ex` 7.16 `A₂` with `ℍ`/`V_±`/simple roots (TikZ, shaded half-spaces); `\defn` **Simple root**; `\rmkb` facts about simple roots; `\defn` **Cartan matrix** `A^{ij}:=2(α^{(i)},α^{(j)})/(α^{(j)},α^{(j)})`.
24. `\ex` 7.19 Cartan matrices of `A₂,B₂,g₂` (root diagrams + matrices); `\subsection{Dynkin diagrams}` (recipe); `\ex` 7.20 Dynkin diagrams.
25. `\rmkb` **Facts about A** (`A^{ii}=2`; `A^{ij}=0⟺A^{ji}=0`; `A^{ij}∈{0,-1,-2,-3}`; `n^{ij}=A^{ij}A^{ji}=4(α^{(i)},α^{(j)})²/(...)∈{0,1,2,3}` ↔ 90/120/135/150°).
26. `\thmp` 7.21 **Classification** — full Dynkin list `A_n…G₂,F₄` (big TikZ); proof slot cites `\cite[Chapter~5]{BrockerRepresentationsCompactLieGroups2010}`.
27. `\defn` **Height of a root**; grading `g=⊕_{j∈ℤ}g_{(j)}`; `\ex` `sl(3)` height grading (hexagon + height line); `\rmkb` highest root `θ`, `(θ,θ)≥(α,α)`, normalize `(θ,θ)=2`.
28. Root strings: `\defn` **Root string** `⊕_m g_{mα+β}`; `\propp` irreducible `sl_α(2)`-module; `\lemp` `α^{(i)}-α^{(j)}` never a root; weights `α^{(i)}(H^{α^{(j)}})=A^{ij}` (neg. integers); `\ex` `B₂` string; `\rmkb` symmetry about hyperplanes `β(H^{α^{(i)}})=0`.
29. `\defn` 7.22 **Weyl group** `W(g)` generated by reflections `s_{α^{(i)}}(β)=β-2(β,α^{(i)})/(α^{(i)},α^{(i)})·α^{(i)}`.

**Stopping point (2026-06-24):** finished through Def 7.22 (Weyl group). Lecturer numbers items Def/Thm 7.xx.

### Ch.6 notation in use
- Cartan denoted `\mathfrak{g}_0` in the root-space decomposition (the α=0 piece); the generic Cartan-subalgebra definition uses `\mathfrak{h}`. Root spaces `\mathfrak{g}_\alpha`, `α ∈ \mathfrak{g}_0^*`. (Ch.5 used `\mathfrak{h}` throughout for sl(3) — kept per the notes.)
- **Cartan matrix `A^{ij}` (superscripts), simple roots `\alpha^{(i)}` (parenthesised superscript).** The notes are inconsistent (`A_{ij}` in some places); kept `A^{ij}` throughout for consistency.
- Killing form `\kappa`; `ad_X=[X,-]`; metric dual `t_α` (`κ(t_α,-)=α`); coroot element `H^α:=2t_α/(α,α)`; structure-constant root vectors `E^α`, normalisation constants `e_{α,β}`, `\tilde\alpha_i`.
- Hyperplane for positive/neg roots: `\mathbb{H}` (blackboard, to avoid clash with `H^i`). `g₂` written `\mathfrak{g}_2`.
- Lecturer flags I did **not** silently fix (confirm with user): `A_n ↔ sl(n)` written under the Dynkin list (standard is `sl(n+1)`); Def 7.18 says "set of positive roots" but means **simple** roots (wrote "simple"); Fact (4) numerator written `(α_i,α_j)` but must be **squared** `(α_i,α_j)²` (wrote squared); the `[H^α,E^-α]` sl(2) relation RHS should be `-2E^{-α}` (notes' superscript ambiguous).
- Purple/blue side-notes in the scans → rendered as plain `\emph{(...)}` (user dislikes the blue `\rmk` inline command); red "(Maybe not mention / Exclude?)" lecturer asides → content kept, the meta-question itself not transcribed.

### Ch.5 notation to stay consistent with
- Cartan `\mathfrak{h}`, basis `H_{12}, H_{23}`. Functionals `L_1,L_2,L_3`, `L_1+L_2+L_3=0`.
- Matrix units `E_{ij}`, weight `L_i-L_j`. Positive roots `E_{12}, E_{13}, E_{23}`.
- Highest weight map `\ell` (a>b>c choice). Root lattice `\Lambda_R`, weight lattice `\Lambda_W`.
- ρ suppressed: `Hv := \rho(H)v`. Reps in bold: `\mathbf{3}, \bar{\mathbf{3}}, \mathbf{8}, \mathbf{10}`.
