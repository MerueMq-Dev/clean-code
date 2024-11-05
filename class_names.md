3.1
AccountManager - UserAccount
// Описывает конкретный объект, не давая ложной информации о его управленческой роли.
ProductData - ProductCatalog
// Более явно указывает, что этот класс хранит список продуктов, а не просто данные.
OrderInfo - OrderProcessor 
// Поясняет, что класс занимается обработкой заказов, а не просто содержит информацию о них.
PaymentDriver - PaymentGateway 
// Подчеркивает, что это интерфейс для платежей, а не драйвер системы.
NotificationSender - EmailNotification 
// Обозначает, что класс занимается конкретной задачей по отправке уведомлений.


3.2
DeleteNode, RemoveNode - RemoveNode
// Метод удаляет узел если он существует.

FindNode, LocateNode, Find - FindNode 
// Метод ищет узел по значение в связнном списке/дереве.

ArrayHelper, ArrayTool - ArrayUtilities 
// Объект хранит общие методы для работы с массивами.

ClearCache, ResetCache - ClearCache.
// Метод очищает весь кэш.

UpdateStatus, ChangeStatus, ModifyStatus - SetStatus
// Метод обновляет статус если он не изменился.

LoadData, FetchData - GetData - GetData
// Метод отправляет запрос на сервер за данными.

ValidateIndex, CheckIndex, VerifyIndex - ValidateIndex
// Метод валидирует индекс.

