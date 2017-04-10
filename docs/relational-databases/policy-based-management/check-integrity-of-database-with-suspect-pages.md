---
title: "Pr&#252;fen der Integrit&#228;t von Datenbanken mit fehlerverd&#228;chtigen Seiten | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Best Practices [Datenbankmodul]"
ms.assetid: 3b1ec9fe-f6c5-46f7-aa63-6e671be1572d
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# Pr&#252;fen der Integrit&#228;t von Datenbanken mit fehlerverd&#228;chtigen Seiten
  Diese Regel überprüft Benutzerdatenbanken, deren Datenbankstatus auf Fehlerverdächtig festgelegt ist. Wenn [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] eine Datenbankseite mit einem Fehler vom Typ 824 liest, wird die Seite als "fehlerverdächtig" betrachtet und ihre Seiten-ID in der suspect_pages-Tabelle der msdb-Datenbank aufgezeichnet. Der Status der Datenbank, die diese Seite enthält, wird auf Fehlerverdächtig festgelegt.  
  
 Der Fehler vom Typ 824 gibt an, dass ein logischer Konsistenzfehler während eines Lesevorgangs aufgetreten ist. Dieser Fehler gibt häufig eine von einer fehlerhaften E/A-Subsystem-Komponente verursachte Datenbeschädigung an. Dies ist ein schwerer Fehler, der die Datenbankintegrität bedroht und sofort behoben werden muss.  
  
## Empfehlungen zu Best Practices  
  
-   Weitere Details zum Fehler des Typs 824 finden Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll dieser Datenbank.  
  
-   Führen Sie eine vollständige Datenbankkonsistenzprüfung ([DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)) aus.  
  
-   Implementieren Sie die Benutzeraktionen, die in [MSSQLSERVER_824](http://go.microsoft.com/fwlink/?LinkId=81397) definiert werden.  
  
## Weitere Informationen  
 [Verwalten der suspect_pages-Tabelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  