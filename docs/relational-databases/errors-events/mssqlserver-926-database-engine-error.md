---
title: MSSQLSERVER_926 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 926 (Database Engine error)
ms.assetid: 57e01668-883b-4be4-84a8-a111caaf0486
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 99cf8fb0d52b4fa9f2040cd5ec8338a3785a5dcd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver926"></a>MSSQLSERVER_926
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|926|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DB_SUSPECT|  
|Meldungstext|Die „%.*ls“-Datenbank kann nicht geöffnet werden. Sie wurde bei der Wiederherstellung als SUSPECT gekennzeichnet. Weitere Informationen finden Sie im SQL Server-Fehlerprotokoll.|  
  
## <a name="explanation"></a>Erklärung  
Diese Datenbank wurde aufgrund eines Fehlers beim Wiederherstellungsvorgang, bei dem eine Datenbank in einen konsistenten Transaktionszustand versetzt wird, als fehlerverdächtig gekennzeichnet. Dies kann während der folgenden Vorgänge auftreten:  
  
-   Beim Starten einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz.  
  
-   Beim Anfügen einer Datenbank  
  
-   Beim Verwenden der RESTORE-Datenbank oder der RESTORE LOG-Prozeduren.  
  
## <a name="user-action"></a>Benutzeraktion  
Überprüfen Sie das Fehlerprotokoll von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und ermitteln Sie die Ursache für den Fehler. Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seit dem Fehler bei der Wiederherstellung erneut gestartet wurde, sehen Sie in vorherigen Fehlerprotokollen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nach, um den Grund für den Fehler bei der Wiederherstellung zu ermitteln.  
  
Wenn der Fehler bei der Wiederherstellung auf einen E/A-Fehler, eine zerrissene Seite oder ein Hardwareproblem zurückzuführen ist, beheben Sie das zugrunde liegende Hardwareproblem, und stellen Sie die Datenbank mithilfe einer Sicherung wieder her. Wenn keine Sicherungen vorhanden sind, können Sie die Reparaturoptionen von DBCC CHECKDB verwenden.  
  
Wenden Sie sich an Ihren primären Anbieter für technischen Support, wenn Sie das Problem nicht selbst beheben können. Halten Sie das Fehlerprotokoll für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur Überprüfung bereit.  
  
## <a name="see-also"></a>Siehe auch  
[Sichern und Wiederherstellen von SQL Server-Datenbanken](~/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
[sys.sysdatabases &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)  
[Anfügen und Trennen von Datenbanken &#40;SQL Server&#41;](~/relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
