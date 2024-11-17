3.1

// Method for testing purposes
public static void CreateCyclic(this LinkedList2 source)
{
    source.tail.next = source.head;
    source.head.prev = source.tail;
}


for (var currentNode = head; currentNode != null; currentNode = currentNode.next)
{
    // We use a manual comparison implementation because the standard implementation
    // does not support comparing objects without specifying IComparer
    if (Compare(val, currentNode.value) == 0)
        return currentNode;
}


// Increase or decrease the array. Minimum capacity - 16 elements,
// to avoid private recalculations for small amounts of data.
public void MakeArray(int newCapacity)
{
    Capacity = newCapacity < 16 ? 16 : newCapacity
    if (array == null)
        array = new T[Capacity]
    var newArr = new T[Capacity];
    Array.Copy(array, newArr, Count);
    array = newArr;
}


// Multiplier for increase dynamic array.
private const int GrowthMultiplier = 2;


// Threshold for reducing the size of a dynamic array
private const double ShrinkThreshold = 1.5;


// ComputeFirstHash and ComputeSecondHash: two independent hash functions to minimize collisions.
// They use different coefficients (17 and 223) to produce two different index values.
// Hash functions ensure that values ​​are evenly distributed across the bitmap.
public int ComputeFirstHash(string str1)
{
    var hash = 0;
    var randomValue = 17;
    for (int i = 0; i < str1.Length; i++)
    {
        hash = (hash * randomValue + str1[i]) % filter_len;
    }
    return hash;
}

public int ComputeSecondHash(string str1)
{
    var hash = 0;
    var randomValue = 223;
    for (int i = 0; i < str1.Length; i++)
    {
        hash = (hash * randomValue + str1[i]) % filter_len;
    }
    return hash;
}


// Flag indicating that an element can be inserted between the current and next node.
var isBetweenNodes = resultOfCurrentNodeCompare >= 0 && resultOfNextNodeCompare <= 0 &&
                     currentNode.next != null;

// Flag indicating that an element can be inserted at the current position.
var isInsertablePosition = resultOfCurrentNodeCompare <= 0 && resultOfNextNodeCompare >= 0 &&
                           currentNode.next != null;