---
title: MSSQLSERVER_2527 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2527 (Database Engine error)
ms.assetid: 1cef90ef-9c39-44e6-bc7f-316c8f53c10c
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4bdf98e0beaed65cac6cd792646bf7441ee5d4fd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver2527"></a>MSSQLSERVER_2527
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|2527|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBCC_INDEX_FILEGROUP_IS_OFFLINE|  
|Meldungstext|Der I_NAME-Index der O_NAME-Tabelle kann nicht bearbeitet werden, da die Dateigruppe F_NAME offline ist.|  
  
## <a name="explanation"></a>Erklärung  
Diese Informationsmeldung gibt an, dass der Index nicht überprüft werden kann, da eine der Dateigruppen, die die Daten für den Index speichert, offline ist. Der Status der Dateien in einer Dateigruppe legt die Verfügbarkeit der gesamten Dateigruppe fest. Damit eine Dateigruppe verfügbar ist, müssen alle Dateien in der Dateigruppe online sein. Wenn keine weiteren Probleme vorhanden sind, werden alle anderen Indizes des gleichen Objekts überprüft.  
  
## <a name="user-action"></a>Benutzeraktion  
Wenn Sie den Status der Dateien für die angegebene Dateigruppe anzeigen möchten, verwenden Sie die **sys.database_files**- oder **sys.master_files**-Katalogsicht.  
  
Stellen Sie die Offlinedatei aus einer Sicherung wieder her.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[sys.database_files &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[sys.master_files &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  
