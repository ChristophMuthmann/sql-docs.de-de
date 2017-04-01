---
title: "Erstellen einer FILESTREAM-aktivierten Datenbank | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-blob"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FILESTREAM [SQL Server], FILESTREAM-aktivierte Datenbanken"
ms.assetid: 0fc16356-76f7-44b8-a58b-f0b7c43694ec
caps.latest.revision: 16
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 16
---
# Erstellen einer FILESTREAM-aktivierten Datenbank
  In diesem Thema erfahren Sie, wie Sie eine Datenbank erstellen, die FILESTREAM unterstützt. Da für FILESTREAM eine besondere Art von Dateigruppe verwendet wird, müssen Sie beim Erstellen der Datenbank die CONTAINS FILESTREAM-Klausel für mindestens eine Dateigruppe angeben.  
  
 Eine FILESTREAM-Dateigruppe kann mehrere Dateien enthalten. Ein Codebeispiel, in dem veranschaulicht wird, wie eine FILESTREAM-Dateigruppe erstellt wird, die mehrere Dateien enthält, finden Sie unter [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
### So erstellen Sie eine FILESTREAM-aktivierte Datenbank  
  
1.  Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]auf **Neue Abfrage** , um den Abfrage-Editor zu öffnen.  
  
2.  Kopieren Sie den [!INCLUDE[tsql](../../includes/tsql-md.md)]-Code aus dem folgenden Beispiel in den Abfrage-Editor. Dieser [!INCLUDE[tsql](../../includes/tsql-md.md)]-Code erstellt eine FILESTREAM-aktivierte Datenbank mit dem Namen Archive.  
  
    > [!NOTE]  
    >  Für dieses Skript muss das Verzeichnis "C:\Data" vorhanden sein.  
  
3.  Klicken Sie auf **Ausführen**, um die Datenbank zu erstellen.  
  
## Beispiel  
 Im folgenden Codebeispiel wird eine Datenbank mit dem Namen `Archive` erstellt. Die Datenbank enthält drei Dateigruppen: `PRIMARY`, `Arch1`und `FileStreamGroup1`. `PRIMARY` und `Arch1` sind normale Dateigruppen, die keine FILESTREAM-Daten enthalten können. `FileStreamGroup1` ist die `FILESTREAM` -Dateigruppe.  
  
 [!code-sql[FILESTREAM#FS_CreateDB](../../relational-databases/blob/codesnippet/tsql/create-a-filestream-enab_1.sql)]  
  
 Bei einer `FILESTREAM` -Dateigruppe verweist `FILENAME` auf einen Pfad. Der Pfad muss bis zum letzten Ordner vorhanden sein, und der letzte Ordner darf nicht vorhanden sein. In diesem Beispiel muss `c:\data` vorhanden sein. Der Unterordner `filestream1` darf beim Ausführen der `CREATE DATABASE`-Anweisung jedoch nicht vorhanden sein. Weitere Informationen über diese Syntax finden Sie unter [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
 Nach der Ausführung des oben stehenden Beispiels sollten die Datei "filestream.hdr" und der Ordner "$FSLOG" im Ordner "c:\Data\filestream1" angezeigt werden. Die Datei "filestream.hdr" ist eine FILESTREAM-Container-Headerdatei.  
  
> [!IMPORTANT]  
>  Die Datei "filestream.hdr" ist eine wichtige Systemdatei. Sie enthält FILESTREAM-Headerinformationen. Diese Datei darf nicht entfernt oder geändert werden.  
  
 Bei vorhandenen Datenbanken können Sie eine FILESTREAM-Dateigruppe mit der [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) -Anweisung hinzufügen.  
  
## Siehe auch  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  