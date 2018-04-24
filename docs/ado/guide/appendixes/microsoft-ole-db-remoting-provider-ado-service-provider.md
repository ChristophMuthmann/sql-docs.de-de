---
title: Microsoft OLE DB-Anbieter für Remoting (ADO-Dienstanbieter) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB remoting provider [ADO]
- providers [ADO], OLE DB remoting provider
- remoting provider [ADO]
ms.assetid: a4360ed4-b70f-4734-9041-4025d033346b
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4f132bb8124afecea1b1f7fb519ecf64d1cfe88a
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="microsoft-ole-db-remoting-provider-overview"></a>Microsoft OLE DB-Remoting-Anbieter (Übersicht)
Der Microsoft OLE DB-Anbieter für Remoting ermöglicht, einen lokalen Benutzer auf einem Clientcomputer aufzurufenden Datenanbieter auf einem Remotecomputer. Geben Sie die Parameter des Datenproviders für den Remotecomputer wie würden Sie einen lokalen Benutzer auf dem Remotecomputer. Geben Sie dann die Parameter, die vom Anbieter-Remoting verwendet wird, auf den Remotecomputer zuzugreifen. Sie können dann den Remotecomputer zugreifen, als wären Sie ein lokaler Benutzer.

> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).

## <a name="provider-keyword"></a>Anbieter-Schlüsselwort
 Um den OLE DB-Anbieter für Remoting aufzurufen, geben Sie die folgenden-Schlüsselwort und Wert in der Verbindungszeichenfolge ein. (Beachten Sie die Leerzeichen im Namen Anbieters.)

```
"Provider=MS Remote"
```

## <a name="additional-keywords"></a>Zusätzliche Schlüsselwörter
 Wenn dieser Dienstanbieter aufgerufen wird, sind die folgenden zusätzlichen Schlüsselwörter relevant.

|Schlüsselwort|Description|
|-------------|-----------------|
|**Datenquelle**|Gibt den Namen der remote-Datenquelle. Es wird an den OLE DB-Anbieter für Remoting zur Verarbeitung übergeben.<br /><br /> Dieses Schlüsselwort entspricht der [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) des Objekts [verbinden](../../../ado/reference/rds-api/connect-property-rds.md) Eigenschaft.|

## <a name="dynamic-properties"></a>Dynamische Eigenschaften
 Wenn dieser Dienstanbieter aufgerufen wird, die folgenden dynamischen Eigenschaften hinzugefügt werden die [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md)des Objekts [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung.

|Name der dynamischen Eigenschaft|Description|
|---------------------------|-----------------|
|**DFMode**|Gibt den DataFactory-Modus. Eine Zeichenfolge, die die gewünschte Version eines gibt die [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) Objekt auf dem Server. Legen Sie diese Eigenschaft vor dem Öffnen einer Verbindung zum Anfordern einer bestimmten Version der **DataFactory**. Wenn die angeforderte Version nicht verfügbar ist, wird es versucht werden, verwenden Sie die vorherige Version. Wenn keine vorherigen Version vorhanden ist, tritt ein Fehler auf. Wenn **DFMode** kleiner als die verfügbare Version ist, wird eine Fehlermeldung angezeigt. Diese Eigenschaft ist schreibgeschützt, nachdem eine Verbindung hergestellt wird.<br /><br /> Die folgenden gültigen Zeichenfolgenwerte sind möglich:<br /><br /> -"25", Version 2.5 (Standard)<br />-"21", Version 2.1<br />-"20", Version 2.0<br />-"15", Version 1.5|
|**Befehlseigenschaften**|Verweist auf Werte, die in der Zeichenfolge der (Rowset)-Befehlseigenschaften, die an den Server gesendet werden, durch den MS Remote-Anbieter hinzugefügt werden. Der Standardwert für diese Zeichenfolge wird Vt_empty.|
|**Aktuelle DFMode**|Gibt die tatsächliche Anzahl von an das **DataFactory** auf dem Server. Überprüfen Sie diese Eigenschaft, um festzustellen, ob die Version im angefordert der **DFMode** Eigenschaft berücksichtigt wurde.<br /><br /> Die folgenden gültigen Long Integer-Werte sind möglich:<br /><br /> – 25 – Version 2.5 (Standard)<br />-21 – Version 2.1<br />– 20 – Version 2.0<br />– 15 – Version 1.5<br /><br /> Hinzufügen von "DFMode = 20;" zur Verbindungszeichenfolge bei Verwendung der **MSRemote** Anbieter kann die Leistung Ihres Servers verbessern, beim Aktualisieren von Daten. Mit dieser Einstellung wird die **RDSServer.DataFactory** Objekt auf dem Server verwendet einen Modus weniger ressourcenintensiv. Die folgenden Funktionen sind jedoch nicht in dieser Konfiguration verfügbar:<br /><br /> -Verwendung parametrisierter Abfragen.<br />-Abrufen-Parameter oder Spalte vor dem Aufruf der **Execute** Methode.<br />-Festlegen von **Transact Updates** auf **"true"**.<br />-Abrufen des Zeilenstatus.<br />-Aufrufen der **Resync** Methode.<br />-Aktualisieren (explizit oder automatisch) über die **Update Resync** Eigenschaft.<br />-Festlegen von **Befehl** oder **Recordset** Eigenschaften.<br />-Mithilfe von **AdCmdTableDirect**.|
|**Ereignishandler**|Gibt den Namen einer serverseitige Anpassung Programm (oder der Handler), die die Funktionalität des erweitert die [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), und alle Parameter, die vom Handler verwendete*,* getrennt durch Kommas ( ","). Ein **Zeichenfolge** Wert.|
|**Internet-Zeitüberschreitung.**|Gibt die maximale Anzahl von Millisekunden zu warten, bis eine Anforderung zum und vom Server zu übertragen. (Die Standardeinstellung ist 5 Minuten.)|
|**Remoteanbieter**|Gibt den Namen des Datenanbieters auf dem Remoteserver verwendet werden.|
|**Remoteserver**|Gibt an, das Serverprotokoll Name und die Kommunikation, die von dieser Verbindung verwendet werden. Diese Eigenschaft ist identisch mit der [RDS. DataContro](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt [Server](../../../ado/reference/rds-api/server-property-rds.md) Eigenschaft.|
|**Transact-Updates**|Bei Festlegung auf **"true"**, dieser Wert gibt an, dass [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) erfolgt auf dem Server, wird Sie innerhalb einer Transaktion ausgeführt. Der Standardwert für diese boolesche Eigenschaft für dynamische ist **"false"**.|

 Sie können auch beschreibbare dynamische Eigenschaften festlegen, durch deren Namen als Schlüsselwörter in der Verbindungszeichenfolge angeben. Legen Sie z. B. die **Internet-Zeitüberschreitung** dynamische Eigenschaft in fünf Sekunden, indem Sie angeben:

```
Dim cn as New ADODB.Connection
cn.Open "Provider=MS Remote;Internet Timeout=5000"
```

 Sie können auch festlegen oder Abrufen eine dynamische Eigenschaft durch Angabe ihres Namens als Index für die **Eigenschaften** Eigenschaft. Das folgende Beispiel zeigt, wie abgerufen und den aktuellen Wert der Drucken der **Internet-Zeitüberschreitung** dynamische Eigenschaft, und legen Sie anschließend einen neuen Wert:

```
Debug.Print cn.Properties("Internet Timeout")
cn.Properties("Internet Timeout") = 5000
```

## <a name="remarks"></a>Hinweise
 In ADO 2.0 konnte die OLE DB-Anbieter für Remoting nur in angegeben werden die *ActiveConnection* Parameter von der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt **öffnen** Methode. Beginnend mit ADO 2.1, der Anbieter kann auch angegeben werden der *"ConnectionString"* Parameter von der [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt **öffnen** Methode.

 Das Äquivalent der **RDS. DataControl** Objekt [SQL](../../../ado/reference/rds-api/sql-property.md) Eigenschaft ist nicht verfügbar. Die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt **öffnen** Methode *Quelle* Argument wird stattdessen verwendet.

 **Hinweis** angeben "...; Remote Provider = MS Remote;... "würde ein Szenario mit vier Ebenen erstellen. Szenarien mit mehr als drei Ebenen wurden nicht getestet und sollte nicht erforderlich sein.

## <a name="example"></a>Beispiel
 In diesem Beispiel führt eine Abfrage für die **Autoren** Tabelle mit den **Pubs** Datenbank auf einem Server mit dem Namen *Server*. Die Namen der remote-Datenquelle und Remoteserver finden Sie unter der [öffnen](../../../ado/reference/ado-api/open-method-ado-connection.md) Methode der[Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt und die SQL-Abfrage wird angegeben, der[öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) Methode von der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt. Ein **Recordset** Objekt zurückgegeben, bearbeitet und zum Aktualisieren der Datenquelle verwendet wird.

```
Dim rs as New ADODB.Recordset
Dim cn as New ADODB.Connection
cn.Open  "Provider=MS Remote;Data Source=pubs;" & _
         "Remote Server=http://YourServer"
rs.Open "SELECT * FROM authors", cn
...                'Edit the recordset
rs.UpdateBatch     'Equivalent of RDS SubmitChanges
...
```

## <a name="see-also"></a>Siehe auch
 [Übersicht über die OLE DB-Anbieter für Remoting](http://msdn.microsoft.com/en-us/4083b72f-68c4-4252-b366-abb70db5ca2b)
