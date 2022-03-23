```cpp
class Solution {
public:
    int getKthElement(const vector<int>& a, const vector<int>& b, int k) {
        int m = a.size();
        int n = b.size();
        int i = 0, j = 0;
        while (true) {
            if (i == m) {
                return b[j + k - 1];
            }
            if (j == n) {
                return a[i + k - 1];
            }
            if (k == 1) {
                return min(a[i], b[j]);
            }
            int ni = min(i + k / 2 - 1, m - 1);
            int nj = min(j + k / 2 - 1, n - 1);
            int p1 = a[ni];
            int p2 = b[nj];
            if (p1 <= p2) {
                k -= ni - i + 1;
                i = ni + 1;
            }
            else {
                k -= nj - j + 1;
                j = nj + 1;
            }
        }
    }

    double findMedianSortedArrays(vector<int>& a, vector<int>& b) {
        int n = a.size() + b.size();
        if (n % 2 == 1) {
            return getKthElement(a, b, (n + 1) / 2);
        }
        else {
            return (getKthElement(a, b, n / 2) + getKthElement(a, b, n / 2 + 1)) / 2.0;
        }
    }
};
```
