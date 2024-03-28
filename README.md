using System;
using System.Diagnostics;

class Program
{
    static int BinarySearchIterative(int[] array, int target)
    {
        int left = 0;
        int right = array.Length - 1;

        while (left <= right)
        {
            int mid = left + (right - left) / 2;

            if (array[mid] == target)
                return mid;
            else if (array[mid] < target)
                left = mid + 1;
            else
                right = mid - 1;
        }

        return -1;
    }

    static void Main()
    {
        int arraySize = 10000000;
        int[] randomArray = new int[arraySize];
        int[] sortedArray = new int[arraySize];

        Random rnd = new Random();
        for (int i = 0; i < arraySize; i++)
        {
            randomArray[i] = rnd.Next(0, arraySize);
            sortedArray[i] = i;
        }

        int target = rnd.Next(0, arraySize);

        Stopwatch sw = new Stopwatch();

        // Измеряем время выполнения на случайном массиве
        sw.Start();
        int resultRandom = BinarySearchIterative(randomArray, target);
        sw.Stop();
        Console.WriteLine($"Random array search time: {sw.Elapsed}");

        // Измеряем время выполнения на отсортированном массиве
        sw.Reset();
        sw.Start();
        int resultSorted = BinarySearchIterative(sortedArray, target);
        sw.Stop();
        Console.WriteLine($"Sorted array search time: {sw.Elapsed}");
    }
}
