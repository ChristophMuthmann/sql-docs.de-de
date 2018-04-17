---
title: Binden von Ergebnis Resultsetspalten | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4bc9c30f-83ae-4766-a746-032953c187ad
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 107a89aeca70d7b28958c475994e3c41f417fa26
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="binding-result-set-columns"></a>Binden von Ergebnis Resultsetspalten
Anwendungen können binden, wie viele oder so wenig Spalten des Resultsets festgelegt werden, da sie auswählen, einschließlich überhaupt keine Spalten binden. Wenn eine Datenzeile abgerufen wird, gibt der Treiber die Daten für die gebundenen Spalten für die Anwendung zurück. Gibt an, ob die Anwendung aller Spalten im Resultset bindet, hängt von der Anwendung ab. Anwendungen, die Berichte in der Regel haben z. B. kein festes Format; solche Anwendungen ein Resultset mit allen der im Bericht verwendeten Spalten erstellen und dann binden und Abrufen der Daten für alle diese Spalten. Anwendungen, die vollständige Datenmenge in einigen Fällen Bildschirme ermöglicht dem Benutzer entscheiden, welche Spalten angezeigt; solche Anwendungen erstellen, ein Resultset mit allen Spalten, die der Benutzer möglicherweise werden soll, aber binden und Abrufen der Daten nur für diejenigen Spalten, die vom Benutzer ausgewählt wurde.  
  
 Daten können durch Aufrufen von nicht gebundenen Spalten abgerufen werden **SQLGetData**. Dies wird häufig aufgerufen, zum Abrufen von long-Daten, die häufig überschreitet die Länge von einem einzigen Puffer und in Teilen abgerufen werden muss.  
  
 Spalten können gebunden werden, jedoch jederzeit, auch nachdem Zeilen abgerufen wurden. Allerdings werden die neuen Bindungen erst beim nächsten Mal wirksam, die eine Zeile abgerufen wird; Sie sind nicht auf Daten aus bereits abgerufenen Zeilen angewendet.  
  
 Eine Variable bleibt an eine Spalte gebunden, bis eine andere Variable an die Spalte gebunden ist, bis die Spalte durch den Aufruf ungebunden ist **SQLBindCol** durch ein null-Zeiger als die Variable Adresse, bis alle Spalten aufgehoben werden, durch den Aufruf von **SQLFreeStmt** mit der Option SQL_UNBIND oder bis die Anweisung aufgehoben wird. Aus diesem Grund muss die Anwendung sicher sein, dass alle gebundene Variablen gültig bleiben, solange sie gebunden sind. Weitere Informationen finden Sie unter [Allocating und Freigeben von Puffern](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Da spaltenbindungen nur Informationen, die die Anweisung Struktur zugeordnet sind, können sie in beliebiger Reihenfolge festgelegt werden. Sie sind jedoch auch unabhängig von der Resultset. Nehmen wir beispielsweise an, dass eine Anwendung die Spalten des Resultsets generiert, indem Sie die folgende SQL-Anweisung gebunden:  
  
```  
SELECT * FROM Orders  
```  
  
 Wenn die Anwendung dann die SQL-Anweisung ausgeführt wird.  
  
```  
SELECT * FROM Lines  
```  
  
 auf dem gleichen Anweisungshandle sind die spaltenbindungen für das erste Resultset immer noch wirksam, da die Bindungen in der Anweisung Struktur gespeichert sind. In den meisten Fällen wird einem schlechten Programmierstil es sollte vermieden werden. Stattdessen sollte die Anwendung aufrufen **SQLFreeStmt** mit der Option SQL_UNBIND, trennen die alte Spalten und dann binden Sie neue.
