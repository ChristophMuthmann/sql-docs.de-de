---
title: Ausrichtung | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- alignment issues [ODBC]
ms.assetid: 06a01e51-e7a5-495f-aa27-e304b0d005ff
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 527e8d47d4d352a0fad579d3c12c5ef3768c402b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="alignment"></a>Ausrichtung
Die, die in einer ODBC-Anwendung Ausrichtungsprobleme unterscheiden sich in der Regel nicht als bei einer anderen Anwendung. Das heißt, haben die meisten ODBC-Anwendungen nur wenige oder gar keine Probleme mit der Ausrichtung. Die Nachteile für die fehlende Ausrichtung von Adressen hängt von der Hardware und Betriebssystem und als kleinere als eine leichte Leistungseinbuße oder als ein schwerwiegender Laufzeitfehler wie Haupt-sein. Aus diesem Grund sollten ODBC-Anwendungen und portable ODBC-Anwendungen insbesondere darauf achten, dass die Daten ordnungsgemäß auszurichten sein.  
  
 Ein Beispiel für ODBC-Anwendungen Ausrichtungsprobleme, wenn auftreten ist, wenn sie einen großen Speicherblock zuordnen und andere Teile der, dass der Arbeitsspeicher auf die Spalten in einem Resultset zu binden. Dies liegt wahrscheinlich auftreten, wenn eine allgemeine Anwendung muss die Form eines Resultsets zur Laufzeit bestimmt und reservieren und Arbeitsspeicher entsprechend binden.  
  
 Nehmen wir beispielsweise an, die eine Anwendung führt eine **wählen** Anweisung vom Benutzer eingegeben werden und die Ergebnisse aus dieser Anweisung abgerufen. Da die Form des dieses Resultset nicht bekannt ist wenn die Anwendung geschrieben wird, muss die Anwendung den Typ der einzelnen Spalten bestimmen, nachdem das Resultset erstellt wurde und Arbeitsspeicher entsprechend zu binden. Die einfachste Möglichkeit hierzu besteht darin einen großen Speicherblock zuordnen und verschiedene Adressen in diesem Block den einzelnen Spalten binden. Für den Zugriff auf die Daten in einer Spalte, wandelt die Anwendung den Arbeitsspeicher für diese Spalte gebunden.  
  
 Das folgende Diagramm zeigt ein beispielresultset festgelegt, und wie ein Speicherblock, der mithilfe der Standard-C-Datentyp für jeden SQL-Datentyp gebunden werden kann. Jedes "X" stellt ein einzelnes Byte an Arbeitsspeicher. (Dieses Beispiel zeigt nur die Datenpuffern, die an Spalten gebunden sind. Dies geschieht aus Gründen der Einfachheit. In den tatsächlichen Code müssen die Längenindikator/Puffer auch ausgerichtet, werden führen.)  
  
 ![Binden von Standard-C-Datentyp in SQL-Datentyp](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 Die gebundenen Adressen vorausgesetzt werden gespeichert, der *Adresse* Array ist, verwendet die Anwendung die folgenden Ausdrücke für den Speicherzugriff an jede Spalte gebunden:  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 Beachten Sie, dass die Adressen gebunden wird, auf dem zweiten und dritten Spalten auf ungerade Byte starten und, dass die Adresse in die dritte Spalte gebunden nicht durch vier, also die Größe des ein SDWORD teilbar. Auf einigen Computern ist dies kein Problem, in anderen wird er dazu führen, dass eine leichte Leistungseinbuße; in anderen noch verursacht dies ein schwerwiegender Laufzeitfehler. Eine bessere Lösung wäre, die jede gebundene Adresse in seiner natürlichen Ausrichtungsgrenze auszurichten. Vorausgesetzt, dass dies 1 für eine UCHAR, 2 für eine SWORD und 4 für eine SDWORD ist würde dies zur Verfügung stellen des Ergebnis in der folgenden Abbildung, in denen ein "X" stellt ein Byte des Arbeitsspeichers, der verwendet wird und kein "O" stellt ein Byte des Arbeitsspeichers, der verwendet wird.  
  
 ![Bindung nach natürlichen Ausrichtungsgrenzen](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 Während dieser Lösung nicht den gesamten Arbeitsspeicher für die Anwendung verwenden, ist es nicht Ausrichtungsprobleme auftreten. Leider dauert es viel Code zur Implementierung dieser Lösung, wie jede Spalte einzeln nach Typ ausgerichtet sein muss. Eine einfachere Lösung besteht darin, alle Spalten auf die Größe des größten Ausrichtungsgrenzen, richten Sie die 4 ist im Beispiel in der folgenden Abbildung gezeigt.  
  
 ![Bindung nach größten Ausrichtungsgrenzen](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 Obwohl diese Lösung größere Löcher verlässt, wird der Code für die Implementierung relativ einfach und schnell. In den meisten Fällen UTC-offsets dies den Nachteil, nicht verwendeten Arbeitsspeicher bezahlt. Ein Beispiel, das diese Methode verwendet, finden Sie unter [SQLBindCol verwenden](../../../odbc/reference/develop-app/using-sqlbindcol.md).
