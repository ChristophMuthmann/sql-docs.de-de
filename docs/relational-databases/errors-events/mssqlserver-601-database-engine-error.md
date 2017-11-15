---
title: MSSQLSERVER_601 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: "601"
helpviewer_keywords: 601 (Database Engine error)
ms.assetid: 2039cc0a-9a43-4369-a04a-935e384388b6
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: c878d848d4acb20a6805f654d66e71b1ad92a8f3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver601"></a>MSSQLSERVER_601
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|601|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name||  
|Meldungstext|Aufgrund von Datenverschiebungen konnte der Scanvorgang mit NOLOCK nicht fortgesetzt werden.|  
  
## <a name="explanation"></a>Erklärung  
Die Abfrage kann von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] nicht weiter ausgeführt werden, da versucht wird, Daten zu lesen, die durch eine andere Transaktion aktualisiert oder gelöscht wurden. Für die Abfrage wird der Sperrhinweis NOLOCK oder die Isolationsstufe für Transaktionen READ UNCOMMITTED verwendet.  
  
Normalerweise wird der Zugriff auf Daten verweigert, die durch eine andere Transaktion geändert wurden, da die Daten mit Sperren belegt werden. Mithilfe des Sperrhinweises NOLOCK und der Isolationsstufe für Transaktionen READ UNCOMMITTED können mit einer Abfrage jedoch Daten gelesen werden, die durch eine andere Transaktion gesperrt sind. Dies wird als Dirty Read bezeichnet, da Sie Werte lesen können, für die noch kein Commit ausgeführt wurde und an denen Änderungen vorgenommen werden.  
  
## <a name="user-action"></a>Benutzeraktion  
Durch diesen Fehler wird die Abfrage abgebrochen. Übermitteln Sie die Abfrage erneut, oder entfernen Sie den Sperrhinweis NOLOCK.  
  
## <a name="see-also"></a>Siehe auch  
[MSSQLSERVER_605](../../relational-databases/errors-events/mssqlserver-605-database-engine-error.md)  
[Tabellenhinweise &#40;Transact-SQL&#41;](~/t-sql/queries/hints-transact-sql-table.md)  
[SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)  
[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](~/t-sql/statements/set-transaction-isolation-level-transact-sql.md)  
  
