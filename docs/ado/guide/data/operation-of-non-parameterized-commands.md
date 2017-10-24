---
title: Von nicht parametrisierten Befehlen | Microsoft Docs
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
- non-parameterized commands [ADO]
- data shaping [ADO], non-parameterized commands
ms.assetid: 9700e50a-9f17-4ba3-8afb-f750741dc6ca
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0a19b939b0b0eb33d436a3924a04562473b4c06a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="operation-of-non-parameterized-commands"></a>Von nicht parametrisierten Befehlen
Für nicht parametrisierte Befehle werden alle Anbieterbefehle ausgeführt und die **Recordsets** werden während der Ausführung des Befehls erstellt. Wenn der Befehl synchron ausgeführt wird alle der **Recordsets** vollständig aufgefüllt. Wenn ein asynchrone Auffüllungsmodus ausgewählt wurde, den Auffüllungsstatus der der **Recordsets** hängt von der Auffüllungsmodus und die Größe des der **Recordsets**.  
  
 Z. B. die *übergeordneten-Befehl* Zurückgeben einer **Recordset** von Kunden für ein Unternehmen aus einer Customers-Tabelle und die *untergeordnete-Befehl* konnte eine zurückgeben**Recordset** der Aufträge für alle Kunden aus einer Orders-Tabelle.  
  
```  
SHAPE {SELECT * FROM Customers}   
   APPEND ({SELECT * FROM Orders} AS chapOrders   
   RELATE customerID TO customerID)  
```  
  
 Für jeden über- und untergeordneten nicht parametrisierten über-und untergeordneten Beziehungen **Recordset** Objekt benötigen eine Spalte gemeinsam, um diese zu verknüpfen. Die Spalten sind in der RELATE-Klausel, mit dem Namen *übergeordnete Spalte* erste und dann *untergeordnete Spalte*. Die Spalten möglicherweise andere Namen in ihren jeweiligen **Recordset** Objekte, sondern muss auf die gleichen Informationen verweisen, um eine sinnvolle Beziehung anzugeben. Z. B. die **Kunden** und **Aufträge Recordset** Objekte konnte eine Feldes "KundenID" verfügen. Da die Mitgliedschaft des untergeordneten Elements **Recordset** richtet sich nach der Anbieterbefehl, der untergeordnete **Recordset** verwaiste Zeilen enthalten kann. Diese verwaisten Zeilen werden ohne zusätzliche umformen kann nicht zugegriffen.  
  
 Fügt an eine Kapitelspalte Strukturieren von Daten an das übergeordnete Element **Recordset**. Die Werte in der Kapitelspalte sind Verweise auf Zeilen im untergeordneten **Recordset**, die die RELATE-Klausel erfüllen. Also der gleiche Wert ist der *übergeordnete Spalte* einer angegebenen übergeordneten Zeile unverändert in die *untergeordnete Spalte* aller Zeilen des untergeordneten Elements Kapitel. Wenn mehrere TO-Klauseln in der gleichen RELATE-Klausel verwendet werden, werden sie implizit die mit einem AND-Operator kombiniert. Wenn die übergeordneten Spalten in der RELATE-Klausel keinen Schlüssel für das übergeordnete Element nicht darstellen **Recordset**, eine einzelne untergeordnete Zeile mehrere übergeordnete Zeilen haben kann.  
  
 Wenn Sie den Verweis in der Kapitelspalte zugreifen, ADO übernimmt die **Recordset** durch den Verweis dargestellt. Beachten Sie, dass zwar in einem nicht parametrisierten Befehl oder das gesamte untergeordnete **Recordset** wurde abgerufen wurden, zeigt das Kapitel nur eine Teilmenge von Zeilen.  
  
 Wenn die angefügte Spalte keine enthält *Kapitel-Alias*, ein Namen wird automatisch für sie generiert werden. Ein [Feld](../../../ado/reference/ado-api/field-object.md) -Objekt für die Spalte angefügt wird die **Recordset** des Objekts [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung und die Angabe des Datentyps werden **AdChapter**.  
  
 Informationen zum Navigieren in einer hierarchischen **Recordset**, finden Sie unter [zugreifen auf Zeilen in einem hierarchischen Recordset](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Daten strukturiert werden, Beispiel](../../../ado/guide/data/data-shaping-example.md)   
 [Formale Grammatik für Formen](../../../ado/guide/data/formal-shape-grammar.md)   
 [Shape-Befehle im Allgemeinen](../../../ado/guide/data/shape-commands-in-general.md)

