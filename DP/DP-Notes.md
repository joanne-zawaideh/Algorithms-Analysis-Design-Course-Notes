# Dynamic Programming Review Session Notes

# A Tip for my fellow colleagues

Although it might feel unfamiliar and out of your comfort zone, try this:

Instead of memorizing the solutions for the problems given in class and attempting to apply them to new DP problems, focus on learning the thinking process when approaching a DP problem.

Once you learn how and where to start, DP will start feeling logical and you will become more confident.

---

# The DP Process

For most DP problems, consider these steps:

1. Define the state
2. Identify the choices
3. Build the smaller subproblems
4. Determine the base cases
5. Write the recurrence
6. Determine traversal order

---

# Step 1 — Define the State

Question:

> “What information do I need to describe the remaining problem?”

The answer to this question becomes the DP state.

---

## Knapsack

Question:

> “If I pause the problem right now, what information do I need to continue solving?”

We need:

* the current item
* the remaining capacity

Knowing only one is not enough; if I only know the current item, how will I know if it fits?

So the state becomes:

```text
dp[i][capacity]
```

Meaning:

```text
maximum value gained
using items 0...i
with remaining capacity = capacity
```

---

## Weighted Activity Selection

Question:

> “If I tell you we are currently at activity i, can you continue solving?”

Yes.

Because:

* the remaining activities are known
* compatibility can be determined

So only the activity index matters.

State:

```text
dp[i]
```

Meaning:

```text
maximum value gained
considering activities i...n−1
```

---

## Collecting Apples

 

Question:

> “If I tell you we are currently at row i, can you continue solving?”

No.

Because different columns have different future moves and lead to different answers, and the same goes for rows.

 Since different rows and columns lead to different future answers, we need both.

  

State:

```text
dp[i][j]
```

Meaning:

```text
maximum apples collectable
from cell (0,0) to cell (i,j)
```

---

# Step 2 — Identify the Choices

Examples of choices:

* take / skip
* right / down
* match / don’t match

The recurrence usually comes from exploring these choices.

**Note:** there could be a problem with more than two choices!

---

## Knapsack

Choices at item `i`:

* take item `i`
* skip item `i`

---

## Weighted Activity Selection

Choices at activity `i`:

* take activity `i`
* skip activity `i`

---

## Collecting Apples

In the original problem, the possible moves are:

* right
* down

However, our DP state represents:

```text
best answer from (0,0) to (i,j)
```

and when computing cell `(i,j)`, we ask:

> “From which cells could we have arrived here?”

So the possible previous moves (choices) become:

* the upper cell
* the left cell

---

# Step 3 — Build the Smaller Subproblems

Question:

> “After making this decision, what smaller problem remains?”

---

## Knapsack

### Take item `i`

What changes?

* value increases
* capacity decreases

And the remaining problem uses previous items.

Smaller problem:

```text
solve(i−1, capacity−w[i])
```

---

### Skip item `i`

Smaller problem:

```text
solve(i−1, capacity)
```

---

## Weighted Activity Selection

### Take activity `i`

Gain:

```text
v[i]
```

Smaller problem:

```text
solve(NEXT(i))
```

---

### Skip activity `i`

Smaller problem:

```text
solve(i+1)
```

---

## Collecting Apples

To reach cell `(i,j)`, we could only come from:

* the upper cell
* the left cell

So the smaller subproblems become:

```text
solve(i−1, j)
```

and

```text
solve(i, j−1)
```

---

# Step 4 — Determine the Base Cases

At some point, the answer becomes obvious and does not need more computation.

---

## Knapsack

### No items left

```text
i == 0
```

Answer:

```text
0
```

---

### Capacity becomes 0

No more items can fit when:

```text
capacity == 0
```

Answer:

```text
0
```

---

## Weighted Activity Selection

If:

```text
i >= n
```

No activities remain.

Answer:

```text
0
```

---

## Collecting Apples

If:

```text
i == 0 && j == 0
```

we are already at the starting cell.

Answer:

```text
grid[0][0]
```

---

# Step 5 — Write the Optimal Substructure

Now combine:

* the choices
* the current value
* the smaller subproblems
* the base cases

**Note:** Most DP *recurrences* = current value + smaller subproblem

---

## Knapsack

### Optimal Substructure

```text
solve(i,c) = 0                          if(i < 0 || c == 0)

solve(i,c) =
max(
    v[i] + solve(i−1,c−w[i]),           otherwise
    solve(i−1,c)
)
```

---

## Weighted Activity Selection

### Optimal Substructure

```text
solve(i) = 0                           if(i >= n)  

solve(i) =
max(
    v[i] + solve(NEXT(i)),             otherwise
    solve(i+1)
)
```

---

## Collecting Apples

### Optimal Substructure

```text
solve(i,j) = grid[i][j]                 if(i == 0 && j == 0) 
 
solve(i,j) =
grid[i][j]
+
max(
    solve(i−1,j),                       otherwise
    solve(i,j−1)
)
```

The current cell value is outside the max because BOTH choices gain the current cell.

---

# Step 6 — Determine Traversal Order

Question:

> “What states must already exist before computing the current state?”

We compute smaller subproblems first, then use them to compute larger ones.

---

## Knapsack

Current state depends on:

```text
i−1
```

So previous rows must already exist first.

Traversal:

```text
top → bottom
```

---

## Weighted Activity Selection

Current state depends on:

* `i+1`
* `NEXT(i)`

So future indices must already exist first.

Traversal:

```text
right → left   or   n−1 → 0
```

---

## Collecting Apples

Current state depends on:

* upper cell
* left cell

So those cells must already exist first.

Traversal:

```text
top-left → bottom-right
```

---

# Final Verdict

Steps to solving DP questions:

1. define the state
2. identify the choices
3. determine the smaller problem
4. determine the base cases
5. build the recurrence
6. determine traversal order
