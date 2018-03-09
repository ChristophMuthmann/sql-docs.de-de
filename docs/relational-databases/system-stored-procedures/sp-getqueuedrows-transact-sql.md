---
title: Sp_getqueuedrows (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_getqueuedrows_TSQL
- sp_getqueuedrows
helpviewer_keywords:
- sp_getqueuedrows
ms.assetid: 139e834f-1988-4b4d-ac81-db1f89ea90e8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 28a6c9eab5c2e6fb52e793e0a25d957335871b7d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spgetqueuedrows-transact-sql"></a>sp_getqueuedrows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ruft beim Abonnenten Zeilen ab, die über ausstehende Updates in der Warteschlange verfügen. Diese gespeicherte Prozedur wird auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_getqueuedrows [ @tablename = ] 'tablename'  
    [ , [ @owner = ] 'owner'  
    [ , [ @tranid = ] 'transaction_id' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@tablename =**] **"***Tablename***"**  
 Ist der Name der Tabelle. *TableName* ist **Sysname**, hat keinen Standardwert. Die Tabelle muss Teil eines Abonnements in einer Warteschlange sein.  
  
 [  **@owner =**] **"***Besitzer***"**  
 Der Abonnementbesitzer. *Besitzer* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@tranid =** ] **"***Transaction_id***"**  
 Ermöglicht das Filtern der Ausgabe nach der Transaktions-ID. *Transaction_id* ist **nvarchar(70)**, hat den Standardwert NULL. Falls angegeben, wird die Transaktions-ID angezeigt, die dem Befehl in der Warteschlange zugeordnet ist. Bei einem Wert von NULL werden alle Befehle in der Warteschlange angezeigt.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Zeigt alle Zeilen an, die zurzeit über mindestens eine Transaktion in der Warteschlange für die abonnierte Tabelle verfügen.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Aktion**|**nvarchar(10)**|Aktionstyp, der bei der Synchronisierung durchgeführt werden soll.<br /><br /> INS= Einfügen<br /><br /> DEL = Löschen<br /><br /> UPD = Aktualisieren|  
|**Der Standard**|**nvarchar(70)**|Die Transaktions-ID, unter der der Befehl ausgeführt wurde.|  
|**Tabelle column1... n**||Der Wert für jede Spalte der Tabelle im angegebenen *Tablename*.|  
|**Bei der MSrepl_tran_version**|**uniqueidentifier**|Diese Spalte wird zum Nachverfolgen von Änderungen an replizierten Daten und für die Konflikterkennung auf dem Verleger verwendet. Diese Spalte wird automatisch der Tabelle hinzugefügt.|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_getqueuedrows** wird verwendet, auf dem Abonnenten Aktualisieren über eine Warteschlange beteiligt.  
  
 **Sp_getqueuedrows** sucht Zeilen einer angegebenen Tabelle für ein Abonnement-Datenbank, die an einem verzögerten Update teilgenommen haben, aber derzeit nicht behoben wurden durch den Warteschlangenlese-Agent.  
  
## <a name="permissions"></a>Berechtigungen  
 **Sp_getqueuedrows** erfordert SELECT-Berechtigungen für die Tabelle, die im angegebenen *Tablename*.  
  
## <a name="see-also"></a>Siehe auch  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Konflikterkennung und -lösung beim verzögerten Update über eine Warteschlange](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
