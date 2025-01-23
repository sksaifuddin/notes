While solving problem I always come across some common techniques, this is the list of all the techniques I come across and need them to solve more Leetcode problems
## 1. Creating frequency array

Creating a frequency array of string. That is, counting number of character of the string and presented in the form of array.

```java
 public int[] getFreq(String word) {
        int freq[] = new int[26];
        for(int i = 0; i<word.length(); i++) {
            freq[word.charAt(i) - 'a']++;
        }

        return freq;
    }
```

## 2. Row and Column Frequency Counting with Two-Pass Optimization

### Core Idea
1. **Precompute Metadata**:  
   - In a **first pass** over a grid/matrix, compute row and column statistics (e.g., counts, sums, flags).  
   - Store these in auxiliary arrays (`rowData`, `colData`).  

2. **Leverage Precomputed Data**:  
   - In a **second pass**, use the metadata to efficiently evaluate properties of individual cells without redundant checks.  

---

### When to Use This Technique
- Problems where an **element's behavior depends on its row/column neighbors**.  
- Use cases include:  
  - Checking isolation (e.g., "Is this the only element in its row/column?").  
  - Validating aggregate conditions (e.g., "Does this cell meet a row/column threshold?").  

### Generic Steps
1. **First Pass** (Metadata Collection):  
   - Traverse the grid to populate `rowData` and `colData` (e.g., count elements per row/column).  

2. **Second Pass** (Analysis):  
   - Revisit each element and use `rowData`/`colData` to apply constraints or adjust results.  
### Example Applications
1. **Isolation Detection**:  
   - Identify elements that are the only one in their row **and** column.  

2. **Aggregate Validation**:  
   - Count elements that meet row/column-specific criteria (e.g., value > row average).  

3. **Dependency Checks**:  
   - Verify if elements have required neighbors (e.g., in a Battleship game).  

### Why It Works
- **Decouples Computation**: Metadata precomputation avoids redundant row/column scans.  
- **Fast Lookups**: Auxiliary arrays act as a cache for quick row/column state checks.  

### Broader Context
- A form of **spatial preprocessing** and **memoization**, optimizing grid-based problems by trading minimal space for significant time savings.  
- Commonly used in algorithms for grids, matrices, image processing, and computational geometry.  

Practice problem: https://leetcode.com/problems/count-servers-that-communicate/