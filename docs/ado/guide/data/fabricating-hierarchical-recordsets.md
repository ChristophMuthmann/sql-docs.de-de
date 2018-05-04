---
title: Hierarchische Recordsets fabricating | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset fabrication [ADO]
- hierarchical Recordsets [ADO]
- fabricating hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: a584e642-a4a3-418e-bc20-3aff81a5625a
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e9301ec9204b5d2d6768f7487f279dd5f1eb0f6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="fabricating-hierarchical-recordsets"></a>Fabricating hierarchische Recordsets
Im folgende Beispiel wird gezeigt, wie ein hierarchisches Recordset ohne eine zugrunde liegende Datenquelle mithilfe der Daten strukturieren Grammatik zum Definieren von Spalten für die übergeordneten und untergeordneten sowie zwei Ebenen untergeordneten bereitzustellen **Recordsets**.  
  
 Eine hierarchische bereitzustellen **Recordset**, geben Sie die [Microsoft-Datenstrukturierungsdiensts für OLE DB (ADO-Dienstanbieter)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (MSDataShape), und Sie können angeben, einen Datenanbieter-Wert ' None ' in der Parameter der Verbindungszeichenfolge von der [öffnen](../../../ado/reference/ado-api/open-method-ado-connection.md) Methode der [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt. Weitere Informationen finden Sie unter [erforderlichen Anbieter für die Daten strukturieren](../../../ado/guide/data/required-providers-for-data-shaping.md).  
  
```  
Dim cn As New ADODB.Connection  
Dim rsCustomers As New ADODB.Recordset  
  
cn.Open "Provider=MSDataShape;Data Provider=NONE;"  
  
strShape = _  
"SHAPE APPEND NEW adInteger AS CustID," & _  
            " NEW adChar(25) AS FirstName," & _  
            " NEW adChar(25) AS LastName," & _  
            " NEW adChar(12) AS SSN," & _  
            " NEW adChar(50) AS Address," & _  
         " ((SHAPE APPEND NEW adChar(80) AS VIN_NO," & _  
                        " NEW adInteger AS CustID," & _  
                        " NEW adChar(20) AS BodyColor, " & _  
                     " ((SHAPE APPEND NEW adChar(80) AS VIN_NO," & _  
                                    " NEW adChar(20) AS Make, " & _  
                                    " NEW adChar(20) AS Model," & _  
                                    " NEW adChar(4) AS Year) " & _  
                        " AS VINS RELATE VIN_NO TO VIN_NO))" & _  
            " AS Vehicles RELATE CustID TO CustID) "  
  
rsCustomers.Open strShape, cn, adOpenStatic, adLockOptimistic, -1  
```  
  
 Sobald die **Recordset** wurde erstellt, es kann werden aufgefüllt, bearbeitet oder in einer Datei gespeichert.  
  
## <a name="see-also"></a>Siehe auch  
 [Zugreifen auf Zeilen in einem hierarchischen Recordset](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Formale Grammatik für Formen](../../../ado/guide/data/formal-shape-grammar.md)   
 [Erforderlichen Anbieter Daten können strukturiert werden.](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Form "APPEND-Klausel](../../../ado/guide/data/shape-append-clause.md)   
 [Shape-Befehle im Allgemeinen](../../../ado/guide/data/shape-commands-in-general.md)
