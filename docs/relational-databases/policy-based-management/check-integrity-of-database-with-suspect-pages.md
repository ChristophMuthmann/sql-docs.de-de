---
title: "Prüfen der Integrität von Datenbanken mit fehlerverdächtigen Seiten | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 3b1ec9fe-f6c5-46f7-aa63-6e671be1572d
caps.latest.revision: "10"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4c27d00dd9b975b8d06e2a9ca9d968e175a0078
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="check-integrity-of-database-with-suspect-pages"></a>Prüfen der Integrität von Datenbanken mit fehlerverdächtigen Seiten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Diese Regel überprüft Benutzerdatenbanken, deren Datenbankstatus auf „Fehlerverdächtig“ festgelegt ist. Wenn [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] eine Datenbankseite mit einem Fehler vom Typ 824 liest, wird die Seite als "fehlerverdächtig" betrachtet und ihre Seiten-ID in der suspect_pages-Tabelle der msdb-Datenbank aufgezeichnet. Der Status der Datenbank, die diese Seite enthält, wird auf Fehlerverdächtig festgelegt.  
  
 Der Fehler vom Typ 824 gibt an, dass ein logischer Konsistenzfehler während eines Lesevorgangs aufgetreten ist. Dieser Fehler gibt häufig eine von einer fehlerhaften E/A-Subsystem-Komponente verursachte Datenbeschädigung an. Dies ist ein schwerer Fehler, der die Datenbankintegrität bedroht und sofort behoben werden muss.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
  
-   Weitere Details zum Fehler des Typs 824 finden Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll dieser Datenbank.  
  
-   Führen Sie eine vollständige Datenbankkonsistenzprüfung ([DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)) aus.  
  
-   Implementieren Sie die Benutzeraktionen, die in [MSSQLSERVER_824](http://go.microsoft.com/fwlink/?LinkId=81397)definiert werden.  
  
## <a name="for-more-information"></a>Weitere Informationen  
 [Verwalten der suspect_pages-Tabelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
