---
title: Schrittweise Wiederherstellung von Datenbanken mit speicheroptimierten Tabellen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 732c9721-8dd4-481d-8ff9-1feaaa63f84f
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b540d4b491980a57ec88d7a7717821a4e38b76a9
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="piecemeal-restore-of-databases-with-memory-optimized-tables"></a>Schrittweise Wiederherstellung von Datenbanken mit speicheroptimierten Tabellen
  Die schrittweise Wiederherstellung wird für Datenbanken mit speicheroptimierten Tabellen unterstützt, allerdings mit der im Folgenden beschriebenen Einschränkung. Weitere Informationen zur schrittweisen Sicherung und Wiederherstellung finden Sie unter [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md) und [Schrittweise Wiederherstellungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md).  
  
 Eine speicheroptimierte Dateigruppe muss zusammen mit der primären Dateigruppe gesichert und wiederhergestellt werden:  
  
-   Wenn Sie die primäre Dateigruppe sichern (oder wiederherstellen), müssen Sie die speicheroptimierte Dateigruppe angeben.  
  
-   Wenn Sie die speicheroptimierte Dateigruppe sichern (oder wiederherstellen), müssen Sie die primäre Dateigruppe angeben.  
  
 Wichtige Szenarien für die schrittweise Sicherung und Wiederherstellung  
  
-   Mithilfe der schrittweisen Sicherung lässt sich die Größe der Sicherung reduzieren. Einige Beispiele:  
  
    -   Konfigurieren Sie die Datenbanksicherung für unterschiedliche Uhrzeiten oder Tage, um die Auswirkungen auf die Arbeitsauslastung zu minimieren. Ein Beispiel hierfür ist eine sehr umfangreiche Datenbank (größer als 1 TB), bei der eine vollständige Datenbanksicherung nicht innerhalb des für die Datenbankwartung vorgesehenen Zeitraums abgeschlossen werden kann. In diesem Fall können Sie die schrittweise Sicherung verwenden, um die vollständige Datenbank in mehreren schrittweisen Sicherungen zu sichern.  
  
    -   Wenn eine Dateigruppe als schreibgeschützt gekennzeichnet ist, erfordert sie keine Transaktionsprotokollsicherung, nachdem sie als schreibgeschützt gekennzeichnet wurde. Nachdem Sie die Dateigruppe als schreibgeschützt gekennzeichnet haben, können Sie sie optional nur einmal sichern.  
  
-   Schrittweise Wiederherstellung.  
  
    -   Das Ziel einer schrittweisen Wiederherstellung besteht darin, die wichtigen Datenbankinhalte online zu schalten, ohne darauf zu warten, dass alle Daten wiederhergestellt sind. Ein Beispiel ist eine Datenbank mit partitionierten Daten, bei der ältere Partitionen nur selten verwendet werden. Diese Partitionen können dann jeweils nur bei Bedarf wiederhergestellt werden. Ähnliches gilt für Dateigruppen, die beispielsweise Vergangenheitsdaten enthalten.  
  
    -   Mithilfe der Seitenreparatur können Sie eine Seitenbeschädigung beheben, indem Sie die jeweilige Seite wiederherstellen. Weitere Informationen finden Sie unter [Wiederherstellung von Seiten &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md).  
  
## <a name="samples"></a>Beispiele  
 In den Beispielen wird das folgende Schema verwendet:  
  
```  
CREATE DATABASE imoltp  
ON PRIMARY (name = imoltp_primary1, filename = 'c:\data\imoltp_data1.mdf')  
LOG ON (name = imoltp_log, filename = 'c:\data\imoltp_log.ldf')  
GO  
  
ALTER DATABASE imoltp ADD FILE (name = imoltp_primary2, filename = 'c:\data\imoltp_data2.ndf')  
GO  
  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_secondary  
ALTER DATABASE imoltp ADD FILE (name = imoltp_secondary, filename = 'c:\data\imoltp_secondary.ndf') TO FILEGROUP imoltp_secondary  
GO  
  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA   
ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod   
ALTER DATABASE imoltp ADD FILE (name='imoltp_mod2', filename='c:\data\imoltp_mod2') TO FILEGROUP imoltp_mod   
GO  
```  
  
### <a name="backup"></a>Sicherung  
 Dieses Beispiel veranschaulicht, wie die primäre Dateigruppe und die speicheroptimierte Dateigruppe gesichert werden. Sie müssen die primäre und speicheroptimierte Dateigruppe zusammen angeben.  
  
```  
backup database imoltp filegroup='primary', filegroup='imoltp_mod' to disk='c:\data\imoltp.dmp' with init  
```  
  
 Das folgende Beispiel veranschaulicht, dass eine Dateigruppensicherung, die keine primäre und speicheroptimierte Dateigruppe umfasst, ähnlich wie bei Datenbanken ohne speicheroptimierte Tabellen funktioniert. Mit dem folgenden Befehl wird die sekundäre Dateigruppe gesichert.  
  
```  
backup database imoltp filegroup='imoltp_secondary' to disk='c:\data\imoltp_secondary.dmp' with init  
```  
  
### <a name="restore"></a>Wiederherstellung  
 Im folgenden Beispiel wird gezeigt, wie die primäre Dateigruppe und speicheroptimierte Dateigruppe zusammen wiederhergestellt werden.  
  
```  
restore database imoltp filegroup = 'primary', filegroup = 'imoltp_mod'   
from disk='c:\data\imoltp.dmp' with partial, norecovery  
  
--restore the transaction log  
 RESTORE LOG [imoltp] FROM DISK = N'c:\data\imoltp_log.dmp' WITH  FILE = 1,  NOUNLOAD,  STATS = 10  
GO  
```  
  
 Das nächste Beispiel veranschaulicht, dass eine Dateigruppenwiederherstellung, die keine primäre und speicheroptimierte Dateigruppe umfasst, ähnlich wie bei Datenbanken ohne speicheroptimierte Tabellen funktioniert.  
  
```  
RESTORE DATABASE [imoltp] FILE = N'imoltp_secondary'   
FROM  DISK = N'c:\data\imoltp_secondary.dmp' WITH  FILE = 1,  RECOVERY,  NOUNLOAD,  STATS = 10  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern und Wiederherstellen speicheroptimierter Tabellen](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  
  

