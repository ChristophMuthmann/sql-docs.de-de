---
title: Sp_addmergealternatepublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_addmergealternatepublisher_TSQL
- sp_addmergealternatepublisher
helpviewer_keywords:
- sp_addmergealternatepublisher
ms.assetid: de46e0b1-d946-4021-bff6-2d8e3187656d
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: cd7c439b29a24c6f1187922a81bbdd3f1acfce0b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spaddmergealternatepublisher-transact-sql"></a>sp_addmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt die Möglichkeit hinzu, dass ein Abonnent einen alternativen Synchronisierungspartner verwendet. Die Veröffentlichungseigenschaften müssen angeben, dass Abonnenten mit anderen Verlegern synchronisieren können. Diese gespeicherte Prozedur wird auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_addmergealternatepublisher [ @publisher= ] 'publisher'  
          , [ @publisher_db= ] 'publisher_db'  
          , [ @publication= ] 'publication'  
          , [ @alternate_publisher= ] 'alternate_synchronization_partner'  
          , [ @alternate_publisher_db= ] 'alternate_publisher_db'  
          , [ @alternate_publication= ] 'alternate_synchronization_partner'  
     , [ @alternate_distributor= ] 'alternate_distributor'   
    [ , [ @friendly_name= ] 'friendly_name' ]   
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publisher=**] **'***publisher***'**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Der Name der Veröffentlichungsdatenbank. *Publisher_db* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@publication=**] **'***publication***'**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@alternate_publisher=**] **"***Alternate_synchronization_partner***"**  
 Der Name des alternativen Verlegers. *Alternate_synchronization_partner* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@alternate_publisher_db=**] **"***Alternate_publisher_db***"**  
 Der Name der Veröffentlichungsdatenbank auf dem alternativen Verleger. *Alternate_publisher_db* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@alternate_publication=**] **"***Alternate_synchronization_partner***"**  
 Der Name der Veröffentlichung auf dem alternativen Synchronisierungspartner. *Alternate_synchronization_partner* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@alternate_distributor=**] **"***Alternate_distributor***"**  
 Der Name des Verteilers für den alternativen Synchronisierungspartner. *Alternate_distributor* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@friendly_name=**] **"***friendly_name wurde***"**  
 Ein Anzeigename, durch den die Zuordnung von Verleger, Veröffentlichung und Verteiler, aus denen ein alternativer Synchronisierungspartner besteht, identifiziert werden kann. *friendly_name wurde* ist **nvarchar(255)**, hat den Standardwert NULL.  
  
 [  **@reserved=**] **"***reservierte***"**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_addmergealternatepublisher** wird bei der Mergereplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_addmergealternatepublisher**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_dropmergealternatepublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergealternatepublisher-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
