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

21. 输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4，5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）