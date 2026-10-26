---
title: "Dictionary"
domain: "Computer Science & Data Engineering"
course: "Data Structures and Algorithms"
unit: "Data Structures"
level: BSc
status: drafted
confidence: 0
tags: [data-structures-algorithms]
---
A dictionary consists of:

1. A hashing function that transforms keys to indexes.
2. A table that relates the indexes with the positions of the keys in the dictionary (the **index table**).
3. A table that relates the positions with the entries (the **entries table**). In this case, our entries are key-value pairs. Positions follow insertion order.

In Python, the index table uses **open addressing**: if a slot is occupied, we probe other slots _of the same table_ (no buckets). In the example below we use **linear probing** ($h, h+1, h+2, \dots \bmod m$) for simplicity; CPython uses a different probe sequence (see the end of this note).

Example: Implement the following dictionary using a table with 10 indexes.

```
D = {
	"Ana": 20,       # 0
	"Luisa": 34,     # 1
	"Carolina": 40,  # 2
	"Juana": 53,     # 3
	"Esmeralda": 36  # 4
}

# m = 10
# hash function: number of letters of the key.
```

So $h(\text{Ana}) = 3$, $h(\text{Luisa}) = 5$, $h(\text{Carolina}) = 8$, $h(\text{Juana}) = 5$, and $h(\text{Esmeralda}) = 9$.

Juana collides with Luisa at index 5, so it probes to index 6. $$ \matrix{ \text{Index} & \text{Position} \\
	0 & - \\ 
	1 & - \\
	2 & - \\ 
	3 & 0 \\ 
	4 & - \\
	5 & 1 \\ 
	6 & 3 \\ 
	7 & - \\ 
	8 & 2 \\ 
	9 & 4 \\ 
}$$
$$ \matrix{ 
	\text{Positions} & \text{Entries} \\
	0 & (\text{Ana}, 20) \\ 
	1 & (\text{Luisa}, 34) \\
	2 & (\text{Carolina}, 40) \\
	3 & (\text{Juana}, 53) \\ 
	4 & (\text{Esmeralda}, 36) \\ 
}$$

**Lookup = hash, then compare keys, probing until a match or an empty slot.**

$D[\text{Juana}]$: $h(\text{Juana}) = 5 \to$ position $1 \to$ key is Luisa $\neq$ Juana $\to$ probe index $6 \to$ position $3 \to (\text{Juana}, 53)$ ✓. So $D[\text{Juana}] = 53$.

$D[\text{Alma}]$: $h(\text{Alma}) = 4 \to$ index 4 is empty $\to$ the key is absent $\to$ `KeyError` (`D.get("Alma")` returns `None`).

## How CPython actually does it

- Table size $m$ is a power of 2 (minimum 8), and the starting index is `i = hash & (m - 1)`, i.e. $\text{hash} \bmod m$.
- Probe sequence on collision: `perturb >>= 5; i = (5*i + perturb + 1) & (m - 1)`, where `perturb` starts as the full hash. The high bits of the hash get mixed in, so collisions don't cluster like in linear probing.
- The entries table stores `(hash, key, value)`. The hash is cached so lookups compare hashes before comparing keys.
- It resizes once more than $\tfrac{2}{3}m$ slots are used (so a size-8 table holds at most 5 entries).
- `str` hashes use SipHash-1-3 (Python ≥ 3.11) and are salted per process (`PYTHONHASHSEED`), so the table layout changes between runs.