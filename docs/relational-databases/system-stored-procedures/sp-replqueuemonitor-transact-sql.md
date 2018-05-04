---
title: Sp_replqueuemonitor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_replqueuemonitor
- sp_replqueuemonitor_TSQL
helpviewer_keywords:
- sp_replqueuemonitor
ms.assetid: 6909a3f1-43a2-4df5-a6a5-9e6f347ac841
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8c1d4737d5f1502d98a58f268b58c93cf71d71ab
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spreplqueuemonitor-transact-sql"></a>sp_replqueuemonitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Listet die Warteschlangennachrichten aus einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Warteschlange oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing für Abonnements mit verzögertem Aktualisieren in einer bestimmten Veröffentlichung. Falls [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Warteschlangen verwendet werden, wird diese gespeicherte Prozedur auf dem Abonnenten für die Abonnementdatenbank ausgeführt. Falls Message Queuing verwendet wird, wird sie auf dem Verteiler für die Verteilungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_replqueuemonitor [ @publisher = ] 'publisher'  
    [ , [ @publisherdb = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @tranid = ] 'tranid' ]  
    [ , [ @queuetype = ] 'queuetype' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publisher** = ] **'***publisher***'**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat den Standardwert NULL. Der Server muss für das Veröffentlichen konfiguriert sein. NULL gibt alle Verleger an.  
  
 [ **@publisherdb** =] **"***Publisher_db***"** ]  
 Der Name der Veröffentlichungsdatenbank. *Publisher_db* ist **Sysname**, hat den Standardwert NULL. NULL gibt alle Veröffentlichungsdatenbanken an.  
  
 [ **@publication** =] **"***Veröffentlichung***"** ]  
 Der Name der Veröffentlichung. *Veröffentlichung*ist **Sysname**, hat den Standardwert NULL. NULL gibt alle Veröffentlichungen an.  
  
 [ **@tranid** =] **"***der Standard***"** ]  
 Ist die Transaktions-ID. *der Standard*ist **Sysname**, hat den Standardwert NULL. NULL gibt alle Transaktionen an.  
  
 [**@queuetype=** ] **"***Queuetype***"** ]  
 Der Typ von Warteschlange, in der Transaktionen gespeichert werden. *Queuetype* ist **"tinyint"** hat den Standardwert **0**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**0**|Alle Warteschlangentypen|  
|**1**|Message Queuing|  
|**2**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Warteschlange|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_replqueuemonitor** momentaufnahmereplikation oder Transaktionsreplikation mit Abonnements mit verzögertem Aktualisieren verwendet wird. Die Warteschlangennachrichten, die keine SQL-Befehle enthalten oder Teil eines umfassenden SQL-Befehls sind, werden nicht angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_replqueuemonitor**.  
  
## <a name="see-also"></a>Siehe auch  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
