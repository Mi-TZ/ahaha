import java.util.*;

public class fdsAssignment1 {
    public static void main(String args[]) {
        // Without pointers

        // 1. Length
        String str1 = "Hello";
        int length = str1.length();
        System.out.println("Length: " + length);

        // 2. Copy
        String copy = new String(str1);
        System.out.println("Copy: " + copy);

        // 3. Concatenate
        String str2 = ",This is FDS assignment";
        String result = str1 + " " + str2;
        System.out.println("Concatenation: " + result);

        // 4. Compare
        boolean same = str1.equals(str2);
        System.out.println("Comparison: " + same);

        // 5. Reverse
        char[] charArray = str1.toCharArray();
        int start = 0;
        int end = charArray.length - 1;
        while (start < end) {
            char temp = charArray[start];
            charArray[start] = charArray[end];
            charArray[end] = temp;
            start++;
            end--;
        }
        String reverse = new String(charArray);
        System.out.println("Reversed String: " + reverse);
    }
}
