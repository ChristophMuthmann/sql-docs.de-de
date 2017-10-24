---
title: Speichern die XML-DOM-Objekt | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML DOM object [ADO], saving to
ms.assetid: 4d20fd28-aaf8-4232-83ce-f9d1e5f93dae
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eb4e758f1aeb83271bde3a515c1a44999199f668
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="saving-to-the-xml-dom-object"></a>Speichern der XML-DOM-Objekt
Ein Recordset können im XML-Format mit einer Instanz eines Objekts MSXML DOM gespeichert werden, wie im folgenden Visual Basic-Code dargestellt:  
  
```  
Dim xDOM As New MSXML.DOMDocument  
Dim rsXML As New ADODB.Recordset  
Dim sSQL As String, sConn As String  
  
sSQL = "SELECT customerid, companyname, contactname FROM customers"  
sConn="Provider=Microsoft.Jet.OLEDB.4.0;Data Source=D:\Program Files" & _  
        "\Common Files\System\msadc\samples\NWind.mdb"  
rsXML.Open sSQL, sConn  
rsXML.Save xDOM, adPersistADO   'Save Recordset directly into a DOM tree.  
...  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Beibehalten von Datensätzen im XML-Format](../../../ado/guide/data/persisting-records-in-xml-format.md)

