# Prefix sum pattern

<details>
<summary>1️⃣ Subarray Sum Equals K</summary>
  
**Problem:**  
Given an integer array `nums` and an integer `k`, return the total number of subarrays whose sum equals `k`.

**Trick:**  
- Use **prefix sums + hashmap**.  
- If `prefix_sum[i] - k` has been seen before, then there exists a subarray ending at `i` with sum `k`.  
- Store counts of prefix sums in a hashmap.
</details>

<details>
<summary>2️⃣ Subarray Sum Divisible by K</summary>
  
**Problem:**  
Given an integer array `nums` and an integer `k`, return the number of subarrays whose sum is divisible by `k`.

**Trick:**  
- Compute prefix sums and take modulo `k`.  
- If two prefix sums have the **same remainder**, the subarray between them is divisible by `k`.  
- Store counts of remainders in a hashmap.  
- Normalize remainder with `remainder = (prefix_sum % k + k) % k` to avoid negatives.
</details>

<details>
<summary>3️⃣ Continuous Subarray Sum (Good Subarray Multiple of K)</summary>

**Problem:**  
Given an integer array `nums` and an integer `k`, return `True` if there exists a subarray of length ≥ 2 whose sum is a multiple of `k`.  

**Trick:**  
- Similar to problem 2, but we need **length ≥ 2**.  
- Store the **first index** where each remainder is seen.  
- If the same remainder reappears at index `i`, check `(i - stored_index) >= 2`.  
- Initialize `freq[0] = -1` to handle subarrays starting from index `0`.
</details>

<details>
<summary>4️⃣ Contiguous Array (Equal 0s and 1s)</summary>
**Problem:**  
Given a binary array `nums`, return the maximum length of a contiguous subarray with equal number of `0`s and `1`s.

**Trick:**  
- Treat `0` as `-1`.  
- Then problem reduces to finding the **longest subarray with sum = 0**.  
- Use prefix sums + hashmap: store earliest index of each prefix_sum.  
- If prefix_sum repeats at index `i`, then subarray `(prev_index+1 ... i)` has equal 0s and 1s.  
- Initialize `freq[0] = -1`.
</details>

<details>
<summary>🧩 Common Pattern (Prefix Sum + HashMap)</summary>
1. Maintain a running `prefix_sum`.  
2. Transform it (plain sum, remainder, etc.).  
3. Use a hashmap to store **earliest index** (for max length problems) or **count** (for total count problems).  
4. Check when a transformed prefix sum reappears.  
</details>

# Array pattern
<details>
<summary>Move Zeroes</summary>

**Problem:**  
Given an integer array `nums`, move all `0`s to the end of it while maintaining the relative order of the non-zero elements.  
Do this **in-place** without making a copy of the array.  

**Trick:**  
- Use a **two-pointer technique**: one pointer (`j`) marks where the next non-zero should go.  
- Traverse the array: whenever you find a non-zero, place it at `nums[j]` and increment `j`.  
- After traversal, fill the remaining elements with `0`s.  
- Alternate trick: swap directly in-place whenever you find a non-zero.

</details>

<details>
<summary>Majority Element</summary>

**Problem:**  
Given an array `nums` of size `n`, return the **majority element**, which appears more than ⌊n/2⌋ times.  
It is guaranteed that a majority element always exists.  

**Trick:**  
- **Boyer–Moore Voting Algorithm** is the optimal approach.  
- Keep a `candidate` and a `count`.  
- If `count == 0`, pick the current number as candidate.  
- Increment `count` if the number matches candidate, otherwise decrement it.  
- At the end, the candidate will be the majority element.  
- Alternatives: counting with HashMap, or sorting and returning the middle element.

</details>

<details>
<summary>Rotate Array</summary>

**Problem:**  
Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.  

**Trick:**  
- Rotating right by `k` is the same as moving the last `k` elements to the front.  
- Handle `k > n` by taking `k % n`.  
- Three common approaches:
  1. **Reverse Method (Optimal O(n), O(1))**:  
     - Reverse entire array.  
     - Reverse first `k` elements.  
     - Reverse last `n-k` elements.  
  2. **Extra Array (O(n), O(n))**: Store rotated result in a new list and copy back.  
  3. **One-by-One Rotation (O(n·k), O(1))**: Not efficient.  

</details>

<details>
<summary>Best Time to Buy and Sell Stock II</summary>

**Problem:**  
You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `i`th day.  

- On each day, you may decide to **buy** and/or **sell** the stock.  
- You can hold **at most one share** of the stock at any time.  
- However, you can **buy and sell on the same day**.  

Return the **maximum profit** you can achieve.  

**Trick:**  
- This is the **“infinite transactions allowed”** version.  
- You don’t need to find local minima/maxima explicitly.  
- Simply **sum up all upward slopes**:  
  - For every consecutive pair of days, if `prices[i] > prices[i-1]`, add the difference to profit.  
- This greedy approach works because small profitable trades combine into the global maximum.  

</details>
