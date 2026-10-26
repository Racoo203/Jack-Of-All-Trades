---
subject: Final Semester Data Science Modules
type: MOC
course_code: TBD
domain: multiple
level: BSc
status: seeding
confidence: 0
tags:
  - moc
  - final-semester
  - data-science
---
> **Placeholder title.** Rename this file and set `course_code` once the official course name/code is confirmed — every note links to modules, not to this file's name, so renaming is safe.

## Concept narrative

The final BSc semester is organised as a set of review and applied modules rather than one subject. They are **not** filed in a single folder: each module's concepts live in the domain they belong to, so a concept seen here and in an earlier course still has exactly one note (the vault's domain-not-degree rule). This MOC is the class-level index that stitches them together.

Two modules are *reviews* of material already in the vault, so they extend existing courses instead of creating new ones. The other five are new territory and live in `09 Computer Science & Data Engineering`.

## Module map

| Module | Notes live in | Status |
|---|---|---|
| Topological Data Analysis Review | `01 Mathematical Foundations/Geometry and Topology for Data Science/` — see [[MOC - Geometry and Topology for Data Science]] | 38 notes drafted/seeding already (MA2007B); review module adds nothing new unless it covers topics outside MA2007B |
| Machine Learning Models Review | `06 Machine Learning & AI/Machine Learning/` | 1 empty stub ([[Regularization]]) — effectively unstarted |
| Data Structures and Algorithms | `09 Computer Science & Data Engineering/Data Structures and Algorithms/` | 16 notes (9 drafted, 6 seeding, 1 empty) |
| Databases & SQL | `09 Computer Science & Data Engineering/Databases & SQL/` | unstarted |
| Cloud Computing | `09 Computer Science & Data Engineering/Cloud Computing/` | unstarted (related class work: federated learning activity) |
| MLOps (MLflow, Optuna, Kedro, GitHub, Docker) | `09 Computer Science & Data Engineering/MLOps/` | unstarted |
| Data Governance & Business Case | `09 Computer Science & Data Engineering/Data Governance & Business Case/` | unstarted |

Course material for each module goes in the mirrored `Resources/09 Computer Science & Data Engineering/<module>/` (and `Resources/06 Machine Learning & AI/Machine Learning/` for the ML review).

## Concept map

### Data Structures and Algorithms

**Complexity**
- [[Ordering Algorithms]] — Big-O definition $\mathcal{O}(g(n))$

**Data structures**
- [[Virtual Memory Model]] — code / data / stack / heap layout; the cost model behind the structures below
- [[List]] → [[Dynamic Array]] → [[Linked List]] — append/remove/get/search costs compared
- [[Dictionary]] — hash function + index table + entries table, open addressing (linear probing)

**Hashing**
- [[Hashing Tables]] — separate chaining; why any fixed hash function has a bad input set
- [[Universal Hashing]] — random choice from $h_{a,b}(x) = ((ax+b) \bmod p) \bmod m$

**Searching**
- [[Binary Search]] — $O(\log n)$ on a sorted list
- [[Graph Codifying]] — adjacency matrix vs adjacency list
- [[Breadth First Search]] — distances and predecessors from a source vertex

**Sorting**
- [[Selection Sort]], [[Bubble Sort]], [[Insertion Sort]] — $O(n^2)$ family
- [[Merge Sort]] — divide and conquer, $O(n \log n)$
- [[Quick Sort]] — pivot partitioning, $O(n \log n)$ expected, $O(n^2)$ worst

### Other modules
_To be mapped when each module's batch starts (see the vault strategy doc for the ranked order)._

## Key dependency chains

```
Ordering Algorithms (Big-O)
   ├─► List ─► Dynamic Array ─► Linked List        (cost trade-offs)
   ├─► Hashing Tables ─► Universal Hashing
   │        └─► Dictionary (open addressing variant)
   ├─► Binary Search  (needs a sorted list ◄── Sorting)
   └─► Sorting: Selection/Bubble/Insertion ─► Merge Sort / Quick Sort

Graph Codifying (adjacency list) ─► Breadth First Search
Dictionary ─► Graph Codifying (adjacency list *is* a dictionary)
```

## Exam focus

_Fill in once each module's assessment format is known (and whether the cumulative BSc exam samples these modules)._

## Open questions

- [ ] Official course name and code for this class — rename this MOC and set `course_code`.
- [ ] Module schedule: which modules are done, current, upcoming, and how each is assessed? Drives the population order.
- [ ] Does the TDA Review module cover anything beyond MA2007B (e.g. persistence landscapes, vectorisations for ML)? If so, add notes to the existing course folder, not a new one.
- [ ] **Correctness flags in existing DSA notes (not edited — check and fix):**
  - [[Universal Hashing]] states $P(h_{a,b}(x)=h_{a,b}(y)) = \tfrac1m$ with only $p>m$. The standard result is $\le \tfrac1m$ with $p \ge |U|$ (key-universe size) and $a \neq 0$ — [[Hashing Tables]] already states it that way, so the two notes disagree. Proof is still a placeholder.
  - [[Ordering Algorithms]]: "We say that $g(n)$ is of class $\mathcal{O}(g(n))$" should read $f(n)$.
  - [[Binary Search]]: the recursive step should continue on the sublist *after* the midpoint (mid+1), not "from the mid-point element"; including the midpoint can loop forever on a two-element sublist.
  - [[Dynamic Array]]: append-at-end is $O(1)$ **amortized** (occasional $O(n)$ resize) — worth stating, it's the whole point of the structure versus [[List]]. Definition sentence is unfinished.
  - [[Insertion Sort]], [[Quick Sort]] examples are unfinished; [[Bubble Sort]] is empty; no note states sorting complexities except Merge Sort.
