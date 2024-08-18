Next Permutation in Java
Here, on this page, we will discuss the program to find the next permutation in Java. We are Given a word and need to find the lexicographically greater permutation of it. For example, lexicographically next permutation of “acb” is “bac”

Java program to find Next Permutation
Find the longest non-increasing suffix and find the pivot.
If the suffix is the whole array, then there is no higher order permutation for the data.
Find the rightmost successor to the pivot.
Swap the successor and the pivot.
Reverse the suffix.
Run
import java.util.Arrays;
public
class Main {
    public
    static int[] swap(int data[], int left, int right) {
        // Swap the data
        int temp = data[left];
        data[left] = data[right];
        data[right] = temp;
        // Return the updated array
        return data;
    }
    public
    static int[] reverse(int data[], int left, int right) {
        // Reverse the sub-array
        while (left < right) {
            int temp = data[left];
            data[left++] = data[right];
            data[right--] = temp;
        }
        // Return the updated array
        return data;
    }
    public
    static boolean findNextPermutation(int data[]) {
        if (data.length <= 1) return false;        
        int last = data.length - 2;        
         while (last >= 0) {
            if (data[last] < data[last + 1]) {
                break;
            }
            last--;
        }
        if (last < 0) return false;        
        int nextGreater = data.length - 1;      
       // Find the rightmost successor to the pivot        
        for (int i = data.length - 1; i > last; i--) {
            if (data[i] > data[last]) {
                nextGreater = i;
                break;
            }
        }
        data = swap(data, nextGreater, last);
        data = reverse(data, last + 1, data.length - 1);
        return true;
    }

    // Driver Code
    public

    static void main(String args[]) {
        int data[] = {1, 2, 3, 7};
        if (!findNextPermutation(data))
            System.out.println("There is no higher" + " order permutation " +
                               "for the given data.");
        else {
            System.out.println(Arrays.toString(data));
        }
    }
}
Output :
[1, 2, 7, 3]
