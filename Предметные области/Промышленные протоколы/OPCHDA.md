По сути, куда обращаться интрефейсу за данными (источник) указывается в `instrument tag` у тэга.
Самому интерфесу в конфиге мы только настраиваем `ps` - `point source`. Это просто метка, по которой интерфейс будет искать тэги. Аналогичная метка - `instanceId`. То есть, интерфейс лезет в TSDB (указываем `<TSDBServerConnect TSDBClientType="WebApiClient" TSDBConnectionName="TSDB1" server="http://192.168.10.162:98"...`) за тэгами с указанным `ps` и `instanceId`. В тэгах указан источник, в который интерфейс лезет за данными. Конкртено адрес истоника указываем:
```xml
<paramGroups>  
  <paramGroup ps="LebOPC" server="opchda://localhost/Insat.ModbusOPCServer.HDA"
```

Также необходима платформа. Что такое - хз. Но пока запускаем локально проект I-DS-P и указываем его как локалхост:
```xml
<ISPServerConnect server="http://192.168.10.162:7701" login="sam" password="sam" authType="Isp" />
```

**Для HDA указываем такой исчтоник в тэге**:
"PN_SIMULATOR.PD_SIMULATOR.Saw50" - для интерфейса пишем такой `instrument tag` у тэга.
