**[](auto &a, auto &b)**

|Capture Form|Access|Modification|Notes|
|---|---|---|---|
|`[]`|❌|❌|Can only use parameters|
|`[=]`|✅|❌|Copies outer variables (read-only)|
|`[&]`|✅|✅|Can read & modify all outer variables|
|`[x]`|✅ (x)|❌|Captures x by value|
|`[&x]`|✅ (x)|✅|Captures x by reference|
|`[x, &y]`|Mixed|Mixed|Fine-grained control|

---
convert 2D matrix to ID
```
index of 1D matrix=rowNo of 2D matrix* row length+column No. of 2D matrix
```
