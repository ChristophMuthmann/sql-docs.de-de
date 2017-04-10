---
title: "Anhalten und Fortsetzen der Datenmigration (Stretch-Datenbank) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/14/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.service: "sql-server-stretch-database"
ms.suite: ""
ms.technology: 
  - "dbe-stretch"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Stretch-Datenbank, anhalten und fortsetzen"
  - "Anhalten der Stretch-Datenbank"
  - "Fortsetzen der Stretch-Datenbank"
ms.assetid: 65d6a990-b295-41b2-97f9-7b6bf3000e4d
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 23
---
# Anhalten und Fortsetzen der Datenmigration (Stretch-Datenbank)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Zum Anhalten oder Fortsetzen der Migration von Daten zu Azure wählen Sie **Stretch** für eine Tabelle in SQL Server Management Studio, und wählen Sie dann **Anhalten** , um die Datenmigration anzuhalten, bzw. **Fortsetzen** , um die Datenmigration fortzusetzen. Sie können auch Transact-SQL verwenden, um die Migration von Daten anzuhalten oder fortzusetzen.  
  
 Halten Sie die Datenmigration für einzelne Tabellen an, wenn Sie Probleme auf dem lokalen Server behandeln oder die verfügbare Netzwerkbandbreite maximieren möchten.  

## Anhalten der Datenmigration  
  
### Verwenden von SQL Server Management Studio zum Anhalten der Datenmigration  
  
1.  Wählen Sie in SQL Server Management Studio im Objekt-Explorer die für die Streckung aktivierte Tabelle aus, für die Sie die Datenmigration anhalten möchten.  
  
2.  Klicken Sie mit der rechten Maustaste, und wählen Sie **Stretch**. Wählen Sie dann **Anhalten** aus.  
  
### Verwenden von Transact-SQL zum Anhalten der Datenmigration  
 Führen Sie den folgenden Befehl aus:  
  
```tsql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <Stretch-enabled table name>  
    SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = PAUSED ) ) ;  
GO 
```  
  
## Fortsetzen der Datenmigration  
  
### Verwenden von SQL Server Management Studio zum Fortsetzen der Datenmigration  
  
1.  Wählen Sie in SQL Server Management Studio im Objekt-Explorer die für die Streckung aktivierte Tabelle aus, für die Sie die Datenmigration fortsetzen möchten.  
  
2.  Klicken Sie mit der rechten Maustaste, und wählen Sie **Stretch**. Wählen Sie dann **Fortsetzen**.  
  
### Verwenden von Transact-SQL zum Fortsetzen der Datenmigration  
 Führen Sie den folgenden Befehl aus:  
  
```tsql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <Stretch-enabled table name>   
    SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = OUTBOUND ) ) ;  
 GO
```  

## Überprüfen Sie, ob die Migration aktiv ist oder angehalten wurde.

### Verwenden Sie SQL Server Management Studio, um zu überprüfen, ob die Migration aktiv ist oder angehalten wurde.
Öffnen Sie in SQL Server Management Studio die Option **Stretch-Datenbanküberwachung**, und überprüfen Sie den Wert der Spalte **Migrationsstatus**. Weitere Informationen finden Sie unter [Überwachung und Problembehandlung für die Datenmigration](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md).

### Überprüfen Sie mit Transact-SQL, ob die Migration aktiv ist oder angehalten wurde.
Fragen Sie die Katalogsicht **sys.remote_data_archive_tables** ab, und überprüfen Sie den Wert der Spalte **is_migration_paused**. Weitere Informationen finden Sie unter [sys.remote_data_archive_tables](sys.remote_data_archive_tables%20\(Transact-SQL\).md).

## Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[Überwachung und Problembehandlung bei der Datenmigration](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md) 
  