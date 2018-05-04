---
title: Sp_addmergepartition (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- sp_addmergepartition
- sp_addmergepartition_TSQL
helpviewer_keywords:
- sp_addmergepartition
ms.assetid: 02a5f46b-e5ff-4932-a3ff-7f0fd82d0981
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e04e556e663b83803e67c7afb7531869f210b7b6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spaddmergepartition-transact-sql"></a>sp_addmergepartition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine dynamisch gefilterte Partition für ein Abonnement, das die Werte der gefiltert wird [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) oder [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) auf dem Abonnenten. Diese gespeicherte Prozedur wird auf dem Verleger in der Datenbank ausgeführt, die veröffentlicht wird, und wird zum manuellen Generieren von Partitionen verwendet.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addmergepartition [ @publication = ] 'publication'  
        , [ @suser_sname = ] 'suser_sname'  
        , [ @host_name = ] 'host_name'  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication**=] **"***Veröffentlichung***"**  
 Die Mergeveröffentlichung, in der die Partition erstellt wird. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert. Wenn *Suser_sname* angegeben wird, den Wert der *Hostname* muss NULL sein.  
  
 [ **@suser_sname**=] **"***Suser_sname***"**  
 Ist der verwendete Wert beim Erstellen der Partition für ein Abonnement, durch den Wert des gefiltert wird die [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) -Funktion beim Abonnenten. *SUSER_SNAME* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@host_name**=] **"***Host_name***"**  
 Ist der verwendete Wert beim Erstellen der Partition für ein Abonnement, durch den Wert des gefiltert wird die [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) -Funktion beim Abonnenten. *HOST_NAME* ist **Sysname**, hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_addmergepartition** wird bei der Mergereplikation verwendet.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-addmergepartition-tra_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_addmergepartition**.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer Momentaufnahme für eine Mergeveröffentlichung mit parametrisierten Filtern](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
