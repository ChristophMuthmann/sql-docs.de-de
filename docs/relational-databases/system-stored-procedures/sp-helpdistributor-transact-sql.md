---
title: Sp_helpdistributor (Transact-SQL) | Microsoft Docs
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
- sp_helpdistributor_TSQL
- sp_helpdistributor
helpviewer_keywords: sp_helpdistributor
ms.assetid: 37b0983e-3b69-4f0f-977e-20efce0a0b97
caps.latest.revision: "32"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f8436c56ec260fdf2f22d5f6ecdb7a1c3102d6be
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdistributor-transact-sql"></a>sp_helpdistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Listet Informationen zu den Verteiler, Verteilungsdatenbank, zum Arbeitsverzeichnis und [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Benutzer-Agent-Dienstkonto. Diese gespeicherte Prozedur wird beim Verleger mit der Veröffentlichungsdatenbank oder einer anderen Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpdistributor [ [ @distributor= ] 'distributor' OUTPUT ]  
    [ , [ @distribdb= ] 'distribdb' OUTPUT ]  
    [ , [ @directory= ] 'directory' OUTPUT ]  
    [ , [ @account= ] 'account' OUTPUT ]  
    [ , [ @min_distretention= ] min_distretention OUTPUT ]  
    [ , [ @max_distretention= ] max_distretention OUTPUT ]  
    [ , [ @history_retention= ] history_retention OUTPUT ]  
    [ , [ @history_cleanupagent= ] 'history_cleanupagent' OUTPUT ]  
    [ , [ @distrib_cleanupagent = ] 'distrib_cleanupagent' OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @local = ] 'local' ]  
    [ , [ @rpcsrvname= ] 'rpcsrvname' OUTPUT ]  
    [ , [ @publisher_type = ] 'publisher_type' OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@distributor=**] **"***Verteiler***"** Ausgabe  
 Entspricht dem Namen des Verteilers. Verteiler handelt es sich **Sysname**, hat den Standardwert  **%** , dies ist der einzige Wert, der ein Resultset zurückgibt.  
  
 [  **@distribdb=**] **"***Distribdb***"** Ausgabe  
 Ist der Name der Verteilungsdatenbank. *Distribdb* ist **Sysname**, hat den Standardwert  **%** , dies ist der einzige Wert, der ein Resultset zurückgibt.  
  
 [  **@directory=**] **"***Directory***"** Ausgabe  
 Ist das Arbeitsverzeichnis an. *Directory* ist **nvarchar(255)**, hat den Standardwert  **%** , dies ist der einzige Wert, der ein Resultset zurückgibt.  
  
 [  **@account=**] **"***Konto***" Ausgabe**  
 Das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Benutzerkonto. *Konto*ist **nvarchar(255)**, hat den Standardwert  **%** , dies ist der einzige Wert, der ein Resultset zurückgibt.  
  
 [  **@min_distretention=**] *Min_distretention***Ausgabe**  
 Die minimale Beibehaltungsdauer (in Stunden) für die Verteilung. *Min_distretention* ist **Int**, hat den Standardwert **-1**.  
  
 [  **@max_distretention=**] *Max_distretention***Ausgabe**  
 Die maximale Beibehaltungsdauer (in Stunden) für die Verteilung. *Max_distretention* ist **Int**, hat den Standardwert **-1**.  
  
 [  **@history_retention=**] *History_retention***Ausgabe**  
 Die Beibehaltungsdauer (in Stunden) für den Verlauf. *History_retention* ist **Int**, hat den Standardwert **-1**.  
  
 [  **@history_cleanupagent=**] **"***History_cleanupagent***" Ausgabe**  
 Ist der Name des Verlaufscleanup-Agents. *History_cleanupagent* ist **nvarchar(100)**, hat den Standardwert  **%** , dies ist der einzige Wert, der ein Resultset zurückgibt.  
  
 [  **@distrib_cleanupagent =**] **"***Distrib_cleanupagent***" Ausgabe**  
 Ist der Name des der Verteilungscleanup-Agents. *Distrib_cleanupagent* ist **nvarchar(100)**, hat den Standardwert  **%** , dies ist der einzige Wert, der ein Resultset zurückgibt.  
  
 [  **@publisher=**] **"***Publisher***"**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@local=**] **"***lokale***"**  
 Gibt an, ob [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lokale Serverwerte abruft. *lokale* ist **nvarchar(5)**, hat den Standardwert NULL.  
  
 [  **@rpcsrvname=**] **"***Rpcsrvname***" Ausgabe**  
 Der Name des Servers, der Remoteprozeduraufrufe ausgibt. *Rpcsrvname* ist **Sysname**, hat den Standardwert  **%** , dies ist der einzige Wert, der ein Resultset zurückgibt.  
  
 [  **@publisher_type** =] **"***Publisher_type***" Ausgabe**  
 Der Verlegertyp des Verlegers. *Publisher_type* ist **Sysname**, hat den Standardwert  **%** , dies ist der einzige Wert, der ein Resultset zurückgibt.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Verteiler**|**sysname**|Name des Verteilers.|  
|**Verteilungsdatenbank**|**sysname**|Der Name der Verteilungsdatenbank.|  
|**Verzeichnis**|**nvarchar(255)**|Name des Arbeitsverzeichnisses.|  
|**Konto**|**nvarchar(255)**|Name des Windows-Benutzerkontos.|  
|**Min Verteil Aufbewahrung**|**int**|Minimale Beibehaltungsdauer für die Verteilung.|  
|**Max. Verteil Aufbewahrung**|**int**|Maximale Beibehaltungsdauer für die Verteilung.|  
|**verlaufsbeibehaltung**|**int**|Aufbewahrungdauer für Verlauf.|  
|**Verlaufscleanup-Agents**|**nvarchar(100)**|Der Name des Verlaufscleanup-Agents.|  
|**Verteilungscleanup-Agents**|**nvarchar(100)**|Der Name des Verteilungscleanup-Agents.|  
|**RPC-Server-name**|**sysname**|Name des lokalen Verteilers oder Remoteverteilers.|  
|**RPC-Anmeldename**|**sysname**|Anmeldename, der für Remoteprozeduraufrufe an den Remoteverteiler verwendet wird.|  
|**Typ des Verlegers**|**sysname**|Typ des Verlegers; kann einer der folgenden sein:<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **ORACLE-GATEWAY**|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpdistributor** wird für alle Replikationstypen verwendet.  
  
 Wenn eine oder mehrere Output-Parameter angegeben werden, für die Ausführung **Sp_helpdistributor**, alle auf NULL gesetzten Ausgabeparameter beenden Werte zugeordnet sind und es wird kein Resultset zurückgegeben. Wenn keine Ausgabeparameter angegeben werden, wird ein Resultset zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Die folgenden Resultsetspalten oder Ausgabeparameter werden an Mitglieder zurückgegeben der **Sysadmin** -Serverrolle auf dem Verleger und dem **Db_owner** festen Datenbankrolle "" für die Veröffentlichungsdatenbank:  
  
|Resultsetspalte|Output-parameter|  
|-----------------------|----------------------|  
|account|**@account**|  
|min distrib retention|**@min_distretention**|  
|max distrib retention|**@max_distretention**|  
|history retention|**@history_retention**|  
|history cleanup agent|**@history_cleanupagent**|  
|distribution cleanup agent|**@distrib_cleanupagent**|  
|rpc login name|none|  
  
 Die folgende Resultsetspalte wird an Benutzer in der Veröffentlichungszugriffsliste für eine Veröffentlichung beim Verteiler zurückgegeben:  
  
-   directory  
  
 Die folgenden Resultsetspalten werden an alle Benutzer zurückgegeben.  
  
|Resultsetspalte|Output-parameter|  
|-----------------------|----------------------|  
|distributor|**@distributor**|  
|distribution database|**@distribdb**|  
|rpc server name|**@rpcsrvname**|  
|publisher type|**@publisher_type**|  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Sp_adddistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [Sp_dropdistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
