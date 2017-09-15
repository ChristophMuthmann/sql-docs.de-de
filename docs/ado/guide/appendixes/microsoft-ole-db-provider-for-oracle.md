---
title: "Microsoft OLE DB-Anbieter für Oracle | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d92236375a3ac152dbe7f5a2f259ce2a5f2edb79
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Microsoft OLE DB-Anbieter für Oracle (Übersicht)
> [!IMPORTANT]
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den Oracle OLE DB-Anbieter.

 Der Microsoft OLE DB-Anbieter für Oracle ermöglicht ADO auf Oracle-Datenbanken zugreifen.

## <a name="connection-string-parameters"></a>Parameter für Verbindungszeichenfolgen
 Zur Verbindung mit diesem Anbieter Festlegen der *Anbieter* Argument der ["ConnectionString"](../../../ado/reference/ado-api/connectionstring-property-ado.md) Eigenschaft:

```
MSDAORA
```

 Lesen der [Anbieter](../../../ado/reference/ado-api/provider-property-ado.md) Eigenschaft wird auch dieser Zeichenfolge zurück.

 Wenn es sich bei eine Join-Abfrage mit einem Keyset oder dynamic-Cursor in einer Oracle-Datenbank ausgeführt wird, tritt ein Fehler auf. Oracle unterstützt nur einen statische schreibgeschützte Cursor.

## <a name="typical-connection-string"></a>Typische Verbindungszeichenfolge
 Eine typische Verbindungszeichenfolge für diesen Anbieter ist:

```
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 Die Zeichenfolge, die dieser Schlüsselwörter besteht aus:

|Schlüsselwort|Description|
|-------------|-----------------|
|**Anbieter**|Gibt die OLE DB-Anbieter für Oracle.|
|**Datenquelle**|Gibt den Namen eines Servers.|
|**Benutzer-ID**|Gibt den Benutzernamen an.|
|**Kennwort**|Gibt das Kennwort des Benutzers an.|

> [!NOTE]
>  Wenn Sie ein Datenquellenanbieter, die Windows-Authentifizierung unterstützt Verbindung, müssen Sie angeben **Trusted_Connection = Yes** oder **Integrated Security = SSPI** anstelle von Benutzer-ID und Kennwort die Informationen in der Verbindungszeichenfolge angegeben.

## <a name="provider-specific-connection-parameters"></a>Anbieterspezifische Verbindungsparameter
 Der Anbieter unterstützt zusätzlich zu den von ADO definierten verschiedene anbieterspezifische Verbindungsparameter. Mit den Eigenschaften der ADO-Verbindung dieser Anbieter-spezifischen Eigenschaften festgelegt werden können, über die [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung von einer [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) oder als Teil der **"ConnectionString"**.

 Diese Parameter sind vollständig beschrieben, in der [OLE DB Programmer's Reference](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8). Die [ADO dynamische Property-Index](../../../ado/reference/ado-api/ado-dynamic-property-index.md) bietet einen Querverweis zwischen diesen Parameternamen und den entsprechenden OLE DB-Eigenschaften.

|Parameter|Description|
|---------------|-----------------|
|**Das Fensterhandle**|Gibt das Fensterhandle verwenden, um zusätzliche Informationen aufzufordern.|
|**Locale Identifier**|Gibt eine eindeutige 32-Bit-Zahl (z. B. 1033), die angibt, Einstellungen, die im Zusammenhang mit der Sprache des Benutzers an. Diese Einstellungen anzugeben, wie Datums- und Uhrzeitangaben formatiert sind, Elemente alphabetisch sortiert sind, die Zeichenfolgen verglichen werden und so weiter.|
|**OLE DB-Dienste**|Gibt an, eine Bitmaske, die angibt, OLE DB-Dienste zum Aktivieren oder deaktivieren.|
|**Auffordern**|Gibt an, ob den Benutzer aufgefordert, während eine Verbindung erstellt werden.|
|**Erweiterte Eigenschaften**|Eine Zeichenfolge mit anbieterspezifischen erweiterten Verbindungsinformationen. Verwenden Sie diese Eigenschaft nur für anbieterspezifische Verbindungsinformationen, die über den Eigenschaftenmechanismus beschrieben werden kann.|

## <a name="see-also"></a>Siehe auch
 [ConnectionString-Eigenschaft (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [Anbietereigenschaft (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

