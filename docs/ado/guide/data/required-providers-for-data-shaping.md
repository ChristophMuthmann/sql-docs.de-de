---
title: "Anbieter für die Strukturierung der Daten erforderlichen | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], data shaping
- data shaping [ADO], providers required
ms.assetid: d49d48d2-ac2d-4c11-895c-5a149b444620
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 123bcb546cabae6895dac5fbf9edd06b97e9400b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="required-providers-for-data-shaping"></a>Erforderlichen Anbieter Daten können strukturiert werden.
Strukturieren von Daten erfordert in der Regel zwei Anbieter. Der Dienstanbieter [-Datenstrukturierungsdiensts für OLE DB-](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md), liefert die Daten strukturieren, Funktionalität und einen Datenanbieter, z. B. der OLE DB-Anbieter für SQL Server, liefert Sie Zeilen mit Daten zum Auffüllen des geformten [Recordset ](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 Der Name des Dienstanbieters (MSDataShape) kann angegeben werden, als Wert des der [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt [Anbieter](../../../ado/reference/ado-api/provider-property-ado.md) Eigenschaft oder das-Schlüsselwort der Verbindungszeichenfolge "Provider = MSDataShape;".  
  
 Der Name des Datenanbieters kann angegeben werden, als Wert des der **Datenanbieter** dynamische Eigenschaft, die hinzugefügt wird die **Verbindung** Objekt [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung nach die-Datenstrukturierungsdiensts für OLE DB oder das-Schlüsselwort der Verbindungszeichenfolge "**Datenanbieter =***Anbieter*".  
  
 Kein Datenanbieter ist erforderlich, wenn die **Recordset** wird nicht aufgefüllt (z. B. wie eine erstellte **Recordset** , in denen Spalten mit dem NEW-Schlüsselwort erstellt werden). Geben Sie in diesem Fall "**Datenanbieter =**none;".  
  
## <a name="example"></a>Beispiel  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Daten strukturiert werden, Beispiel](../../../ado/guide/data/data-shaping-example.md)   
 [Formale Grammatik für Formen](../../../ado/guide/data/formal-shape-grammar.md)   
 [Shape-Befehle im Allgemeinen](../../../ado/guide/data/shape-commands-in-general.md)
