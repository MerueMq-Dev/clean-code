Пункт 1. Неочевидные комментарии
Добавил больше контекста в комментарий
Было:
// TODO: rewrite all while loops to for loops in this class
    public class OrderedList<T>
Стало:
// TODO: rewrite all while loops to for loops in this class to improve readability
    public class OrderedList<T>


Пункт 2. Бормотание
// Дал более чёткое описание методу
До:
// Be careful with this method - it deletes all data!
public void Clear(bool asc = true)
{
    _ascending = asc;
    head = null;
    tail = null;
}
После:
// Clears the list and resets the sorting order.
public void Clear(bool asc = true)
{
    _ascending = asc;
    head = null;
    tail = null;
}

Пункт 2. Бормотание
Убрал комментарий и добавил метод ExpandCapacity() сделав тем самым код самодокументируемым.
До:
// Capacity increases based on the GrowthMultiplier growth factor.
if (Count == Capacity)
    MakeArray(Capacity * CapacityGrowthFactor);
После:
if (Count == Capacity)
    ExpandCapacity();


Пункт 3. Недостоверные комментарии
Опустил комментарий ниже — логика очевидна.
До:
// Check to avoid double initialization
if (array == null)
    array = new T[Capacity];
После:
if (array == null)
    array = new T[Capacity];


Пункт 4. Шум.
Удалил следующий комментарий ниже, так как он повторяет код.
До:
// If the array is full, create a new array with increased capacity.
if (Count == Capacity)
    MakeArray(Capacity * CapacityGrowthFactor);
После:
if (Count == Capacity)
    MakeArray(Capacity * CapacityGrowthFactor);

Пункт 4. Шум.
Удалил комментарий, так как он описывает очевидное — поведение модульного деления. 
До:
// Convert the string to an array index using modular arithmetic.
// Hashing is performed on the remainder of the division
// so that the result falls into the index range.
var valueHash = value.GetHashCode();
var slotIndex = Math.Abs(valueHash % size);
После
var valueHash = value.GetHashCode();
var slotIndex = Math.Abs(valueHash % size);

Пункт 4. Шум.
Удалил комментарий, так как он не несёт полезной информации, из контекста кода и так понятно, что метод может использоваться для тестирования.
До:
// For testing purposes
public static void CreateCyclic(this LinkedList2 source)
{
    ...
}       
После:
public static void CreateCyclic(this LinkedList2 source)
{
    ...
}

Пункт 4. Шум
Сделал комметарий более кратким
До:
// We use a manual comparison implementation because the standard implementation
// does not support comparing objects without specifying IComparer
if (Compare(val, currentNode.value) == 0)                
После:
// Manual comparison for unsupported types.
if (Compare(val, currentNode.value) == 0)

Пункт 8. Слишком много информации
Указал более конкретную зону отвествености переменной.
До: 
// Changing this variable affects the entire processing process
private bool _ascending;
После:
// Indicates the sort order of the ordered list
private bool _ascending;

Пункт 9. Нелокальная информация
В комментарии к MergeTwoLists уточняется требование сортировки, хотя это уже реализовано в коде.
Поэтому я удалил этот комментарий.
До:
public static LinkedList2 MergeTwoLists(this LinkedList2 source, LinkedList2 secondSource)
{
    // Sorting is required before merger
    source.Sort();
    secondSource.Sort();
    ...
}
После:
public static LinkedList2 MergeTwoLists(this LinkedList2 source, LinkedList2 secondSource)
{
    source.Sort();
    secondSource.Sort();
    ...
}
        
Пункт 11. Закомментированный код. 
Удалил закомментированый код из PowerSet.
До:
// if (startIndex > slotIndex || startIndex + step > slots.Length)
// {
//     startIndex = 0;
// }
После:

Пункт 11. Закомментированный код. 
Удалил закомментированый код из NativeCache.
До:
// if (startIndex > slotIndex || startIndex + step > slots.Length)
// {
//     startIndex = 0;
// }
После:

Пункт 12. Не используйте комментарии там, где можно использовать функцию или переменную.
Переименовал переменную и удалил поясняющий комментарий
До:
// Multiplier for increase dynamic array.
private const int GrowthMultiplier = 2;
После:
private const int CapacityGrowthFactor  = 2;
        
Пункт 12. Не используйте комментарии там, где можно использовать функцию или переменную.
Переименовал переменную и удалил поясняющий комментарий
До:
// Threshold for reducing the size of a dynamic array
private const double ShrinkThreshold = 1.5;
После:
private const double CapacityShrinkThreshold  = 1.5;

Пункт 12. Не используйте комментарии там, где можно использовать функцию или переменную.
До:
public PowerSet(int slotCount = 20000, int stepSize = 10) : base(slotCount, stepSize)
{
    step = stepSize;
    // Initializing slots
    size = slotCount;
    _sourcePowerSet = new List<T>();
    slots = new string[size];
    for (int i = 0; i < slots.Length; i++)
        slots[i] = null;
}
После:
public PowerSet(int slotCount = 20000, int stepSize = 10) : base(slotCount, stepSize)
{
    step = stepSize;
    InitializeSlots(slotCount);
}

private void InitializeSlots(int slotCount)
{
    size = slotCount;
    _sourcePowerSet = new List<T>();
    slots = new string[size];
    for (int i = 0; i < slots.Length; i++)
        slots[i] = null;
}