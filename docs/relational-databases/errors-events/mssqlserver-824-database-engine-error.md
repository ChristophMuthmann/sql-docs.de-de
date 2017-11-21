---
title: MSSQLSERVER_824 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 824 (Database Engine error)
ms.assetid: 2aa22246-2712-4fdb-9744-36e7e6f3175e
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 95ecf5e2bf8a43eb46e14281d356a2b029b0b490
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver824"></a>MSSQLSERVER_824
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|824|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|B_HARDSSERR|  
|Meldungstext|SQL Server hat einen logischen, konsistenzbasierten E/A-Fehler gefunden: %ls Der Fehler ist beim %S_MSG von Seite %S_PGID in der Datenbank mit der ID %d bei Offset %#016I64x in der Datei '%ls' aufgetreten.  Weitere Informationen finden Sie möglicherweise in anderen Fehlermeldungen im SQL Server-Fehlerprotokoll oder im Systemereignisprotokoll.|  
  
## <a name="explanation"></a>Erklärung  
Mit diesem Fehler wird angegeben, dass in Windows eine Meldung ausgegeben wurde, gemäß der die Seite erfolgreich vom Datenträger gelesen, aber in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Fehler auf der Seite festgestellt wurde. Dieser Fehler ist mit dem Fehler 823 vergleichbar, nur wurde er nicht von Windows erkannt. Dies führt in der Regel zu einem Problem im E/A-Subsystem. Dazu gehören beispielsweise der Ausfall von Festplattenlaufwerken, Firmwareprobleme auf Datenträgern, fehlerhafte Gerätetreiber usw. Weitere Informationen zu E/A-Fehlern finden Sie unter [Microsoft SQL Server I/O Basics, Chapter 2 (Microsoft SQL Server - Grundlagen zur E/A, Kapitel 2)](http://go.microsoft.com/fwlink/?LinkId=69370).  
  
## <a name="user-action"></a>Benutzeraktion  
  
### <a name="look-for-hardware-failure"></a>Hardwarefehlersuche  
Führen Sie eine Hardwarediagnose aus, und beheben Sie alle Probleme. Überprüfen Sie auch das Systemprotokoll und das Anwendungsprotokoll von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows sowie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll, um festzustellen, ob der Fehler aufgrund eines Hardwarefehlers aufgetreten ist. Beheben Sie alle hardwarebedingten Probleme, die in den Protokollen enthalten sind.  
  
Lagern Sie verschiedene Hardwarekomponenten aus, um das Problem zu isolieren, falls Beschädigungsprobleme bei permanenten Daten auftreten. Stellen Sie sicher, dass beim System der Schreibcache auf dem Datenträgercontroller nicht aktiviert ist. Wenden Sie sich an Ihren Hardwarehersteller, falls Sie beim Schreibcache das Problem vermuten.  
  
Letztendlich kann es vorteilhaft sein, wenn Sie zu einem neuen Hardwaresystem wechseln. Der Wechsel kann die Neuformatierung der Laufwerke und eine Neuinstallation des Betriebssystems beinhalten.  
  
### <a name="restore-from-backup"></a>Sicherungswiederherstellung  
Wenn das Problem nicht hardwarebedingt ist und eine bekanntermaßen fehlerfreie Sicherung zur Verfügung steht, stellen Sie die Datenbank mithilfe der Sicherung wieder her.  
  
Ändern Sie die Datenbanken so, dass Sie die PAGE_VERIFY CHECKSUM-Option verwenden können. Weitere Informationen zu PAGE_VERIFY finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="see-also"></a>Siehe auch  
[Verwalten der suspect_pages-Tabelle &#40;SQL Server&#41;](~/relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  

