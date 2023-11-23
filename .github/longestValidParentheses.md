---
name: Longest Valid Parentheses Problem
about: Solution and notes on Longest Valid Parentheses Problem
title: 'Longest Valid Parentheses'
labels: C++, Hard
assignees: 'Shivam Patel'

---

# 

## Code
```cpp
#include <stack>
#include <algorithm>

using namespace std;

class Solution {
public:
    int longestValidParentheses(string s) {
        int maxLen = 0;
        stack<int> stk;
        stk.push(-1);

        for (int i = 0; i < s.length(); ++i) {
            if (s[i] == '(') {
                stk.push(i);
            } else {
                stk.pop();
                if (stk.empty()) {
                    stk.push(i);
                } else {
                    maxLen = max(maxLen, i - stk.top());
                }
            }
        }

        return maxLen;
    }
};

```

## Notes
### Longest Valid Parentheses Problem Solution in C++

#### Problem Description
This solution addresses the problem of finding the length of the longest valid parentheses substring in a given string. The problem requires determining the length of the longest substring containing valid parentheses pairs.

#### Solution Overview
- The algorithm uses a stack to keep track of the indices of characters in the string.
- Initialize the stack with -1 to represent the base index.
- Iterate through the characters of the input string.
- If an opening parenthesis is encountered, push its index onto the stack.
- If a closing parenthesis is encountered:
  - Pop the top element from the stack.
  - If the stack is not empty, update the maximum length by calculating the difference between the current index and the index at the top of the stack.
  - If the stack becomes empty, push the current index onto the stack.
- The result is the maximum length of a valid parentheses substring.

