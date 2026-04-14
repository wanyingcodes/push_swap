# 🔢 push_swap

## 📌 Overview

`push_swap` is a constrained sorting project: given a list of integers, the goal is to sort them using two stacks (`a` and `b`) and a limited set of operations, while minimizing the total number of moves.  
Unlike traditional sorting, the challenge is not correctness alone, but **operation efficiency under strict constraints**.  

## ⚙️ Approach

After experimenting with different strategies (including the commonly used *Turk algorithm*), the final solution adopts a **cost-based greedy approach**.  

Instead of following a fixed sequence of operations, the algorithm:  
> evaluates all possible moves at each step and selects the one with the **lowest cost**  
This method proved to be both **simpler to reason about** and **consistently optimal within project constraints**.  

## 🧠 Algorithm Strategy

The implementation is structured in four stages:  

### 1. Initial Reduction

* Split the input:  

  * smaller elements → pushed to stack `b`  
  * larger elements → rotated within `a`  

* Reduce `a` to a small base case (3 elements)  

👉 This avoids expensive operations on large stacks and simplifies later steps.  

### 2. Base Case Sorting

* Sort the remaining 3 elements in `a`  
* Achieved in constant time (≤ 2 operations)  

### 3. Cost-Driven Reinsertion (Core)

Elements are reinserted from `b → a` one by one.  

For each element in `b`, the algorithm computes:  

* rotations needed in `a` to reach its target position  
* rotations needed in `b` to bring it to the top  

A total **cost** is then calculated:  

* same direction → `max(|a|, |b|)`  
* opposite direction → `|a| + |b|`  

The element with the **lowest cost** is selected and executed.  

#### 🔑 Key Optimization

When both stacks rotate in the same direction:  

* `ra + rb → rr`  
* `rra + rrb → rrr`  

This reduces the total number of operations significantly and is central to achieving good performance.  

### 4. Final Alignment

* Rotate stack `a` so that the smallest element is at the top  

## 🚀 Key Insights

* **Local optimal choices lead to global efficiency**  
  A greedy strategy is sufficient when combined with a good cost model.  

* **Operation merging matters more than raw logic**  
  Reducing instruction count (via `rr` / `rrr`) has a major impact.  

* **Perfect algorithms are not required**  
  The goal is not theoretical optimality, but staying within strict operation limits reliably.  

## 📊 Performance

The implementation meets full-score benchmarks:  

* ✅ 100 numbers → well below 700 operations  
* ✅ 500 numbers → well below 5500 operations  

Additionally, the algorithm maintains a **safe margin**, ensuring stable performance across different inputs.  

## 🔧 Usage

```bash
make
./push_swap 3 2 1 6 5 4
```

The program outputs a sequence of operations:  

```text
pb
pb
sa
pa
pa
...
```

## ⚠️ Constraints

* No global variables  
* Only allowed functions (`malloc`, `free`, `write`, etc.)  
* Input must be:  

  * valid integers  
  * within int range  
  * without duplicates  

Errors are handled by printing:  

```text
Error
```

## ✨ Final Note

This project highlights an important idea:  

> In constrained systems, the problem is not just *what works*,  
> but *what works with the lowest cost*.  

The shift from fixed strategies to a **cost-evaluated decision model** was the key step that made the solution both robust and efficient.  

## 📬 Contact
GitHub: https://github.com/wanyingcodes  
Email: wanyingt@hotmail.com  