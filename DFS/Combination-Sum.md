##Combination Sum

27% Accepted

	Given a set of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

	The same repeated number may be chosen from C unlimited number of times.



	For example, given candidate set 2,3,6,7 and target 7,
	A solution set is:
	[7]
	[2, 2, 3]

	Have you met this question in a real interview? Yes
	Example
	given candidate set 2,3,6,7 and target 7,
	A solution set is:
	[7]
	[2, 2, 3]

####Note
	All numbers (including target) will be positive integers.
	Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).
	The solution set must not contain duplicate combinations.
####Tags Expand
- Backtracking Array

####思路1
- 标准DFS题
- 易错点在于pos的传递
- 因为提供的数组可能存在duplicate number,所以在挑选的时候,因为前一个数已经无限次使用过了,所以不需要duplicate number了,所以跳过

```java
public class Solution {
    /**
     * @param candidates: A list of integers
     * @param target:An integer
     * @return: A list of lists of integers
     */
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        // write your code here
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> combo = new ArrayList<Integer>();
        Arrays.sort(candidates);
        dfs(result, combo, candidates, 0, target, 0);
        return result;
    }

    public void dfs(List<List<Integer>> result, List<Integer> combo, int[] candidates, int pos, int target, int sum) {

        if (sum > target) {
            return;
        } else if (sum == target) {
            result.add(new ArrayList<Integer>(combo));
        }

        for (int i = pos; i <candidates.length; i++) {
            if (i != candidates.length - 1 && candidates[i] == candidates[i + 1]) {
                continue;
            }
            combo.add(candidates[i]);
            sum += candidates[i];
            dfs(result, combo, candidates, i, target, sum);
            sum -= candidates[i];
            combo.remove(combo.size() - 1);
        }
    }
}

```


###思路2
- 在传递进DFS的时候，已经完成了去重，之后再DFS里边的条件就好写了

```java
public class Solution {
    /**
     * @param candidates: A list of integers
     * @param target: An integer
     * @return: A list of lists of integers
     */
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        // write your code here
        List<List<Integer>> results = new ArrayList<List<Integer>>();
        List<Integer>  combination = new ArrayList<Integer>();
        
        if (candidates == null || candidates.length == 0) {
            return results;
        }
        
        Arrays.sort(candidates);
        List<Integer> candidateList = new ArrayList<Integer>();
        
        for (int i = 0; i < candidates.length; i++) {
            if (i >= 1 && candidates[i] == candidates[i - 1]) {
                continue;
            }
            candidateList.add(candidates[i]);
        }
        
        dfs(results, combination, candidateList, target, 0);
        
        return results;
        
    }
    
    public void dfs(List<List<Integer>> results, List<Integer> combination, List<Integer> candidateList, int target, int index) {
        
        if (target < 0) {
            return;
        }
        
        if (target == 0) {
            results.add(new ArrayList<Integer>(combination));
            return;
        }
        
        for (int i = index; i < candidateList.size(); i++) {
            int element = candidateList.get(i);
            combination.add(element);
            dfs(results, combination, candidateList, target - element, i);
            combination.remove(combination.size() - 1);
        }
    }
}
```
