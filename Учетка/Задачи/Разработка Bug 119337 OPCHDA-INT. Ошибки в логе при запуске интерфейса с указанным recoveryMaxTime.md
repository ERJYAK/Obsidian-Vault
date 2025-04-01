
Мы рассматриваем случай, только когда параметр `HistoryRecoveryOnly == false`. В этом случае в**ремя конца восстановления** истории считается как `DateTime.Now`, а **время начала восстановления** истории - разница между концом и `recoveryMaxTime`. 
**Поэтому важно либо задавать параметр `recoveryMaxTime`, либо если он не задан а восстановление истории нужно - выставить дефолт**

Заходим в `Connection.MainMode` - стартовый метод. 
`_srvConnect` инициализируется тут
Есть 3 варианта развития событий:
1. Если указать только `recoveryMaxTime`, но не указывать `maxTimePeriodPerCycle`. В этом случае 

**Если `maxTimePeriodPerCycle` не задан или 0, то делаем его равным `recoveryMaxTime`.**
# Первая проблема. Запрос истории данных сначала в Utc.

В `Connection.cs` при вызове класса `HistoryRecovery` вызывается `DateTime.UtcNow` вместо обычного времени

# Соединение с сервером

Проеблема соединения с сервером возникает всегда в одном месте - при попытке к нему обратиться в методе `ValidateItems` выбрасывается ошибка.
Туда мы приходим:
`ConnectionManager.ReadHistorianData` $\rightarrow$  `ConvertValues` $\rightarrow$  `DataReader.ReadValues` $\rightarrow$  `DataReader.ReadValues` $\rightarrow$  `Server.ValidateItems`

При инициализации `ConnectionManager` соединение есть, однако, когда мы передаем сервер в  `ReadValues` - соединение уже отсутствует...