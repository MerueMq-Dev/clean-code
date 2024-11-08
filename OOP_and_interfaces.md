3.1
// Метод FromArray создает и возвращает новый объект LinkedList с переданными в него элементами.
public static LinkedList FromArray(params Node[] nodes)
{
    var newList = new LinkedList2();
    foreach (var node in nodes)
    {
        newList.AddInTail(node);
    }
    return newList;
}

// Метод FromArrayDescending создает и возвращает новый объект OrderedList с переданными в него элементами, отсортированными по убыванию.
public static OrderedList<T> FromArrayDescending(params T[] values)
{
    var descendingOrderedList = new OrderedList<T>(false);
    foreach (var node in values)
    {
        descendingOrderedList.Add(node);
    }
    
    return descendingOrderedList;
}


// Метод WithSize создает и возвращает новый объект BloomFilter с заданной длиной фильтра.
public static BloomFilter WithSize(int filterLength)
{
    var newFilter = new BloomFilter(filterLength);
    return newFilter;
}




3.2
EmailNotifier - интерфейс для отправки уведомлений по электронной почте.
GuidFactory - интерфейс, представляющий фабрику для генерации GUID
MomentProvider - интерфейс для предоставления текущего момента времени. 