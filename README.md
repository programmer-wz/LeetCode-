# LeetCode
LeetCode题解（正在更新中...）
### 217存在重复元素
1. 暴力破解
```class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        for(int i;i<nums.size();i++){
            if(nums[i]==nums[i+1]){
                return true;
            }
        }
        return false;
    }
};
```
2. 哈希表
```class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> set;
        for(auto num: nums){
            if(set.find(num)!=set.end()){
                return true;
            }
            set.insert(num); 
        }
        return false;
    }
};
```
### 136 只出现一次的数字
1. 按位异或
```class Solution {
public:
    int singleNumber(vector<int>& nums) {
        for(int i=1;i<nums.size();i++){
            nums[0]=nums[0]^nums[i];
        }
        return nums[0];
    }
};
```
### 169 多数元素
1. 排序后，出现次数大于n/2的元素，一定在中间位置上
```
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        int length=nums.size();
        return nums[length/2];
    }
};
```
### 617 合并二叉树
1. 递归法（前序遍历）
```class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        if(root1==nullptr) return root2;
        if(root2==nullptr) return root1;
        root1->val+=root2->val;
        root1->left=mergeTrees(root1->left,root2->left);
        root1->right=mergeTrees(root1->right,root2->right);
        return root1;
    }
};
```
2. 迭代法
```class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        if(root1==nullptr) return root2;
        if(root2==nullptr) return root1;
        queue<TreeNode*> que;
        que.push(root1);
        que.push(root2);
        while(!que.empty()){
            TreeNode* node1=que.front();
            que.pop();
            TreeNode* node2=que.front();
            que.pop();
            node1->val+=node2->val;
            if(node1->left!=nullptr&&node2->left!=nullptr){
                que.push(node1->left);
                que.push(node2->left);
            }
            if(node1->right!=nullptr&&node2->right!=nullptr){
                que.push(node1->right);
                que.push(node2->right);
            }
            if(node1->left==nullptr&&node2->left!=nullptr){
                node1->left=node2->left;
            }
            if(node1->right==nullptr&&node2->right!=nullptr){
                node1->right=node2->right;
            }
        }
        return root1;
    }
};
```
### 700 二叉搜索树中的搜素
1. 递归法
```class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
        if(root==nullptr||root->val==val){
            return root;
        }
        if(root->val>val){
            return searchBST(root->left,val);
        }else{
            return searchBST(root->right,val);
        }
        /*if(root->val<val){
            return searchBST(root->right,val);
        }*/
        return nullptr;
    }
};
```
2. 迭代法
```class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
        while(root!=nullptr){
            if(root->val>val){
                root=root->left;
            }else if(root->val<val){
                root=root->right;
            }else{
                return root;
            }
        }
        return nullptr;
    }
};
```
### 98 验证二叉搜索树
1. 递归
```class Solution {
private:
    vector<int> vec;
    void traversal(TreeNode* node){
        if(node==nullptr) return;
        if(node->left){
            traversal(node->left);
        }
        vec.push_back(node->val);
        if(node->right){
            traversal(node->right);
        }
    }
public:
    bool isValidBST(TreeNode* root){
        vec.clear();
        traversal(root);
        for(int i=1;i<vec.size();i++){
            if(vec[i]<=vec[i-1]){
                return false;
            }
        }
        return true;
    }
};
```
2. 迭代法
```class Solution {
public:
    bool isValidBST(TreeNode* root) {
        stack<TreeNode*> st;
        TreeNode* cur=root;
        TreeNode* pre=nullptr;
        while(!st.empty()||cur!=nullptr){
            if(cur!=nullptr){
                st.push(cur);
                cur=cur->left;
            }else{
                cur=st.top();
                st.pop();
                if(pre!=nullptr&&cur->val<=pre->val){
                    return false;
                }
                pre=cur;
                cur=cur->right;
            }
        }  
        return true; 
    }
};
```

