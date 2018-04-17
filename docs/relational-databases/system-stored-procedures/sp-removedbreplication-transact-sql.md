---
title: Sp_removedbreplication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_removedbreplication
- sp_removedbreplication_TSQL
helpviewer_keywords:
- sp_removedbreplication
ms.assetid: cb98d571-d1eb-467b-91f7-a6e091009672
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bd63c99efa1b5f2b9701b278916cd1b5bf66b555
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spremovedbreplication-transact-sql"></a>sp_removedbreplication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Diese gespeicherte Prozedur entfernt alle Replikationsobjekte aus der Veröffentlichungsdatenbank auf der Verlegerinstanz von SQL Server oder aus der Abonnementdatenbank auf der Abonnenteninstanz von SQL Server. Führen Sie sie in der entsprechenden Datenbank aus, oder geben Sie bei Ausführung im Kontext einer anderen Datenbank auf derselben Instanz die Datenbank an, aus der die Replikationsobjekte entfernt werden sollen. Diese Prozedur entfernt keine Objekte von anderen Datenbanken, wie z. B. der Verteilungsdatenbank.  
  
> [!NOTE]  
>  Die Prozedur sollte nur verwendet werden, wenn bei anderen Methoden zum Entfernen von Replikationsobjekten Fehler aufgetreten sind.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_removedbreplication [ [ @dbname = ] 'dbname' ]  
    [ , [ @type = ] type ]   
```  
  
## <a name="arguments"></a>Argumente  
 [ **@dbname=**] **'***dbname***'**  
 Der Name der Datenbank. *dbname* ist vom Datentyp **sysname**. Der Standardwert ist NULL. Bei NULL wird die aktuelle Datenbank verwendet.  
  
 [ **@type** =] *Typ*  
 Der Typ der Replikation, für den Datenbankobjekte entfernt werden. *type* ist vom Datentyp **nvarchar(5)** . Die folgenden Werte sind möglich:  
  
|||  
|-|-|  
|**TRAN**|Entfernt Transaktionsreplikations-Veröffentlichungsobjekte.|  
|**Zusammenführen**|Entfernt Mergereplikations-Veröffentlichungsobjekte.|  
|**both** (Standard)|Entfernt alle Replikationsveröffentlichungsobjekte.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **sp_removedbreplication** wird für alle Replikationstypen verwendet.  
  
 **sp_removedbreplication** ist hilfreich beim Wiederherstellen einer replizierten Datenbank, für die keine Replikationsobjekte wiederhergestellt werden müssen.  
  
 **sp_removedbreplication** kann nicht bei schreibgeschützten Datenbanken verwendet werden.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_removedbreplication](../../relational-databases/replication/codesnippet/tsql/sp-removedbreplication-t_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle **sysadmin** können **sp_removedbreplication**ausführen.  
  
## <a name="example"></a>Beispiel  
  
```  
-- Remove replication objects from the subscription database on MYSUB.  
DECLARE @subscriptionDB AS sysname  
SET @subscriptionDB = N'AdventureWorksReplica'  
  
-- Remove replication objects from a subscription database (if necessary).  
USE master  
EXEC sp_removedbreplication @subscriptionDB  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Deaktivieren der Veröffentlichung und Verteilung](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
