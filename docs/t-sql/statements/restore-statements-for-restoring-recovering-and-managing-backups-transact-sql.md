---
title: "RESTORE-Anweisungen für wiederherstellen, wiederherstellen und Verwalten von Sicherungen (T-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- restoring files [SQL Server], RESTORE statement
- RESTORE statement, about restore operations
- database restores [SQL Server], RESTORE statement
- restoring databases [SQL Server], RESTORE statement
- database backups [SQL Server], RESTORE statement
- backing up databases [SQL Server], RESTORE statement
- file restores [SQL Server], RESTORE statement
- transaction log backups [SQL Server], RESTORE statement
ms.assetid: fb29a151-f312-4f85-b857-5deeca0de8ce
caps.latest.revision: "15"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d756c4fb9f299abe88ef46c14726f613e8f66497
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="restore-statements-for-restoring-recovering-and-managing-backups-transact-sql"></a>RESTORE-Anweisungen für das Wiederherstellen und Verwalten von Sicherungen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In diesem Abschnitt werden die RESTORE-Anweisungen für Sicherungen beschrieben. Neben der RESTORE {DATABASE | LOG}-Hauptanweisung für das Wiederherstellen von Sicherungen unterstützen eine Reihe von RESTORE-Hilfsanweisungen Sie beim Verwalten von Sicherungen und Planen von Wiederherstellungssequenzen. Zu den RESTORE-Hilfsbefehlen gehören die folgenden Befehle: RESTORE FILELISTONLY, RESTORE HEADERONLY, RESTORE LABELONLY, RESTORE REWINDONLY und RESTORE VERIFYONLY.  
  
> [!IMPORTANT]  
>  In früheren Versionen von SQL Server konnte jeder Benutzer mit den Transact-SQL-Anweisungen RESTORE FILELISTONLY, RESTORE HEADERONLY, RESTORE LABELONLY und RESTORE VERIFYONLY Informationen zu Sicherungssätzen und Sicherungsgeräten erhalten. Da diese Anweisungen jedoch Informationen zum Inhalt der Sicherungsdateien zurückgeben, erfordern sie in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und späteren Versionen die CREATE DATABASE-Berechtigung. Dadurch werden Ihre Sicherungsdateien und Sicherungsinformationen umfassender geschützt als in vorherigen Versionen. Informationen über diese Berechtigung finden Sie unter [GRANT (Datenbankberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|-Anweisung.|Description|  
|---------------|-----------------|  
|[RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)|Beschreibt die Transact-SQL-Anweisungen RESTORE DATABASE und RESTORE LOG, die für die Wiederherstellung einer Datenbank mithilfe von mit dem BACKUP-Befehl erstellten Sicherungen verwendet werden. RESTORE DATABASE wird für Datenbanken unter allen Wiederherstellungsmodellen verwendet. RESTORE LOG wird nur unter dem vollständigen und dem massenprotokollierten Wiederherstellungsmodell verwendet. Mithilfe von RESTORE DATABASE kann außerdem eine Datenbank mit einer Datenbankmomentaufnahme wiederhergestellt werden.|  
|[RESTORE-Argumente &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)|Dokumentiert die Argumente, die in den Abschnitten über die Syntax der RESTORE-Anweisung und der zugeordneten Gruppe der folgenden Hilfsanweisungen beschrieben werden: RESTORE FILELISTONLY, RESTORE HEADERONLY, RESTORE LABELONLY, RESTORE REWINDONLY und RESTORE VERIFYONLY. Die meisten der Argumente werden nur von einer Untermenge dieser sechs Anweisungen unterstützt. Die Unterstützung für jedes Argument wird in der Beschreibung des Arguments angezeigt.|  
|[RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)|Beschreibt die Transact-SQL-Anweisung RESTORE FILELISTONLY, mit deren Hilfe ein Resultset zurückgegeben wird, das eine Liste der in dem Sicherungssatz enthaltenen Datenbank- und Protokolldateien enthält.|  
|[RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)|Beschreibt die Transact-SQL-Anweisung RESTORE HEADERONLY, mit deren Hilfe ein Resultset zurückgegeben wird, das die gesamten Sicherungsheaderinformationen für alle Sicherungssätze auf einem bestimmten Sicherungsmedium enthält.|  
|[RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)|Beschreibt die Transact-SQL-Anweisung RESTORE LABELONLY, mit deren Hilfe ein Resultset zurückgegeben wird, das Informationen über die durch das Sicherungsmedium identifizierten Sicherungsmedien enthält.|  
|[RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)|Beschreibt die Transact-SQL-Anweisung RESTORE REWINDONLY, mit deren Hilfe Bandmedien, die nach dem Ausführen der Anweisungen BACKUP oder RESTORE mit der NOREWIND-Option geöffnet blieben, zurückgespult und geschlossen werden.|  
|[RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)|Beschreibt die Transact-SQL-Anweisung RESTORE VERIFYONLY, mit deren Hilfe die Sicherung überprüft, aber nicht wiederhergestellt wird. Außerdem wird überprüft, ob der Sicherungssatz vollständig ist und die gesamte Sicherung gelesen werden kann. Diese Anweisung versucht nicht, die Struktur der Daten zu überprüfen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
