1. 在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

   ```
   public class Solution {
       public boolean Find(int target, int [][] array) {
   		int posX = 0, posY = array.length -1;
   		
   		while (posX >=0 && posX < array.length && posY >=0 && posY < array[0].length){
   			if (target == array[posX][posY]){
   				return true;
   			}
   			
   			if (target < array[posX][posY]){
   				posY--;
   			}else{
   				posX++;
   			}
   		}
   		
       	return false;
       
       }
   }
   ```

2. 请实现一个函数，将一个字符串中的空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

   ```
   class Solution {
   public:
   	void replaceSpace(char *str,int length) {
           int cnt = 0;
           for (int i = 0 ; i < length; i++){
               if (str[i] == ' '){
                   cnt++;
               }
           }
           
           int j = length + 2 * cnt - 1;
           for(int i = length - 1; i >= 0; i--){
               if (str[i] == ' '){
                   str[j--] = '0';
                   str[j--] = '2';
                   str[j--] = '%';
               }else{
                   str[j--] = str[i];
               }
           }
   	}
   };
   ```

3. 输入一个链表，从尾到头打印链表每个节点的值。

   ```
   /**
   *  struct ListNode {
   *        int val;
   *        struct ListNode *next;
   *        ListNode(int x) :
   *              val(x), next(NULL) {
   *        }
   *  };
   */
   class Solution {
   public:
       vector<int> printListFromTailToHead(ListNode* head) {
           vector<int> numArray;
   		stack<int> numStack;

   		ListNode* pointer = head;

   		while (pointer != NULL){
   			numStack.push(pointer->val);
   			pointer = pointer->next;
   		}

   		while (!numStack.empty()){
   			numArray.push_back(numStack.top());
   			numStack.pop();
   		}
   		return numArray;
       }
   };
   ```

4. 输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

   ```
   class Solution {
   public:
       TreeNode* reConstructBinaryTree(vector<int> pre,vector<int> vin) {
           int pre_size = pre.size();
           int vin_size = vin.size();
           if(pre_size == 0 && vin_size == 0){
               return NULL;
           }
           
           if(pre_size == 1 && vin_size == 1){
               TreeNode* leaf = new TreeNode(pre[0]);
               return leaf;
           }
           
           int root_value = pre[0];
           int pos = 0;
           for(; pos < vin_size; pos++){
               if(vin[pos] == root_value){
                   break;
               }
           }
           
           vector<int> left_pre = vector<int>(pre.begin() + 1, pre.begin() + pos + 1);
           vector<int> right_pre = vector<int>(pre.begin() + pos + 1, pre.end());
           vector<int> left_vin = vector<int>(vin.begin(), vin.begin() + pos);
           vector<int> right_vin = vector<int>(vin.begin() + pos + 1, vin.end());
           
           TreeNode* left_tree = reConstructBinaryTree(left_pre, left_vin);
           TreeNode* right_tree = reConstructBinaryTree(right_pre, right_vin);
           TreeNode* root = new TreeNode(root_value);
           root->left = left_tree;
           root->right = right_tree;
           
           return root;
       }
   };
   ```

5. 用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

   ```
   class Solution
   {
   public:
       void push(int node) {
           stack1.push(node);
       }

       int pop() {
           if(stack2.empty()){
               while(!stack1.empty()){
                   stack2.push(stack1.top());
                   stack1.pop();
               }
           }
           int ret_value = -1;
           if (!stack2.empty()){
               ret_value = stack2.top();
               stack2.pop();
           }
           
           return ret_value;
       }

   private:
       stack<int> stack1;
       stack<int> stack2;
   };
   ```

6. 把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。 输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。 例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。 NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。

   ```
   class Solution {
   public:
       int minNumberInRotateArray(vector<int> rotateArray) {
           int arr_size = rotateArray.size();
           if (arr_size == 0){
               return 0;
           }
           
           if (arr_size == 1){
               return rotateArray[0];
           }
           
           int low = 0;
           int high = arr_size - 1;
           
           if (rotateArray[low] < rotateArray[high]){
               return rotateArray[low];
           }
           
           while(low < high - 1){
               int mid = (low + high) / 2;
               if (rotateArray[mid] == rotateArray[low] && rotateArray[mid] == rotateArray[high]){
                   int min_num = INT_MAX;
                   for(int i = low ; i <= high; i++){
                       if (min_num > rotateArray[i]){
                           min_num = rotateArray[i];
                       }
                   }
                   return min_num;
               }
               
               if (rotateArray[mid] >= rotateArray[low]){
                   low = mid;
               }else{
                   high = mid;
               }
           }
           
           return rotateArray[high];
       }
   };
   ```

7. 大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项。n <= 39

   ```
   class Solution {
   public:
       int Fibonacci(int n) {
           
           if (n == 0){
               return 0;
           }
           if (n == 1){
               return 1;
           }
           if (n == 2){
               return 1;
           }
           
           int n_1 = 1;
           int n_2 = 1;
           for (int i = 3; i <= n; i++){
               int tmp = n_2;
               n_2 = n_1 + n_2;
               n_1 = tmp;
           }
           
           return n_2;
       }
   };
   ```

8. 一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法.

   ```
   class Solution {
   public:
       int jumpFloor(int number) {
           if (number == 0){
               return 1;
           }
           if (number == 1){
               return 1;
           }

           int n_0 = 1;
           int n_1 = 1;
           for (int i = 2; i <= number; i++){
               int tmp = n_1;
               n_1 = n_0 + n_1;
               n_0 = tmp;
           }

           return n_1;
       }
   };
   ```

9. 一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法.

   ```
   class Solution {
   public:
       int jumpFloorII(int number) {
           vector<int> dp(number + 1, 0);
           dp[1] = 1;
           for (int i = 2 ; i <= number; i++){
               int sum = 0;
               for (int j = 1 ; j < i ;j++){
                   sum += dp[j];
               }
               dp[i] = sum + 1;
           }

           return dp[number];
       }
   };
   ```

10. 我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法

  ```
  class Solution {
  public:
      int rectCover(int number) {
          if (number == 0){
              return 0;
          }

          if (number == 1){
              return 1;
          }

          if (number == 2){
              return 2;
          }

          int num_1 = 1;
          int num_2 = 2;

          for (int i = 3; i <= number;i++){
              int tmp = num_2;
              num_2 = num_1 + num_2;
              num_1 = tmp;
          }

          return num_2;
      }
  };
  ```

11. 输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示.

    ```
    class Solution {
    public:
         int  NumberOf1(int n) {
            int cnt = 0;
            for (int i = 0; i < 32 ; i++){
                // cout << n << " " << (int(n & 1) == 1) << endl;
                if (int(n & 1) == 1){
                    cnt++;
                }
                n = n >> 1;
            }
            return cnt;
         }
    };
    ```

12. 给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

    ```
    class Solution {
    public:
        double Power(double base, int exponent) {
            int flag = true;
            if (exponent < 0){
                flag = false;
            }
            
            exponent = abs(exponent);
            if (exponent == 0){
                return 1;
            }
            if (exponent == 1){
                return base;
            }
            
            if (exponent % 2 == 1){
                if (flag){
                    return Power(base, exponent / 2) * base * Power(base, exponent / 2);
                }else{
                    return 1. / (Power(base, exponent / 2) * base * Power(base, exponent / 2));
                }
            }else{
                if (flag){
                    return Power(base, exponent / 2) * Power(base, exponent / 2);
                }else{
                    return 1. / (Power(base, exponent / 2) * Power(base, exponent / 2));
                }
            }
        }
    };
    ```

13. 输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

    ```
    class Solution {
    public:
        void reOrderArray(vector<int> &nums) {
            int nums_size = nums.size();
            int low = 0;
            int high = nums_size - 1;
            while(low < nums_size){
                while(low < nums_size && nums[low] % 2 == 0){
                    low++;
                }

                if (low < nums_size){
                    int pos = low - 1;
                    int cur_num = nums[low];
                    while(pos >= 0 && nums[pos] % 2 == 0){
                        nums[pos + 1] = nums[pos];
                        pos--;
                    }
                    nums[pos + 1] = cur_num;
                    low++;
                }
            }
            
        }
    };
    ```

14. 输入一个链表，输出该链表中倒数第k个结点

    ```
    /*
    struct ListNode {
    	int val;
    	struct ListNode *next;
    	ListNode(int x) :
    			val(x), next(NULL) {
    	}
    };*/
    class Solution {
    public:
        ListNode* FindKthToTail(ListNode* pListHead, unsigned int k) {
            if (pListHead == NULL){
                return NULL;
            }
            
            ListNode* fast = pListHead;
            ListNode* slow = pListHead;
            
            int i = 0;
            for(; i < k && fast != NULL; i++){
                fast = fast->next;
            }
            
            if (fast == NULL && i < k){
                return NULL;
            }
            
            while(fast != NULL){
                slow = slow->next;
                fast = fast->next;
            }
            
            return slow;
        }
    };
    ```

15. 输入一个链表，反转链表后，输出链表的所有元素。

    ```
    /*
    struct ListNode {
    	int val;
    	struct ListNode *next;
    	ListNode(int x) :
    			val(x), next(NULL) {
    	}
    };*/
    class Solution {
    public:
        ListNode* ReverseList(ListNode* pHead) {
            ListNode* pre = NULL;
            ListNode* p_node = pHead;
            while(p_node != NULL){
                ListNode* tmp = p_node->next;
                p_node->next = pre;
                pre = p_node;
                p_node = tmp;
            }
            return pre;
        }
    };
    ```

16. 输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则.

    ```
    /*
    struct ListNode {
    	int val;
    	struct ListNode *next;
    	ListNode(int x) :
    			val(x), next(NULL) {
    	}
    };*/
    class Solution {
    public:
        ListNode* Merge(ListNode* pHead1, ListNode* pHead2)
        {
            ListNode* dummy = new ListNode(-1);
            ListNode* p_node_1 = pHead1;
            ListNode* p_node_2 = pHead2;
            ListNode* p_merge_node = NULL;
            
            while(p_node_1 != NULL && p_node_2 != NULL){
                if (p_node_1->val < p_node_2->val){
                    if (dummy->next == NULL){
                        dummy->next = p_node_1;
                        p_merge_node = p_node_1;
                    }else{
                        p_merge_node->next = p_node_1;
                        p_merge_node = p_merge_node->next;
                    }
                    p_node_1 = p_node_1->next;
                }else{
                    if (dummy->next == NULL){
                        dummy->next = p_node_2;
                        p_merge_node = p_node_2;
                    }else{
                        p_merge_node->next = p_node_2;
                        p_merge_node = p_merge_node->next;
                    }
                    p_node_2 = p_node_2->next;
                }
            }
            
            if (p_node_1 != NULL){
                if (dummy->next == NULL){
                    dummy->next = p_node_1;
                    p_merge_node = p_node_1;
                }else{
                    p_merge_node->next = p_node_1;
                }
            }
            
            if (p_node_2 != NULL){
                if (dummy->next == NULL){
                    dummy->next = p_node_2;
                    p_merge_node = p_node_2;
                }else{
                    p_merge_node->next = p_node_2;
                }
            }
            
            return dummy->next;
        }
    };
    ```

17. 输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）

18. 操作给定的二叉树，将其变换为源二叉树的镜像。

19. 输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.

    ```
    class Solution {
    public:
        vector<int> printMatrix(vector<vector<int> > matrix) {
            vector<int> results;
            if (matrix.size() == 0 || matrix[0].size() == 0){
                return results;
            }
            
            int m = matrix.size();
            int n = matrix[0].size();
            int limits = min((n - 1) / 2, (m - 1) / 2);
            
            for(int i = 0 ; i <= limits; i++){
                int pos_x = i, pos_y = i;
                if (i == m - 1 - i){
                    for(; pos_y < n - i; pos_y++){
                        results.push_back(matrix[i][pos_y]);
                    }
                }else if (i == n - 1 - i){
                    for(; pos_x < m - i; pos_x++){
                        results.push_back(matrix[pos_x][i]);
                    }
                }else{
                    while(pos_y < n - 1 - i){
                        results.push_back(matrix[pos_x][pos_y++]);
                    }
                    
                    while(pos_x < m - 1 - i){
                        results.push_back(matrix[pos_x++][pos_y]);
                    }
                    
                    while(pos_y > i){
                        results.push_back(matrix[pos_x][pos_y--]);
                    }
                    
                    while(pos_x > i){
                        results.push_back(matrix[pos_x--][pos_y]);
                    }
                }
            }
            
            return results;
        }
    };
    ```

20.  定义栈的数据结构，请在该类型中实现一个能够得到栈最小元素的min函数

    ```
    class Solution {
    public:
        stack<int> min_stack;
        stack<int> data_stack;
        
        void push(int value) {
            if(data_stack.empty()){
                data_stack.push(value);
                min_stack.push(value);
            }else{
                int min_value = min_stack.top();
                if (min_value > value){
                    min_value = value;
                }
                data_stack.push(value);
                min_stack.push(min_value);
            }
        }
        void pop() {
            if(data_stack.empty()){
                // throw exception("the stack is empty");
            }else{
                data_stack.pop();
                min_stack.pop();
            }
        }
        
        int top() {
            if (data_stack.empty()){
                // throw exception("the stack is empty");
                return -1;
            }else{
                return data_stack.top();
            }
        }
        
        int min() {
            if(min_stack.empty()){
                // throw exception("the stack is empty");
                return -1;
            }else{
                return min_stack.top();
            }
        }
    };
    ```

21. 输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

    ```
    class Solution {
    public:
        bool IsPopOrder(vector<int> pushV,vector<int> popV) {
            int n = pushV.size();
            stack<int> data_stack;
            int pos_v = 0;
            for(int i = 0 ; i < n ; i++){
                // 负责构建栈
                if (data_stack.empty()){
                    while(pos_v < n && pushV[pos_v] != popV[i]){
                        data_stack.push(pushV[pos_v++]);
                    }

                    if (pos_v == n && data_stack.empty()){
                        return false;
                    }
                    if(pushV[pos_v] == popV[i]){
                        data_stack.push(pushV[pos_v++]);
                    }

                }else{
                    int top_value = data_stack.top();
                    if (top_value != popV[i]){
                        while(pos_v < n && pushV[pos_v] != popV[i]){
                            data_stack.push(pushV[pos_v++]);
                        }
                        if (pos_v == n && data_stack.empty()){
                            return false;
                        }
                        if(pushV[pos_v] == popV[i]){
                            data_stack.push(pushV[pos_v++]);
                        }
                    }
                }

    //            stack<int> tmp = data_stack;
    //            while(!tmp.empty()){
    //                cout << tmp.top() << " ";
    //                tmp.pop();
    //            }
    //            cout << endl;

                // 负责查看顶部与弹出序列是否相等
                if (data_stack.empty()){
                    return false;
                }else{
                    int top_value = data_stack.top();
                    if (top_value == popV[i]){
                        data_stack.pop();
                    }else{
                        return false;
                    }
                }
            }

            return true;
        }
    };
    ```

22. 从上往下打印出二叉树的每个节点，同层节点从左至右打印

    ```
    /*
    struct TreeNode {
    	int val;
    	struct TreeNode *left;
    	struct TreeNode *right;
    	TreeNode(int x) :
    			val(x), left(NULL), right(NULL) {
    	}
    };*/
    class Solution {
    public:
        vector<int> PrintFromTopToBottom(TreeNode* root) {
            vector<int> results;
            if (root == NULL){
                return results;
            }
            
            queue<TreeNode*> queue_1, queue_2;
            queue_1.push(root);
            
            while(!queue_1.empty() || !queue_2.empty()){
                while(!queue_1.empty()){
                    TreeNode* tmp = queue_1.front();
                    queue_1.pop();
                    results.push_back(tmp->val);
                    if(tmp->left != NULL){
                        queue_2.push(tmp->left);
                    }
                    if(tmp->right != NULL){
                        queue_2.push(tmp->right);
                    }
                }
                
                while(!queue_2.empty()){
                    TreeNode* tmp = queue_2.front();
                    queue_2.pop();
                    results.push_back(tmp->val);
                    if (tmp->left != NULL){
                        queue_1.push(tmp->left);
                    }
                    if (tmp->right != NULL){
                        queue_1.push(tmp->right);
                    }
                }
            }
            
            return results;
        }
    };
    ```

23. 输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出Yes,否则输出No。假设输入的数组的任意两个数字都互不相同。

    ```
    class Solution {
    public:
        bool VerifySquenceOfBST(vector<int> sequence) {
            int sequence_size = sequence.size();
            if (sequence_size == 0){
                return false;
            }
            
            int root_num = sequence[sequence_size - 1];
            int pos = 0;
            while(pos < sequence_size - 1 && sequence[pos] < root_num){
                pos++;
            }

            while(pos < sequence_size - 1){
                if (sequence[pos++] < root_num){
                    return false;
                }
            }
            
            vector<int> left_sequence = vector<int>(sequence.begin(), sequence.begin() + pos);
            vector<int> right_sequence = vector<int>(sequence.begin() + pos, sequence.end() - 1);
            
            bool left_flag = true;
            if (pos > 0){
                left_flag = VerifySquenceOfBST(left_sequence);
            }
            bool right_flag = true;
            if (pos < sequence_size - 1){
                right_flag = VerifySquenceOfBST(right_sequence);
            }
            return (left_flag && right_flag);
        }
    };
    ```

24. 输入一颗二叉树和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。

    ```
    /*
    struct TreeNode {
    	int val;
    	struct TreeNode *left;
    	struct TreeNode *right;
    	TreeNode(int x) :
    			val(x), left(NULL), right(NULL) {
    	}
    };*/
    class Solution {
    public:
        vector<vector<int> > FindPath(TreeNode* root,int expectNumber) {
            vector<vector<int>> results;
            if (root == NULL){
                return results;
            }
            vector<int> out;
            dfs(root, expectNumber, results, out);
            return results;
        }
        
        void dfs(TreeNode* root, int expectNumber, vector<vector<int>>& results, vector<int>& out){
            if (root->left == NULL && root->right == NULL){
                if (expectNumber - root->val == 0){
                    out.push_back(root->val);
                    results.push_back(out);
                    out.pop_back();
                }
                return ;
            }
            
            out.push_back(root->val);
            if (root->left != NULL){
                dfs(root->left, expectNumber - root->val, results, out);
            }
            
            if (root->right != NULL){
                dfs(root->right, expectNumber - root->val, results, out);
            }
            out.pop_back();
        }
    };
    ```

25. 输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针指向任意一个节点），返回结果为复制后复杂链表的head。（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）

    ```

    ```

26. 输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。

    ```

    ```

27. 输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串abc,则打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。

    ```
    class Solution {
    public:
        vector<string> Permutation(string str) {
            int str_size = str.size();
            set<string> results_set;
            vector<string> results;
            string out = "";
            
            if (str_size == 0){
                return results; 
            }
            vector<bool> visited(str_size, false);
            
            dfs(str, visited, out, results_set);
            
            for(string str_tmp : results_set){
                results.push_back(str_tmp);
            }
            
            return results;
        }
        
        void dfs(string str, vector<bool>& visited, string out, set<string>& results_set){
            if (str.size() == out.size()){
                results_set.insert(out);
                return ;
            }
            
            for (int i = 0 ; i < str.size(); i++){
                if(!visited[i]){
                    visited[i] = true;
                    out += str[i];
                    
                    dfs(str, visited, out, results_set);
                    
                    out = out.substr(0, out.size() - 1);
                    visited[i] = false;
                }
            }
        }
    };
    ```

28. 数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。

    ```
    class Solution {
    public:
        int MoreThanHalfNum_Solution(vector<int> numbers) {
            int nums_size = numbers.size();
            
            if (nums_size == 0){
                return 0;
            }
            if (nums_size == 1){
                return numbers[0];
            }
            
            int low = 0;
            int high = nums_size - 1;
            int target = (low + high) / 2 + 1;
            int result = 0;
            
            search_kth_num(numbers, low, high, target, result);
            return result;
        }

        void search_kth_num(vector<int>& numbers, int low, int high, int target, int& result){
            if (low < high){
                int pivot = numbers[low];
                int left = low;
                int right = high;
                while(left < right){
                    while(left < right && numbers[right] > pivot){
                        right--;
                    }
                    swap(numbers[left], numbers[right]);
    				
    				// 这里这个<=很重要
                    while(left < right && numbers[left] <= pivot){
                        left++;
                    }
                    swap(numbers[right], numbers[left]);
                }
                numbers[left] = pivot;

                if (left == target){
                    result = numbers[left];
                }else if (left < target){
                    search_kth_num(numbers, left + 1, high, target, result);
                }else{
                    search_kth_num(numbers, low, left - 1, target, result);
                }
            }
        }
    };
    ```

29. 输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

    ```
    class Solution {
    public:
        vector<int> GetLeastNumbers_Solution(vector<int> input, int k) {
            vector<int> result;
            int input_size = input.size();
            if (input_size == 0){
                return result;
            }
            
            if (input_size - k < 0){
                return result;
            }
            
            int heap_size = input_size;
            int limit = max(input_size - k, 0);
            min_heap(input, heap_size);
            for (int i = input_size - 1 ; i >= limit ; i--){
                result.push_back(input[0]);
                swap(input[0], input[i]);
                min_heapify(input, 0 , --heap_size);
            }

            return result;
        }

        void min_heapify(vector<int>& input, int i, int heap_size){
            int left = 2 * (i + 1) - 1;
            int right = 2 * (i + 1) + 1 - 1;

            int smallest = i;
            if (left < heap_size && input[smallest] > input[left]){
                smallest = left;
            }

            if (right < heap_size && input[smallest] > input[right]){
                smallest = right;
            }
            if (smallest != i){
                swap(input[i], input[smallest]);
                min_heapify(input, smallest, heap_size);
            }
        }

        void min_heap(vector<int>& input, int heapsize){
            for (int i = heapsize / 2 - 1; i >= 0; i--){
                min_heapify(input, i, heapsize);
            }
        }
    };
    ```

30. HZ偶尔会拿些专业问题来忽悠那些非计算机专业的同学。今天测试组开完会后,他又发话了:在古老的一维模式识别中,常常需要计算连续子向量的最大和,当向量全为正数的时候,问题很好解决。但是,如果向量中包含负数,是否应该包含某个负数,并期望旁边的正数会弥补它呢？例如:{6,-3,-2,7,-15,1,2,2},连续子向量的最大和为8(从第0个开始,到第3个为止)。你会不会被他忽悠住？(子向量的长度至少是1)

    ```
    class Solution {
    public:
        int FindGreatestSumOfSubArray(vector<int> array) {
            int result = array[0];
            int sum = array[0];
            for (int i = 1 ; i < array.size(); i++){
                if (array[i] > sum + array[i]){
                    sum = array[i];
                }else{
                    sum += array[i];
                }
                result = max(sum, result);
            }
            
            return result;
        }
    };
    ```

31. 求出1~13的整数中1出现的次数,并算出100~1300的整数中1出现的次数？为此他特别数了一下1~13中包含1的数字有1、10、11、12、13因此共出现6次,但是对于后面问题他就没辙了。ACMer希望你们帮帮他,并把问题更加普遍化,可以很快的求出任意非负整数区间中1出现的次数。

32. 输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。例如输入数组{3，32，321}，则打印出这三个数字能排成的最小数字为321323。

    ```
    class Solution {
    public:
        string PrintMinNumber(vector<int> numbers) {
            sort(numbers.begin(), numbers.end(), [](int a, int b){
                ostringstream a_tmp, b_tmp;
                a_tmp << a;
                string a_str = a_tmp.str();

                b_tmp << b;
                string b_str = b_tmp.str();

                stringstream b_all(b_str + a_str), a_all(a_str + b_str);
                int a_all_tmp, b_all_tmp;
                a_all >> a_all_tmp;
                b_all >> b_all_tmp;

                return a_all_tmp < b_all_tmp;
            });

            ostringstream result;
            for(int num : numbers){
                result << num;
            }
            return result.str();
        }
    };
    ```

33. 把只包含因子2、3和5的数称作丑数（Ugly Number）。例如6、8都是丑数，但14不是，因为它包含因子7。 习惯上我们把1当做是第一个丑数。求按从小到大的顺序的第N个丑数。

    ```
    class Solution {
    public:
        int GetUglyNumber_Solution(int index) {
            if (index == 0){
                return 0;
            }
            
            vector<int> dp(index, 0);
            dp[0] = 1;
            for (int i = 1; i < index; i++){
                int two_num, three_num, five_num;
                for(int j = 0 ; j < i ; j++){
                    two_num = dp[j] * 2;
                    if (two_num > dp[i - 1]){
                        break;
                    }
                }
                
                for(int j = 0 ; j < i ; j++){
                    three_num = dp[j] * 3;
                    if (three_num > dp[i - 1]){
                        break;
                    }
                }
                
                for(int j = 0 ; j < i ; j++){
                    five_num = dp[j] * 5;
                    if (five_num > dp[i - 1]){
                        break;
                    }
                }
                
                int min_num = min(two_num, three_num);
                min_num = min(min_num, five_num);
                dp[i] = min_num;
            }
            
            return dp[index - 1];
        }
    };
    ```

34. 在一个字符串(1<=字符串长度<=10000，全部由字母组成)中找到第一个只出现一次的字符,并返回它的位置

    ```
    class Solution {
    public:
        int FirstNotRepeatingChar(string str) {
            vector<int> cnt(256, 0);
            vector<int> pos(256, -1);
            
            for(int i = 0 ; i < str.size(); i++){
                char ch = str[i];
                if (cnt[int(ch)] == 0){
                    cnt[int(ch)] += 1;
                    pos[int(ch)] = i;
                }else{
                    cnt[int(ch)] += 1;
                    pos[int(ch)] = -1;
                }
            }
            
            int min_pos = INT_MAX;
            for(int i = 0; i < 256; i++){
                if (pos[i] != -1){
                    if (pos[i] < min_pos){
                        min_pos = pos[i];
                    }
                }
            }
            if (min_pos == INT_MAX){
                return -1;
            }
            return min_pos;
        }
    };
    ```

35. 在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组,求出这个数组中的逆序对的总数P。并将P对1000000007取模的结果输出。 即输出P%1000000007

    ```

    ```

36. 输入两个链表，找出它们的第一个公共结点。

    ```
    /*
    struct ListNode {
    	int val;
    	struct ListNode *next;
    	ListNode(int x) :
    			val(x), next(NULL) {
    	}
    };*/
    class Solution {
    public:
        ListNode* FindFirstCommonNode( ListNode* pHead1, ListNode* pHead2) {
            if (pHead1 == NULL ||pHead2 == NULL){
                return NULL;
            }
            
            int p_head1_len = 0, p_head2_len = 0;
            ListNode* p_head1_node = pHead1;
            ListNode* p_head2_node = pHead2;
            
            while(p_head1_node != NULL){
                p_head1_node = p_head1_node->next;
                p_head1_len += 1;
            }
            
            while(p_head2_node != NULL){
                p_head2_node = p_head2_node->next;
                p_head2_len += 1;
            }
            
            int diff = abs(p_head1_len - p_head2_len);
            p_head1_node = pHead1;
            p_head2_node = pHead2;
            if(p_head1_len > p_head2_len){
                for(int i = 0; i < diff; i++){
                    p_head1_node = p_head1_node->next;
                }
            }else{
                for(int i = 0 ; i < diff; i++){
                    p_head2_node = p_head2_node->next;
                }
            }
            
            while(p_head1_node != p_head2_node){
                p_head1_node = p_head1_node->next;
                p_head2_node = p_head2_node->next;
            }
            
            return p_head1_node;
        }
    };
    ```

37. 统计一个数字在排序数组中出现的次数。

    ```
    class Solution {
    public:
        int GetNumberOfK(vector<int> data ,int k) {
            int data_size = data.size();
            if(data_size == 0){
                return 0;
            }

            int first_k_pos = getFirstKPos(data, k);
            int last_k_pos = getLastKPos(data, k);

            if (first_k_pos == -1 || last_k_pos == -1){
                return 0;
            }else{
                return last_k_pos - first_k_pos + 1;
            }
        }

        int getFirstKPos(vector<int> data, int k){
            int data_size = data.size();
            int low = 0;
            int high = data_size - 1;

            while(low <= high){
                int mid = (low + high) / 2;
                if (data[mid] == k){
                    if (mid - 1 >= 0 && data[mid - 1] == k){
                        high = mid - 1;
                    }else{
                        return mid;
                    }
                }else if (data[mid] < k){
                    low = mid + 1;
                }else{
                    high = mid - 1;
                }
            }

            return -1;
        }

        int getLastKPos(vector<int> data, int k){
            int data_size = data.size();
            int low = 0;
            int high = data_size - 1;

            while(low <= high){
                int mid = (low + high) / 2;
                if (data[mid] == k){
                    if (mid + 1 < data_size && data[mid + 1] == k){
                        low = mid + 1;
                    }else{
                        return mid;
                    }
                }else if (data[mid] < k){
                    low = mid + 1;
                }else{
                    high = mid - 1;
                }
            }

            return -1;
        }
    };
    ```

38. 输入一棵二叉树，求该树的深度。从根结点到叶结点依次经过的结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度。

    ```
    /*
    struct TreeNode {
    	int val;
    	struct TreeNode *left;
    	struct TreeNode *right;
    	TreeNode(int x) :
    			val(x), left(NULL), right(NULL) {
    	}
    };*/
    class Solution {
    public:
        int TreeDepth(TreeNode* pRoot)
        {
            if (pRoot == NULL){
                return 0;
            }
            
            return max(TreeDepth(pRoot->left), TreeDepth(pRoot->right)) + 1;
        }
    };
    ```

39. 输入一棵二叉树，判断该二叉树是否是平衡二叉树。

    ```
    class Solution {
    public:
        bool IsBalanced_Solution(TreeNode* pRoot) {
            int depth = 0;
            return IsBalanced_Solution(pRoot, depth);
        }
        
        bool IsBalanced_Solution(TreeNode* root, int& depth){
            if (root == NULL){
                depth = 0;
                return true;
            }
            
            int left = 0, right = 0;
            if (IsBalanced_Solution(root->left, left) && IsBalanced_Solution(root->right, right)){
                depth = 1 + max(left, right);
                if (abs(left - right) <= 1){
                    return true;
                }
            }
            
            return false;
        }
        
    };
    ```

40. 一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字

    ```
    #ifndef FINDNUMSAPPEARONCE_H_INCLUDED
    #define FINDNUMSAPPEARONCE_H_INCLUDED

    #include <vector>

    #endif // FINDNUMSAPPEARONCE_H_INCLUDED

    using namespace std;

    class Solution {
    public:
        void FindNumsAppearOnce(vector<int> data,int* num1,int *num2) {
            //对数组全体做一次异或，得到第一个为1的位置
            int tmp = 0;
            for(int num : data){
                tmp ^= num;
            }

            int flag = 1;
            while(int(tmp & flag) == 0){
                flag = flag << 1;
            }

            *num1 = 0;
            *num2 = 0;
            for(int num : data){
                if (int(num & flag) > 0){
                    *num1 ^= num;
                }else{
                    *num2 ^= num;
                }
            }
        }
    };
    ```

41. 小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? Good Luck!

    输出所有和为S的连续正数序列。序列内按照从小至大的顺序，序列间按照开始数字从小到大的顺序

    ```
    class Solution {
    public:
        vector<vector<int> > FindContinuousSequence(int sum) {
            vector<vector<int> > results;
            
            if (sum < 3){
                return results;
            }
            
            int small = 1;
            int big = 2;
            int cur_sum = small + big;
            int mid = (sum + 1) / 2;
            while(small < mid){
                if (cur_sum == sum){
                    vector<int> solution;
                    for(int i = small; i <= big; i++){
                        solution.push_back(i);
                    }
                    results.push_back(solution);
                    
                    big++;
                    cur_sum += big;
                }else if (cur_sum < sum){
                    big++;
                    cur_sum += big;
                }else{
                    cur_sum -= small;
                    small++;
                }
            }
            
            return results;
        }
    };
    ```

42. 输入一个递增排序的数组和一个数字S，在数组中查找两个数，是的他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。

    ```
    class Solution {
    public:
        vector<int> FindNumbersWithSum(vector<int> array,int sum) {
            vector<int> results;
            int array_size = array.size();
            
            if (array_size < 2){
                return results;
            }
            
            int low = 0;
            int high = array_size - 1;
            
            while(low < high){
                if (array[low] + array[high] == sum){
                    if (results.size() == 0){
                        results.push_back(array[low]);
                        results.push_back(array[high]);
                    }else{
                        if (results[0] * results[1] > array[low] * array[high]){
                            results.pop_back();
                            results.pop_back();
                            results.push_back(array[low]);
                            results.push_back(array[high]);
                        }
                    }
                    low++;
                }else if (array[low] + array[high] < sum){
                    low++;
                }else{
                    high--;
                }
            }
            
            return results;
            
        }
    };
    ```

43. 汇编语言中有一种移位指令叫做循环左移（ROL），现在有个简单的任务，就是用字符串模拟这个指令的运算结果。对于一个给定的字符序列S，请你把其循环左移K位后的序列输出。例如，字符序列S=”abcXYZdef”,要求输出循环左移3位后的结果，即“XYZdefabc”。是不是很简单？OK，搞定它！

    ```
    class Solution {
    public:
        string LeftRotateString(string str, int n) {
            
            if (str.size() == 0){
                return str;
            }
            
            n = n % str.size();
            if (n == 0){
                return str;
            }
            
            int first_start = 0;
            int first_end = n - 1;
            
            int second_start = n;
            int second_end = str.size() - 1;
            
            Reverse(str, first_start, first_end);
            Reverse(str, second_start, second_end);
            Reverse(str, first_start, second_end);
            
            return str;
        }
        
        void Reverse(string& str, int low, int high){
            int length = high - low + 1;
            for (int i = 0 ; i <= (length - 1) / 2; i++){
                swap(str[low + i], str[high - i]);
            }
        }
    };
    ```

44. 牛客最近来了一个新员工Fish，每天早晨总是会拿着一本英文杂志，写些句子在本子上。同事Cat对Fish写的内容颇感兴趣，有一天他向Fish借来翻看，但却读不懂它的意思。例如，“student. a am I”。后来才意识到，这家伙原来把句子单词的顺序翻转了，正确的句子应该是“I am a student.”。Cat对一一的翻转这些单词顺序可不在行，你能帮助他么？

45. LL今天心情特别好,因为他去买了一副扑克牌,发现里面居然有2个大王,2个小王(一副牌原本是54张^_^)...他随机从中抽出了5张牌,想测测自己的手气,看看能不能抽到顺子,如果抽到的话,他决定去买体育彩票,嘿嘿！！“红心A,黑桃3,小王,大王,方片5”,“Oh My God!”不是顺子.....LL不高兴了,他想了想,决定大\小 王可以看成任何数字,并且A看作1,J为11,Q为12,K为13。上面的5张牌就可以变成“1,2,3,4,5”(大小王分别看作2和4),“So Lucky!”。LL决定去买体育彩票啦。 现在,要求你使用这幅牌模拟上面的过程,然后告诉我们LL的运气如何。为了方便起见,你可以认为大小王是0。

46. 每年六一儿童节,牛客都会准备一些小礼物去看望孤儿院的小朋友,今年亦是如此。HF作为牛客的资深元老,自然也准备了一些小游戏。其中,有个游戏是这样的:首先,让小朋友们围成一个大圈。然后,他随机指定一个数m,让编号为0的小朋友开始报数。每次喊到m-1的那个小朋友要出列唱首歌,然后可以在礼品箱中任意的挑选礼物,并且不再回到圈中,从他的下一个小朋友开始,继续0...m-1报数....这样下去....直到剩下最后一个小朋友,可以不用表演,并且拿到牛客名贵的“名侦探柯南”典藏版(名额有限哦!!^_^)。请你试着想下,哪个小朋友会得到这份礼品呢？(注：小朋友的编号是从0到n-1)

47. 求1+2+3+...+n，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

48. 写一个函数，求两个整数之和，要求在函数体内不得使用+、-、*、/四则运算符号。

49. 将一个字符串转换成一个整数，要求不能使用字符串转换整数的库函数。 数值为0或者字符串不是一个合法的数值则返回0

50. 在一个长度为n的数组里的所有数字都在0到n-1的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。 例如，如果输入长度为7的数组{2,3,1,0,2,5,3}，那么对应的输出是第一个重复的数字2。

51. 给定一个数组A[0,1,...,n-1],请构建一个数组B[0,1,...,n-1],其中B中的元素B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]。不能使用除法。

52. 请实现一个函数用来匹配包括'.'和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（包含0次）。 在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但是与"aa.a"和"ab*a"均不匹配

53. 请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100","5e2","-123","3.1416"和"-1E-16"都表示数值。 但是"12e","1a3.14","1.2.3","+-5"和"12e+4.3"都不是。

54. 请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符"go"时，第一个只出现一次的字符是"g"。当从该字符流中读出前六个字符“google"时，第一个只出现一次的字符是"l"。

55. 一个链表中包含环，请找出该链表的环的入口结点。

56. 在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。 例如，链表1->2->3->3->4->4->5 处理后为 1->2->5

57. 给定一个二叉树和其中的一个结点，请找出中序遍历顺序的下一个结点并且返回。注意，树中的结点不仅包含左右子结点，同时包含指向父结点的指针。

58. 请实现一个函数，用来判断一颗二叉树是不是对称的。注意，如果一个二叉树同此二叉树的镜像是同样的，定义其为对称的。

59. 请实现一个函数按照之字形打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右至左的顺序打印，第三行按照从左到右的顺序打印，其他行以此类推。

60. 从上到下按层打印二叉树，同一层结点从左至右输出。每一层输出一行。

61. 请实现两个函数，分别用来序列化和反序列化二叉树

62. 给定一颗二叉搜索树，请找出其中的第k大的结点。例如， 5 / \ 3 7 /\ /\ 2 4 6 8 中，按结点数值大小顺序第三个结点的值为4。

63. 如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

64. 给定一个数组和滑动窗口的大小，找出所有滑动窗口里数值的最大值。例如，如果输入数组{2,3,4,2,6,2,5,1}及滑动窗口的大小3，那么一共存在6个滑动窗口，他们的最大值分别为{4,4,6,6,6,5}； 针对数组{2,3,4,2,6,2,5,1}的滑动窗口有以下6个： {[2,3,4],2,6,2,5,1}， {2,[3,4,2],6,2,5,1}， {2,3,[4,2,6],2,5,1}， {2,3,4,[2,6,2],5,1}， {2,3,4,2,[6,2,5],1}， {2,3,4,2,6,[2,5,1]}。

65. 请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一个格子开始，每一步可以在矩阵中向左，向右，向上，向下移动一个格子。如果一条路径经过了矩阵中的某一个格子，则该路径不能再进入该格子。 例如 a b c e s f c s a d e e 矩阵中包含一条字符串"bcced"的路径，但是矩阵中不包含"abcb"路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入该格子。

66. 地上有一个m行和n列的方格。一个机器人从坐标0,0的格子开始移动，每一次只能向左，右，上，下四个方向移动一格，但是不能进入行坐标和列坐标的数位之和大于k的格子。 例如，当k为18时，机器人能够进入方格（35,37），因为3+5+3+7 = 18。但是，它不能进入方格（35,38），因为3+5+3+8 = 19。请问该机器人能够达到多少个格子？