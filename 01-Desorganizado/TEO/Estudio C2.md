# CC3102 Theory of Computation: Lecture Notes for Control 2

*From context-free languages to undecidability. Written for a beginner, built around the three evaluations you attached (Control 2 2026, the pre-control 2 auxiliar, Control 2 2025) and Classes 01-17.*

**Language note:** explanations are in English, but the course vocabulary is Spanish, so key terms appear as English (español). Direction symbols: the class uses **I** (izquierda = Left) and **D** (derecha = Right); I write **L** and **R**.

---

## How to use these notes

1. Read a chapter, then close it and re-derive the worked examples on a blank page.
2. Every chapter ends with an **Exam connection** section. Try the exam problem *before* opening the `<details>` block with the guided solution.
3. The **Recap** at the end is a memory-helper: the definitions, the 7 proof templates, the pitfalls.

### The 7 problem types in the evaluations

| # | Problem type | Where it appears | Chapter |
|---|---|---|---|
| 1 | Prove a language is **not context-free** (pumping lemma for CFLs) | C2-2026 P1.1 | 4 |
| 2 | Prove CFLs are **not closed** under an operation | C2-2025 P1 (CUT), Pre-control P2 (perfect shuffle) | 4 |
| 3 | **Build a TM** (compute a function / recognize a language) | C2-2025 P2 (i mod 3), Pre-control P3 (average), P4 (Fermat) | 5, 6, 8 |
| 4 | **Simulation / equivalence of models** | C2-2026 P1.2 (2-stack PDA), Pre-control P1 (single-overwrite TM), C2-2025 P3 (queue automaton) | 7 |
| 5 | Prove a language is **decidable** | C2-2026 P2.1(a) | 9 |
| 6 | **Diagonalization** argument | C2-2026 P2.1(b) | 9 |
| 7 | **Reduction from A_TM** | C2-2026 P2.2 (L_estado) | 10 |

---

# Chapter 1. Foundations: strings, languages, closure, proof tools

**Goal:** speak the vocabulary used in every later chapter and own the three proof tools (contradiction, pigeonhole, countability) plus the pumping-lemma *pattern*.

## 1.1 Vocabulary

| Term | Meaning | Example |
|---|---|---|
| Alphabet Σ | a finite, non-empty set of symbols | Σ = {0,1} |
| String / word (cadena, palabra) | a finite sequence of symbols of Σ | 0110 |
| ε | the **empty string**, length 0 (ε ∉ Σ) | |ε| = 0 |
| \|w\| | length of w | \|0110\| = 4 |
| w·x or wx | concatenation | 01·10 = 0110 |
| wᵏ | w written k times; w⁰ = ε | (01)³ = 010101 |
| wᴿ | w reversed | (011)ᴿ = 110 |
| Σ* | **all** finite strings over Σ | {ε,0,1,00,01,...} |
| Language (lenguaje) | **any subset of Σ*** | {0ⁿ1ⁿ \| n ≥ 0} |

**Two things beginners confuse:**

- `∅` is the language with **no** strings. `{ε}` is the language with **exactly one** string, the empty one. They are different: `{ε}` has one element, `∅` has none.
- Every string in Σ* has finite length. The *language* may be infinite, but each string is finite.

**Why Σ* is countable:** list strings by length, and within a length alphabetically: ε, 0, 1, 00, 01, 10, 11, 000, ... Every string appears at a finite position.

## 1.2 Operations on languages and "closure"

For languages A, B over Σ:

| Operation | Definition |
|---|---|
| Union | A ∪ B = {w \| w ∈ A or w ∈ B} |
| Intersection | A ∩ B = {w \| w ∈ A and w ∈ B} |
| Complement | Aᶜ = Σ* \ A |
| Concatenation | A∘B = {xy \| x ∈ A, y ∈ B} |
| Kleene star | A* = A⁰ ∪ A¹ ∪ A² ∪ ..., with A⁰ = {ε} |

**Closure.** A class of languages C (for instance "regular languages") is **closed under an operation** if applying the operation to members of C always gives a member of C.

- To prove **closed**: give a construction that works for *arbitrary* members (e.g. "given automata for A and B, build one for A ∪ B").
- To prove **not closed**: exhibit **one specific** pair (A, B) in the class such that the result is *not* in the class. You must show both facts: A, B really are in the class, and the result is not.

This second pattern is exactly what Chapter 4 uses (CUT, perfect shuffle).

## 1.3 Three proof tools

**Proof by contradiction.** To show P is false, assume P, derive something impossible. Every "is not regular", "is not context-free" and "is undecidable" proof in this course has this shape.

**Pigeonhole principle (principio del palomar).** If you put more than k objects into k boxes, some box has two. In automata: a DFA with p states reading p+1 symbols visits p+1 states, so some state repeats. That repeat is the whole engine of the regular pumping lemma.

**Countable vs. uncountable.**

- A set is *countable* if its elements can be listed as a first, second, third... item.
- Σ* is countable (above). The set of all TMs is countable because each TM is described by a finite string.
- The set of all languages is **uncountable**: a language L ⊆ Σ* is the same thing as its infinite binary *characteristic sequence* χ_L (position k is 1 iff the k-th string is in L). Cantor's diagonal argument: given any list of infinite binary sequences, flip the k-th digit of the k-th sequence; the resulting sequence is not in the list. So no list covers all languages.
- Conclusion (used in Chapter 9): **countably many TMs, uncountably many languages ⇒ some language has no TM.**

## 1.4 Automata in ten minutes

A **DFA** (AFD) is a 5-tuple (Q, Σ, δ, q₀, F): finite states Q, alphabet Σ, transition function δ : Q × Σ → Q, start state q₀, accepting states F ⊆ Q. It reads the input left to right, one symbol at a time, and accepts iff it ends in F.

An **NFA** (AFND) allows several transitions for the same symbol and ε-transitions: δ : Q × Σ_ε → P(Q). It accepts iff **some** branch ends in an accepting state.

**NFA = DFA** (subset construction): a DFA whose states are *sets* of NFA states remembers "all places the NFA copies could be." With k NFA states the DFA has up to 2ᵏ states.

**Regular language** = recognized by a DFA = recognized by an NFA = described by a regular expression.

**Intuition for non-regularity:** a DFA has *finite memory*. A language that requires counting to an unbounded number (like 0ⁿ1ⁿ) cannot be regular.

## 1.5 The regular pumping lemma: learn the *pattern*

**Lemma.** If A is regular, there is a number p (the pumping length) such that every s ∈ A with |s| ≥ p can be split s = xyz with
1. xyⁱz ∈ A for every i ≥ 0,
2. |y| > 0,
3. |xy| ≤ p.

**Why it is true (proof idea).** Let p = number of states of a DFA for A. Reading the first p symbols of s visits p+1 states, so one state repeats. The stretch of input between the two visits is y. The DFA is in the same state before and after y, so it can go around the loop 0, 1, 2, ... times and still end where it ended before.

**Strategy to prove L is not regular**

1. Assume L is regular; let p be its pumping length.
2. Choose a concrete s ∈ L with |s| ≥ p (it depends on p).
3. Show that for **every** split s = xyz satisfying (2) and (3), some i gives xyⁱz ∉ L.
4. Contradiction.

**Worked example: L = {0ⁿ1ⁿ | n ≥ 0} is not regular.**
Take s = 0ᵖ1ᵖ ∈ L. Because |xy| ≤ p, both x and y lie inside the block of 0s, so y = 0ᵏ with k ≥ 1. Then xy²z = 0^(p+k)1ᵖ has more 0s than 1s, so it is not in L. Contradiction. ∎

**Self-check (from the study plan): why does the regular lemma say |xy| ≤ p but the CFL lemma says |vxy| ≤ p?** In a DFA the repeated state shows up within the *first* p symbols, so the pumped piece sits at the beginning. In a parse tree the repeated variable shows up on the *lowest* part of a long path, so the pumped piece is *somewhere* in the string; all we control is that the piece "v x y" is short. That is why in Chapter 4 the pumped part can be in the middle and you must analyze where it can lie.

**Practice (Class 06):** show that "equal number of 0s and 1s", "balanced parentheses", {aⁿ | n prime} and {0ⁿ1ᵐ | n ≠ m} are not regular. (Hint for "equal number of 0s and 1s": intersect with 0*1* and use closure, or pump directly with s = 0ᵖ1ᵖ.)

---

# Chapter 2. Context-free grammars (CFG / GLC)

**Goal:** know what a grammar *generates*, how to design one, what ambiguity is, and what Chomsky normal form buys you.

## 2.1 What a grammar is

Finite automata fail on {0ⁿ1ⁿ}. A **context-free grammar** can generate it. A grammar does not *read* strings, it **generates** them by rewriting.

```
A → 0A1 | B
B → #
```

- **Variables** (non-terminals): A, B. **Terminals**: 0, 1, #. **Start variable**: A (the left side of the first rule).
- A **rule** `X → w` says "the variable X may be replaced by the string w."
- `X → Y | Z` is shorthand for two rules.

A **derivation** starts from the start variable and applies rules one at a time (⇒):

A ⇒ 0A1 ⇒ 00A11 ⇒ 000A111 ⇒ 000B111 ⇒ 000#111

The same derivation drawn as a **parse tree** (árbol de derivación): the root is the start variable, each internal node is a variable, its children are the right-hand side of the rule used, and the leaves read left to right are the generated string. Parse trees are the key object for the pumping lemma.

## 2.2 Formal definition

A CFG is a 4-tuple **G = (V, Σ, R, S)**:
- V: finite set of variables,
- Σ: finite set of terminals, disjoint from V,
- R ⊆ V × (V ∪ Σ)*: rules,
- S ∈ V: start variable.

Notation: `u ⇒ v` means one rule application; `u ⇒* v` means zero or more. The language is **L(G) = {w ∈ Σ* | S ⇒* w}**. A language is **context-free (LLC)** if some CFG generates it.

## 2.3 Designing grammars: four recipes

| Situation | Recipe | Example |
|---|---|---|
| **Union** L₁ ∪ L₂ | new start `S → S₁ \| S₂` | {0ⁿ1ⁿ} ∪ {1ᵐ0ᵐ} |
| **Regular language** | one variable Rᵢ per DFA state; for δ(qᵢ,a)=qⱼ add `Rᵢ → aRⱼ`; for each final qᵢ add `Rᵢ → ε`; start = R₀ | "ends in 1" |
| **Interdependent parts** (the two sides must match) | a rule that wraps: `R → u R v` | 0ⁿ1ⁿ: `S → 0S1 \| ε` |
| **Repetition** (Kleene star) | `R → T R \| ε`, `T → u` | (0*1*)* |

**Worked example 1: L = {aⁱbʲcᵏ | i = j or j = k}** (this is "union + interdependence"):

```
S  → S₁ | S₂
S₁ → X C          // aⁱbⁱ followed by any cᵏ  (case i = j)
X  → aXb | ε
C  → cC | ε
S₂ → A Y          // any aⁱ followed by bʲcʲ  (case j = k)
A  → aA | ε
Y  → bYc | ε
```

**Worked example 2: palindromes over {a,b}:** `S → aSa | bSb | a | b | ε`. The outer pair must match (interdependence); the middle is empty or one symbol.

**Worked example 3 (Class 07, G₂):** `S → aSb | SS | ε` generates balanced "a = open, b = close" strings: every prefix has at least as many a's as b's, and the totals are equal.

## 2.4 Ambiguity

A grammar is **ambiguous** if some string has two different parse trees (equivalently two different leftmost derivations). Example: `E → E+E | E×E | (E) | 0..9` and the string `2+3×5` has two trees, one grouping `(2+3)×5`, one grouping `2+(3×5)`; "5+3×2 is 16 or 11?" has no single meaning.

Key facts:
- Ambiguity is a property of **the grammar**, not of the language. You can often fix it by rewriting: `E → E+T | T`, `T → T×F | F`, `F → (E) | a` generates the same language unambiguously (it forces × to bind tighter).
- Some languages are **inherently ambiguous** (every grammar is ambiguous), e.g. {aⁱbʲcᵏ | i = j or j = k}.
- To *show* a grammar is ambiguous you only need to exhibit **one string with two trees**.

## 2.5 Chomsky normal form (FNC)

A grammar is in **Chomsky normal form** if every rule is `A → BC` or `A → a` (B, C are not the start variable), plus `S → ε` allowed for the start variable only. Every CFL has a grammar in this form (the conversion removes ε-rules, unit rules, and long rules).

**Why it matters:** in CNF, every string of length n ≥ 1 is derived in **exactly 2n − 1** steps. Reason: each `A → BC` step increases the number of symbols by one, starting from one symbol (S) and ending with n symbols, so n − 1 of them are needed; each of the n terminals needs one `A → a` step. Total (n − 1) + n = 2n − 1.

Consequence: to test whether G generates w, convert to CNF and try *all* derivations of 2|w| − 1 steps. There are finitely many, so the test always terminates. This is why **A_CFG is decidable** (Chapter 9).

## 2.6 Checklist

- [ ] Can I write G = (V, Σ, R, S) for a given language?
- [ ] Can I show ambiguity by drawing two trees for one string?
- [ ] Do I know why a CNF derivation of a length-n string takes 2n − 1 steps?

**Practice:** grammars for {0ⁿ1ⁿ}, the language of G₂, {0ⁿ1ⁿ} ∪ {1ᵐ0ᵐ}, {aⁱbʲcᵏ | i=j or j=k}, palindromes.

---

# Chapter 3. Pushdown automata and the equivalence with CFGs

**Goal:** understand the PDA (AP) as "NFA + stack," trace one, and know the equivalence PDA ⇔ CFG and the closure properties of CFLs. The closure properties are used directly in Chapter 4.

## 3.1 The idea

An NFA has finite memory. Add a **stack** (pila): memory you can only access at the top, by **push** (put a symbol on top) and **pop** (remove the top symbol). A stack can count: push a symbol per 0, pop one per 1.

Transition label **`a, b → c`** means: read `a` from the input, pop `b` from the stack, push `c`.
- `a = ε`: do not read input. `b = ε`: do not pop. `c = ε`: do not push.

**The `$` trick.** You cannot ask "is the stack empty?" directly, so the first move pushes a marker `$` at the bottom; seeing `$` on top means "nothing else is there."

**Acceptance in this course (Class 08):** the PDA accepts if there is a computation where the input is fully read, the machine is in an accepting state, **and the stack is empty**. (Note: the 2-stack PDA of Control 2 2026 is defined with the simpler rule "accepts if some computation ends in an accepting state.")

## 3.2 Formal definition

A PDA is a 6-tuple **(Q, Σ, Γ, δ, q₀, F)**:
- Q states, Σ input alphabet, Γ stack alphabet,
- **δ : Q × Σ_ε × Γ_ε → P(Q × Γ_ε)** (non-deterministic: a set of possible moves),
- q₀ start, F accepting states.

**Formal acceptance:** w = w₁...wₘ (wᵢ ∈ Σ_ε) is accepted if there are states r₀,...,rₘ and stack contents s₀,...,sₘ ∈ Γ* with
1. r₀ = q₀, s₀ = ε (start with empty stack),
2. each step is a legal transition: (rᵢ₊₁, c) ∈ δ(rᵢ, wᵢ₊₁, b) where sᵢ = b·t and sᵢ₊₁ = c·t,
3. rₘ ∈ F and sₘ = ε.

## 3.3 Worked example: {0ⁿ1ⁿ | n ≥ 0}

States q₀,q₁,q₂,q₃; F = {q₀,q₃}.

```
q₀ --ε,ε→$--> q₁
q₁ --0,ε→0--> q₁        (push a 0 per 0 read)
q₁ --1,0→ε--> q₂        (first 1: pop a 0)
q₂ --1,0→ε--> q₂        (further 1s: pop a 0 each)
q₂ --ε,$→ε--> q₃        (stack down to $: remove it, accept)
```

Trace on `0011` (stack top written first): start (q₀, ε) → (q₁, $) → read 0: (q₁, 0$) → read 0: (q₁, 00$) → read 1: (q₂, 0$) → read 1: (q₂, $) → ε-move: (q₃, ε). Input finished, accepting state, empty stack, accepted.

**Why a PDA cannot do {0ⁿ1ⁿ0ⁿ}:** after popping n zeros to check the 1s, the stack has forgotten n, so it cannot check the final block of 0s. (Stack information is destroyed when you read it.) This is exactly what the pumping lemma will prove formally.

## 3.4 Design recipes (Class 08 list)

- **w wᴿ (even palindromes):** push the first half; **non-deterministically guess** the midpoint (ε-transition) and then pop to match each symbol. The guess is why PDAs need nondeterminism: unlike a DFA, you cannot know where the middle is.
- **{aⁱbʲcᵏ | i=j or j=k}:** branch non-deterministically at the start: one branch checks i=j (push a's, pop on b's, ignore c's), the other checks j=k (ignore a's, push b's, pop on c's).
- **Complement of {aⁿbⁿ}:** accept strings *not* of the form aⁿbⁿ: branch to check (i) wrong order (a b a ...), (ii) more a's than b's, (iii) more b's than a's.

## 3.5 PDA ⇔ CFG (the idea of each direction)

**Theorem.** A language is context-free iff some PDA recognizes it.

**CFG → PDA (simulate a derivation).** The PDA keeps the "not yet resolved" part of the sentential form on the stack.
1. Push `S$`.
2. Loop non-deterministically:
   - top is a variable A: pop it and push the right side of a rule `A → z` (guess which rule), i.e. `ε, A → z`;
   - top is a terminal a: it must match the next input symbol: `a, a → ε`;
   - top is `$`: pop it and accept (`ε, $ → ε`).

Because only terminals at the top are compared to input and variables are expanded, the PDA accepts x iff some derivation `S ⇒* x` exists. (A rule's right side with several symbols is pushed using intermediate states; this is the "convention" slide.)

**PDA → CFG (idea only).** Normalize the PDA to have a single accepting state, empty the stack before accepting, and make each move either a pure push or a pure pop. Create a variable **A_pq** meaning "the PDA can go from state p (empty stack) to state q (empty stack) reading exactly this string." Rules:
- `A_pq → a A_rs b` when p →(a, push t)→ r and s →(b, pop t)→ q (a push and its matching pop wrap an inner computation),
- `A_pq → A_pm A_mq` (split at an intermediate point where the stack is empty),
- `A_pp → ε`.
Start variable: A_{q₀, q_accept}. Correctness is proved by induction on derivation length / computation length (Sipser pp. 123-124).

## 3.6 Closure properties of CFLs

| Operation | CFLs closed? | Why |
|---|---|---|
| Union | **Yes** | new start `S → S₁ \| S₂` |
| Concatenation | **Yes** | `S → S₁S₂` |
| Kleene star | **Yes** | `S → S₁S \| ε` |
| Intersection | **No** | counterexample below |
| Complement | **No** | De Morgan: A ∩ B = (Aᶜ ∪ Bᶜ)ᶜ; closure under complement + union would give closure under intersection |
| Intersection with a **regular** language | **Yes** | product construction: run the PDA and the DFA simultaneously, states Q₁ × Q₂, still a single stack |

**Counterexample for intersection.**
- A = {aⁿbⁿcᵐ | n,m ≥ 0} is context-free (`S → XC`, `X → aXb | ε`, `C → cC | ε`).
- B = {aᵐbⁿcⁿ | n,m ≥ 0} is context-free (symmetric).
- A ∩ B = {aⁿbⁿcⁿ | n ≥ 0}, which is **not** context-free (Chapter 4). So CFLs are not closed under intersection.

**Self-check: why does the product construction work for PDA × DFA but fail for PDA × PDA?** Two stacks would be needed (one per PDA) and a PDA has only one. A DFA needs no stack, only a state.

**The "intersect with regular" tool is very useful in Chapter 4**: if you suspect L is not context-free but pumping is messy, intersect L with a regular language to isolate a clean sub-case. If L were context-free, L ∩ regular would be too.

## 3.7 Checklist

- [ ] Can I read `a, b → c` and trace a computation with the stack contents?
- [ ] Can I design a PDA using "push, guess the middle, pop"?
- [ ] Can I state which operations CFLs are/aren't closed under, and give the counterexample for ∩?
- [ ] Do I know why ∩ with a regular language works?

---

# Chapter 4. The pumping lemma for context-free languages

**Goal:** prove a language is *not* context-free, and prove CFLs are *not closed* under an operation. This topic is on **every** attached evaluation.

## 4.1 Statement

**Lemma (pumping lemma for CFLs).** If L is context-free, there is a number p (the pumping length) such that every s ∈ L with |s| ≥ p can be written **s = u v x y z** with

1. **uvⁱxyⁱz ∈ L for every i ≥ 0** (pump v and y *together*, the same number of times),
2. **|vy| > 0** (at least one of v, y is non-empty),
3. **|vxy| ≤ p** (the middle window is short).

Compared with the regular lemma: *two* pumped pieces (v and y) instead of one, and the window condition is on vxy, not on a prefix.

## 4.2 Why it is true (the parse-tree idea)

Take a grammar for L in which every right-hand side has at most b symbols, and let p = b^(|V|+1).

- A parse tree of height h generates a string of length at most bʰ. So a string of length ≥ p needs a tree of height ≥ |V| + 1.
- A path from the root to a leaf in such a tree passes through ≥ |V| + 1 variables, so by the **pigeonhole principle some variable R appears twice** on the path. Take the repeat among the *lowest* |V| + 1 variables.
- Call the upper occurrence of R the *outer* R and the lower the *inner* R. The tree looks like this:

```
          S
         /|\
        u  R  z            outer R generates  v x y
          /|\
         v  R  y           inner R generates  x
            |
            x
```

- Since the outer and inner nodes are both R, we may replace the outer subtree by the inner one (this gives i = 0: u x z) or replace the inner one by the outer one again and again (i = 2, 3, ...: u v v x y y z). Condition 1 holds.
- v and y cannot both be empty, otherwise (choosing the tree with the fewest nodes) the repeat would be redundant. Condition 2 holds.
- The outer R was chosen among the lowest |V| + 1 variables on the path, so its subtree has height ≤ |V| + 1 and generates at most b^(|V|+1) = p symbols. Condition 3 holds.

## 4.3 What each condition buys you in a proof

- **Condition 1** is what you attack: you will exhibit an i for which uvⁱxyⁱz ∉ L.
- **Condition 2** guarantees pumping actually *changes* the string, so counts really change.
- **Condition 3** is your weapon for case analysis: because the window vxy is shorter than p, it **cannot span far**. If s consists of blocks (a's then b's then c's...) of length ≥ p, the window can touch **at most two adjacent blocks** and can never reach two blocks separated by a whole block.

## 4.4 The proof template

1. **Assume** L is context-free. Let p be the pumping length.
2. **Choose** a specific s ∈ L with |s| ≥ p. It must depend on p. *This is the creative step.* Choose s so that it is made of blocks whose lengths are tied together, and so that condition 3 will confine the window.
3. **Consider every decomposition** s = uvxyz that satisfies conditions 2 and 3. Organize the cases by **where v and y can lie** (inside one block; straddling two adjacent blocks; one piece in each of two adjacent blocks).
4. For each case **find an i** (usually 0 or 2) such that uvⁱxyⁱz ∉ L.
5. **Contradiction.** ∎

**Tip: classify by the *content* of vy, not by the exact position.** What breaks membership is which letters are in vy and how their counts change. Cases like "vy contains some a" and "vy contains no a" are often enough.

**The most common mistakes:** (a) forgetting the case where v and y are in *different* blocks; (b) choosing an s that does not depend on p; (c) pumping with only one i when another i is needed in some case; (d) not using |vxy| ≤ p.

## 4.5 Worked examples

### Example A: L = {aⁿbⁿcⁿ | n ≥ 0} is not context-free (Class 10)

Take s = aᵖbᵖcᵖ ∈ L. Since |vxy| ≤ p, the window cannot touch both an a and a c (the b-block of length p separates them). So vy has no a or has no c.

- vy contains an **a** (so no c): pump to i = 2. The a's increase, the c's stay p, so #a ≠ #c. Out of L.
- vy contains a **c** (so no a): pump to i = 2. #c increases, #a stays p. Out.
- vy contains **only b's**: i = 2. #b increases, #a = #c = p. Out.

(Any vy with |vy| > 0 falls under at least one of these.) Contradiction. ∎

### Example B: L = {aⁱbʲcᵏ | i ≤ j ≤ k} is not context-free

Take s = aᵖbᵖcᵖ ∈ L. The window cannot contain both a's and c's.

- If **vy contains an a** (so no c): pump **up**, i = 2. If vy has no b, then #a > p = #b, so i ≤ j fails. If vy also has a b, then #b > p = #c, so j ≤ k fails.
- If **vy contains no a** (so it has b's and/or c's): pump **down**, i = 0. If vy has a b, then #b < p = #a, so i ≤ j fails. If vy has only c's, then #c < p = #b, so j ≤ k fails.

These two cases cover everything (vy containing both an a and a c is impossible). Contradiction. ∎

**Lesson:** this example needed *both* pumping up and pumping down. Always check whether you need i = 0 or i = 2 per case.

## 4.6 Non-closure proofs: the recipe

To show "CFLs are not closed under operation Φ":

1. **Pick specific CFLs A (and B).** Prove they are context-free: give a grammar or PDA. (A frequent lost point: skipping this.)
2. **Compute (or bound) Φ(A, B)** and show it equals, or intersects with a regular language to give, a language you can prove non-context-free.
3. **Prove that language non-CFL** with the pumping lemma.
4. **Conclude:** if the class were closed, Φ(A, B) would be context-free, contradiction.

**Useful tools:** closure under ∩ with a *regular* language (Chapter 3) and the **counting trick**: when the result's membership condition is a set of counting equations, then pumping breaks one equation. Also: a word in a language of the form `b*c*a*d*` is *uniquely determined by its letter counts*, which kills case analysis (see CUT below).

## 4.7 Exam connection

### C2-2026 P1.1: L = {aⁱbʲcᵏ | j = max{i, k}} is not context-free

*Try it yourself first.* Hints: the word s = aᵖbᵖcᵖ is in L. The window cannot touch both a's and c's. Decide *for each possible content of vy* whether i = 0 or i = 2 breaks j = max{i, k}. Note that **pumping down one block can leave max unchanged** (look at what happens when you delete only a's), so think before choosing i = 0 everywhere.

<details>
<summary>Guided solution</summary>

Assume L is context-free with pumping length p. Let s = aᵖbᵖcᵖ; j = p = max{p, p}, so s ∈ L. Let s = uvxyz with |vy| > 0 and |vxy| ≤ p. As in the previous examples, vy cannot contain both an a and a c.

**Rule:** use **i = 0** unless vy is *only a's* or *only c's*, in which case use **i = 2**.

- **vy only a's:** i = 2 gives #a = p + |vy| > p, #b = #c = p, so max = #a > p = #b. Out of L. (i = 0 would not work here: #a < p, then max{#a, #c} = p = #b, still in L.)
- **vy only c's:** symmetric, i = 2 gives max = #c > #b. Out.
- **vy only b's:** i = 0 gives #b < p but #a = #c = p, so max = p ≠ #b. Out.
- **vy contains an a and a b (no c):** i = 0 gives #b < p (a b was deleted) and #c = p so max ≥ p > #b. Out.
- **vy contains a b and a c (no a):** i = 0 gives #b < p, #a = p, so max ≥ p > #b. Out.

(Pure-a and pure-c can't be broken by i = 0; mixed or b-containing cases can.) Contradiction, so L is not context-free. ∎
</details>

### Pre-control P2: CFLs are not closed under perfect shuffle

Definition: shuffle(A, B) = {a₁b₁a₂b₂...aₖbₖ | a₁...aₖ ∈ A and b₁...bₖ ∈ B}, interleaving letter by letter. Both words must have the same length k.

*Try it yourself first.* Plan: choose A and B, each context-free, with **two blocks each** whose lengths are in ratio 1:2 and 2:1, so that the shuffle has **three** blocks of equal length n, a pattern a CFL cannot enforce.

<details>
<summary>Guided solution</summary>

Use four distinct letters so the shuffled word is easy to read.

- A = {aⁿb²ⁿ | n ≥ 0}, context-free: `S → aSbb | ε`.
- B = {c²ⁿdⁿ | n ≥ 0}, context-free: `S → ccSd | ε`.

A word in A has length 3n, a word in B of the same length has the same n. Pair letter t of the A-word with letter t of the B-word:
- t ≤ n: (a, c), t in (n, 2n]: (b, c), t in (2n, 3n]: (b, d).

So C = shuffle(A, B) = {(ac)ⁿ (bc)ⁿ (bd)ⁿ | n ≥ 0}.

*(Check against your handwritten attempt: with the same idea but the letters a, b in both languages, the middle block is (ab)ⁿ, not (ba)ⁿ, because the A-letter comes first in each pair.)*

**C is not context-free.** Every word of C has #a = #d = n and #b = #c = 2n. Suppose C is context-free with pumping length p and take s = (ac)ᵖ(bc)ᵖ(bd)ᵖ ∈ C. The window vxy has length ≤ p, so it cannot contain both an a and a d (the middle block (bc)ᵖ has length 2p between them).

- If vy contains an **a**: #d stays p (no d in vy) but #a changes when pumped (i = 0 or 2). So #a ≠ #d. Out.
- If vy contains a **d**: symmetric. Out.
- If vy contains **neither a nor d**, it only has b's and c's; pumping changes #b or #c while #a stays p, but membership demands #b = #c = 2#a = 2p. Out.

Contradiction. So C ∉ CFL, while A and B are CFLs, therefore CFLs are not closed under perfect shuffle. ∎

*Comment on your attempt:* "any partition pumped with i = 2 leaves the language" is correct but must be justified by a case analysis or a counting argument like the one above; and always verify the word you pump really belongs to your language.
</details>

### C2-2025 P1: CFLs are not closed under CUT

> **Heads-up about the statement:** as transcribed, the exam defines CUT(L) = {xyz | xyz ∈ L}, which equals L itself, so it would trivially be closed. The standard definition, which the hint (the language bᵐcⁿaᵐdⁿ) matches, is **CUT(L) = {xzy | xyz ∈ L}**: cut the word into three parts and swap the last two. I use it below. Check your original paper.

*Try it yourself first.* Plan: (1) show A = {bᵐcⁿaᵐdⁿ} is not context-free; (2) find a context-free L whose CUT, intersected with a regular language, is exactly A; (3) conclude with the closure under ∩ regular.

<details>
<summary>Guided solution</summary>

**Step 1: A = {bᵐcⁿaᵐdⁿ | m, n ≥ 0} is not context-free.** Let p be the pumping length and s = bᵖcᵖaᵖdᵖ ∈ A. The window has length ≤ p, so it cannot contain both b and a (c's of length p between), nor both c and d (a's between).
- vy contains a **b**: then it contains no a, so #b changes while #a stays p. Out.
- vy contains an **a**: then it contains no b, so #a changes while #b stays p. Out.
- vy contains **neither a nor b**: it lies in the c's and d's, and cannot contain both (a's lie between). If it has a c, #c changes while #d stays p; if it has a d, #d changes while #c stays p. Out.
Every vy ≠ ε falls in one of these. Contradiction. ∎

**Step 2: choose L.** L = {bᵐaᵐdⁿcⁿ | m, n ≥ 0}, context-free (concatenation of {bᵐaᵐ} and {dⁿcⁿ}).

**Step 3: CUT(L) ∩ b\*c\*a\*d\* = A.**
- (⊇) For bᵐcⁿaᵐdⁿ ∈ A take w = bᵐaᵐdⁿcⁿ ∈ L with x = bᵐ, y = aᵐdⁿ, z = cⁿ. Then xzy = bᵐcⁿaᵐdⁿ.
- (⊆) Any word of CUT(L) is a **rearrangement** of the letters of some bᵐaᵐdⁿcⁿ. If it also lies in b\*c\*a\*d\*, its letters are sorted in the order b, c, a, d, and a sorted word is **determined by its letter counts**: it must be bᵐcⁿaᵐdⁿ ∈ A.

**Step 4: conclude.** If CUT(L) were context-free, then CUT(L) ∩ b\*c\*a\*d\* = A would be context-free (CFLs are closed under ∩ with a regular language). Contradiction with Step 1. So CFLs are not closed under CUT. ∎
</details>

## 4.8 Checklist

- [ ] State the lemma exactly (p, uvxyz, three conditions).
- [ ] Explain the parse-tree intuition in two sentences.
- [ ] For a fresh language: justify my s, enumerate cases by the content of vy, choose i per case.
- [ ] For non-closure: prove A and B are CFLs *first*.

---

# Chapter 5. The Turing machine model

**Goal:** know exactly what a Turing machine (MT) is, how it computes step by step, and the three possible outcomes of a run.

## 5.1 Idea

A finite automaton has finite memory; a PDA has a stack you can only reach at the top. A **Turing machine** has an **infinite tape** it can read *and write*, and a head that moves **left or right** freely. It is the standard model of "an algorithm" (Chapter 8 explains why).

```
 control (finite states)
        ↓ head
 ┌───┬───┬───┬───┬───┬───┬───┐
 │ 0 │ 1 │ 1 │ ⊔ │ ⊔ │ ⊔ │ ... →  infinite to the right
 └───┴───┴───┴───┴───┴───┴───┘
 input at the left, then blanks ⊔
```

## 5.2 Formal definition

A TM is a 7-tuple **(Q, Σ, Γ, δ, q₀, q_acepta, q_rechaza)**:

1. Q: finite set of states.
2. Σ: **input alphabet**, ⊔ ∉ Σ.
3. Γ: **tape alphabet**, ⊔ ∈ Γ and Σ ⊂ Γ. (Γ contains extra symbols used as marks, like X.)
4. **δ : Q × Γ → Q × Γ × {L, R}**: from (state, symbol under the head) it determines (new state, symbol to write, direction).
5. q₀: start state.
6. q_acepta: accepting state. 7. q_rechaza ≠ q_acepta: rejecting state. Both **halt** the machine immediately.

**One step:** if the state is q, the head reads a, and δ(q, a) = (r, b, X), then the machine (1) writes b over a, (2) moves one cell left (X = L) or right (X = R), (3) enters state r.

## 5.3 Conventions you must know

- The input w₁...wₙ starts in the first cell, the rest of the tape is ⊔, and the head starts on the first cell.
- If the head is on the **first cell and must move left, it stays** (the tape is infinite only to the right).
- In state diagrams we **omit every transition into q_rechaza**: any (state, symbol) with no arrow goes to reject.
- Transition notation: `a → b, X` (read a, write b, move X), `a → X` (write back a), `a, b → X` (two transitions at once).
- Three levels of description: **formal** (the full transition table/diagram), **implementation** (a numbered verbal algorithm describing head movements and tape changes, like "zig-zag and mark with X"), **high level** (just the algorithm). The exams ask for formal or implementation level, as stated in each problem.

## 5.4 Configurations ("photographs")

A **configuration** (configuración) is a snapshot: tape contents, head position, current state. Written **u q v**: the tape holds uv, the machine is in state q, the head is on the **first symbol of v**.

Example: tape `01101`, state q, head on the 3rd cell: **01 q 101**.

**"Yields" relation (C₁ ⊢ C₂ , "lleva a"):**
- If δ(qᵢ, b) = (qⱼ, c, R): `ua qᵢ bv ⊢ uac qⱼ v`.
- If δ(qᵢ, b) = (qⱼ, c, L): `ua qᵢ bv ⊢ u qⱼ acv`.
- Head on first cell moving left: `qᵢ bv ⊢ qⱼ cv`. Head past the last symbol (reading ⊔) moving right: `u qᵢ ⊢ uc qⱼ`.

**Acceptance:** M accepts w if there is a sequence of configurations C₁,...,Cₖ with C₁ = q₀w (initial), each Cᵢ ⊢ Cᵢ₊₁, and Cₖ contains q_acepta. ⊢\* means "yields in zero or more steps."

**Language of M:** L(M) = {w ∈ Σ* | M accepts w}.

## 5.5 Three outcomes: accept, reject, loop

For each input a TM does exactly one of: **accepts**, **rejects**, or **loops** (runs forever, never reaching q_acepta or q_rechaza). *Halting* means accepting or rejecting; *accepting* is only one way of halting. This distinction drives Chapters 6 and 9.

## 5.6 Worked example: a TM for {0ⁿ1ⁿ | n ≥ 0}

**Implementation level.** "On input w:
1. If the first symbol is ⊔, accept (the empty word).
2. Replace the leftmost unmarked 0 by X; if there is none, go to step 5.
3. Move right over 0s and Ys to the first 1; replace it by Y. If no 1 is found, reject.
4. Move left over Ys and 0s to the last X, step right, go to step 2.
5. Move right over Ys; if a ⊔ is reached, accept; if a 0 or 1 is found, reject."

**Formal** (omitted arrows reject). Γ = {0,1,X,Y,⊔}.

| State | Meaning | Transitions |
|---|---|---|
| q₁ | seek leftmost 0 | `0 → X, R` to q₂; `Y → R` to q₄; `⊔ →` accept |
| q₂ | go right to a 1 | `0, Y → R` (stay); `1 → Y, L` to q₃ |
| q₃ | return left | `0, Y → L` (stay); `X → R` to q₁ |
| q₄ | check only Ys remain | `Y → R` (stay); `⊔ →` accept |

**Trace on 0011** (configurations): q₁0011 ⊢ Xq₂011 ⊢ X0q₂11 ⊢ X q₃ 0Y1 ⊢ q₃X0Y1 ⊢ Xq₁0Y1 ⊢ XXq₂Y1 ⊢ XXYq₂1 ⊢ XXq₃YY ⊢ Xq₃XYY ⊢ XXq₁YY ⊢ XXYq₄Y ⊢ XXYYq₄⊔ ⊢ accept.

On `0001`: after marking one pair, q₁ keeps finding 0s and q₂ eventually reads ⊔ with no arrow, so it rejects. On `0` alone, q₂ reads ⊔ and rejects. The machine halts on every input, so it is a *decider*.

## 5.7 Checklist

- [ ] Write the 7-tuple and explain each component.
- [ ] Trace a machine by hand writing configurations u q v.
- [ ] Explain halting vs accepting vs looping.
- [ ] State the first-cell convention and the "omit reject arrows" convention.

---

# Chapter 6. Recognizing vs. deciding, and building TMs that compute functions

**Goal:** acquire the *craft* of designing Turing machines (exam problems C2-2025 P2 and Pre-control P3).

## 6.1 Recognize vs. decide

- **Turing-recognizable** (reconocible; recursively enumerable): some TM *accepts exactly* the words of L. On words outside L it may reject **or loop**.
- **Turing-decidable** (decidible; recursive): some TM **always halts**, accepting words of L and rejecting the rest. Such a TM is a *decider*.
- Every decidable language is recognizable; the converse is false (Chapter 9).

## 6.2 Computing a function

Beyond yes/no questions, a TM can leave an answer on the tape. M **computes f : Σ* → Σ*** if for every w, q₀w ⊢\* q_acepta f(w).

**Exam convention for numbers (unary):** the input is **0ⁱ** (the number i), and the output must be **0^F(i)**. For two inputs the exam uses **0ⁱ ⊔ 0ʲ**. You must say where the output ends up: it must **start in the first cell** with nothing else on the tape.

## 6.3 The designer's toolkit

Most TM designs combine these standard subroutines.

| Subroutine | How |
|---|---|
| **Go to the end of the input** | move right while reading symbols of the input alphabet, stop at ⊔ |
| **Mark and return** | overwrite a symbol with a mark (X) and sweep back to a known anchor |
| **State as memory** | the finite control remembers a bounded amount: a counter mod k, one symbol, a flag |
| **Find the left end** | the tape's first cell is not detectable by itself (moving left there stays). Either (1) overwrite cell 1 at the start with a special symbol, or (2) rely on an already-erased/marked region, or (3) exploit the stay convention in a way that your states *know* the head is on cell 1 |
| **Erase from the right** | scan right to ⊔, step left, erase one symbol at a time; the state tracks a small count |
| **Compact / shift** | after erasing, slide symbols into the gaps one by one, using blanks as anchors |
| **Compare two blocks** | zig-zag, marking one symbol on each side (the w#w machine) |

**Design checklist (do this every time):**
1. Write the idea in one sentence.
2. Decide the *invariant* (what each phase leaves on the tape).
3. Write transitions or numbered steps.
4. **Trace** on at least: the empty input, a single symbol, and a typical case.
5. Check output format and final head position.

## 6.4 Worked example: F(i) = i mod 2 (output 0^(i mod 2))

**Idea.** Erase zeros from the **right** one at a time, using the state to remember parity. The left end is detected for free: when the head erases the very first cell and tries to move left it stays there, and then reads ⊔.

| State | Reads | Writes | Move | Next |
|---|---|---|---|---|
| s₀ | 0 | 0 | R | s₀ |
| s₀ | ⊔ | ⊔ | L | r₀ |
| r₀ | 0 | ⊔ | L | r₁ |
| r₀ | ⊔ | ⊔ | L | q_acepta |
| r₁ | 0 | ⊔ | L | r₀ |
| r₁ | ⊔ | 0 | L | q_acepta |

- s₀ scans to the end; r₀ means "an **even** number of zeros erased so far"; r₁ means "odd."
- Reaching ⊔ in r₀: total was even, output empty. Reaching ⊔ in r₁: total was odd, **write back one 0** (we are on cell 1) and accept.

**Trace i = 3 (000):** s₀ scans, then r₀ erases cell 3 → r₁ erases cell 2 → r₀ erases cell 1 and, being on cell 1, stays → r₁ reads ⊔ → writes 0 → accept. Output `0` (3 mod 2 = 1). ✓
**i = 0:** s₀ reads ⊔, goes L (stays on cell 1) into r₀, reads ⊔, accepts with empty tape. ✓

**This design is the template for i mod 3.**

## 6.5 Exam connection

### C2-2025 P2: F(i) = i mod 3, listing all transitions

*Try it yourself first.* Hints: replace the 2-state parity counter by a 3-state one (r₀, r₁, r₂). Erasing from the right leaves you with the number of erased zeros mod 3 in the state, but now **when you reach ⊔ you must rewrite up to two zeros**, so decide how the machine writes them and how it ends on cell 1. Trace i = 0, 1, 2, 3, 4, 5.

<details>
<summary>Guided solution</summary>

| State | Reads | Writes | Move | Next |
|---|---|---|---|---|
| s₀ | 0 | 0 | R | s₀ |
| s₀ | ⊔ | ⊔ | L | r₀ |
| r₀ | 0 | ⊔ | L | r₁ |
| r₀ | ⊔ | ⊔ | L | q_acepta |
| r₁ | 0 | ⊔ | L | r₂ |
| r₁ | ⊔ | 0 | L | q_acepta |
| r₂ | 0 | ⊔ | L | r₀ |
| r₂ | ⊔ | 0 | R | t₁ |
| t₁ | ⊔ | 0 | L | t₂ |
| t₂ | 0 | 0 | L | q_acepta |

All other combinations go to q_rechaza (never used).

**Meaning.** r_k: "I have erased 3m + k zeros so far in this erase-from-the-right pass."
- Hitting ⊔ in r₀ (we are on cell 1): the count was a multiple of 3, the output is empty.
- Hitting ⊔ in r₁: exactly one zero too many was erased (the last one was cell 1): rewrite 0 on cell 1, accept.
- Hitting ⊔ in r₂: two erased (cells 2 and 1): rewrite 0 on cell 1, move right, rewrite 0 on cell 2, move left back to cell 1, accept.

**Trace i = 5:** zeros in cells 1-5. s₀ goes to ⊔ then L to cell 5. r₀ erases 5 → r₁ erases 4 → r₂ erases 3 → r₀ erases 2 → r₁ erases 1 and (on cell 1) stays → r₂ reads ⊔ → writes 0 on cell 1, R → t₁ reads ⊔ at cell 2, writes 0, L → t₂ reads 0 at cell 1 → accept. Tape `00` ✓.
**i = 3:** ends in r₀ reading ⊔ → empty ✓. **i = 4:** ends in r₁ reading ⊔ → `0` ✓. **i = 0:** s₀ reads ⊔, L (stays), r₀ reads ⊔, accepts ✓. **i = 1:** r₀ erases cell 1 and stays, r₁ reads ⊔, writes 0 ✓. **i = 2:** r₀ erases cell 2, r₁ erases cell 1 (stays), r₂ reads ⊔, rewrites `00` ✓.
</details>

### Pre-control P3: f(i, j) = ⌊(i + j) / 2⌋ on input 0ⁱ ⊔ 0ʲ

*Try it yourself first.* Steps to think through: (1) turn the two blocks into **one** block 0^(i+j); (2) **halve** a unary number; (3) mind the floor (odd sum) and the edge cases i = 0, j = 0.

<details>
<summary>Guided solution (implementation level)</summary>

**Phase 1: merge.** Move right over the first block to the separator ⊔; write 0 there. Continue right to the next ⊔, step left onto the last 0 and erase it. The tape now holds 0^(i+j) (we filled the gap with one 0 and removed the extra last 0). If i = 0 the separator is cell 1 itself; if j = 0 the "last 0" is the one just written.

**Phase 2: halve (floor).** Repeat rounds. Each round turns *one* zero into a **kept** mark X and **erases one partner zero**, so every pair of zeros produces one X:
1. Go to the leftmost unmarked cell (the first cell after the block of Xs). If it is ⊔, halving is finished.
2. Overwrite it by X.
3. Move right to the first ⊔, step left. If the symbol is a **0**, erase it (the partner) and return to step 1. If the symbol is **X**, it means the zero just marked had **no partner** (the sum was odd): erase that X and finish. (This is exactly where the floor happens.)

**Phase 3: restore.** Sweep left over the Xs rewriting each as 0, and stop on cell 1. The tape holds 0^⌊(i+j)/2⌋. Accept.

**Left-end technique.** Returning to the first unmarked cell is easy because the Xs form a block starting at cell 1: sweep left until you read X, then step right. For the very first round (no X yet) and for Phase 3 you need to recognize cell 1: use the technique from §6.3 (for instance, overwrite cell 1 by a special symbol at the beginning and treat it as a kept/zero unit, remembering whether it was a 0 or the separator).

**Check on:** (i,j) = (3,2): sum 5 → rounds produce XX with one leftover zero that is erased as unpaired → `00` ✓. (1,0): X marked, last symbol is X → erase → empty ✓. (0,0): empty tape ✓. (2,2): XX ✓.

*Comment on your attempt:* your merge step (erase the last 0, fill the separator) is correct. Make steps 2-4 precise: say where the output ends up, how you detect the start of the tape, and what happens when the sum is odd.
</details>

## 6.6 Checklist

- [ ] Define recognizable vs decidable and explain a machine that is a recognizer but not a decider.
- [ ] State "M computes f" formally and the unary convention.
- [ ] Write a complete transition table and trace edge cases (i = 0, 1, 2, 3).
- [ ] Explain the left-end technique and the "state as counter" technique.

---

# Chapter 7. Variants of Turing machines and simulation proofs

**Goal:** master the *simulation proof*, the single technique behind three exam problems (2-stack PDA, single-overwrite TM, queue automaton).

## 7.1 The question

We can make a machine "stronger" (extra tapes, extra heads, a "stay" move, nondeterminism) or "weaker" (no left moves). Does the strengthened model recognize *more* languages? For Turing machines the surprising answer is nearly always **no**: they are equivalent to the basic model. You prove this by **simulation**: show one model can imitate the other.

## 7.2 What "equivalent" means

- **Equivalent w.r.t. recognizing:** for every w, M₁ accepts w ⇔ M₂ accepts w. Then L(M₁) = L(M₂).
- **Equivalent w.r.t. deciding (or simply equivalent):** additionally M₁ rejects w ⇔ M₂ rejects w, so they also *loop* on the same inputs.
- **Model T₂ is at least as powerful as T₁ (T₁ ≤ T₂):** every machine of type T₁ has an equivalent machine of type T₂. **T₁ ≡ T₂** means T₁ ≤ T₂ and T₂ ≤ T₁.

To show T₁ ≡ T₂ you must prove **two directions**. Usually one is trivial (a special case of the other) and the other needs a construction. *Always identify which is which.*

## 7.3 The simulation-proof template (7 steps)

Suppose you want to show "every machine A of model 𝒜 can be simulated by a machine B of model ℬ":

1. **Direction.** State it: "Given a machine of model 𝒜 we build a machine of model ℬ."
2. **Encode the configuration.** Say precisely how a configuration of A (state, tape/stack/queue contents, head position) is stored inside B. State the **invariant**.
3. **Initialization.** Describe how B turns its input into the encoding of A's initial configuration.
4. **One step.** For every kind of transition of A, describe how B updates the encoding (possibly with many steps of B), case by case, including **edge cases** (left end of the tape, empty stack, end of the tape).
5. **Acceptance / rejection.** When A accepts, B accepts. When A rejects, B rejects (or simply never accepts, if only recognizing). If A loops, B loops.
6. **Correctness.** By induction on the number of steps: after k steps of A, B's encoding equals A's k-th configuration. Hence A accepts w ⇔ B accepts w.
7. **Other direction.** If it is not trivial, prove it too.

## 7.4 Standard examples

### Stay-move TM ≡ standard TM

A TM with "stay" has δ : Q × Γ → Q × Γ × {L, R, S}. A standard TM is a special case (no S), so only one direction needs work.
**Construction:** replace each (q, a) ↦ (r, b, S) by two transitions:
- (q, a) ↦ (r_{q,a}, b, **R**) and, for every x ∈ Γ, (r_{q,a}, x) ↦ (r, x, **L**).
The machine steps right and immediately back, ending in the same cell with the same tape and in state r. Equivalent, even w.r.t. deciding. ∎

### Multitape TM ≡ single-tape TM

Given a k-tape machine, the one-tape machine stores all tapes on one tape separated by `#`, and marks each virtual head with a **dotted** symbol:

```
# ẇ₁ w₂ ... wₙ # ṫ # ṫ # ... #       (tape 1 | tape 2 | ... | tape k)
```

One simulated step = sweep left to right reading the k dotted symbols (state remembers them), then a second sweep updating each tape and moving its dot. If a dot moves onto a `#`, **shift** the rest of the tape one cell right to make room for a blank. Acceptance is copied. Conclusion: a language is recognizable iff some multitape TM recognizes it.

*Other simple variants* you should be able to simulate by the same method: doubly infinite tape (fold it in half onto two tracks), several heads, a 2D tape, a TM that can create new tapes.

## 7.5 Which models are weaker, which are equal?

| Model | Power vs. TM | Idea |
|---|---|---|
| TM with "stay" | equal | go right and back |
| Multitape, several heads, 2D, doubly infinite | equal | encode extra structure on one tape |
| **PDA with two stacks** | **equal** | two stacks = left and right of the head (7.6.1) |
| **PDA with a queue** | **equal** | rotate the queue (7.6.3) |
| **TM that can only move R or S (never L)** | **weaker** (only regular languages) | each cell is passed once; no information can be revisited, so only finite memory remains |
| TM with moves R, S and "Reset to first cell" | equal | to move left, mark the head cell, reset, scan right until just before the mark |
| NTM | equal (Chapter 8) | breadth-first search of the computation tree |

**Intuition:** a *stack* loses information when read; *two* stacks can hold an entire tape (left part and right part) and can move a symbol from one to the other, which is a head movement.

## 7.6 Exam connection

### 7.6.1 C2-2026 P1.2: a 2-stack PDA (2-APND) simulates a TM

**Setting.** The 2-APND is a PDA with two stacks. In one move it can: read an input symbol (or ε), pop one symbol from each stack (either may be ε), push one symbol on each stack (either may be ε), and change state. It **accepts if some computation ends in an accepting state**. You must show every TM can be simulated by a 2-APND. Encoding: **stack 1 = tape left of the head, stack 2 = the scanned cell and everything to the right.**

*Try it yourself first.* Hints: put `$` at the bottom of each stack. Decide which symbol must be on top of each stack so that the TM's scanned symbol can be read by popping. A right move = move a symbol from stack 2 to stack 1; a left move = the reverse. How do you *write* α? What about an empty stack?

<details>
<summary>Guided solution</summary>

Let M = (Q, Σ, Γ, δ, q₀, q_a, q_r). Stack alphabet Γ ∪ {$}.

**Invariant.** For a configuration ⊔w₁...wᵢ₋₁ **Q** wᵢ...wₙ⊔:
- **Stack 1** (bottom → top): `$ ⊔ w₁ w₂ ... wᵢ₋₁`. Top = wᵢ₋₁, the cell just left of the head.
- **Stack 2** (bottom → top): `$ ⊔ wₙ ... wᵢ₊₁ wᵢ`. **Top = wᵢ, the scanned symbol.**
- The control state remembers Q.
(The `$` at the bottom of stack 2 stands for the infinite blanks to the right; `⊔` is pushed on demand.)

**(a) Initialization** (configuration ⊔ Q₀ ŵ₁ w₂ ... wₙ ⊔):
1. Push `$` on both stacks (ε, ε → $ on each stack).
2. For each input symbol a read, push a on stack 1. After the input: stack 1 = `$ w₁ ... wₙ`, top wₙ. Stack 2 = `$`.
3. Transfer: while the top of stack 1 is not `$`, pop z from stack 1 and push z on stack 2 (ε-moves, one per symbol z ∈ Γ). The order flips, so the result is:
   - **Stack 2 = `$ wₙ ... w₂ w₁`, top = w₁**, the scanned symbol.
   - **Stack 1 = `$`** (nothing left of the head).
4. Push `⊔` on stack 1 to represent the blank cell left of w₁ in the exam's picture. If the input is empty, push `⊔` on stack 2, so the head scans a blank.
5. Go to the simulation state with TM state Q₀.

**Final contents at the start:** stack 1: `$` (and the optional blank ⊔) with **top = ⊔ (or $)**; stack 2: **top = w₁**, then w₂, ..., wₙ, then `$`.

**(b) One simulated step δ(Q, wᵢ) = (Q′, α, D).** The 2-APND, in state Q and with top of stack 2 equal to wᵢ, does (one transition for each Q ∈ Q, wᵢ ∈ Γ):

*Case D = R (move right):*
- **One move:** pop wᵢ from stack 2, push **α** on stack 1, go to state Q′.
- Effect: the written α is now immediately left of the head (top of stack 1), and stack 2 has lost the scanned cell, so its new top is wᵢ₊₁, the new scanned symbol.
- **Edge:** if the top of stack 2 is now `$`, the head has moved onto a fresh blank: push ⊔ on stack 2.

*Case D = L (move left):*
- **Move 1:** pop wᵢ from stack 2, pop z from stack 1 (z = wᵢ₋₁, the top; one transition for each possible z, the state remembers it), push **α** on stack 2, go to state (Q′, z).
- **Move 2:** push z on stack 2 (ε-move), go to state Q′.
- Effect: stack 2 is now `... wᵢ₊₁ α z` with **z on top = new scanned symbol** (the old wᵢ₋₁), the written α is just below it, and stack 1's top is wᵢ₋₂.
- **Edge:** if stack 1's top is `$` (head on the leftmost cell): with the two-way blank-padded tape of the exam, treat z as ⊔ (put `$` back, push ⊔ on stack 2). With the semi-infinite tape of the course, the head stays: only write α on stack 2 and keep it on top.

**Acceptance.** When the simulated state is q_a, go to the accepting state of the 2-APND. When it is q_r, give no transition (no accepting computation continues). If M loops, the 2-APND loops. All moves are deterministic, so nondeterminism isn't even needed.

**Correctness.** By induction on the number of TM steps: after k simulated steps the stacks and state encode the k-th configuration of M. Therefore the 2-APND has an accepting computation on w ⇔ M reaches q_a on w, so L(2-APND) = L(M).

**Converse (so the models are equivalent).** A 2-APND can be simulated by a (nondeterministic, multitape) TM that keeps each stack on its own tape and guesses nondeterministic moves; by Chapters 7 and 8 this is equivalent to a standard TM. ∎
</details>

### 7.6.2 Pre-control P1: a single-overwrite TM (MT-SEU) ≡ a standard TM

**Setting.** An MT-SEU may overwrite each cell **at most once**. (Convention used below: *overwriting* means replacing a **non-blank** symbol; writing onto a blank cell is free. State this assumption in your answer.) Show MT-SEU ≡ standard TM.

*Try it yourself first.* Which direction is trivial? For the other, think about "never edit; **copy the whole tape after each step** with the modification applied."

<details>
<summary>Guided solution</summary>

**Trivial direction (MT-SEU ≤ TM):** an MT-SEU *is* a TM; it just uses fewer abilities.

**Main direction (TM ≤ MT-SEU).** Given a standard M, build an MT-SEU M′ that keeps a **history of configurations**, each stored as a block on the tape.

**Encoding.** The tape of M′ looks like
```
 X X X X # X X X X # [q, c] ... # ...
 old block   old block   latest block
```
Each block holds a whole tape of M. The head and state of M are encoded in the scanned cell as a composite symbol **[q, c]**, so each block has exactly one such cell. Blocks are separated by `#`. Copied cells that have been consumed are overwritten once by **X**.

**Initialization.** Write `#` after the input (writing on blank: free). Copy the input to the right of `#`, left to right, overwriting each original cell by X (one overwrite per cell), and write the first symbol as **[q₀, w₁]** (or **[q₀, ⊔]** if the input is empty). End the block with `#`.

**Simulating one step of M.** Copy the latest block into a **new block** to its right, symbol by symbol, marking each source cell X once. While copying:
- Normal cell c: write c.
- The cell [q, c]: look up δ(q, c) = (q′, α, D).
  - **D = R:** write α, and write the *next* source symbol d as **[q′, d]**. If there is no next symbol (end of block), write α then **[q′, ⊔]**.
  - **D = L:** the cell to the left was already copied, so the machine keeps a **one-cell delay buffer in its finite control**: it writes each copied symbol only after reading the next. When it meets [q, c] it writes **[q′, p]** for the buffered previous symbol p, then α. If there is no previous symbol (head on the first cell), the head stays: write [q′, α].
- If q′ = q_a, M′ accepts; if q′ = q_r, M′ rejects.

**Telling the blocks apart.** To find the next source symbol the head sweeps left to right over X's and `#`'s to the first unmarked symbol. To know whether that symbol is in the source block or already in the new block, the blocks alternate between two copies of the alphabet (Γ and Γ′), so the parity tells which block a symbol belongs to. When the source is exhausted, write `#` after the new block; it becomes the latest block.

**Why each cell is overwritten at most once:** every cell is first written onto a blank (free) when its block is created, and later turned into X when it is consumed as a source (the one allowed overwrite). It is never touched again.

**Correctness.** By induction, the k-th block encodes M's k-th configuration, so M′ accepts/rejects/loops exactly as M does. ∎

*Comment on your attempt:* your idea is exactly right. Improve it by (i) saying how the state is stored (composite symbol), (ii) handling left moves, and (iii) justifying the one-overwrite count.
</details>

### 7.6.3 C2-2025 P3: a deterministic queue automaton (AC) ≡ Turing-recognizable

**Setting.** An AC works like a PDA but with a **queue** instead of a stack: push adds a symbol at the *left* end, pull reads and removes a symbol at the *right* end (first in, first out). The input is on a separate read-only tape, read once left to right, with a blank at its end. It accepts as soon as it enters an accepting state. Show: *L is recognized by a deterministic AC ⇔ L is Turing-recognizable.*

*Try it yourself first.* (⇒) is easy: a TM can store a queue on a tape. (⇐) needs a trick: the queue is a **circular buffer**; rotating it (pull then push the same symbol) walks the head position around.

<details>
<summary>Guided solution</summary>

**(⇒) AC ⇒ TM.** Build a 2-tape deterministic TM: tape 1 holds the input and is read left to right (this simulates the input head); tape 2 holds the queue contents written so that the **pull end is on the left and the push end on the right**. A **pull** reads the leftmost non-blank cell of tape 2 and erases it; a **push** appends a symbol after the last non-blank symbol. The window drifts right across the infinite tape but never needs anything else. The TM mirrors the AC's states and enters q_acepta iff the AC enters an accepting state. A 2-tape TM is equivalent to a 1-tape TM (Chapter 7), so L is recognizable. If a pull occurs on an empty queue the AC is stuck and the TM rejects (or loops); in either case no wrong acceptance.

**(⇐) TM ⇒ AC.** Let M be a (deterministic) one-tape TM recognizing L. Build an AC Q.

**Encoding.** The queue always contains, front to back (pull side first):

```
 c₁ c₂ ... ċᵢ ... cₘ #
```

the whole tape contents of M up to its last used cell, with the scanned cell marked with a **dot**, then an end marker `#`. The state of M is kept in the AC's control.

**Initialization.** Read the input w₁...wₙ from the input tape and push each symbol; the first pushed symbol is pushed as **ẇ₁** (dotted; **⊔̇** if the input is empty). When the end-of-input blank is read, push `#`. The front of the queue is w₁ (it was pushed first), as required.

**One simulated step.** The AC performs **one full rotation** of the queue: it pulls every symbol and pushes it back, applying the change near the head. Because it cannot edit symbols already pushed, it keeps a **one-symbol buffer** in its control (the previously pulled symbol p is pushed only after the next symbol has been pulled).
- Pull ordinary symbol c: push the buffer, store c in the buffer.
- Pull the dotted symbol ċ in state Q with δ(Q, c) = (Q′, α, D):
  - **D = R:** push the buffer, push **α** (undotted), then **pull the next symbol d and push ḋ** (dotted); if the next symbol is `#`, push **⊔̇** then `#`. State becomes Q′.
  - **D = L:** push **ṗ** (the buffered previous symbol, now dotted), then push **α**. If the buffer is empty (head on first cell), push **α̇** (head stays). State becomes Q′.
- Pull `#`: flush the buffer, push `#`, a rotation is complete; start the next rotation (next simulated step).

**Acceptance.** When the simulated TM state is q_acepta, the AC enters its accepting state. When it is q_rechaza, the AC moves to a dead (non-accepting) state. M loops ⇒ the AC keeps rotating forever, never accepting.

**Determinism.** Every AC move is determined by its state, the pulled symbol, and the input symbol (only used during initialization).

**Correctness.** After the k-th rotation the queue encodes the k-th configuration of M, so Q enters an accepting state ⇔ M accepts. ∎

**Conclusion.** Deterministic ACs recognize exactly the Turing-recognizable languages.
</details>

## 7.7 Checklist

- [ ] State the 7-step template from memory.
- [ ] For each exam model, say which direction is trivial and which needs a construction.
- [ ] For the 2-stack PDA: what is on top of each stack at the start, and how are left/right moves done?
- [ ] Why is a TM that can't move left weaker?

---

# Chapter 8. Nondeterminism, the Church-Turing thesis, encodings and the universal TM

**Goal:** understand NTMs and why they add no power, what the Church-Turing thesis says, how objects become strings, and how to build a *recognizer* by exhaustive search (Fermat, Pre-control P4).

## 8.1 Nondeterministic TMs (MTND / NTM)

**Definition.** Same as a TM except **δ : Q × Γ → P(Q × Γ × {L, R, S})**: from a configuration the machine may have several possible moves.

- The **computation tree** of N on w: root = initial configuration, children = configurations reachable in one step.
- **N accepts w if some branch reaches q_acepta.**
- **N decides** if on every input **every branch halts**.

**Writing NTMs: "guess, then verify."**
- *L = {x#y#z | x = y or x = z}*: guess which comparison to perform, then check it deterministically.
- *L = {x#y | x is a substring of y}*: guess a starting position in y, then compare.
- *L = {0^n₁ # 0^n₂ # 0^n₃ # 0^m | m = sum of a subset of the nᵢ}*: guess for each nᵢ whether it is in the subset, then add and compare.

## 8.2 NTM ⇒ TM (the BFS simulation)

**Theorem.** Every NTM N has an equivalent deterministic TM M.

**Idea.** Visit the computation tree **breadth-first** (level by level), so that if some branch accepts, we eventually find it. Use a 3-tape machine:
- **Tape 1:** the input w, never changed.
- **Tape 2:** a work copy where we simulate N along one branch.
- **Tape 3:** the **address** of the branch to try: a string over {1, ..., b} where b is the maximum number of choices in δ; the digit tells which choice to take at each step.

**Algorithm.** "On input w: (1) tape 3 starts empty. (2) Copy tape 1 to tape 2. (3) Simulate N on tape 2, at each step reading the next digit of tape 3 to pick the choice. If digits run out, the choice is invalid, or N rejects, go to (4). If N reaches q_acepta, **accept**. (4) Replace tape 3 by the **next string in shortlex order** (by length first, then lexicographically), return to (2)."

**Why breadth-first and not depth-first?** A depth-first search could sink into an **infinite branch** (a looping computation) and never look at the accepting branch. Shortlex enumeration tries all addresses of length 1, then 2, ... so every finite branch is eventually tried.

**Consequences.**
- A language is Turing-recognizable ⇔ some NTM recognizes it.
- Decidable version: if N is a decider, modify M to **reject when every branch up to the maximum depth has rejected**. This is possible because the tree is finite when all branches halt. So decidable ⇔ some NTM decider exists.

## 8.3 The Church-Turing thesis

In 1936 Church (λ-calculus) and Turing (Turing machines) independently proposed formal models for the informal notion of an **algorithm** (a mechanical step-by-step procedure). Other models appeared (RAM machines, recursive functions, semi-Thue systems...) and **all were proven equivalent to TMs**.

> **Church-Turing thesis:** the intuitive notion of "algorithm" = "computable by a Turing machine."

It is a **thesis, not a theorem**, because "intuitive algorithm" is not a mathematical object that could be proven equivalent. Historical motivation: Hilbert's 10th problem asked for a procedure deciding whether a multivariate polynomial has an integer root; without a formal model one could not even *state* that no such procedure exists (Matiyasevich proved in 1970 that the language of such polynomials is undecidable).

**Practical consequence:** to show a problem is solvable by a TM, it suffices to describe an informal algorithm in clear steps ("high-level description"), as long as each step is plainly mechanical. We use this for decidability proofs.

## 8.4 Encodings

A TM takes strings as input, but we want to give it graphs, automata, grammars, even other TMs. Fix an **encoding**: any finite object X is written as a string **⟨X⟩** over a finite alphabet (in the extreme, as a binary string). A TM can **check that a string is a valid encoding** (e.g. that it describes a 7-tuple satisfying the definition: finite sets, δ a function, q_acepta ≠ q_rechaza).

Examples: a TM M becomes ⟨M⟩; a pair becomes ⟨M, w⟩; a graph becomes its vertex list and edge list; a polynomial p becomes ⟨p⟩.

## 8.5 The universal Turing machine

A **universal TM U** is a TM that on input ⟨M, w⟩ **simulates M on w**:

"U = on input ⟨M, w⟩: (1) check it is a valid encoding; (2) simulate M on w step by step; (3) if M reaches q_acepta, accept; if M reaches q_rechaza, reject."

So **U(⟨M, w⟩) = M(w)** in every case (including when M loops, then U loops). U is the theoretical ancestor of the stored-program computer. We will see (Chapter 9) that U **recognizes** A_TM but does **not decide** it.

## 8.6 Exam connection: Pre-control P4 (Fermat) and dovetailing

**Statement.** Fermat's Last Theorem: for n > 2 there are no positive integers x, y, z with xⁿ + yⁿ = zⁿ. Build a TM M that **accepts the empty word iff the theorem is false**.

*Try it yourself first.* Hints: a counterexample, if it exists, is a quadruple (n, x, y, z) of naturals with n ≥ 3. A naive "for n = 3, 4, ...: for x = 1, 2, ...: for y: for z:" never leaves the first innermost loop forever. What do you do instead?

<details>
<summary>Guided solution</summary>

**Idea: dovetailing.** The search space ℕ⁴ is infinite, and nested unbounded loops get stuck in the first infinite loop. Instead use **one outer counter i** and, for each i, test **all** quadruples with every component bounded by i. Every quadruple is eventually tested.

M = "On input w:
1. If w ≠ ε, **reject**.
2. For i = 1, 2, 3, ... (forever):
   - For n = **3** to i, for x = 1 to i, for y = 1 to i, for z = 1 to i:
     - Compute xⁿ + yⁿ and zⁿ (by repeated multiplication, using TM subroutines for addition and multiplication; all loops are bounded).
     - If xⁿ + yⁿ = zⁿ, **accept**."

(Note the bound is n ≥ 3, since the theorem says n > 2; with n ≥ 2 the triple (3, 4, 5) would be found at once. *In your attempt you wrote 2 ≤ n; it must be 3 ≤ n.*)

**Correctness.**
- If the theorem is false, there is a counterexample (n, x, y, z); once i ≥ max{n, x, y, z}, M finds it and accepts ε.
- If the theorem is true, no quadruple ever satisfies the equation, so M never accepts and **loops forever** on ε.
So **M accepts ε ⇔ Fermat's theorem is false**, L(M) = {ε} or ∅.

**Self-check: why can't such a machine *decide* the statement?** When the theorem is true M never stops; at no finite time can it conclude "no counterexample exists," because the next iteration might find one. M is a **recognizer**, not a decider. (This only shows the language is recognizable; it says nothing about whether it is decidable.)
</details>

## 8.7 Checklist

- [ ] Define an NTM and its acceptance; explain why BFS (and why 3 tapes).
- [ ] State the Church-Turing thesis and say why it is not a theorem.
- [ ] Explain ⟨X⟩ and the universal TM.
- [ ] Explain dovetailing and why nested unbounded loops fail.

---

# Chapter 9. Decidability, existence of undecidable languages, and diagonalization

**Goal:** prove a language decidable (with termination), understand why undecidable languages exist, and master the diagonal argument for A_TM (exam P2.1).

## 9.1 Decidable problems and the proof template

A language L is **decidable** if some TM D **always halts**: it accepts every w ∈ L and rejects every w ∉ L. It is **recognizable** if some TM accepts exactly L (on w ∉ L it may reject or loop).

**Template to prove "L is decidable":**
1. Describe a TM M, in clear steps, taking the input (with an encoding check).
2. Argue **M can be built** (each step is mechanical).
3. Argue **M always halts**. *This is the key step.* Without it you only have a recognizer.
4. Argue **M accepts exactly L**: if x ∈ L then accept; if x ∉ L then reject.

### Examples

**A_DFA = {⟨B, w⟩ | B is a DFA and accepts w}.** M: check the encoding; simulate B on w (|w| steps); accept iff B ends in an accepting state. Halts after |w| steps. ✓

**A_CFG = {⟨G, w⟩ | G is a CFG generating w}.** M: convert G to Chomsky normal form; if w = ε check S → ε; otherwise list **all derivations of exactly 2|w| − 1 steps** (a finite set); accept iff one generates w. Halts because the set is finite and, in CNF, every derivation of a string of length n takes exactly 2n − 1 steps (Chapter 2).

**E_DFA = {⟨A⟩ | L(A) = ∅}.** M: mark the start state; repeatedly mark states reachable from marked states; accept iff no accepting state is marked. Halts after at most |Q| rounds.

**EQ_DFA = {⟨A, B⟩ | L(A) = L(B)}.** Build a DFA C for the **symmetric difference** (A ∩ Bᶜ) ∪ (Aᶜ ∩ B) using the closure constructions, then run the E_DFA decider on C. Accept iff it says "empty."

## 9.2 Undecidable languages exist (counting)

- Every TM has a finite description ⟨M⟩ ∈ {0,1}*, and {0,1}* is countable, so **there are countably many TMs**.
- A language is a subset of Σ*, i.e. an infinite binary sequence (its characteristic sequence); by Cantor's diagonal argument there are **uncountably many languages**.
- Each decidable (or even recognizable) language needs a TM, so **most languages have no TM at all.**

This proves existence only; it does not point to a specific one. For that:

## 9.3 A_TM: recognizable but not decidable

**A_TM = {⟨M, w⟩ | M is a TM and M accepts w}**

**A_TM is recognizable:** the universal TM U accepts ⟨M, w⟩ iff M accepts w.

**A_TM is undecidable (diagonalization).** Suppose a TM H decides A_TM: H(⟨M, w⟩) accepts if M accepts w and rejects if M does not accept w (rejects or loops). Define a new machine **D**:

> D = "On input ⟨M⟩, where M is a TM:
> 1. Run H on ⟨M, ⟨M⟩⟩ (M's code given to M as input).
> 2. Output the **opposite** of H: if H accepts, **reject**; if H rejects, **accept**."

Then D(⟨M⟩) accepts ⇔ M does **not** accept ⟨M⟩. Now run D on its **own description**:

> D accepts ⟨D⟩ ⇔ D does not accept ⟨D⟩.

A contradiction. So no such H exists. ∎

**Why this is "diagonalization."** Build the infinite table with rows M₁, M₂, ... and columns ⟨M₁⟩, ⟨M₂⟩, ...; the entry (i, j) says whether Mᵢ accepts ⟨Mⱼ⟩ (H would fill every entry with accept/reject). D is a machine whose row is the **flip of the diagonal**: D differs from Mᵢ on input ⟨Mᵢ⟩. So D cannot be any row Mᵢ, yet it is a TM, so it must be a row. Contradiction.

**Memorize the pattern**: *assume a decider; build a machine that does the opposite of the decider on a machine's own code; feed it its own code.* This is exam problem P2.1(b).

## 9.4 The Halting Problem and useful facts

**HALT_TM = {⟨M, w⟩ | M halts on w}** is undecidable. Proof by **reduction from A_TM** (Chapter 10).

**Facts you must know:**
- If L is decidable then its **complement** Lᶜ is decidable (swap accept and reject in the decider).
- **L is decidable ⇔ L and Lᶜ are both recognizable.** (⇒ is clear. ⇐: run the two recognizers **in parallel**; exactly one of them accepts; accept if the recognizer for L accepts, reject if the one for Lᶜ accepts.)
- Consequently **the complement of A_TM is not even recognizable** (otherwise A_TM would be decidable). This is an example of a language that is neither decidable nor recognizable.

## 9.5 Exam connection: C2-2026 P2.1

**Setting.** Call a TM *10-compatible* if (i) it **always halts** on every input and (ii) **deciding whether an arbitrary TM is 10-compatible is itself decidable**. Define
**L₂ = {⟨M⟩ | M is a TM, M is 10-compatible, and M rejects ⟨M⟩}.**
(a) Show L₂ is decidable. (b) Show that **no 10-compatible machine can decide L₂.**

*Try it yourself first.* For (a): you are *given* that compatibility can be decided; what do you do if the machine is not compatible, and why is it safe to simulate it if it is? For (b): imitate the A_TM diagonalization: take a supposed 10-compatible decider D and run it on ⟨D⟩. Be explicit about why D being 10-compatible is used.

<details>
<summary>Guided solution</summary>

**(a) L₂ is decidable.** Let C be the (given) decider that decides whether a TM is 10-compatible. Define
**T = "On input x:**
1. Check that x = ⟨M⟩ is a valid encoding of a TM; if not, reject.
2. Run C on ⟨M⟩. If C says *not 10-compatible*, **reject**.
3. Otherwise, **simulate M on ⟨M⟩**. If M rejects, **accept**; if M accepts, **reject**."

*Buildable:* every step is mechanical (C exists by hypothesis; step 3 is the universal machine).
*Always halts:* step 1 and step 2 halt (C is a decider). In step 3 we only get there when M is 10-compatible, and **10-compatible machines halt on every input**, in particular on ⟨M⟩, so the simulation terminates.
*Correct:* ⟨M⟩ ∈ L₂ ⇔ M is 10-compatible and M rejects ⟨M⟩ ⇔ T accepts. If M is not 10-compatible, T correctly rejects; if M is compatible, T accepts iff M rejects ⟨M⟩. ∎

**(b) A 10-compatible decider for L₂ is impossible.** Suppose D is a 10-compatible TM that decides L₂. Consider the input ⟨D⟩. Because D is **10-compatible**, the membership condition "M is 10-compatible" is true for M = D, so

⟨D⟩ ∈ L₂ ⇔ D rejects ⟨D⟩.

Because D **decides** L₂ and halts:

⟨D⟩ ∈ L₂ ⇔ D accepts ⟨D⟩.

Combining: **D accepts ⟨D⟩ ⇔ D rejects ⟨D⟩**. But D halts and can't both accept and reject. Contradiction. ∎

**Why D must be 10-compatible:** the diagonal trick needs "D ∈ the class being talked about," i.e. D must pass the first condition of L₂'s definition, otherwise ⟨D⟩ ∉ L₂ for the trivial reason that D isn't compatible, and no contradiction appears. Interesting consequence: the decider T from (a) exists but is **not 10-compatible**, so "10-compatible" machines cannot capture all decidable languages: the rule set is incomplete.
</details>

## 9.6 Checklist

- [ ] Prove a language decidable with all four template steps, especially termination.
- [ ] Explain why undecidable languages must exist (countable vs uncountable).
- [ ] Reproduce the A_TM diagonal proof and the table picture.
- [ ] State "L decidable ⇔ L and Lᶜ recognizable" and deduce that Ā_TM isn't recognizable.
- [ ] Adapt the diagonal argument to a variant (10-compatible).

---

# Chapter 10. Reductions, more undecidable languages, and Rice's theorem

**Goal:** prove new languages undecidable by reducing from A_TM, in the **correct direction**, with both implications (exam P2.2).

## 10.1 What a reduction is

**A ≤ B** ("A reduces to B") means: *if we could decide B, we could decide A.* Concretely, from a hypothetical decider R for B we build a decider S for A.

> **Direction rule (the most common error is reversing it):** to prove that **B is undecidable**, reduce a **known undecidable** language A to B (A ≤ B). Then: if B were decidable, A would be decidable, contradiction.

## 10.2 The reduction template

To show a new language **B** undecidable:

1. **Assume** a TM R decides B.
2. **Build** a TM S that decides A_TM (the known undecidable language). On input ⟨M, w⟩, S **constructs** a new object (usually the *code* of a new machine M′, or a new input) from ⟨M, w⟩.
3. S **runs R** on the constructed object and **copies or flips** R's answer.
4. **Prove S decides A_TM, both directions:** ⟨M, w⟩ ∈ A_TM ⇒ the construction is in B, and ⟨M, w⟩ ∉ A_TM ⇒ the construction is not in B.
5. **Contradiction:** A_TM is undecidable, so R cannot exist.

**Critical subtlety, build vs. run:** inside S, the machine M′ is only **written down** (its code is produced); S never runs M′ itself. M′ is *run* only inside R, as part of R's analysis, which halts because R is a decider. Running M(w) directly inside S would make S possibly loop and would invalidate the proof.

## 10.3 Worked reductions

### HALT_TM = {⟨M, w⟩ | M halts on w} is undecidable (A_TM ≤ HALT_TM)

Suppose R decides HALT_TM. Build S for A_TM: "On ⟨M, w⟩: run R on ⟨M, w⟩. If R rejects (M loops on w), **reject**. If R accepts (M halts on w), **simulate M on w**, which is guaranteed to terminate: accept if M accepts, reject if M rejects." S always halts and decides A_TM. Contradiction. ∎

### E_TM = {⟨M⟩ | L(M) = ∅} is undecidable (A_TM ≤ E_TM)

Suppose R decides E_TM. Given ⟨M, w⟩, S **constructs** the code of

> M′ = "On input x: if x ≠ w, **reject**. If x = w, **run M on w** and answer what M answers (accept if M accepts, reject if M rejects)."

Then **L(M′) = {w} if M accepts w, and L(M′) = ∅ otherwise.** S then runs R on ⟨M′⟩ and **flips**:

> S = "On ⟨M, w⟩: build ⟨M′⟩; run R on ⟨M′⟩. If R **accepts** (L(M′) = ∅), **reject**. If R **rejects**, **accept**."

*Both directions:* ⟨M, w⟩ ∈ A_TM ⇒ L(M′) = {w} ≠ ∅ ⇒ R rejects ⇒ S accepts. ⟨M, w⟩ ∉ A_TM ⇒ L(M′) = ∅ ⇒ R accepts ⇒ S rejects. So S decides A_TM, contradiction. ∎

### EQ_TM = {⟨M₁, M₂⟩ | L(M₁) = L(M₂)} is undecidable (E_TM ≤ EQ_TM)

Given R for EQ_TM, decide E_TM: on ⟨M⟩ run R on ⟨M, M_∅⟩, where M_∅ rejects everything; accept iff R accepts. (Here the known undecidable language is E_TM.)

## 10.4 Rice's theorem

**Theorem (Rice).** Let P be a set of TM descriptions such that
1. **P is non-trivial:** some TM is in P and some TM is not;
2. **P depends only on the language:** if L(M₁) = L(M₂) then ⟨M₁⟩ ∈ P ⇔ ⟨M₂⟩ ∈ P.

Then P is **undecidable**.

**Slogan:** every non-trivial property of the *language* a TM recognizes is undecidable.

**Examples of Rice applying:** REGULAR_TM (L(M) is regular), INFINITE_TM (L(M) is infinite), ALL_TM (L(M) = Σ*), E_TM.
**When Rice does NOT apply:** properties of the machine's **structure or behavior**, not its language, e.g. "M has a useless/unreachable state," "M has at least 5 states," "M halts within 100 steps on input ε." Two machines can have the same language but differ in these properties, so condition 2 fails. These need a direct reduction (like L_estado below).

## 10.5 Exam connection: C2-2026 P2.2

**L_estado = {⟨M, q⟩ | M is a TM and the state q is never reached on any input x}.** Show L_estado is undecidable by a reduction from A_TM.

*Try it yourself first.* Hints: given ⟨M, w⟩ you want to build a machine M′ and a state q such that "q is reached" ⇔ "M accepts w." Make q a **new** state. Remember the direction, the "build, don't run," and both implications. Why can't you just cite Rice?

<details>
<summary>Guided solution</summary>

Suppose R decides L_estado. Build S deciding A_TM.

**Construction of M′ from ⟨M, w⟩.** M′ has all the states of M plus one **fresh** state q_new that appears in no other transition.

> M′ = "On any input x: **ignore x**. Erase the tape and write w. Simulate M on w. If M reaches q_acepta, **move to q_new** (and then accept, say). If M rejects or loops, M′ does the same, and q_new is never entered."

By construction q_new is entered **if and only if** M accepts w, and then it is entered on *every* input x (since M′ ignores x). So

- ⟨M, w⟩ ∈ A_TM (M accepts w) ⇒ q_new **is** reached ⇒ ⟨M′, q_new⟩ **∉** L_estado.
- ⟨M, w⟩ ∉ A_TM (M doesn't accept w) ⇒ q_new is **never** reached ⇒ ⟨M′, q_new⟩ **∈** L_estado.

**The decider for A_TM:**
> S = "On input ⟨M, w⟩:
> 1. Construct (do **not** run) ⟨M′, q_new⟩ as above.
> 2. Run R on ⟨M′, q_new⟩.
> 3. If R **accepts**, **reject**. If R **rejects**, **accept**."

S halts (the construction is mechanical, R is a decider) and, by the two implications above, **accepts ⟨M, w⟩ ⇔ M accepts w.** So S decides A_TM, which is impossible. Hence L_estado is undecidable. ∎

**Checks for yourself:** (i) *direction:* we reduced from the known undecidable A_TM *to* L_estado ✓; (ii) M′ is only *built* inside S ✓; (iii) *both implications* proved ✓; (iv) q_new truly fresh and entered only after M accepts ✓ (otherwise the equivalence breaks).

**Why not Rice?** "State q is never reached" is a property of the machine's *behavior/structure*, not of L(M); two machines with the same language can differ on it. So Rice's condition 2 fails, and a direct reduction is required.
</details>

## 10.6 More practice (Class 17 "Propuestos")

Prove undecidable: **REGULAR_TM, INFINITE_TM, ALL_TM, USELESS-STATE_TM.** The first three are properties of L(M): Rice's theorem applies directly, or imitate the E_TM reduction (build an M′ whose language is a regular/infinite/Σ* language when M accepts w, and a non-regular/finite/not-Σ* language otherwise). USELESS-STATE_TM is like L_estado: reduce from A_TM with a fresh state.

## 10.7 Checklist

- [ ] State the direction of a reduction and why it is "A_TM ≤ new language."
- [ ] Run through the 5-step template without notes.
- [ ] Explain "build, don't run" and why the new state must be fresh.
- [ ] State Rice's two hypotheses and give an example where it does *not* apply.
- [ ] Explain why Ā_TM is not recognizable.

---

# RECAP: the memory-helper

*Read this the night before. Each block is a compressed version of a chapter.*

## R1. Core definitions

| Concept | One-line definition |
|---|---|
| Alphabet / string / language | finite set of symbols / finite sequence / any subset of Σ* |
| ∅ vs {ε} | no strings vs. exactly one string (the empty one) |
| Closed under Φ | applying Φ to members always gives a member |
| DFA / NFA | (Q,Σ,δ,q₀,F); NFA branches, accepts if some branch accepts; same power |
| Regular | recognized by DFA/NFA, described by a regex |
| CFG | G = (V,Σ,R,S); *generates* strings by rewriting; L(G) = {w \| S ⇒* w} |
| Ambiguous grammar | some string has two parse trees (property of the grammar) |
| CNF | rules A → BC or A → a; strings of length n take 2n − 1 steps |
| PDA | NFA + stack; `a, b → c` = read a, pop b, push c; accepts with input read, final state, empty stack |
| TM | (Q,Σ,Γ,δ,q₀,q_acepta,q_rechaza), δ : Q×Γ → Q×Γ×{L,R}; infinite tape; halts only at accept/reject |
| Configuration | **u q v**: tape uv, state q, head on first symbol of v; ⊢ = one step |
| Outcomes of a run | accept, reject, **loop** |
| Recognizable (r.e.) | a TM accepts exactly L (may loop outside L) |
| Decidable (recursive) | a TM that **always halts** accepts L and rejects the rest |
| M computes f | q₀w ⊢* q_acepta f(w) |
| Equivalent machines (deciding) | same accept / reject / loop behavior on every input |
| NTM | δ gives a set of moves; accepts if **some** branch accepts |
| ⟨X⟩ | string encoding of an object X |
| Universal TM U | on ⟨M,w⟩ simulates M on w; recognizes A_TM |
| A_TM | {⟨M,w⟩ \| M accepts w}: recognizable, **undecidable** |
| A ≤ B | a decider for B yields a decider for A |

## R2. Hierarchy of models

```
 DFA = NFA = regex  (regular)   ⊂   PDA = CFG (context-free)   ⊂   decidable   ⊂   recognizable   ⊂   all languages
                                                                      TM = NTM = multitape = 2-stack PDA = queue automaton = RAM = λ-calculus
```
Examples separating them: 0ⁿ1ⁿ is context-free but not regular; aⁿbⁿcⁿ is decidable (a TM) but not context-free; A_TM is recognizable but not decidable; Ā_TM is not even recognizable.

## R3. Closure tables

| Operation | Regular | Context-free |
|---|---|---|
| Union | yes | yes |
| Concatenation | yes | yes |
| Star | yes | yes |
| Intersection | yes | **no** (aⁿbⁿcᵐ ∩ aᵐbⁿcⁿ) |
| Complement | yes | **no** (De Morgan) |
| ∩ with regular | yes | **yes** (product construction) |
| Perfect shuffle | (not needed) | **no** (Pre-control P2) |
| CUT | (not needed) | **no** (C2-2025 P1) |

## R4. The seven templates, compressed

**1. Pumping lemma (not context-free).**
Assume CFL ⇒ p. Pick s ∈ L, |s| ≥ p, depending on p. Any split s = uvxyz with |vy| > 0, |vxy| ≤ p. Window touches ≤ 2 adjacent blocks. Classify by *content of vy*; per case pick i ∈ {0, 2} so uvⁱxyⁱz ∉ L. Contradiction.
*Memory:* "**choose s, classify vy, pick i, contradict.**"

**2. Non-closure.**
Pick CFLs A (B) **and prove they are CFLs** → compute/intersect with a regular language to get a recognizable non-CFL → prove it non-CFL → conclude.
*Tools:* ∩ regular; counting; sorted words (b\*c\*a\*d\*) are determined by counts.

**3. Build a TM.**
Idea in one sentence → invariant → transitions or numbered steps → trace on ε, one symbol, typical → say where the output ends. Toolkit: state as counter, erase from the right, mark and return, left-end technique, compact/shift, dovetailing for recognizers.
*Unary convention:* input 0ⁱ (or 0ⁱ⊔0ʲ), output 0^f.

**4. Simulation / equivalence.**
Direction → encode configuration (invariant) → initialization → one step case by case (edge cases!) → accept/reject/loop correspondence → correctness by induction → other direction.
- **2-stack PDA ⇒ TM:** stack 1 = left of head (top = cell left of head), stack 2 = scanned cell and right (top = scanned symbol). Init: push input on stack 1, move all to stack 2. Right: move α to stack 1. Left: pop z from stack 1, push α then z on stack 2.
- **Single-overwrite TM:** append a new copy of the whole configuration after each step, marking sources with X; state stored in composite symbol [q,c]; left moves via one-cell buffer.
- **Queue automaton ⇒ TM:** queue = circular tape with dotted head cell and `#`; one rotation = one step; one-symbol buffer for left moves. TM ⇒ AC is easy (queue on a tape).

**5. Decidable.**
(1) describe M, (2) buildable, (3) **always halts**, (4) accepts exactly L. Run an assumed decider, then simulate a machine only when you know it halts.

**6. Diagonalization.**
Assume decider H/D → build D that does the **opposite** on a machine's own code → feed D its own code → D accepts ⟺ D doesn't accept. Check why the hypothesis (e.g. 10-compatible) makes D a legitimate candidate.

**7. Reduction from A_TM.**
Assume decider R for B → build S deciding A_TM: from ⟨M,w⟩ **construct** (don't run) M′ → run R → copy/flip → both implications → contradiction. Direction: **known-undecidable ≤ new**.

## R5. Key results in one line each

- Pumping lemma (regular): s = xyz, |y| > 0, |xy| ≤ p, xyⁱz ∈ L.
- Pumping lemma (CFL): s = uvxyz, |vy| > 0, |vxy| ≤ p, uvⁱxyⁱz ∈ L.
- CFG ⇔ PDA. NFA ⇔ DFA ⇔ regex.
- Every NTM has an equivalent deterministic TM (3 tapes, BFS, shortlex addresses).
- Church-Turing: algorithm = TM (thesis, not theorem).
- Undecidable languages exist (countably many TMs, uncountably many languages).
- A_TM is recognizable (universal TM), not decidable (diagonalization).
- L decidable ⇔ L and Lᶜ both recognizable ⇒ Ā_TM is not recognizable.
- HALT_TM, E_TM, EQ_TM, REGULAR_TM, INFINITE_TM, ALL_TM are undecidable.
- Rice: non-trivial **language** properties of TMs are undecidable (not structural ones).

## R6. Which technique? (decision tree)

```
"Show L is not context-free"          → pumping lemma for CFLs (or ∩ regular + pumping)
"Show CFLs are not closed under Φ"    → pick CFL A,B; show Φ(A,B) (∩ regular) is a non-CFL
"Build/describe a TM for ..."         → toolkit + invariant + trace
"Show model X ≡ TM"                   → simulation template (find the nontrivial direction)
"Show L decidable"                    → decider + termination argument
"Show nobody can decide L with property Π" (Π-machines) → diagonalization
"Show L undecidable"                  → reduction FROM A_TM (build M′, flip R's answer)
"Accept iff some infinite search succeeds" → dovetailing (recognizer only)
```

## R7. Pitfalls checklist (check every solution)

- **Pumping (CFL):** forgot the case with v and y in *different* blocks; s doesn't depend on p; only tried i = 2 when i = 0 was needed (or vice versa); didn't use |vxy| ≤ p to limit the blocks.
- **Closure:** didn't prove A, B are context-free; didn't prove the result is *not* context-free; transcribed definition (CUT = {xzy | xyz ∈ L}) wrong.
- **Shuffle:** wrong letter order inside each pair (A-letter first); pumped a word not actually in the language.
- **TM construction:** forgot i = 0 / empty input; output in the wrong place or wrong format; didn't list *every* transition when asked; unmarked left end.
- **Dovetailing:** nested unbounded loops; bound n ≥ 3 (not 2) for Fermat; didn't reject w ≠ ε.
- **Simulation:** proved only one direction; no left-end / right-end edge cases; didn't say what happens when the simulated machine rejects or loops.
- **Decidability:** forgot to argue the machine always halts.
- **Reduction:** wrong direction; *ran* M inside the construction instead of building M′; one implication only; the "fresh" state isn't fresh.
- **Diagonalization:** didn't state what happens on input ⟨D⟩; didn't justify why D qualifies (e.g. is 10-compatible).

## R8. Exam problem → one-line idea

| Problem | Idea |
|---|---|
| C2-2026 P1.1: {aⁱbʲcᵏ \| j = max{i,k}} | s = aᵖbᵖcᵖ; i = 0 unless vy is pure a or pure c, then i = 2 |
| C2-2026 P1.2: 2-APND simulates a TM | stack 1 = left tape, stack 2 = head + right; init by push then transfer; R = move to stack 1; L = move back |
| C2-2026 P2.1(a): L₂ decidable | run compatibility decider; if compatible, simulate M on ⟨M⟩ (it halts); accept iff it rejects |
| C2-2026 P2.1(b): no 10-compatible decider | feed D its own code ⟨D⟩ ⇒ D accepts ⟨D⟩ ⇔ D rejects ⟨D⟩ |
| C2-2026 P2.2: L_estado undecidable | A_TM ≤ L_estado; M′ ignores input, simulates M on w, enters fresh q_new iff M accepts; flip R |
| C2-2025 P1: CUT | CUT(L) = {xzy \| xyz ∈ L}; L = {bᵐaᵐdⁿcⁿ}; CUT(L) ∩ b\*c\*a\*d\* = {bᵐcⁿaᵐdⁿ}, non-CFL by pumping |
| C2-2025 P2: i mod 3 | erase from the right with a 3-state counter; rewrite 0–2 zeros at cell 1 |
| C2-2025 P3: queue automaton ≡ TM | TM ⇒ AC: circular queue with dotted head; AC ⇒ TM: queue on a tape |
| Pre-control P1: single-overwrite TM | append a copy of the whole configuration after each step, marking sources with X |
| Pre-control P2: perfect shuffle | A = {aⁿb²ⁿ}, B = {c²ⁿdⁿ}; shuffle = {(ac)ⁿ(bc)ⁿ(bd)ⁿ}; counting breaks it |
| Pre-control P3: ⌊(i+j)/2⌋ | merge blocks, then halve by marking one zero and erasing one partner per round |
| Pre-control P4: Fermat | dovetail over i; test n ∈ [3,i], x, y, z ∈ [1,i]; accept on counterexample; loops otherwise |

## R9. Final checklist

- [ ] I can state both pumping lemmas exactly and apply the CFL one with a full case analysis.
- [ ] I know which closure properties CFLs have, with counterexamples for the others.
- [ ] I can explain PDA ⇔ CFG at the level of "idea of the construction."
- [ ] I can write a complete TM (all transitions) for a simple function and trace it.
- [ ] I can write a simulation proof between two models in the 7 steps.
- [ ] I can prove a language decidable and argue termination.
- [ ] I can reproduce the A_TM diagonal argument and adapt it to a variant.
- [ ] I can do a reduction from A_TM in the right direction, with both implications.
- [ ] I know decidable vs recognizable vs neither, and why Ā_TM is not recognizable.
- [ ] I know when Rice's theorem applies and when it does not.
