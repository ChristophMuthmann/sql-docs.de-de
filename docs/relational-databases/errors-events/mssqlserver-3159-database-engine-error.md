---
title: MSSQLSERVER_3159 | Microsoft-Dokumentation
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
- 3159 (Database Engine error)
ms.assetid: c93c1003-0e3a-40aa-9873-44a0f5b8b57e
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2cbb7fbb13780dac80c8c8b4f4c38734df2f0f4a
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver3159"></a>MSSQLSERVER_3159
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Ereignis-ID|3159|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|LDDB_LOGNOTBACKEDUP|  
|Meldungstext|Das Protokollfragment für die "%ls"-Datenbank wurde nicht gesichert. Sichern Sie das Protokoll mit BACKUP LOG WITH NORECOVERY, falls es Daten enthält, die Sie nicht verlieren möchten. Verwenden Sie die WITH REPLACE- oder WITH STOPAT-Klausel der RESTORE-Anweisung, um den Inhalt des Protokolls zu überschreiben.|  
  
## <a name="explanation"></a>Erklärung  
In den meisten Fällen ist es bei Verwendung des vollständigen oder des massenprotokollierten Wiederherstellungsmodells in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erforderlich, das Protokollfragment zu sichern, um die Protokolldatensätze aufzuzeichnen, die noch nicht gesichert wurden. Eine Protokollsicherung des Protokollfragments, die unmittelbar vor einem Wiederherstellungsvorgang erstellt wurde, wird als Sicherung des Protokollfragments bezeichnet.  
  
Wenn Sie eine Datenbank bis zum Zeitpunkt des Fehlers wiederherstellen, ist die Sicherung des Protokollfragments im Wiederherstellungsplan die letzte relevante Sicherung. Wenn Sie das Protokollfragment nicht sichern können, kann eine Datenbank nur bis zum Ende der letzten Sicherung wiederhergestellt werden, die vor dem Fehler erstellt wurde.  
  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist es normalerweise erforderlich, eine Sicherung des Protokollfragments auszuführen, bevor die Wiederherstellung einer Datenbank gestartet wird. Durch die Sicherung des Protokollfragments wird Datenverlust verhindert und die Protokollkette intakt gehalten. Nicht für alle Wiederherstellungsszenarien ist jedoch eine Sicherung des Protokollfragments erforderlich. Es ist keine Sicherung des Protokollfragments erforderlich, wenn der Wiederherstellungspunkt in einer früheren Protokollsicherung enthalten ist oder wenn Sie die Datenbank verschieben oder ersetzen (überschreiben) und sie nicht für einen Zeitpunkt nach der letzten Sicherung wiederherstellen müssen. Wenn die Protokolldateien beschädigt sind und keine Sicherung des Protokollfragments erstellt werden kann, müssen Sie zudem die Datenbank ohne Verwendung einer Sicherung des Protokollfragments wiederherstellen. Dabei gehen alle Transaktionen verloren, die nach der letzten Protokollsicherung ausgeführt wurden. Weitere Informationen finden Sie im Folgenden unter „Wiederherstellen ohne Verwendung einer Sicherung des Protokollfragments“.  
  
> [!CAUTION]  
> REPLACE sollte selten und nur nach sorgfältiger Überlegung verwendet werden.  
  
## <a name="user-action"></a>Benutzeraktion  
Nehmen Sie eine Sicherung des Protokollfragments vor, und wiederholen Sie den Wiederherstellungsvorgang.  
  
Wenn Sie das Protokollfragment nicht sichern können, verwenden Sie in Ihren RESTORE-Anweisungen WITH STOPAT oder WITH REPLACE.  
  
## <a name="see-also"></a>Siehe auch  
[Wiederherstellen einer SQL Server-Datenbank zu einem bestimmten Zeitpunkt &#40;Full Recovery Model&#41;](~/relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
[Sichern des Transaktionsprotokolls bei beschädigter Datenbank &#40;SQL Server&#41;](~/relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
[Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](~/relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
[Sicherungen des Protokollfragments &#40;SQL Server&#41;](~/relational-databases/backup-restore/tail-log-backups-sql-server.md)  
  

