---
title: Weitere Möglichkeiten zum Verschieben in einem Recordset | Microsoft Docs
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
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- Recordset object [ADO], moving
- MovePrevious method [ADO]
ms.assetid: 9f8cf1b2-3def-453f-a0ff-4646c5f15262
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4fec2b2c8fa338f6f9e05c4dab5e2732e3f270ba
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="more-ways-to-move-in-a-recordset"></a>Weitere Möglichkeiten zum Verschieben in einem Recordset
Die folgenden vier Methoden werden zum Verschieben oder einen Bildlauf in der **Recordset**: [MoveFirst, MoveLast, MoveNext und MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md). (Einige dieser Methoden sind für Vorwärtscursor nicht verfügbar.)  
  
 **MoveFirst** ändert die Position des aktuellen Datensatzes auf den ersten Eintrag in der **Recordset**. **MoveLast** Aufzeichnen von Änderungen, die bis zum letzten positionieren Sie der aktuelle Datensatz in der **Recordset**. Mit **MoveFirst** oder **MoveLast**, **Recordset** Objekt muss Lesezeichen oder Bewegung des Cursors nach hinten unterstützen; andernfalls wird der Methodenaufruf ein Fehler generiert.  
  
 **MoveNext** den aktuellen Datensatz positionieren zentral vorwärts verschoben. Zeichnen Sie bei der letzten beim Aufruf **MoveNext**, **EOF** festgelegt, um **"true"**. **MovePrevious** positionieren Sie der aktuelle Datensatz zentral rückwärts bewegt. Wenn Sie beim Aufrufen des ersten Datensatzes arbeiten **MovePrevious**, **BOF** festgelegt, um **"true"**. Es ist ratsam, überprüfen Sie die **EOF** und **BOF** Eigenschaften, die bei Verwendung dieser Methoden und den Cursor wieder eine gültige Position des aktuellen Datensatzes verschieben, wenn Sie sich über das Ende des Verschieben der **Recordset**, wie hier gezeigt:  
  
```  
. . .  
oRs.MoveNext  
If oRs.EOF Then oRs.MoveLast  
. . .   
```  
  
 Oder, im Fall von der **MovePrevious** Methode:  
  
```  
. . .   
oRs.MovePrevious  
If oRs.BOF Then oRs.MoveFirst  
. . .  
```  
  
 In Fällen, in denen die **Recordset** gefiltert oder sortiert wurde und die Daten des aktuellen Datensatzes geändert werden, werden möglicherweise auch die Position ändern. In solchen Fällen das **MoveNext** Methode funktioniert normal, aber beachten Sie, dass die Position verschoben wird vorwärts aus die neue Position, nicht die alte Position aufzeichnen. Ändern Sie die Daten in den aktuellen Datensatz z. B., dass der Datensatz an das Ende der sortierten verschoben wird **Recordset**, würde bedeuten, dass der Aufruf **MoveNext** führt zu ADO, wenn des aktuellen Datensatzes auf der die Position hinter dem letzten Datensatz in der **Recordset** (**EOF** = **"true"**).  
  
 Das Verhalten der verschiedenen Methoden der Verschiebung der **Recordset** Objekt abhängig ist, in gewissem Umfang für die Daten innerhalb der **Recordset**. Neue Einträge hinzugefügt, um die **Recordset** werden zunächst in einer bestimmten Reihenfolge, die von der Datenquelle definiert ist und möglicherweise implizit abhängige oder explizit auf die Daten im neuen Datensatz hinzugefügt. Z. B. wenn eine Sortierung oder ein Join erfolgt innerhalb der Abfrage, die füllt die **Recordset**, wird der neue Datensatz eingefügt werden, in die gewünschte Position im die **Recordset**. Wenn die Sortierung nicht explizit angegeben werden beim Erstellen der **Recordset**, Änderungen in der Data Source-Implementierung möglicherweise die Reihenfolge der zurückgegebenen Zeilen versehentlich ändern. In hinzufügen, die Sortierung, Filterung und Bearbeitungsfunktionen von der **Recordset** können die Reihenfolge beeinflussen und möglicherweise die Zeilen im Recordset angezeigt werden.  
  
 Aus diesem Grund **MoveNext**, **MovePrevious**, **MoveFirst**, **MoveLast**, und **verschieben** sind alle vertraulich an andere Vorgänge ausgeführt werden, auf dem gleichen **Recordset**. ADO wird immer versucht, auf die aktuelle Position beizubehalten, bis Sie explizit verschieben, aber in manchen Fällen beteiligten Änderungen es schwierig ist, die Auswirkungen einer nachfolgenden Verschiebung verstehen. Angenommen, Sie rufen **MoveFirst** Position in der ersten Zeile von einer sortierten **Recordset** und Sie nicht die Sortierung von aufsteigend, absteigend ändern, können Sie weiterhin in der gleichen Zeile – aber jetzt ist die letzte Zeile in der **Recordset**. **MoveFirst** gelangen Sie zu einer anderen Zeile (die neue erste Zeile).  
  
 Ein weiteres Beispiel: Wenn Sie auf eine bestimmte Zeile in der Mitte des positioniert sind eine **Recordset** und rufen Sie **löschen** und rufen Sie anschließend **MoveNext**, Sie sind jetzt im Datensatz unmittelbar nach der gelöschte Datensatz. Aber aufrufenden **MovePrevious** wird der Datensatz, der vor dem Sie den aktuellen Datensatz gelöscht, da der gelöschte Datensatz nicht mehr in der aktiven Mitgliedschaft gezählt wird die **Recordset**.  
  
 Es ist besonders schwierig, konsistente Move-Semantik für alle Anbieter für Methoden definieren, die relativ zum aktuellen Datensatz wechseln – **MovePrevious**, **MoveNext**, und **Verschieben** – beim Ändern von Daten im aktuellen Datensatz. Wenn Sie mit einer sortierten arbeiten, z. B. gefiltert **Recordset**, und ändern Sie die Daten im aktuellen Datensatz, sodass sich alle Datensätze davor würde jedoch die geänderten Daten auch nicht mehr dem Filter entspricht, wo nicht eindeutig eine **MoveNext** Vorgang sollte Sie dauern. Die sicherste Schlussfolgerung ist diese relative Bewegung innerhalb einer **Recordset** risikoreicher als absolute Bewegung ist (z. B. mit **MoveFirst** oder **MoveLast**) Wenn die Daten enthalten Ändern von während Datensätze bearbeitet werden, hinzugefügt oder gelöscht werden. Sortieren und Filtern sollte auf einen Primärschlüssel oder eine ID, basieren, da dieser Typ des Werts nicht geändert werden sollte.
