---
title: Sp_helpmergealternatepublisher (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- sp_helpmergealternatepublisher_TSQL
- sp_helpmergealternatepublisher
helpviewer_keywords: sp_helpmergealternatepublisher
ms.assetid: a96e365f-5967-4580-9d79-5bacf2d12211
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c1b6cdc6bc5d7a19a6b7c27fc282233310da658
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpmergealternatepublisher-transact-sql"></a>sp_helpmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Liste aller Server zurück, die als alternative Verleger für Mergeveröffentlichungen aktiviert sind. Diese gespeicherte Prozedur wird auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpmergealternatepublisher [ @publisher = ] 'publisher', [ @publisher_db = ] 'publisher_db', [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publisher=**] **"***Publisher***"**  
 Ist der Name des alternativen Verlegers. *Publisher* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@publisher_db=**] **"***Publisher_db***"**  
 Ist der Name der Veröffentlichungsdatenbank. *Publisher_db* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@publication=**] **"***Veröffentlichung***"**  
 Ist der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**alternate_publisher**|**sysname**|Name des alternativen Verlegers.|  
|**alternate_publisher_db**|**sysname**|Der Name der Veröffentlichungsdatenbank.|  
|**alternate_publication**|**sysname**|Name der Veröffentlichung.|  
|**alternate_distributor**|**sysname**|Der Name des Verteilers.|  
|**friendly_name wurde**|**nvarchar(255)**|Die Beschreibung des alternativen Verlegers.|  
|**aktiviert**|**bit**|Gibt an, ob der Server ein alternativer Verleger ist. **1** gibt an, dass der Verleger als alternativer Verleger aktiviert ist. **0** gibt an, dass sie nicht aktiviert ist.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpmergealternatepublisher** wird bei der Mergereplikation verwendet.  
  
 Während jeder Mergesitzung fragt das System sowohl den Verleger als auch den Abonnenten nach ihren Listen alternativer Verleger ab. Der Mergeprozess fügt der Liste der alternativen Verleger Einträge hinzu bzw. entfernt Einträge aus der Liste, sodass die Liste der alternativen Verleger auf dem Abonnenten mit derjenigen auf dem Verleger übereinstimmt.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der veröffentlichungszugriffsliste für die Veröffentlichung können ausführen **Sp_helpmergealternatepublisher**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
