---
title: Sp_helpsubscriberinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
f1_keywords:
- sp_helpsubscriberinfo
- sp_helpsubscriberinfo_TSQL
helpviewer_keywords:
- sp_helpsubscriberinfo
ms.assetid: fbabe1ec-57cf-425c-bae7-af7f5d3198fd
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b90e740346089d13c7406a3c454bd6d9afa835d2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpsubscriberinfo-transact-sql"></a>sp_helpsubscriberinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt Informationen zu einem Abonnenten an. Diese gespeicherte Prozedur wird auf dem Verleger für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpsubscriberinfo [ [ @subscriber =] 'subscriber']  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@subscriber =** ] **"***Abonnenten***"**  
 Der Name des Abonnenten. *Abonnenten* ist **Sysname**, hat den Standardwert **%**, womit alle Informationen zurückgegeben.  
  
 [  **@publisher =** ] **"***Publisher***"**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, und der Standardwert ist der Name des aktuellen Servers.  
  
> [!NOTE]  
>  *Publisher* sollte nicht angegeben werden, außer wenn es sich um einen Oracle-Verleger ist.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Name des Verlegers.|  
|**subscriber**|**sysname**|Der Name des Abonnenten.|  
|**type**|**tinyint**|Typ des Abonnenten:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank **1** = ODBC-Datenquelle|  
|**login**|**sysname**|Anmelde-ID für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung.|  
|**password**|**sysname**|Kennwort für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung.|  
|**commit_batch_size**|**int**|Nicht unterstützt.|  
|**status_batch_size**|**int**|Nicht unterstützt.|  
|**flush_frequency**|**int**|Nicht unterstützt.|  
|**frequency_type**|**int**|Häufigkeit, mit der der Verteilungs-Agent ausgeführt wird:<br /><br /> **1** = einmalige Ausführung<br /><br /> **2** = bedarfsgesteuert<br /><br /> **4** = täglich<br /><br /> **8** = wöchentlich<br /><br /> **16** = monatlich<br /><br /> **32** = mit relativem Monatsintervall<br /><br /> **64** = Autostart<br /><br /> **128** = wiederholt|  
|**frequency_interval**|**int**|Wert der Häufigkeit festgelegt angewendet *Frequency_type*.|  
|**frequency_relative_interval**|**int**|Datum des Verteilungs-Agent verwendet wird, wenn *Frequency_type* festgelegt ist, um **32** (mit relativem Monatsintervall):<br /><br /> **1** = erster<br /><br /> **2** = Sekunde<br /><br /> **4** = Dritter<br /><br /> **8** = vierter<br /><br /> **16** = letzter|  
|**frequency_recurrence_factor**|**int**|Von verwendete Wiederholungsfaktor *Frequency_type*.|  
|**frequency_subday**|**int**|Häufigkeit der erneuten Planung während des definierten Zeitraumes:<br /><br /> **1** = einmal<br /><br /> **2** = Sekunde<br /><br /> **4** = Minute<br /><br /> **8** = Stunde|  
|**frequency_subday_interval**|**int**|Intervall für *Frequency_subday*.|  
|**das Format HHMMSS verwendet**|**int**|Zeitpunkt, zu dem der Einsatz des Verteilungs-Agents zum ersten Mal geplant wird (Format: HHMMSS).|  
|**das Format HHMMSS verwendet**|**int**|Zeitpunkt, zu dem die Planung des Einsatzes des Verteilungs-Agents beendet wird (Format: HHMMSS).|  
|**active_start_date**|**int**|Datum, an dem der Einsatz des Verteilungs-Agents zum ersten Mal geplant wird (Format: YYYYMMDD).|  
|**active_end_date**|**int**|Datum, an dem die Planung des Einsatzes des Verteilungs-Agents beendet wird (Format: YYYYMMDD).|  
|**retryattempt**|**int**|Nicht unterstützt.|  
|**"retryDelay"**|**int**|Nicht unterstützt.|  
|**description**|**nvarchar(255)**|Beschreibungstext des Abonnenten.|  
|**security_mode**|**int**|Implementierter Sicherheitsmodus:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Authentifizierung|  
|**frequency_type2**|**int**|Häufigkeit, mit der der Merge-Agent ausgeführt wird:<br /><br /> **1** = einmalige Ausführung<br /><br /> **2** = bedarfsgesteuert<br /><br /> **4** = täglich<br /><br /> **8** = wöchentlich<br /><br /> **16** = monatlich<br /><br /> **32** = mit relativem Monatsintervall<br /><br /> **64** = Autostart<br /><br /> **128** = wiederholt|  
|**frequency_interval2**|**int**|Wert der Häufigkeit festgelegt angewendet *Frequency_type*.|  
|**frequency_relative_interval2**|**int**|Datum des Merge-Agents verwendet wird, wenn *Frequency_type* auf 32 (monatlich, relativ) festgelegt wird:<br /><br /> **1** = erster<br /><br /> **2** = Sekunde<br /><br /> **4** = Dritter<br /><br /> **8** = vierter<br /><br /> **16** = letzter|  
|**frequency_recurrence_factor2**|**int**|Von verwendete Wiederholungsfaktor *Frequency_type **.*|  
|**frequency_subday2**|**int**|Häufigkeit der erneuten Planung während des definierten Zeitraumes:<br /><br /> **1** = einmal<br /><br /> **2** = Sekunde<br /><br /> **4** = Minute<br /><br /> **8** = Stunde|  
|**frequency_subday_interval2**|**int**|Intervall für *Frequency_subday*.|  
|**active_start_time_of_day2**|**int**|Zeitpunkt, zu dem der Einsatz des Merge-Agents zum ersten Mal geplant wird (Format: HHMMSS).|  
|**active_end_time_of_day2**|**int**|Zeitpunkt, zu dem die Planung des Einsatzes des Merge-Agents beendet wird (Format: HHMMSS).|  
|**active_start_date2**|**int**|Datum, an dem der Einsatz des Merge-Agents zum ersten Mal geplant wird (Format: YYYYMMDD).|  
|**active_end_date2**|**int**|Datum, an dem die Planung des Einsatzes des Merge-Agents beendet wird (Format: YYYYMMDD).|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpsubscriberinfo** wird bei der Momentaufnahme-, Transaktions- und Mergereplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** festen Serverrolle, die **Db_owner** festen Datenbankrolle oder der veröffentlichungszugriffsliste für die Veröffentlichung kann ausführen **Sp_helpsubscriberinfo**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [Sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [Sp_changesubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [Sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [Sp_helpserver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
