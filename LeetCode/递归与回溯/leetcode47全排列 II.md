#题目描述
给定一个可包含重复数字的序列 nums ，按任意顺序 返回所有不重复的全排列。
###示例 1：
输入：nums = [1,1,2]
输出：
[[1,1,2],
 [1,2,1],
 [2,1,1]]
###示例 2：
输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
![alt 属性文本](47.png)
```
public class text {
   boolean[] used;
   int[] nums;
    public List<List<Integer>> permuteUnique(int[] nums){
        List<List<Integer>> ans = new ArrayList<List<Integer>>();
        List<Integer> perm = new ArrayList<Integer>();
       used=new boolean[nums.length];
        this.nums=nums;
        Arrays.sort(nums);
        if(nums.length==0){
            return ans;
        }
        backtrack(perm,ans,0);
        return ans;
    }
    public void  backtrack(List<Integer> perm,List<List<Integer>> ans,int path){
        if(perm.size()==nums.length){
            ans.add(new LinkedList<>(perm));
            return;
        }

        for(int i=0;i<nums.length;i++){
          /*  */
            if (used[i] || (i>0 && nums[i]==nums[i-1] && !used[i-1])){
                continue;

            }
                perm.add(nums[i]);
                used[i]=true;
                backtrack(perm,ans,path+1);
                used[i]=false;
                perm.remove(perm.size()-1);

        }
    }
        public static void main(String[] args) {
          /*  HashMap<String,Integer> hashMap= new HashMap<>();
           hashMap.put("123",12);*/
            int[] nums = {3,3,0,3};
            text solution = new text();
            List<List<Integer>> lists = solution.permuteUnique(nums);
            System.out.println(lists);
        }
    }
```

if (vis[i] || (i > 0 && nums[i] == nums[i - 1] && !vis[i - 1])) {
      continue;
}

加上 !vis[i - 1]来去重主要是通过限制一下两个相邻的重复数字的访问顺序
对于两个相同的数11，我们将其命名为1a1b, 1a表示第一个1，1b表示第二个1； 那么，不做去重的话，会有两种重复排列 1a1b, 1b1a， 我们只需要取其中任意一种排列； 为了达到这个目的，限制一下1a, 1b访问顺序即可。 比如我们只取1a1b那个排列的话，只有当visit nums[i-1]之后我们才去visit nums[i]， 也就是如果!visited[i-1]的话则continue
