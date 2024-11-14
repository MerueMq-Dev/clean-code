private T[] sourceDynamicArray;
// Сделал внутренний массив приватным, чтобы защитить динамический массив от внешних изменений 
Это помогает избежать ошибок и контролировать увеличение размера массива, сохраняя целостность данных 
и правильную работу алгоритмов.

public int Count { get; private set; }
// Заменил поле count на свойство Count с приватным сеттером, чтобы защитить его от внешних изменений, сохранив доступ для чтения. Это защищает внутреннюю логику класса и обеспечивает корректный подсчёт элементов, сохраняя целостность данных.

private readonly List<T> _queueSource;
public List<T> GetElements()
{
    return new List<T>(_queueSource);
}
// Сделал внутренний список очереди приватным, чтобы защитить очередь от внешних изменений, так же добавил метод который позволяет получить все элементы в виде списка. Это защищает внутреннюю логику очереди, сохранив доступ для чтения и тестирования. 

public int Capacity { get; private set; }
// Заменил поле capacity на свойство Capacity с приватным сеттером, чтобы защитить его от внешних изменений, сохранив доступ для чтения. Это защищает внутреннюю логику класса и обеспечивает корректный подсчёт вместимости динамического массива, сохраняя целостность данных и доступность для тестирования.   

private void ValidateIndex(int targetIndex, bool includeLastItem = false)
{
    var itemsCount = includeLastItem ? count : count - 1
    if (targetIndex > itemsCount || targetIndex < 0)
    {
        throw new IndexOutOfRangeException();
    }
}
// Вынес проверку индекса в отдельный метод, чтобы улучшить читаемость и повторное использование логики валидации.

public int Size { get; protected set; }
// Заменил поле size на свойство Size с защищённым сеттером, чтобы предотвратить внешние изменения, но позволить наследникам изменять значение, сохраняя доступ для чтения. Это защищает внутреннюю логику класса и обеспечивает корректный подсчёт вместимости хэш-таблицы, сохраняя целостность данных и доступность для тестирования.

protected readonly int step;
// Сделал поле шага для поиска в хэш-таблице защищённым, чтобы защитить хэш-таблицу от внешних изменений, но позволяя наследникам изменять значение. Это помогает избежать ошибок и контролировать увеличение шага для поиска в хэш-таблице, сохраняя целостность данных и правильную работу алгоритмов.


private readonly List<T> _stackSource;
public List<T> GetElements()
{
    return new List<T>(_stackSource);
}
// Сделал внутренний список стека приватным, чтобы защитить стек от внешних изменений, так же добавил метод который позволяет получить все элементы в виде списка. Это защищает внутреннюю логику стека, сохранив доступ для чтения и тестирования.


// Полностью переписал метод Add в классе для отсортированного списка. Улучшил минимизацию области видимости переменных, ограничив их использование внутри соответствующих методов, таких как TryInsertAtStart, TryInsertAtEnd и TryInsertAtMiddle. Это уменьшает их жизнь и увеличивает локализацию. Кроме того, разбив логику вставки на более мелкие методы, я улучшил группировку связанных команд и сделал каждый метод более сфокусированным на одной задаче. Это улучшает читаемость и облегчает поддержку кода, поскольку теперь каждый метод выполняет одну конкретную операцию.
public void Add(T value)
{
    var item = new Node<T>(value);
    if (head == null)
    {
        head = item;
        head.next = null;
        head.prev = null;
        tail = item;
        return;
    }

    bool wasItemInsertedAtStart = TryInsertAtStart(item);
    if (wasItemInsertedAtStart)
        return;
    
    bool wasItemInsertedAtEnd = TryInsertAtEnd(item);
    if (wasItemInsertedAtEnd)
        return;
    
    bool wasItemInsertedAtMiddle = TryInsertAtMiddle(item);
    if(!wasItemInsertedAtMiddle)
        throw new Exception();
}


private bool TryInsertAtStart(Node<T> item)
{
    ref var currentNode = ref (_ascending ? ref head : ref tail);
    var resultOfCompare = Compare(item.value, currentNode.value);
    
    if (head != tail && resultOfCompare > -1)
        return false;
    
    if (resultOfCompare >= 0 && !_ascending || resultOfCompare <= 0 && _ascending)
    {
        item.next = head;
        head.prev = item;
        item.prev = null;
        head = item;
        return true;
    }
    tail.next = item;
    item.prev = tail;
    tail = item;
    return true;
}


private bool TryInsertAtEnd(Node<T> item)
{
    ref var currentNode = ref (!_ascending ? ref head : ref tail);
    var resultOfCompare = Compare(item.value, currentNode.value);

    if (resultOfCompare != 1)
        return false;
    
    if (_ascending)
    {
        currentNode.next = item;
        item.prev = currentNode;
        currentNode = item;
        return true;
    }

    currentNode.prev = item;
    item.next = currentNode;
    currentNode = item;
    return true;
}

// В методе TryInsertAtMiddle, переменные в цикле for теперь объявляются непосредственно в теле цикла. Это уменьшает область видимости переменных и предотвращает их ненужное использование за пределами цикла.
private bool TryInsertAtMiddle(Node<T> item)
{
    for (var currentNode = head; currentNode != null; currentNode = currentNode.next)
    {
        var resultOfCurrentNodeCompare = Compare(item.value, currentNode.value);
        var resultOfNextNodeCompare = Compare(item.value, currentNode.next.value);
        var isBetweenNodes = resultOfCurrentNodeCompare >= 0 && resultOfNextNodeCompare <= 0 &&
                                          currentNode.next != null;
        var isInsertablePosition =  resultOfCurrentNodeCompare <= 0 && resultOfNextNodeCompare >=0 &&currentNode.next != null;
        
        if (resultOfCurrentNodeCompare >= 0 && currentNode.next == null)
        {
            item.prev = currentNode;
            item.next = null;
            currentNode.next = item;
            tail = item;
            return true;
        }
        if (isInsertablePosition || isBetweenNodes)
        {
            var next = currentNode.next;
            next.prev = item;
            currentNode.next = item;
            item.prev = currentNode;
            item.next = next;
            return true;
        }
    }
    return false;
}



// Старая реализация метода Add для сравнения:

public void Add(T value)
{
    var item = new Node<T>(value);
    if (head == null)
    {
        head = item;
        head.next = null;
        head.prev = null;
        tail = item;
        return;
    }
    if (_ascending)
    {
        AddAsc(item);
    }
    else
    {
        AddDesc(item);
    }
}


private void AddAsc(Node<T> item)
{
    var resultOfHeadCompare = Compare(item.value, head.value);
    if (head == tail)
    {
        if (resultOfHeadCompare <= 0)
        {
            item.next = head;
            head.prev = item;
            item.prev = null;
            head = item;
            return;
        }
        tail.next = item;
        item.next = null;
        item.prev = tail;
        tail = item;
        return;
    }
    if (resultOfHeadCompare == -1)
    {
        head.prev = item;
        item.next = head;
        head = item;
        return;
    }
    var currentNode = head;
    while (currentNode != null)
    {
        var resultOfCurrentNodeCompare = Compare(item.value, currentNode.value);
        if (resultOfCurrentNodeCompare >= 0 && currentNode.next == null)
        {
            item.prev = currentNode;
            item.next = null;
            currentNode.next = item;
            tail = item;
            return;
        }
        var resultOfNextNodeCompare = Compare(item.value, currentNode.next.value);
        if (resultOfCurrentNodeCompare <= 0 && resultOfNextNodeCompare >= 0 && currentNode.next!=null)
        {
            var next = currentNode.next;
            next.prev = item;
            currentNode.next = item;
            item.prev = currentNode;
            item.next = next;
            return;
        }
        if (resultOfCurrentNodeCompare >= 0 && resultOfNextNodeCompare <= 0 && currentNode.next!=null)
        {
            var next = currentNode.next;
            next.prev = item;
            currentNode.next = item;
            item.prev = currentNode;
            item.next = next;
            return;
        }
        currentNode = currentNode.next;
    }
}

private void AddDesc(Node<T> item)
{
    var resultOfHeadCompare = Compare(item.value, head.value);
    var resultOfTailCompare = Compare(item.value, tail.value);
    if (head == tail)
    {
        if (resultOfHeadCompare >= 0)
        {
            item.next = head;
            head.prev = item;
            item.prev = null;
            head = item;
            return;
        }
        tail.next = item;
        item.next = null;
        item.prev = tail;
        tail = item;
        return;
    }
    if (resultOfTailCompare <= 0)
    {
        item.prev = tail;
        tail.next = item;
        item.next = null;
        tail = item;
        return;
    }
    if (resultOfHeadCompare == 1)
    {
        head.prev = item;
        item.next = head;
        head = item;
        return;
    }
    var currentNode = head;
    while (currentNode != null)
    {
        var resultOfCurrentNodeCompare = Compare(item.value, currentNode.value);
        if (resultOfCurrentNodeCompare >= 0 && currentNode.next == null)
        {
            item.prev = currentNode;
            item.next = null;
            currentNode.next = item;
            tail = item;
            return;
        }
        var resultOfNextNodeCompare = Compare(item.value, currentNode.next.value);
        if (resultOfCurrentNodeCompare >= 0 && resultOfNextNodeCompare <= 0 && currentNode.next!=null)
        {
            var next = currentNode.next;
            next.prev = item;
            currentNode.next = item;
            item.prev = currentNode;
            item.next = next;
            return;
        }
        if (resultOfCurrentNodeCompare <= 0 && resultOfNextNodeCompare >= 0 && currentNode.next!=null)
        {
            var next = currentNode.next;
            next.prev = item;
            currentNode.next = item;
            item.prev = currentNode;
            item.next = next;
            return;
        }
        currentNode = currentNode.next;
    }
}