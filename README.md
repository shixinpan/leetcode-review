# leetcode-review

06/27
1. Given an array and find the second largest number, like an array[1,2,3,4,5,5], the second largest number is 4;

input: array[1,2,3,4,5,5]
output: 4


Way 1: set two variables, find the largest one and second largest one, return the second largest one; -->time complexity:O(n) space complexity:O(1)

public static int secondLargest(int[] nums) {
    int largest = Integer.MIN_VALUE;
    int secondLargest = Integer.MIN_VALUE;

    for (int num : nums) {
        if (num > largest) {
            secondLargest = largest;
            largest = num;
        } else if (num < largest && num > secondLargest) {
            secondLargest = num;
        }
    }

    return secondLargest;
}

way2: TreeSet will do the ordering and remove the duplicate number  -> time complexity: O(nlogn)/ sapce complexity:O(n) 
import java.util.TreeSet;

public class Main {
    public static int secondLargest(int[] nums) {
        TreeSet<Integer> set = new TreeSet<>();

        for (int num : nums) {
            set.add(num);
        }

        if (set.size() < 2) {
            throw new IllegalArgumentException("No second largest distinct number");
        }

        set.pollLast(); // 删除最大值
        return set.last(); // 剩下的最大值就是第二大
    }

    public static void main(String[] args) {
        int[] nums = {12, 3, 4, 5, 5};
        System.out.println(secondLargest(nums)); // 5
    }
}
