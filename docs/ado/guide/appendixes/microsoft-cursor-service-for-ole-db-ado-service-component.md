---
title: "Microsoft Cursordiensts für OLE DB (ADO-Dienstkomponente) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9ba0513f0a450a57e4d25088f16d96398af9f936
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>Microsoft Cursor Service für OLE DB-Übersicht
Der Microsoft Cursor Service für OLE DB ergänzt die Cursorfunktionen der Unterstützung von Datenanbietern. Daher nimmt der Benutzer relativ einheitliche Funktionalität von allen Datenanbietern.

 Der Cursor-Dienst stellt die dynamische Eigenschaften zur Verfügung und verbessert das Verhalten bestimmter Methoden. Z. B. die [optimieren](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) dynamische Eigenschaft ermöglicht das Erstellen temporärer Indizes, um bestimmte Vorgänge wie z. B. erleichtern die [suchen](../../../ado/reference/ado-api/find-method-ado.md) Methode.

 Der Cursor-Dienst ermöglicht die Unterstützung für BatchUpdates in allen Fällen. Es simuliert auch leistungsfähigere Cursortypen, wie dynamische Cursor, wenn ein Datenanbieter nur weniger leistungsfähige Cursor, wie statische Cursor bereitstellen kann.

## <a name="keyword"></a>Schlüsselwort
 Um diese Dienstkomponente aufzurufen, legen die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oder [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) des Objekts [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft **AdUseClient**.

```
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>Dynamische Eigenschaften
 Wenn der Cursor Service für OLE DB aufgerufen wird, die folgenden dynamischen Eigenschaften hinzugefügt werden die **Recordset** des Objekts [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung. Die vollständige Liste der **Verbindung** und **Recordset** dynamische Objekteigenschaften abgelesen werden die [ADO dynamische Property-Index](../../../ado/reference/ado-api/ado-dynamic-property-index.md). Die zugeordneten OLE DB-Eigenschaftennamen sind gegebenenfalls in Klammern nach dem Namen des ADO-Eigenschaft enthalten.

 Änderungen an einige dynamischen Eigenschaften sind nicht mit der zugrunde liegenden Datenquelle sichtbar, nachdem der Cursor-Dienst aufgerufen wurde. Z. B. die *Befehlstimeout* Eigenschaft auf einen **Recordset** werden nicht an den zugrunde liegenden Datenanbieter angezeigt.

```

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 Wenn Ihre Anwendung die Cursor-Dienst erfordert, jedoch müssen Sie die dynamischen Eigenschaften für den zugrunde liegenden Anbieter festlegen, legen Sie die Eigenschaften vor dem Aufrufen der Cursor-Diensts. Befehl Objekt eigenschafteneinstellungen werden immer an den zugrunde liegenden Datenanbieter unabhängig von der Cursorposition übergeben. Aus diesem Grund können Sie auch ein Command-Objekt zum Festlegen der Eigenschaften zu einem beliebigen Zeitpunkt verwenden.

> [!NOTE]
>  Die dynamische Eigenschaft DBPROP_SERVERDATAONINSERT wird vom Cursordienst nicht unterstützt, auch wenn es vom zugrunde liegenden Datenanbieter unterstützt wird.

|Eigenschaftsname|Description|
|-------------------|-----------------|
|Auto Recalc (DBPROP_ADC_AUTORECALC)|Für Recordsets erstellt mit dem-Datenstrukturierungsdiensts dieser Wert gibt an, wie oft werden berechnete und aggregierte Spalten berechnet. Die Standardeinstellung (Wert = 1) ist, neu zu berechnen, bei jedem-Datenstrukturierungsdiensts bestimmt, dass die Werte geändert haben. Wenn der Wert 0 ist, werden die berechneten oder aggregierten Spalten nur berechnet, wenn die Hierarchie anfänglich basiert.|
|Batchgröße (DBPROP_ADC_BATCHSIZE)|Gibt die Anzahl der updateanweisungen, die zusammengefasst werden können, bevor Sie mit dem Datenspeicher gesendet werden. Weitere Anweisungen in einem Batch, weniger Roundtrips an den Daten zu speichern.|
|Cache Child Rows (DBPROP_ADC_CACHECHILDROWS)|Für Recordsets, die mit dem Datendienst strukturiert werden, erstellt werden gibt dieser Wert an, ob untergeordneten Recordsets in einem Cache für die spätere Verwendung gespeichert werden.|
|Cursor Engine Version (DBPROP_ADC_CEVER)|Gibt die Version des Diensts Cursor verwendet wird.|
|Maintain Change Status (DBPROP_ADC_MAINTAINCHANGESTATUS)|Gibt den Text des Befehls zum erneuten Synchronisieren einer eine oder mehrere Zeilen in einer Verknüpfung aus mehreren Tabellen verwendet.|
|[Optimieren](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|Gibt an, ob ein Index erstellt werden soll. Bei Festlegung auf **"true"**, wird das temporäre Erstellen von Indizes, die die Ausführung bestimmter Vorgänge zu verbessern.|
|[Umstrukturieren von Namen](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Gibt den Namen der der **Recordset**. Können verwiesen wird, in der aktuellen oder nachfolgenden Daten strukturieren Befehle sein.|
|[Resync-Befehl](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Gibt eine benutzerdefinierte Befehlszeichenfolge, die von verwendet wird, an der [Resync](../../../ado/reference/ado-api/resync-method.md) Methode beim der [eindeutige Tabelle](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) Eigenschaft wirksam ist.|
|[Eindeutige Katalog](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Gibt den Namen der Datenbank mit der Tabelle verwiesen wird, der **eindeutige Tabelle** Eigenschaft.|
|[Eindeutiges Schema](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Gibt den Namen des Besitzers der Tabelle verwiesen wird, der **eindeutige Tabelle** Eigenschaft.|
|[Eindeutige Tabelle](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|Gibt den Namen der eine Tabelle in einer **Recordset** erstellt, die aus mehreren Tabellen, die von einfügungen, Updates oder Löschvorgänge geändert werden können.|
|Update Criteria (DBPROP_ADC_UPDATECRITERIA)|Gibt an, welche Felder in der **, in denen** Klausel werden zur Behandlung von Konflikten, die während einer Aktualisierung verwendet.|
|[Aktualisieren Sie die Neusynchronisierung](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) (DBPROP_ADC_UPDATERESYNC)|Gibt an, ob die **Resync** Methode wird implizit aufgerufen, nachdem die [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) -Methode (und sein Verhalten), wenn die **eindeutige Tabelle** Eigenschaft wirksam ist.|

 Sie können auch festlegen, oder rufen Sie eine dynamische Eigenschaft durch Angabe ihres Namens als Index für die **Eigenschaften** Auflistung. Beispielsweise erhalten und drucken Sie den aktuellen Wert der die [optimieren](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) dynamische Eigenschaft legen Sie dann einen neuen Wert wie folgt:

```
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>Integrierte Eigenschaftenverhalten
 Der Cursor Service für OLE DB-wirkt sich auch das Verhalten bestimmter integrierten Eigenschaften.

|Eigenschaftsname|Description|
|-------------------|-----------------|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|Ergänzen Sie die Typen von Cursorn, die für die verfügbaren einen **Recordset**.|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|Stellt eine Ergänzung der verfügbaren Typen von Sperren für eine **Recordset**. Aktiviert die batch-Updates.|
|[Sort](../../../ado/reference/ado-api/sort-property.md)|Gibt einen oder mehrere Feldnamen, die die **Recordset** sortiert ist und ob jedes Feld in aufsteigender oder absteigender Reihenfolge sortiert wird.|

## <a name="method-behavior"></a>Methodenverhalten
 Der Cursor-Dienst für OLE DB ermöglicht oder wirkt sich auf das Verhalten von der [Feld](../../../ado/reference/ado-api/field-object.md) des Objekts [Anfügen](../../../ado/reference/ado-api/append-method-ado.md) Methode und die **Recordset** des Objekts [öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), und [speichern](../../../ado/reference/ado-api/save-method.md) Methoden.
