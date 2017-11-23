---
title: Sp_markpendingschemachange (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- sp_markpendingschemachange
- sp_markpendingschemachange_TSQL
helpviewer_keywords: sp_markpendingschemachange
ms.assetid: 01100309-7bef-4154-85bf-f18489577e37
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc1712e646a8efda1fdc4f06d912a1021a0beaff
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spmarkpendingschemachange-transact-sql"></a>sp_markpendingschemachange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wird für die Unterstützung von Mergeveröffentlichungen verwendet, indem ein Administrator die Möglichkeit erhält, bestimmte ausstehende Schemaänderungen auszulassen, sodass sie nicht repliziert werden. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
> [!CAUTION]  
>  Diese gespeicherte Prozedur kann zur Folge haben, dass Schemaänderungen nicht repliziert werden. Sie sollte nur zur Problembehandlung verwendet werden, nachdem andere Methoden, wie z. B. die erneute Initialisierung, bereits versucht wurden oder die Leistung zu stark einschränken.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_markpendingschemachange [@publication = ] 'publication'  
    [ , [ @schemaversion = ] schemaversion ]  
    [ , [ @status = ] 'status' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [**@publication=** ] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@schemaversion=** ] *Schemaversion*  
 Identifiziert eine ausstehende Schemaänderung. *Schemaversion* ist **Int**, hat den Standardwert des **0**. Verwendung [Sp_enumeratependingschemachanges &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md) um die ausstehenden schemaänderungen für die Veröffentlichung aufzulisten.  
  
 [  **@status=** ] **"***Status***"**  
 Gibt an, ob eine ausstehende Schemaänderung übersprungen wird. *Status* ist **nvarchar(10)** hat den Standardwert des **active**. Wenn der Wert der *Status* ist **übersprungen**, und klicken Sie dann die entsprechende schemaänderung nicht repliziert wird.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_markpendingschemachange** wird bei der Mergereplikation verwendet.  
  
 **Sp_markpendingschemachange** ist eine gespeicherte Prozedur zur Unterstützung der Mergereplikation und sollte verwendet werden, nur, wenn Sie z. B. eine erneute Initialisierung, andere korrigierenden Maßnahmen gescheitert, um das Problem zu beheben oder zu in stark Begriffe der Leistung.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_markpendingschemachange**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sysmergeschemachange &#40; Transact-SQL &#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
