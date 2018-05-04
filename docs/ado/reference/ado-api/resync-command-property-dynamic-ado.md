---
title: Resync-Befehl Eigenschaft dynamisch (ADO) | Microsoft Docs
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
apitype: COM
helpviewer_keywords:
- Resync Command property [ADO]
ms.assetid: 4e2bb601-0fe8-4d61-b00e-38341d85a6bb
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 240c4d6ce4aa392f01ebb27a4a52fd73c684b981
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="resync-command-property-dynamic-ado"></a>Resync-Befehl Eigenschaft dynamisch (ADO)
Gibt an, ein Befehl Benutzer bereitgestellte Zeichenfolge, die [Resync](../../../ado/reference/ado-api/resync-method.md) Probleme der Methode zum Aktualisieren der Daten in der Tabelle mit dem Namen der [eindeutige Tabelle](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) dynamische Eigenschaft.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **Zeichenfolge** Wert, der eine Befehlszeichenfolge ist.  
  
## <a name="remarks"></a>Hinweise  
 Die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt ist das Ergebnis einer JOIN-Operation, die auf mehrere Basistabellen ausgeführt. Hängen von den betroffenen Zeilen die *AffectRecords* Parameter von der [Resync](../../../ado/reference/ado-api/resync-method.md) Methode. Der Standard **Resync** Methode wird ausgeführt, wenn die [eindeutige Tabelle](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) und **Resync Command** keine Eigenschaften festgelegt werden.  
  
 Der Befehlszeichenfolge von der **Resync Command** Eigenschaft ist ein parametrisierter Befehl oder gespeicherte Prozedur, die die zu aktualisierende Zeile eindeutig identifiziert und gibt eine einzelne Zeile mit die gleiche Anzahl und Reihenfolge der Spalten der Zeile sein aktualisiert. Die Befehlszeichenfolge enthält einen Parameter für jede Primärschlüsselspalte in der **eindeutige Tabelle**ist, andernfalls ein Laufzeitfehler wird zurückgegeben. Die Parameter sind mit Primärschlüsselwerten aus der Zeile aktualisiert werden automatisch ausgefüllt.  
  
 Hier sind zwei Beispiele, die basierend auf SQL an:  
  
 1\) der **Recordset** wird durch einen Befehl definiert:  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 Die **Resync Command** Eigenschaft auf festgelegt ist:  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 Die **eindeutige Tabelle** ist *Aufträge* und dem Primärschlüssel *OrderID*, parametrisiert wird. Die Unterauswahl bietet eine einfache Möglichkeit zum programmgesteuerten stellen Sie sicher, dass die gleiche Anzahl und Reihenfolge der Spalten von den ursprünglichen Befehl zurückgegeben werden.  
  
 2\) der **Recordset** wird durch eine gespeicherte Prozedur definiert:  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 Die **Resync** Methode sollte die folgende gespeicherte Prozedur ausführen:  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 Die **Resync Command** Eigenschaft auf festgelegt ist:  
  
```  
"{call CustordersResync (?)}"  
```  
  
 Noch einmal: die **eindeutige Tabelle** ist *Aufträge* und dem Primärschlüssel *OrderID*, parametrisiert wird.  
  
 **Resync-Befehl** ist eine dynamische Eigenschaft angefügt die **Recordset** Objekt [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung bei der [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft auf festgelegtist**AdUseClient**.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
