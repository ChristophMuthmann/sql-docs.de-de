---
title: Sp_replmonitorhelppublisher (Transact-SQL) | Microsoft Docs
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
- sp_replmonitorhelppublisher_TSQL
- sp_replmonitorhelppublisher
helpviewer_keywords:
- sp_replmonitorhelppublisher
ms.assetid: 171501fe-4b74-4647-96c3-7691c777e01b
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca7ba5f15c56eef17808510dbf1a33de5f6fadc3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spreplmonitorhelppublisher-transact-sql"></a>sp_replmonitorhelppublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt aktuelle Statusinformationen für mindestens einen Verleger zurück, der einem Verteiler zugeordnet ist. Diese gespeicherte Prozedur, die zum Überwachen der Replikation verwendet wird, wird auf dem Verteiler für die Verteilungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_replmonitorhelppublisher [ [ @publisher = ] 'publisher' ]  
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publisher** = ] **'***publisher***'**  
 Der Name des Verlegers, dessen Status überwacht wird. *Publisher* ist **Sysname**, hat den Standardwert NULL. Bei NULL werden Informationen zu allen Verlegern zurückgegeben, die den Verteiler verwenden.  
  
 [  **@refreshpolicy=** ] *Refreshpolicy*  
 Nur interne Verwendung.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Der Name eines Verlegers.|  
|**distribution_db**|**sysname**|Der Name der Verteilungsdatenbank, die von einem bestimmten Verleger verwendet wird.|  
|**status**|**int**|Maximalstatus aller Replikations-Agents, die Veröffentlichungen auf diesem Verleger zugeordnet sind. Folgende Werte sind möglich.<br /><br /> **1** = gestartet<br /><br /> **2** = war erfolgreich<br /><br /> **3** = wird ausgeführt<br /><br /> **4** = im Leerlauf<br /><br /> **5** = wird wiederholt<br /><br /> **6** = Fehler|  
|**Warnung**|**int**|Warnung bezüglich des maximalen Schwellenwerts, die von einem Abonnement generiert wird, das zu einer Veröffentlichung auf diesem Verleger gehört. Dies kann das Ergebnis einer logischen OR-Operation mit mindestens einem der folgenden Werte sein.<br /><br /> **1** = Expiration ein Abonnement für eine transaktionsveröffentlichung wurde nicht innerhalb der Schwellenwerts für die Beibehaltungsdauer synchronisiert.<br /><br /> **2** = Latency - die Zeitdauer für die Replikation von Daten von einem Transaktionsverleger auf den Abonnenten überschreitet den Schwellenwert in Sekunden.<br /><br /> **4** = Mergeexpiration - ein Abonnement für eine Mergeveröffentlichung wurde nicht innerhalb der Schwellenwerts für die Beibehaltungsdauer synchronisiert.<br /><br /> **8** = Mergefastrunduration - die Zeit zum Abschließen der Synchronisierung eines Mergeabonnements überschreitet den Schwellenwert in Sekunden an, über eine schnelle Netzwerkverbindung.<br /><br /> **16** = Mergeslowrunduration – die Zeit zum Abschließen der Synchronisierung eines Mergeabonnements überschreitet den Schwellenwert in Sekunden an, über eine langsame oder DFÜ Netzwerkverbindung.<br /><br /> **32** = Mergefastrunspeed-die Übermittlungsrate für Zeilen während der Synchronisierung eines Mergeabonnements konnte die Schwellenwert-Rate in Zeilen pro Sekunde, über eine schnelle Netzwerkverbindung zu verwalten.<br /><br /> **64** = Mergeslowrunspeed-die Übermittlungsrate für Zeilen während der Synchronisierung eines Mergeabonnements konnte die Schwellenwert-Rate in Zeilen pro Sekunde, über eine langsame oder DFÜ Netzwerkverbindung zu verwalten.|  
|**PublicationCount**|**int**|Die Anzahl der Veröffentlichungen, die zum Verleger gehören.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_replmonitorhelppublisher** wird für alle Replikationstypen verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** auf dem Verteiler oder Mitglieder der festen Serverrolle die **Db_owner** oder **Replmonitor** können festen Datenbankrollen in der Verteilungsdatenbank Führen Sie **Sp_replmonitorhelppublisher**.  
  
## <a name="see-also"></a>Siehe auch  
 [Programmgesteuertes Überwachen der Replikation](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
