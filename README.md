# tugas-algoritma-sesi-10
<!-- heapshort -->
public class HeapSort {
    public void sort(int arr[], String order) {
        if (order.equals("asc")) {
            sortAscending(arr);
        } else if (order.equals("dsc")) {
            sortDescending(arr);
        } else {
            System.out.println("Invalid order parameter. Please use 'asc' for ascending or 'dsc' for descending.");
        }
    }

    private void sortAscending(int arr[]) {
        int N = arr.length;

        for (int i = N / 2 - 1; i >= 0; i--)
            heapify(arr, N, i);

        for (int i = N - 1; i > 0; i--) {
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;

            heapify(arr, i, 0);
        }
    }

    private void heapify(int arr[], int N, int i) {
        int largest = i;
        int l = 2 * i + 1;
        int r = 2 * i + 2;

        if (l < N && arr[l] > arr[largest])
            largest = l;

        if (r < N && arr[r] > arr[largest])
            largest = r;

        if (largest != i) {
            int swap = arr[i];
            arr[i] = arr[largest];
            arr[largest] = swap;

            heapify(arr, N, largest);
        }
    }

    private void sortDescending(int arr[]) {
        int N = arr.length;

        for (int i = N / 2 - 1; i >= 0; i--)
            heapifyDescending(arr, N, i);

        for (int i = N - 1; i > 0; i--) {
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;

            heapifyDescending(arr, i, 0);
        }
    }

    private void heapifyDescending(int arr[], int N, int i) {
        int smallest = i;
        int l = 2 * i + 1;
        int r = 2 * i + 2;

        if (l < N && arr[l] < arr[smallest])
            smallest = l;

        if (r < N && arr[r] < arr[smallest])
            smallest = r;

        if (smallest != i) {
            int swap = arr[i];
            arr[i] = arr[smallest];
            arr[smallest] = swap;

            heapifyDescending(arr, N, smallest);
        }
    }

    static void printArray(int arr[]) {
        int N = arr.length;

        for (int i = 0; i < N; ++i)
            System.out.print(arr[i] + " ");
        System.out.println();
    }

    public static void main(String args[]) {
        int arr[] = { 12, 11, 13, 5, 6, 7 };
        int N = arr.length;

        HeapSort ob = new HeapSort();

        System.out.println("Sorted Array in Ascending Order:");
        ob.sort(arr, "asc");
        printArray(arr);

        System.out.println("Sorted Array in Descending Order:");
        ob.sort(arr, "dsc");
        printArray(arr);
    }
}


<!-- mergeshrot -->

public class MergeSort {

    void merge(int arr[], int l, int m, int r) {
        int n1 = m - l + 1;
        int n2 = r - m;

        int L[] = new int[n1];
        int R[] = new int[n2];

        for (int i = 0; i < n1; ++i)
            L[i] = arr[l + i];
        for (int j = 0; j < n2; ++j)
            R[j] = arr[m + 1 + j];

        int i = 0, j = 0;
        int k = l;

        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k] = L[i];
                i++;
            } else {
                arr[k] = R[j];
                j++;
            }
            k++;
        }

        while (i < n1) {
            arr[k] = L[i];
            i++;
            k++;
        }

        while (j < n2) {
            arr[k] = R[j];
            j++;
            k++;
        }
    }

    void sort(int arr[], int l, int r, String order) {
        if (l < r) {
            int m = l + (r - l) / 2;

            sort(arr, l, m, order);
            sort(arr, m + 1, r, order);

            if (order.equals("asc"))
                merge(arr, l, m, r);
            else if (order.equals("dsc"))
                mergeDescending(arr, l, m, r);
            else
                System.out.println("Invalid order parameter. Please use 'asc' for ascending or 'dsc' for descending.");
        }
    }

    void mergeDescending(int arr[], int l, int m, int r) {
        int n1 = m - l + 1;
        int n2 = r - m;

        int L[] = new int[n1];
        int R[] = new int[n2];

        for (int i = 0; i < n1; ++i)
            L[i] = arr[l + i];
        for (int j = 0; j < n2; ++j)
            R[j] = arr[m + 1 + j];

        int i = 0, j = 0;
        int k = l;

        while (i < n1 && j < n2) {
            if (L[i] >= R[j]) {
                arr[k] = L[i];
                i++;
            } else {
                arr[k] = R[j];
                j++;
            }
            k++;
        }

        while (i < n1) {
            arr[k] = L[i];
            i++;
            k++;
        }

        while (j < n2) {
            arr[k] = R[j];
            j++;
            k++;
        }
    }

    static void printArray(int arr[]) {
        int n = arr.length;
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
        System.out.println();
    }

    public static void main(String args[]) {
        int arr[] = { 12, 11, 13, 5, 6, 7 };

        System.out.println("Sorted Array in Ascending Order:");
        MergeSort ob = new MergeSort();
        ob.sort(arr, 0, arr.length - 1, "asc");
        printArray(arr);

        System.out.println("Sorted Array in Descending Order:");
        ob.sort(arr, 0, arr.length - 1, "dsc");
        printArray(arr);
    }
}
