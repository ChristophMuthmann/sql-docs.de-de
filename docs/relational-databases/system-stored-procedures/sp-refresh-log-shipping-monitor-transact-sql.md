---
title: Sp_refresh_log_shipping_monitor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_refresh_log_shipping_monitor
- sp_refresh_log_shipping_monitor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refresh_log_shipping_monitor
ms.assetid: edefb912-31c5-4d99-9aba-06629afd0171
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2cda4f72387da9f35824fe4747eb31a0d5ec454d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sprefreshlogshippingmonitor-transact-sql"></a>sp_refresh_log_shipping_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Diese gespeicherte Prozedur aktualisiert die Remoteüberwachungstabellen mit den neuesten Informationen von einem angegebenen primären oder sekundären Server für den angegebenen Protokollversand-Agent. Die Prozedur wird auf dem primären oder sekundären Server aufgerufen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_refresh_log_shipping_monitor  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
[ @database = ] 'database'  
[ @mode ] n  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@agent_id=** ] **'***agent_id***'**  
 Die primäre ID für Sicherungsvorgänge oder die sekundäre ID für Kopier- oder Wiederherstellungsvorgänge. *agent_id* ist vom Datentyp **uniqueidentifier** und darf nicht NULL sein.  
  
 [ **@agent_type=** ] **'***agent_type***'**  
 Der Typ des Protokollversandauftrags.  
  
 0 = Sicherungsauftrag  
  
 1 = Kopierauftrag  
  
 2 = Wiederherstellungsauftrag  
  
 *agent_type* ist vom Datentyp **tinyint** und kann nicht NULL sein.  
  
 [  **@database=** ] **"***Datenbank***"**  
 Die primäre oder sekundäre Datenbank, die von der Protokollierung oder von Sicherungs- oder Wiederherstellungs-Agents verwendet wird.  
  
 [ **@mode** ] *n*  
 Gibt an, ob die Überwachungsdaten aktualisiert oder geleert werden. Der Datentyp des *m* ist "tinyint" und die unterstützten Werte sind:  
  
 1 = aktualisieren (Dies ist der Standardwert.)  
  
 2 = löschen  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine.  
  
## <a name="remarks"></a>Hinweise  
 **Sp_refresh_log_shipping_monitor** aktualisiert die **Log_shipping_monitor_primary**, **Log_shipping_monitor_secondary**, **Log_shipping_monitor_history_detail** , und **Log_shipping_monitor_error_detail** Tabellen mit jeder, der noch nicht übertragenen Sitzungsinformationen. Dies ermöglicht das Synchronisieren des Überwachungsservers mit dem primären oder einem sekundären Server, wenn der Überwachungsserver für einen bestimmten Zeitraum nicht mehr synchronisiert wurde. Zudem können Sie die Überwachungsinformationen auf dem Überwachungsserver bei Bedarf leeren.  
  
 **Sp_refresh_log_shipping_monitor** muss ausgeführt werden, aus der **master** Datenbank auf dem primären oder sekundären Server.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle **sysadmin** können diese Prozedur ausführen.  
  
## <a name="see-also"></a>Siehe auch  
 [Über den Protokollversand & #40; SQLServer & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
