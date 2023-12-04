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

----------------------------------
-----------------
--------------------------------------------------------------------
-----------------
--------------------------------------------------------------------
-----------------
----------------------------------

//simple transpose

public class fdsb2 {
    static class SparseMatrixElement {
        int row;
        int col;
        int value;

        public SparseMatrixElement(int row, int col, int value) {
            this.row = row;
            this.col = col;
            this.value = value;
        }
    }

    public static SparseMatrixElement[] transposeSparseMatrix(SparseMatrixElement[] matrix) {
       
        SparseMatrixElement[] transpose = new SparseMatrixElement[matrix.length];

        // Iterate over the original matrix and transpose it
        for (int i = 0; i < matrix.length; i++) {
            transpose[matrix[i].col] = new SparseMatrixElement(matrix[i].col, matrix[i].row, matrix[i].value);
        }

        // Return the transposed matrix
        return transpose;
    }

    public static void main(String[] args) {
        // Create a sparse matrix
        SparseMatrixElement[] matrix = new SparseMatrixElement[] {
            new SparseMatrixElement(0, 1, 2),
            new SparseMatrixElement(1, 2, 3),
            new SparseMatrixElement(2, 0, 4)
        };

        // Transpose the sparse matrix
        SparseMatrixElement[] transpose = transposeSparseMatrix(matrix);

        // Print the transposed sparse matrix
        System.out.println("The transpose of the sparse matrix is:");
        for (int i = 0; i < transpose.length; i++) {
            System.out.println(transpose[i].row + " " + transpose[i].col + " " + transpose[i].value);
        }
    }
}

----------------------------------
-----------------
----------------------------------
----------------------------------
-----------------
--------------------------------------------------------------------
-----------------
----------------------------------



//fast transpose


import java.util.ArrayList;

class SparseMatrix {
    int rows, cols;
    ArrayList<SparseElement> elements;

    public SparseMatrix(int rows, int cols) {
        this.rows = rows;
        this.cols = cols;
        this.elements = new ArrayList<>();
    }

    public void addElement(int row, int col, int value) {
        if (row >= 0 && row < rows && col >= 0 && col < cols) {
            elements.add(new SparseElement(row, col, value));
        } else {
            System.out.println("Invalid row or column index");
        }
    }

    public void fastTranspose() {
        // Initialize an array to store the number of non-zero elements in each column of the transpose
        int[] colCounts = new int[cols];
        
        // Count the number of non-zero elements in each column
        for (SparseElement element : elements) {
            colCounts[element.col]++;
        }
        
        // Compute the starting index for each column in the transpose
        int[] colStart = new int[cols];
        colStart[0] = 0;
        for (int i = 1; i < cols; i++) {
            colStart[i] = colStart[i - 1] + colCounts[i - 1];
        }
        
        // Create a new array to store the transposed elements
        SparseElement[] transposedElements = new SparseElement[elements.size()];
        
        // Populate the transposedElements array by rearranging the elements
        for (SparseElement element : elements) {
            int transposedIndex = colStart[element.col];
            transposedElements[transposedIndex] = new SparseElement(element.col, element.row, element.value);
            colStart[element.col]++;
        }
        
        // Update the elements list with the transposed elements
        elements.clear();
        for (SparseElement element : transposedElements) {
            elements.add(element);
        }
    }

    public void display() {
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                int value = 0;
                for (SparseElement element : elements) {
                    if (element.row == i && element.col == j) {
                        value = element.value;
                        break;
                    }
                }
                System.out.print(value + " ");
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        SparseMatrix matrix = new SparseMatrix(3, 3);
        matrix.addElement(0, 0, 1);
        matrix.addElement(0, 2, 2);
        matrix.addElement(1, 1, 3);
        matrix.addElement(2, 0, 4);
        matrix.addElement(2, 2, 5);

        System.out.println("Original Matrix:");
        matrix.display();

        matrix.fastTranspose();

        System.out.println("\nTransposed Matrix:");
        matrix.display();
    }
}

class SparseElement {
    int row, col, value;

    public SparseElement(int row, int col, int value) {
        this.row = row;
        this.col = col;
        this.value = value;
    }
}

----------------------------------
-----------------
----------------------------------
----------------------------------
-----------------
--------------------------------------------------------------------
-----------------
----------------------------------

//bubble sort

import java.util.*;


class bubblesort {
   public static void printArray(int arr[]) {
       for(int i=0; i<arr.length; i++) {
           System.out.print(arr[i]+" ");
       }
      
   }
    public static void main(String args[]) {
       int arr[] = {7, 8, 3, 1, 2};


       //bubble sort
       for(int i=0; i<arr.length-1; i++) {
           for(int j=0; j<arr.length-i-1; j++) {
               if(arr[j] > arr[j+1]) {
                   //swap
                   int temp = arr[j];
                   arr[j] = arr[j+1];
                   arr[j+1] = temp;
               }
           }
       }
     printArray(arr);
   }
}

----------------------------------
-----------------
----------------------------------
----------------------------------
-----------------
--------------------------------------------------------------------
-----------------
----------------------------------

//employee

//linked list


class Employee {
    int empId;
    String name;
    String position;
    double salary;
    Employee next;

    public Employee(int empId, String name, String position, double salary) {
        this.empId = empId;
        this.name = name;
        this.position = position;
        this.salary = salary;
        this.next = null;
    }
}

class EmployeeLinkedList {
    private Employee head;

    public void display() {
        Employee current = head;
        while (current != null) {
            System.out.println("Employee ID: " + current.empId + ", Name: " + current.name + ", Position: " + current.position + ", Salary: " + current.salary);
            current = current.next;
        }
    }

    public void insert(int empId, String name, String position, double salary) {
        Employee newEmployee = new Employee(empId, name, position, salary);
        newEmployee.next = head;
        head = newEmployee;
    }

    public Employee search(int empId) {
        Employee current = head;
        while (current != null) {
            if (current.empId == empId) {
                return current;
            }
            current = current.next;
        }
        return null;
    }

    public void delete(int empId) {
        if (head == null) {
            return;
        }
        if (head.empId == empId) {
            head = head.next;
            return;
        }
        Employee current = head;
        Employee prev = null;
        while (current != null && current.empId != empId) {
            prev = current;
            current = current.next;
        }
        if (current == null) {
            return;
        }
        prev.next = current.next;
    }

    public void modify(int empId, String newName, String newPosition, double newSalary) {
        Employee employee = search(empId);
        if (employee != null) {
            employee.name = newName;
            employee.position = newPosition;
            employee.salary = newSalary;
        }
    }
}

public class fdsa4 {
    public static void main(String[] args) {
        EmployeeLinkedList employeeList = new EmployeeLinkedList();

        employeeList.insert(612, "rahul", "HR", 1000000);
        employeeList.insert(613, "jannat", "manager", 500000);
        employeeList.insert(614, "shreya", "doctor", 4500000);

        System.out.println("Employees:");
        employeeList.display();

        Employee result = employeeList.search(102);
        if (result != null) {
            System.out.println("Employee is found: " + result.name);
        } else {
            System.out.println("Employee is not found");
        }

        employeeList.modify(613, "jannat", "Senior Manager", 550000);
        employeeList.delete(614);

        System.out.println("Modified Employees List:");
        employeeList.display();
    }
}

----------------------------------
-----------------
----------------------------------
----------------------------------
-----------------
--------------------------------------------------------------------
-----------------
----------------------------------

//stack
//stack using LL


import java.util.*;

class Node {
    int data;
    Node next;

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class Stack {
    private Node top;
    private int size;
    private int capacity;

    public Stack(int capacity) {
        this.top = null;
        this.size = 0;
        this.capacity = capacity;
    }

    public boolean isFull() {
        return size == capacity;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public void push(int data) {
        if (isFull()) {
            System.out.println("stack overflow");
            return;
        }

        Node newNode = new Node(data);
        newNode.next = top;
        top = newNode;
        size++;
    }

    public int pop() {
        if (isEmpty()) {
            throw new EmptyStackException();
        }

        int data = top.data;
        top = top.next;
        size--;
        return data;
    }

    public void display() {
        Node current = top;
        System.out.print("Stack: ");
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }
}

public class fds{
    public static void main(String[] args) {
        Stack stack = new Stack(4);

        stack.push(13);
        stack.push(22);
        stack.push(39);
        stack.push(45);

        stack.display();

        stack.push(26); 

        System.out.println("Popped element: " + stack.pop());
        stack.display();
    }
}Certainly! Below, I'll provide examples for various searching and sorting algorithms in Java. Keep in mind that these are basic implementations, and you may need to adjust them based on specific use cases.

### Searching Algorithms:

1. **Linear Search:**
```java
public class LinearSearch {
    public static int search(int[] array, int target) {
        for (int i = 0; i < array.length; i++) {
            if (array[i] == target) {
                return i;
            }
        }
        return -1; // Not found
    }
}
```

2. **Binary Search (for sorted arrays):**
```java
import java.util.Arrays;

public class BinarySearch {
    public static int search(int[] array, int target) {
        int left = 0;
        int right = array.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (array[mid] == target) {
                return mid;
            } else if (array[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return -1; // Not found
    }
}
```

### Sorting Algorithms:

1. **Bubble Sort:**
```java
public class BubbleSort {
    public static void sort(int[] array) {
        int n = array.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (array[j] > array[j + 1]) {
                    // Swap array[j] and array[j+1]
                    int temp = array[j];
                    array[j] = array[j + 1];
                    array[j + 1] = temp;
                }
            }
        }
    }
}
```

2. **Selection Sort:**
```java
public class SelectionSort {
    public static void sort(int[] array) {
        int n = array.length;
        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;
            for (int j = i + 1; j < n; j++) {
                if (array[j] < array[minIndex]) {
                    minIndex = j;
                }
            }
            // Swap array[i] and array[minIndex]
            int temp = array[i];
            array[i] = array[minIndex];
            array[minIndex] = temp;
        }
    }
}
```

3. **Insertion Sort:**
```java
public class InsertionSort {
    public static void sort(int[] array) {
        int n = array.length;
        for (int i = 1; i < n; i++) {
            int key = array[i];
            int j = i - 1;

            while (j >= 0 && array[j] > key) {
                array[j + 1] = array[j];
                j--;
            }

            array[j + 1] = key;
        }
    }
}
```

4. **Merge Sort:**
```java
public class MergeSort {
    public static void sort(int[] array, int left, int right) {
        if (left < right) {
            int mid = left + (right - left) / 2;

            // Recursive sort for both halves
            sort(array, left, mid);
            sort(array, mid + 1, right);

            // Merge the sorted halves
            merge(array, left, mid, right);
        }
    }

    private static void merge(int[] array, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;

        int[] leftArray = new int[n1];
        int[] rightArray = new int[n2];

        // Copy data to temporary arrays
        for (int i = 0; i < n1; i++) {
            leftArray[i] = array[left + i];
        }
        for (int j = 0; j < n2; j++) {
            rightArray[j] = array[mid + 1 + j];
        }

        // Merge the two arrays
        int i = 0, j = 0, k = left;
        while (i < n1 && j < n2) {
            if (leftArray[i] <= rightArray[j]) {
                array[k] = leftArray[i];
                i++;
            } else {
                array[k] = rightArray[j];
                j++;
            }
            k++;
        }

        // Copy remaining elements of leftArray[], if any
        while (i < n1) {
            array[k] = leftArray[i];
            i++;
            k++;
        }

        // Copy remaining elements of rightArray[], if any
        while (j < n2) {
            array[k] = rightArray[j];
            j++;
            k++;
        }
    }
}
```

These examples cover linear search, binary search, bubble sort, selection sort, insertion sort, and merge sort. Remember to adapt them to your specific needs and handle edge cases accordingly.
