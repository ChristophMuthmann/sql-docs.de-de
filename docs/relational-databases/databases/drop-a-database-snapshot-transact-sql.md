---
title: "Löschen einer Datenbankmomentaufnahme (Transact-SQL) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing database snapshots
- deleting database snapshots
- database snapshots [SQL Server], deleting
ms.assetid: ad70ec97-d5fb-41aa-b72a-915e74b61b76
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2a86dbd8133febc11c103a97515fe486a79726de
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="drop-a-database-snapshot-transact-sql"></a>Löschen einer Datenbankmomentaufnahme (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Wenn Sie eine Datenbank-Momentaufnahme löschen, wird sie aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gelöscht. Außerdem werden die Sparsedateien gelöscht, die von der Momentaufnahme verwendet werden. Wenn Sie eine Datenbank-Momentaufnahme löschen, werden alle Benutzerverbindungen damit beendet.  
  
## <a name="security"></a>Sicherheit  
  
###  <a name="Permissions"></a> Berechtigungen  
 Jeder Benutzer mit DROP DATABASE-Berechtigungen kann eine Datenbank-Momentaufnahme löschen.  
  
##  <a name="TsqlProcedure"></a> Löschen einer Datenbank-Momentaufnahme (mit Transact-SQL)  
 **So löschen Sie eine Datenbank-Momentaufnahme**  
  
1.  Identifizieren Sie die Datenbank-Momentaufnahme, die Sie löschen möchten. Sie können die Momentaufnahmen einer Datenbank in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]anzeigen. Weitere Informationen finden Sie unter [Anzeigen einer Datenbankmomentaufnahme &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)anzeigen.  
  
2.  Geben Sie eine [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md) -Anweisung aus, und geben Sie den Namen der Datenbank-Momentaufnahme an, die gelöscht werden soll. Die Syntax lautet wie folgt:  
  
     DROP DATABASE *database_snapshot_name* [ **,**...*n* ]  
  
     Dabei ist *database_snapshot_name* der Name der Datenbank-Momentaufnahme, die gelöscht werden soll.  
  
####  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 In diesem Beispiel wird eine Datenbank-Momentaufnahme namens SalesSnapshot0600 ohne Auswirkungen auf die Quelldatenbank gelöscht.  
  
```  
DROP DATABASE SalesSnapshot0600 ;  
```  
  
 Alle Benutzerverbindungen mit SalesSnapshot0600 werden beendet, und alle von der Momentaufnahme verwendeten Sparsedateien des NTFS-Dateisystems werden gelöscht.  
  
> [!NOTE]  
>  Informationen zum Verwenden von Sparsedateien für Datenbank-Momentaufnahmen finden Sie unter [Datenbankmomentaufnahmen &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)anzeigen.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Erstellen einer Datenbankmomentaufnahme &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [Anzeigen einer Datenbankmomentaufnahme &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [Wiederherstellen einer Datenbank zu einer Datenbank-Momentaufnahme](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)  
  
  
## <a name="see-also"></a>Siehe auch  
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [Datenbankmomentaufnahmen &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
