# Dynamic Programming — TA Session Notes

## Introduction

A lot of students feel that DP is one of the hardest topics in algorithms.

Usually not because the code is difficult, but because when you see a new problem, it is hard to know how to START.

So instead of memorizing formulas and tables, we will focus on a process that helps us discover the solution ourselves.

For most DP problems, I try to think about these steps:

1. What choices do I have?
2. What information matters?
3. After making a choice, what smaller problem remains?
4. When does the answer become obvious?
5. Write the recurrence / optimal structure
6. How do we know the traversal order?

---

# 1) What choices do I have?

Many DP problems are built around decisions.

Examples:

* take / skip
* right / down
* match / don’t match

### Knapsack

At item `i`:

* take item `i`
* skip item `i`

### Weighted Activity Selection

At activity `i`:

* take activity `i`
* skip activity `i`

Idea:
DP recurrences are usually built from exploring these choices.

---

# 2) What information matters?

Question:
What information changes the remaining answer?

Or:

If we pause the problem right now, what information would another person need to continue solving the problem without re-solving everything?

The information that affects the future answer must be part of the DP state.

---

## Knapsack

Suppose I only tell you:
“We are currently at item `i`.”

Can you continue solving the problem?

No.

Because different remaining capacities lead to different future answers.

So we need:

1. which item we reached
2. remaining capacity

DP state:

```text
dp[i][capacity]
```

Meaning:

```text
maximum value obtainable using items 0...i
with remaining capacity = capacity
```

Idea:
If changing some information changes the future answer, that information must be in the state.

---

## Weighted Activity Selection

Suppose I only tell you:
“We are currently at activity `i`.”

Can you continue solving?

Yes.

Because:

* the remaining activities are already known
* compatibility is already determined

So the activity index alone is enough.

DP state:

```text
dp[i]
```

Meaning:

```text
maximum value obtainable
considering activities i...n−1
```

---

## Collecting Apples

Suppose I only tell you:
“We are currently at row 0.”

Can you continue solving?

No.

Because `(0,0)` and `(0,1)` are different positions and lead to different future answers.

Row alone is not enough.

Column alone is also not enough.

So we need both row and column.

DP state:

```text
dp[i][j]
```

Meaning:

```text
maximum apples collectable
starting from cell (i,j)
```

---

# 3) After making a choice, what smaller problem remains?

DP problems are usually reduced into smaller versions of the same problem.

---

## Knapsack

### Choice 1: Take item `i`

What changes?

1. value increases
2. capacity decreases
3. move to previous items

Smaller problem:

```text
solve(i−1, capacity−w[i])
```

---

### Choice 2: Skip item `i`

What changes?

1. capacity stays the same
2. move to previous items

Smaller problem:

```text
solve(i−1, capacity)
```

Idea:
Most DP recurrences are:

```text
current gain/value
+
answer to a smaller subproblem
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
dp[NEXT(i)]
```

---

### Skip activity `i`

Smaller problem:

```text
dp[i+1]
```

---

## Collecting Apples

Choices:

* move right
* move down

Smaller problems:

* `dp[i][j+1]`
* `dp[i+1][j]`

Important:
The current cell value is outside the max because BOTH moves collect the current cell.

---

# 4) Base Cases

At some point, the answer becomes obvious and does not need more computation.

---

## Knapsack

### Capacity = 0

No items fit.

Answer = 0

---

### No items left

Nothing left to take.

Answer = 0

---

## Weighted Activity Selection

If:

```text
i >= n
```

No activities remain.

Answer = 0

---

## Fibonacci

If:

* `i = 0`
* `i = 1`

Answers are already known:

```text
F(0)=0
F(1)=1
```

Idea:
Base cases stop the recursion.

---

# 5) Write the recurrence / optimal structure

Now we combine:

* the choices
* the state
* the smaller subproblems
* the base cases

to build the recurrence.

Idea:

```text
DP recurrence =
current gain/value
+
smaller subproblem
```

---

## Knapsack

```text
dp[i][c] =
max(
    v[i] + dp[i−1][c−w[i]],
    dp[i−1][c]
)
```

Current gain is inside the max because it depends on the choice.

---

## Weighted Activity Selection

```text
dp[i] =
max(
    v[i] + dp[NEXT(i)],
    dp[i+1]
)
```

---

## Collecting Apples

```text
dp[i][j] =
grid[i][j]
+
max(
    dp[i+1][j],
    dp[i][j+1]
)
```

The current cell value is outside the max because we collect it regardless of the move chosen.

Important:
There is often more than one valid DP definition.

We usually choose the definition that makes:

* the recurrence simpler
* the transitions more natural

---

# 6) How do we know traversal order?

Traversal order is NOT memorized.

It comes from the dependencies in the recurrence.

Question:

Before computing this state, which states must already be solved?

---

## Knapsack

```text
dp[i][c]
depends on
dp[i−1][...]
```

So previous rows must already exist.

Traversal:
top → bottom

---

## Collecting Apples

```text
dp[i][j]
depends on:
- right
- down
```

So those cells must already exist first.

Traversal:
bottom-right → top-left

---

## Fibonacci

```text
dp[i]
depends on:
dp[i−1], dp[i−2]
```

Traversal:
left → right

---

# Final Idea

The goal is NOT to instantly see the recurrence.

Good DP solving is usually a process:

1. define the state
2. identify choices
3. determine the smaller problem
4. build the recurrence
5. determine dependencies/traversal

If you repeatedly practice this process, DP problems become much less intimidating.
