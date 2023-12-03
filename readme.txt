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

public class bubblesort {
    public static void main(String[] args) {
        int[] array = {43, 12, 89, 54, 27, 63, 59, 78};
        System.out.println("Original array:");
        printArray(array);
        
        bubbleSort(array);
        
        System.out.println("\nSorted array:");
        printArray(array);
    }
    
    public static void bubbleSort(int[] array) {
        int n = array.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                // Swap if the element found is greater than the next element
                if (array[j] > array[j + 1]) {
                    // Swap array[j] and array[j + 1]
                    int temp = array[j];
                    array[j] = array[j + 1];
                    array[j + 1] = temp;
                }
            }
        }
    }
    
    public static void printArray(int[] array) {
        for (int i = 0; i < array.length; i++) {
            System.out.print(array[i] + " ");
        }
        System.out.println();
    }
}

