---
title: Sp_helpserver (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helpserver
- sp_helpserver_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpserver
ms.assetid: e8f42de7-c738-41c3-8bf5-dbd559dc7184
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 31e66de5957e55dfe3676a30ec435c303df910f0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpserver-transact-sql"></a>sp_helpserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu einem bestimmten Remoteserver oder Replikationsserver oder zu beiden Servertypen zurück. Stellt den Servernamen, den Netzwerknamen des Servers, den Replikationsstatus des Servers, die ID des Servers und den Sortierungsnamen bereit. Gibt außerdem Timeoutwerte für die Verbindungsherstellung zu sowie Abfragen auf Verbindungsservern an.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpserver [ [ @server = ] 'server' ]   
  [ , [ @optname = ] 'option' ]   
  [ , [ @show_topology = ] 'show_topology' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@server =** ] **"***Server***"**  
 Der Server, zu dem Informationen ausgegeben werden. Wenn *Server* nicht angegeben ist, Informationen zu allen Servern in **master.sys.servers**. *Server* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@optname =** ] **"***Option***"**  
 Die Option, die den Server beschreibt. *Option* ist **Varchar (**35**)**, hat den Standardwert NULL und muss einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Sortierung kompatibel**|Betrifft die Ausführung verteilter Abfragen für Verbindungsserver. Wenn diese Option auf "true" festgelegt wird,|  
|**Datenzugriff**|Aktiviert und deaktiviert den Zugriff auf verteilte Abfragen für Verbindungsserver.|  
|**dist**|Der Verteiler.|  
|**dpub**|Der Remoteverleger zu diesem Verteiler.|  
|**Verzögerte schemaüberprüfung**|Lässt die Schemaüberprüfung von Remotetabellen zu Beginn der Abfrage aus.|  
|**pub**|Verleger.|  
|**RPC**|Aktiviert RPC (Remote Procedure Call, Remoteprozeduraufruf) von dem angegebenen Server.|  
|**RPC-Ausgabe**|Aktiviert RPC zu dem angegebenen Server.|  
|**Sub**|Der Abonnent ist.|  
|**System**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Remotesortierung verwenden**|Verwendet die Sortierung einer Remotespalte anstelle der des lokalen Servers.|  
  
 [  **@show_topology =** ] **"***Show_topology***"**  
 Die Beziehung des angegebenen Servers zu anderen Servern. *Show_topology* ist **Varchar (**1**)**, hat den Standardwert NULL. Wenn *Show_topology* stimmt nicht mit **t** oder ist NULL, **Sp_helpserver** im Abschnitt Resultsets aufgelisteten Spalten zurück. Wenn *Show_topology* gleich **t**, zusätzlich zu den in den Resultsets aufgelisteten Spalten **Sp_helpserver** gibt auch **Topx** und **topy** Informationen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Servername.|  
|**Netzwerkname**|**sysname**|Netzwerkname des Servers.|  
|**status**|**Varchar (**70**)**|Serverstatus.|  
|**id**|**Char (**4**)**|ID des Servers.|  
|**Sortierungsname**|**sysname**|Sortierung des Servers.|  
|**connect_timeout**|**int**|Der Timeoutwert für die Verbindung mit dem Verbindungsserver.|  
|**query_timeout**|**int**|Timeoutwert für Abfragen auf einem Verbindungsserver.|  
  
## <a name="remarks"></a>Hinweise  
 Ein Server kann mehr als einen Status haben.  
  
## <a name="permissions"></a>Berechtigungen  
 Es werden keine Berechtigungen geprüft.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-displaying-information-about-all-servers"></a>A. Anzeigen von Informationen zu allen Servern  
 Im folgenden Beispiel werden Informationen zu allen Servern angezeigt. Dazu wird `sp_helpserver` ohne Parameter verwendet.  
  
```  
USE master;  
GO  
EXEC sp_helpserver;  
```  
  
### <a name="b-displaying-information-about-a-specific-server"></a>B. Anzeigen von Informationen zu einem bestimmten Server  
 Im folgenden Beispiel werden alle Informationen zum Server `SEATTLE2` angezeigt.  
  
```  
USE master;  
GO  
EXEC sp_helpserver 'SEATTLE2';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankmodul gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Sp_adddistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [Sp_addserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [Sp_addsubscriber &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [Sp_changesubscriber &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [Sp_dropserver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [Sp_dropsubscriber &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [Sp_helpremotelogin &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [Sp_serveroption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
