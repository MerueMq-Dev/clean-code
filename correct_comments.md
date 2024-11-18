// 1. Информативный комментарий
protected int HashFun(string value)
{
    // Convert the string to an array index using modular arithmetic.
    // Hashing is performed on the remainder of the division
    // so that the result falls into the index range.
    var valueHash = value.GetHashCode();
    var slotIndex = Math.Abs(valueHash % size);
    return slotIndex;
}


// 1. Информативный комментарий
// If the array is full, create a new array with increased capacity.
// Capacity increases based on the GrowthMultiplier growth factor.
if (Count == Capacity)
    MakeArray(Capacity * GrowthMultiplier);



// 2. Представление намерений
// Check to avoid double initialization.
if (array == null)
    array = new T[Capacity];


// 2. Представление намерений
// We are trying to check how the Find method works when searching for a non-existent element.
var list = new LinkedList(new Node(3), new Node(1), new Node(4));
var foundNode = list.Find(5);


// 3. Прояснение
// resultOfCompare == 0 means that the elements being compared are equal.  
int resultOfCompare = Compare(head.value, val);
if (resultOfCompare == 0)
{
    if (head == tail)
    {
        Clear();
    }
    else
    {
        head = head.next;
        head.prev = null;
    }
    return;
}

// 3. Прояснение
// The method returns -1 if an empty slot is not found.
var slotIndex = SeekSlot(value);
if (slotIndex != -1)
{
    slots[slotIndex] = value;
    return slotIndex;
}


// 4. Предупреждения о последствиях
// Be careful with this method - it deletes all data!
public void Clear(bool isAscendingOrder = true)
{
    _isAscendingOrder = isAscendingOrder;
    head = null;
    tail = null;
}   


// 4. Предупреждения о последствиях
// Changing this variable affects the entire processing process!
private bool _isAscendingOrder;


// 5. Усиление
// Removing whitespace is critical for correct string comparisons.
var firstSting = v1.ToString().Trim();
var secondString = v2.ToString().Trim();
var resultStringCompare = String.Compare(firstSting, secondString, StringComparison.Ordinal);


// 5. Усиление
public static LinkedList MergeTwoLists(this LinkedList source, LinkedList secondSource)
{
    // Sorting is required before merger.
    source.Sort();
    secondSource.Sort();


    var firstNode = source.head;
    var secondNode = secondSource.head;
    var mergedList = new LinkedList();
    while (firstNode != null || secondNode != null)
    {
        if (firstNode?.value < secondNode.value)
        {
            mergedList.AddInTail(new Node(firstNode.value));
            firstNode = firstNode.next;
        }
        else
        {
            mergedList.AddInTail(new Node(secondNode.value));
            secondNode = secondNode.next;
        }
    }
    return mergedList;
}


// 6. Комментарий TODO
// TODO: rewrite all while loops to for loops in this class. 
public class OrderedList<T>
{
    // realisation...
}


// 6. Комментарий TODO
// TODO: Add a method that adds an element to the head of a linked list.

