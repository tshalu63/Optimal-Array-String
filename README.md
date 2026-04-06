# Deep Dive: Array & String Algorithmic Patterns

This repository documents the evolution of logic from naive approaches to optimized solutions for six essential coding patterns.

---

## 1. Two Sum
**Problem:** Find indices of two numbers in an array that add up to a specific `target`.

### 1.1 Brute Force
- **Method:** Use two nested loops. The outer loop picks an element $i$, and the inner loop checks every other element $j$ to see if $arr[i] + arr[j] == target$.
- **TC:** $O(n^2)$
- **SC:** $O(1)$

### 1.2 Optimized (Hash Map)
- **Method:** Iterate through the array once. For each element, calculate the `complement` ($target - current$). Check if this complement exists in a Hash Map. If it does, return the current index and the stored index. If not, add the current number and its index to the map.
- **TC:** $O(n)$
- **SC:** $O(n)$

---

## 2. Three Sum
**Problem:** Find all unique triplets $(a, b, c)$ such that $a + b + c = 0$.

### 2.1 Brute Force
- **Method:** Use three nested loops to find all triplets. To handle duplicates, you would need to sort each triplet and add it to a `Set`.
- **TC:** $O(n^3)$
- **SC:** $O(n)$ (to store unique triplets)

### 2.2 Optimized (Two Pointers)
- **Method:** 1. **Sort** the array first.
  2. Iterate through the array with pointer `i`. 
  3. For each `i`, set `left = i + 1` and `right = last_index`.
  4. While `left < right`:
     - If $sum == 0$, save the triplet and move both pointers, skipping identical values to avoid duplicates.
     - If $sum < 0$, move `left++` to increase the sum.
     - If $sum > 0$, move `right--` to decrease the sum.
- **TC:** $O(n^2)$
- **SC:** $O(1)$ (excluding output space)

---

## 3. Four Sum
**Problem:** Find unique quadruplets that sum to a `target`.

### 3.1 Brute Force
- **Method:** Four nested loops checking every combination of four numbers.
- **TC:** $O(n^4)$
- **SC:** $O(1)$

### 3.2 Optimized (Two Pointers)
- **Method:** This is an extension of 3Sum.
  1. **Sort** the array.
  2. Use two nested loops (pointers `i` and `j`) to fix the first two numbers.
  3. Inside the second loop, use the **Two Pointer** technique (`left` and `right`) to find the remaining two numbers.
  4. Crucial: Skip duplicate elements at every level (i, j, left, and right) to keep the results unique.
- **TC:** $O(n^3)$
- **SC:** $O(1)$

---

## 4. Subarray Sum Equals K
**Problem:** Count the total number of continuous subarrays whose sum equals `k`.

### 4.1 Brute Force
- **Method:** Generate all possible subarrays using two loops. For each subarray, calculate the sum and compare it to `k`.
- **TC:** $O(n^2)$
- **SC:** $O(1)$

### 4.2 Optimized (Prefix Sum + Hash Map)
- **Method:** 1. Maintain a `running_sum`.
  2. Use a Hash Map to store how many times a particular `prefix_sum` has occurred (initialize with `{0: 1}`).
  3. At each step, check if `running_sum - k` exists in the map.
  4. If it exists, it means there is a subarray ending here that sums to `k`. Add the frequency to your count.
- **TC:** $O(n)$
- **SC:** $O(n)$

---

## 5. String Compression
**Problem:** Compress an array of characters in-place. `["a","a","b","b","b"]` becomes `["a","2","b","3"]`.

### 5.1 Brute Force
- **Method:** Create a new string/list. Iterate through the input, count consecutive characters, and append the character and count to the new list.
- **TC:** $O(n)$
- **SC:** $O(n)$

### 5.2 Optimized (Two Pointers - In-Place)
- **Method:** 1. Use a `read` pointer and a `write` pointer.
  2. The `read` pointer finds the end of a group of identical characters.
  3. Calculate the length of the group.
  4. Write the character at the `write` pointer, then write the digits of the length if it's greater than 1.
  5. Return the position of the `write` pointer as the new length.
- **TC:** $O(n)$
- **SC:** $O(1)$

---

## 6. Permutation in String
**Problem:** Check if `s2` contains a permutation of `s1`.

### 6.1 Brute Force
- **Method:** Generate every possible permutation of `s1` ($n!$ permutations) and check if any of them exist as a substring in `s2`.
- **TC:** $O(n! \cdot m)$
- **SC:** $O(n)$

### 6.2 Optimized (Sliding Window)
- **Method:** 1. A permutation means the character counts are identical.
  2. Create a frequency array (size 26) for `s1`.
  3. Use a **Sliding Window** of size `len(s1)` on `s2`.
  4. As the window slides:
     - Add the new character to the window's frequency count.
     - Remove the character that is no longer in the window.
     - If the window's frequency array matches `s1`'s array, return true.
- **TC:** $O(n)$
- **SC:** $O(1)$ (Array size is fixed at 26)

---

## Performance Comparison

| Algorithm | Best Strategy | Time | Space |
| :--- | :--- | :--- | :--- |
| **Two Sum** | Hash Map | $O(n)$ | $O(n)$ |
| **Three Sum** | Sort + 2 Pointers | $O(n^2)$ | $O(1)$ |
| **Four Sum** | Sort + 2 Pointers | $O(n^3)$ | $O(1)$ |
| **Subarray Sum** | Prefix Sum + Map | $O(n)$ | $O(n)$ |
| **String Comp.** | Two Pointers | $O(n)$ | $O(1)$ |
| **Permutation** | Sliding Window | $O(n)$ | $O(1)$ |
