排序

- 希尔排序

  ```

  ```

- 插入排序

  ```
  void insert_sort(vector<int>& nums){
      for (int i = 1; i < nums.size(); i++){
          int cur_num = nums[i];
          int pos = i - 1;

          while(pos >= 0 && nums[pos] > cur_num){
              nums[pos + 1] = nums[pos];
              pos--;
          }

          nums[pos + 1] = cur_num;
      }
  }
  ```
