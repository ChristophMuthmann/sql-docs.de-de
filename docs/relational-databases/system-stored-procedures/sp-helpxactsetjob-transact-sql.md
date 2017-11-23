---
title: Sp_helpxactsetjob (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_helpxactsetjob
- sp_helpxactsetjob_TSQL
helpviewer_keywords: sp_helpxactsetjob
ms.assetid: 242cea3e-e6ac-4f84-a072-b003b920eb33
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 52fb4f08d51379368a99647a3e2a1cbe86c8fba5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpxactsetjob-transact-sql"></a>sp_helpxactsetjob (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt Informationen zum Xactset-Auftrag für einen Oracle-Verleger an. Diese gespeicherte Prozedur wird auf dem Verteiler für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpxactsetjob [ @publisher = ] 'publisher'   
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publisher**  =] **"***Publisher***"**  
 Der Name des Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verlegers, zu dem der Auftrag gehört. *Publisher* ist **Sysname**, hat keinen Standardwert.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Auftragsnummer**|**int**|Die Nummer des Oracle-Auftrags.|  
|**lastdate**|**varchar(22)**|Das Datum, an dem der Auftrag zuletzt ausgeführt wurde.|  
|**thisdate**|**varchar(22)**|Der Zeitpunkt der Änderung.|  
|**NextDate**|**varchar(22)**|Das nächste Datum, an dem der Auftrag ausgeführt wird.|  
|**Fehlerhafte**|**varchar(1)**|Flag, das angibt, ob der Auftrag unterbrochen wurde.|  
|**Intervall**|**varchar(200)**|Das Intervall für den Auftrag.|  
|**Fehler**|**int**|Die Anzahl Fehler für den Auftrag.|  
|**xactsetjobwhat**|**varchar(200)**|Der Name der Prozedur, die von dem Auftrag ausgeführt wird.|  
|**xactsetjob**|**varchar(1)**|Der Status des Auftrags, der einen der folgenden Werte haben kann:<br /><br /> **1** -der Auftrag aktiviert ist.<br /><br /> **0** -der Auftrag ist deaktiviert.|  
|**xactsetlonginterval**|**int**|Das lange Intervall für den Auftrag.|  
|**xactsetlongthreshold**|**int**|Der lange Schwellenwert für den Auftrag.|  
|**xactsetshortinterval**|**int**|Das kurze Intervall für den Auftrag.|  
|**xactsetshortthreshold**|**int**|Der kurze Schwellenwert für den Auftrag.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpxactsetjob** wird bei Momentaufnahme- und Transaktionsreplikation für Oracle-Verleger verwendet.  
  
 **Sp_helpxactsetjob** gibt immer die aktuellen Einstellungen für den Xactset-Auftrag (HREPL_XactSetJob) auf dem Verleger zurück. Wenn sich der Xactset-Auftrag derzeit in der Auftragswarteschlange befindet, gibt er zusätzlich Attribute des Auftrags aus der USER_JOB Datadictionary-Sicht zurück, die unter dem Administratorkonto am Oracle-Verleger erstellt wurden.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur ein Mitglied der **Sysadmin** -Serverrolle kann ausführen **Sp_helpxactsetjob**.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren des Transaktionssatz-Auftrags für einen Oracle-Verleger &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [Sp_publisherproperty &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)  
  
  
