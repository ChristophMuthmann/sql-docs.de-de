---
title: Anzeigen der Größe der Datei mit geringer Dichte einer Datenbank-Momentaufnahme (Transact-SQL) | Microsoft-Dokumentation
ms.date: 07/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server database snapshots], sparse files
- space [SQL Server], sparse files
- sparse files [SQL Server]
- size [SQL Server], sparse files
- maximum sparse file size
- database snapshots [SQL Server], sparse files
- space [SQL Server], database snapshots
ms.assetid: 1867c5f8-d57c-46d3-933d-3642ab0a8e24
caps.latest.revision: 41
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 48a50ff9ed0fe49b9f6821ef598e2961253a87c1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql"></a>Anzeigen der Größe der Datei mit geringer Dichte einer Datenbank-Momentaufnahme (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie Sie mit [!INCLUDE[tsql](../../includes/tsql-md.md)] überprüfen, ob eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbankdatei eine Sparsedatei ist, und wie Sie die tatsächliche und maximale Größe ermitteln. Dateien mit geringer Dichte, die in Verbindung mit dem NTFS-Dateisystem vorkommen, werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankmomentaufnahmen verwendet.  
  
> [!NOTE]  
>  Beim Erstellen von Datenbankmomentaufnahmen werden Sparsedateien mithilfe der Dateinamen in der CREATE DATABASE-Anweisung erstellt. Diese Dateinamen werden in der Spalte **physical_name** in **sys.master_files** gespeichert. In **sys.database_files** (sowohl in der Quelldatenbank wie auch in einer Momentaufnahme) enthält die Spalte **physical_name** immer die Namen der Quelldatenbankdateien.  
  
## <a name="verify-that-a-database-file-is-a-sparse-file"></a>Überprüfen, ob eine Datenbankdatei eine Datei mit geringer Dichte ist  
  
1.  Auf der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
     Wählen Sie entweder in der Datenbank-Momentaufnahme unter **sys.database_files** oder in **sys.master_files** die Spalte **is_sparse**aus. Der Wert gibt wie folgt an, ob die Datei eine Sparsedatei ist:  
  
     1 = Die Datei ist eine Sparsedatei.  
  
     0 = Die Datei ist keine Sparsedatei.  
  
## <a name="find-out-the-actual-size-of-a-sparse-file"></a>Ermitteln der tatsächlichen Größe einer Datei mit geringer Dichte  
  
> [!NOTE]  
>  Sparsedateien wachsen in 64-KB-Schritten, weshalb die Größe einer Sparsedatei auf dem Datenträger immer einem Vielfachen von 64 KB entspricht.  
  
 Sie können die Spalte **size_on_disk_bytes** der dynamischen Verwaltungssicht [sys.dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden, um den belegten Speicherplatz (in Bytes) der Sparsedateien einer Momentaufnahme anzuzeigen.  
  
 Zum Anzeigen des Speicherplatzes, der durch eine Sparsedatei in Anspruch genommen wird, klicken Sie in Microsoft Windows mit der rechten Maustaste auf **Eigenschaften**, und lesen Sie den Wert unter **Größe auf Datenträger** ab.  
  
## <a name="find-out-the-maximum-size-of-a-sparse-file"></a>Ermitteln der maximalen Größe einer Datei mit geringer Dichte  
 Eine Datei mit geringer Dichte kann maximal die Größe der Quelldatenbankdatei erreichen, die zum Zeitpunkt der Momentaufnahmeerstellung festgelegt wurde. Zur Ermittlung dieser Größe stehen Ihnen die folgenden Alternativen zur Auswahl:  
  
-   Verwenden der Windows-Eingabeaufforderung:  
  
    1.  Verwenden Sie die **dir** -Befehle an der Eingabeaufforderung von Windows.  
  
    2.  Wählen Sie die Datei mit geringer Größe aus, öffnen Sie in Windows das Dialogfeld **Eigenschaften** der Datei, und lesen Sie den Wert für die **Größe** ab.  
  
-   Auf der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
     Wählen Sie entweder in **sys.database_files** in der Datenbank-Momentaufnahme oder in **sys.master_files** die **size**-Spalte aus. Der Wert in der **size** -Spalte gibt den maximal durch eine Momentaufnahme verwendbaren Speicherplatz in SQL-Seiten an. Dieser Wert entspricht dem Feld **Größe** in Windows. Der einzige Unterschied besteht darin, dass hierbei die Anzahl der SQL-Seiten in der Datei angegeben wird. Die Größe in Bytes kann daraus wie folgt errechnet werden:  
  
     ( *Seitenanzahl* * 8192)  

## <a name="example"></a>Beispiel
Das folgende Skript zeigt für jede Sparsedatei die Größe auf dem Datenträger in KB an.  Das Skript zeigt außerdem die maximale Größe in MB an, auf die eine Sparsedatei anwachsen kann.  Führen Sie das Transact-SQL-Skript in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aus.

```sql
SELECT  DB_NAME(sd.source_database_id) AS [SourceDatabase], 
        sd.name AS [Snapshot],
        mf.name AS [Filename], 
        size_on_disk_bytes/1024 AS [size_on_disk (KB)],
        mf2.size/128 AS [MaximumSize (MB)]
FROM sys.master_files mf
JOIN sys.databases sd
    ON mf.database_id = sd.database_id
JOIN sys.master_files mf2
    ON sd.source_database_id = mf2.database_id
    AND mf.file_id = mf2.file_id
CROSS APPLY sys.dm_io_virtual_file_stats(sd.database_id, mf.file_id)
WHERE mf.is_sparse = 1
AND mf2.is_sparse = 0
ORDER BY 1;
```
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datenbank-Momentaufnahmen &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [sys.fn_virtualfilestats &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
