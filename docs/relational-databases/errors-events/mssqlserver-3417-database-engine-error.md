---
title: MSSQLSERVER_3417 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 3417 (Database Engine error)
ms.assetid: 005829c8-cf57-4828-818a-bbe8ee2e00f0
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: c97cd13d12af2fbfc4c0bb413b36e25b6fba87cd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver3417"></a>MSSQLSERVER_3417
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|3417|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|REC_BADMASTER|  
|Meldungstext|Die master-Datenbank kann nicht wiederhergestellt werden. SQL Server kann nicht ausgeführt werden. Stellen Sie die master-Datenbank von einer vollständigen Sicherung wieder her, reparieren Sie sie, oder erstellen Sie sie neu. Weitere Informationen zum Neuerstellen der master-Datenbank finden Sie in der SQL Server-Onlinedokumentation.|  
  
## <a name="explanation"></a>Erklärung  
Die **master**-Datenbank kann von SQL Server nicht gestartet werden. Wenn die Datenbanken **master** oder **tempdb** nicht in den Onlinemodus gebracht werden können, kann SQL Server nicht ausgeführt werden. Diesem Fehler sind normalerweise andere Fehler vorausgegangen. Überprüfen Sie die Fehlerprotokolle, um die eigentliche Ursache des Fehlers zu finden.  
  
## <a name="user-action"></a>Benutzeraktion  
Stellen Sie eine Sicherung der Datenbank wieder her, oder reparieren Sie die Datenbank.  
  
