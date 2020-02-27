---
title: LeetCode 394. Decode String
date: 2020-02-26 22:47:15
tags: LeetCode
---

**First Submission**

```cpp
class Solution {
public:
    string decodeString(string s) {
        vector <vector <int>> encoded = findNum(s);
        if (encoded.size() == 0) {
            return s;
        }
        string ret = "";
        int i = 0;
        int j = 0;
        while(i<s.length()) {
            if (s[i] >= '0' && s[i] <= '9') {
                vector<int> token = encoded[j];
                ret += dupString(decodeString(s.substr(token[1]+1,token[2]-token[1]-1)),token[0]);
                j++;
                i = token[2];
            }
            else {
                ret += s[i];
            }
            i++;
        }
        return ret;
    }
    string dupString(string s, int n) {
        string str = "";
        for (int i = 0; i<n; i++) {
            str += s;
        }
        return str;
    }
    
    vector<vector <int>> findNum(string s) { //find [] in string s
        vector<vector <int> >encoded = {}; 
        for(int i = 0; i<s.length(); i++) {
            if (s[i] >= '0' && s[i] <= '9') {
                vector<int> token = {0,0,0};
                bool found = false;
                vector<int> stack = {};
                for(int j = i; j<s.length(); j++) {
                    if (!found && s[j] >= '0' && s[j] <= '9') {
                        token[0] = token[0]*10+s[j]-'0';
                    }
                    if (s[j] == '[') {
                        found = true;
                        stack.push_back(j);
                    }
                    if (s[j] == ']') {
                        if (stack.size() == 1) {
                            token[1] = stack[0];
                            token[2] = j;
                            encoded.push_back(token);
                            stack.pop_back();
                            i = j;
                            break; //found
                        }
                        stack.pop_back();
                    }
                    
                }
            }
        }
        return encoded;
    }
};
```

**Simplified**

```cpp
class Solution {
public:
    string decodeString(string s) {
        int i = 0;
        return decodeString(s,i); //start from index 0;
         // a temporary cannot bind to a non-const reference. Have declare an int.
    }
    string decodeString(const string &s, int &i) { // i is starting index
        // Forgot to use reference in parameters
        
        string res = "";
        
        while(i<s.length() && s[i] != ']') {
            if (!isdigit(s[i])) {
                res += s[i++];
            }
            else {
                int n = 0;
                while(i<s.length() && isdigit(s[i])) {
                    n = n*10 + s[i++] - '0';
                }
                i++; // '['
                string str = decodeString(s,i);
                i++; // ']'
                while(n-- > 0) {
                    res += str;
                }
            }
        }
        return res;
    }
};
```

