---
title: MSSQLSERVER_2516 | Microsoft-Dokumentation
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
- 2516 (Database Engine error)
ms.assetid: 79ed14b5-f53c-40c6-8334-8a083f732207
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c8ccf3ec56b38fa53290531aac17e966a23a5a8d
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver2516"></a>MSSQLSERVER_2516
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|2516|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBCC_REPAIR_DIFF_MAP_INVALIDATED|  
|Meldungstext|Die Reparatur hat das differenzielle Bitmuster für die NAME-Datenbank für ungültig erklärt. Die Kette differenzieller Sicherungen ist unterbrochen. Vor einer differenziellen Sicherung müssen Sie eine vollständige Datenbanksicherung ausführen.|  
  
## <a name="explanation"></a>Erklärung  
Diese Informationsmeldung wird zurückgegeben, wenn Fehler MSSQLEngine_2515 behoben wird.  
  
## <a name="user-action"></a>Benutzeraktion  
Führen Sie eine vollständige Datenbanksicherung aus.  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](~/relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  

