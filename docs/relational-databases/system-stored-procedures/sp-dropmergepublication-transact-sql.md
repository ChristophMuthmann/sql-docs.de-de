---
title: Sp_dropmergepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- sp_dropmergepublication
- sp_dropmergepublication_TSQL
helpviewer_keywords:
- sp_dropmergepublication
ms.assetid: 9e1cb96e-5889-4f97-88cd-f60cf313ce68
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 225b5424b12bba73e975fdd17ca3d374e4c9b9a4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spdropmergepublication-transact-sql"></a>sp_dropmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht eine Mergeveröffentlichung und den zugehörigen Momentaufnahme-Agent. Vor dem Löschen einer Mergeveröffentlichung müssen alle Abonnements gelöscht werden. Die Artikel in der Veröffentlichung werden automatisch gelöscht. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dropmergepublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication=**] **'***publication***'**  
 Der Name der Veröffentlichung, die gelöscht werden soll. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert. Wenn **alle**, werden alle vorhandenen mergeveröffentlichungen sowie die ihnen zugeordneten Momentaufnahme-Agent-Aufträge entfernt. Wenn Sie einen bestimmten Wert für angeben *Veröffentlichung*, nur diese Veröffentlichung und die zugeordneten Momentaufnahme-Agent-Auftrag gelöscht werden.  
  
 [  **@ignore_distributor =**] *Ignore_distributor*  
 Wird verwendet, um eine Veröffentlichung zu löschen, ohne beim Verteiler Cleanuptasks auszuführen. *Ignore_distributor* ist **Bit**, hat den Standardwert **0**. Dieser Parameter wird auch bei der Neuinstallation des Verteilers verwendet.  
  
 [  **@reserved=**] *reservierte*  
 Ist für die zukünftige Verwendung reserviert. *reservierte* ist **Bit**, hat den Standardwert **0**.  
  
 [  **@ignore_merge_metadata=** ] *Ignore_merge_metadata*  
 Nur interne Verwendung.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_dropmergepublication** wird bei der Mergereplikation verwendet.  
  
 **Sp_dropmergepublication** rekursiv löscht alle Artikel, die einer Veröffentlichung zugeordnet sind, und anschließend wird die Veröffentlichung selbst gelöscht. Solange für eine Veröffentlichung ein Abonnement vorhanden ist, kann sie nicht gelöscht werden. Informationen zum Entfernen von Abonnements finden Sie unter [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md) und [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
 Ausführen von **Sp_dropmergepublication** zum Löschen einer Veröffentlichung entfernt nicht veröffentlichten Objekte aus der Veröffentlichungsdatenbank noch die zugehörigen Objekte aus der Abonnementdatenbank. Verwenden Sie DROP \<Objekt > um diese Objekte manuell bei Bedarf entfernen.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#sp_dropmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepublication-_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder die **Db_owner** feste Datenbankrolle können ausführen **Sp_dropmergepublication**.  
  
## <a name="see-also"></a>Siehe auch  
 [Löschen einer Veröffentlichung](../../relational-databases/replication/publish/delete-a-publication.md)   
 [Sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
