---
title: Sp_dropdistributiondb (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_dropdistributiondb_TSQL
- sp_dropdistributiondb
helpviewer_keywords: sp_dropdistributiondb
ms.assetid: b6dd1846-2259-4d29-93af-a70a5d25a0c5
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b83c24e226b7ef99e2c7b4b56bfcda9cc64df80b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spdropdistributiondb-transact-sql"></a>sp_dropdistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht eine Verteilungsdatenbank. Löscht die von der Datenbank verwendeten physischen Dateien, falls sie nicht von einer anderen Datenbank verwendet werden. Diese gespeicherte Prozedur wird auf dem Verteiler für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dropdistributiondb [ @database= ] 'database'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@database=**] **"***Datenbank***"**  
 Die Datenbank, die gelöscht werden soll. *Datenbank* ist **Sysname**, hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_dropdistributiondb** wird für alle Replikationstypen verwendet.  
  
 Diese gespeicherte Prozedur muss ausgeführt werden, bevor der Verteiler durch Ausführen **Sp_dropdistributor**.  
  
 **Sp_dropdistributiondb** auch einen Warteschlangenlese-Agent-Auftrag für die Verteilungsdatenbank entfernt, sofern vorhanden.  
  
 Zum Deaktivieren der Verteilung muss die Verteilungsdatenbank online geschaltet sein. Wenn eine Datenbankmomentaufnahme für die Verteilungsdatenbank vorhanden ist, muss diese vor dem Deaktivieren der Verteilung gelöscht werden. Eine Datenbankmomentaufnahme ist eine schreibgeschützte Offlinekopie einer Datenbank und steht nicht in Verbindung mit einer Replikationsmomentaufnahme. Weitere Informationen finden Sie unter [Datenbankmomentaufnahmen &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributiondb-tr_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_dropdistributiondb**.  
  
## <a name="see-also"></a>Siehe auch  
 [Deaktivieren der Veröffentlichung und Verteilung](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [Sp_adddistributiondb &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [Sp_changedistributiondb &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
