---
title: MSSQLSERVER_11409 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 11409 (Database Engine error)
ms.assetid: 99b71a1c-a72d-4ca9-9d00-4230c9042ba5
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 06919db12a917a28234a88c99f678f5a6b60a933
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver11409"></a>MSSQLSERVER_11409
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|11409|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|ALTERCOL_COLSET_DROP|  
|Meldungstext|Der '%.*ls'-Spaltensatz in der '%.\*ls'-Tabelle kann nicht entfernt werden, da die Tabelle mehr als 1025 Spalten enthält.|  
  
## <a name="explanation"></a>Erklärung  
Tabellen können maximal 1024 Spalten enthalten, die nicht als Spalte mit geringer Dichte oder berechnete Spalte festgelegt sind. Wenn die Tabelle aufgrund von Spalten mit geringer Dichte mehr als 1024 Spalten aufweist, muss für die Tabelle ein Spaltensatz definiert werden. Die Tabelle, auf die verwiesen wird, weist mehr als 1024 Spalten auf, und Sie haben versucht, den Spaltensatz zu entfernen.  
  
## <a name="user-action"></a>Benutzeraktion  
Mit den aktuellen Spalten in der Tabelle müssen Sie den Spaltensatz beibehalten.  
  
Zum Entfernen des Spaltensatzes entfernen Sie zunächst Spalten aus der Tabelle, bis nur noch 1024 Spalten enthalten sind. Dann können Sie den Spaltensatz entfernen.  
  

