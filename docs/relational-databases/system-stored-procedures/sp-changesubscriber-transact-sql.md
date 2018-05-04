---
title: Sp_changesubscriber (Transact-SQL) | Microsoft Docs
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
applies_to:
- SQL Server
f1_keywords:
- sp_changesubscriber
- sp_changesubscriber_TSQL
helpviewer_keywords:
- sp_changesubscriber
ms.assetid: d453c451-e957-490f-b968-5e03aeddaf10
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b1e04326cc3b17a47bcbf5baf43d81b238963d72
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spchangesubscriber-transact-sql"></a>sp_changesubscriber (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Optionen für einen Abonnenten. Alle Verteilungstasks für die Abonnenten des Verlegers werden aktualisiert. Diese gespeicherte Prozedur schreibt in die **MSsubscriber_info** Tabelle in der Verteilungsdatenbank. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_changesubscriber [ @subscriber= ] 'subscriber'  
    [ , [ @type= ] type ]  
    [ , [ @login= ] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @commit_batch_size= ] commit_batch_size ]  
    [ , [ @status_batch_size= ] status_batch_size ]  
    [ , [ @flush_frequency= ] flush_frequency ]  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @security_mode= ] security_mode ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@subscriber=**] **"***Abonnenten***"**  
 Der Name des Abonnenten, auf dem die Optionen geändert werden sollen. *Abonnenten* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@type=**] *Typ*  
 Der Abonnententyp. *Typ* ist **"tinyint"**, hat den Standardwert NULL. **0** gibt eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten. **1** gibt einen nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder andere ODBC-Datenquellenserver Abonnenten.  
  
 [  **@login=**] **"***Anmeldung***"**  
 Die Anmelde-ID für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung. *login* ist vom Datentyp **sysname**und hat den Standardwert NULL.  
  
 [  **@password=**] **"***Kennwort***"**  
 Ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierungskennwort. *Kennwort* ist **Sysname**, hat den Standardwert **%**. **%** Gibt an, dass keine Änderung an der Password-Eigenschaft vorhanden ist.  
  
 [  **@commit_batch_size=**] *Commit_batch_size*  
 Wird nur aus Gründen der Abwärtskompatibilität unterstützt.  
  
 [  **@status_batch_size=**] *Status_batch_size*  
 Wird nur aus Gründen der Abwärtskompatibilität unterstützt.  
  
 [  **@flush_frequency=**] *Flush_frequency*  
 Wird nur aus Gründen der Abwärtskompatibilität unterstützt.  
  
 [  **@frequency_type=**] *Frequency_type*  
 Die Häufigkeit für die Zeitplanung des Verteilungstasks. *Frequency_type* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Einmal|  
|**2**|Bedarfsgesteuert|  
|**4**|Täglich|  
|**8**|Wöchentlicher Zeitplan|  
|**16**|Monatlicher Zeitplan|  
|**32**|Monatlich, relativ|  
|**64**|Autostart|  
|**128**|Wiederholt|  
  
 [  **@frequency_interval=**] *Frequency_interval*  
 Das Intervall für *Frequency_type*. *Frequency_interval* ist **Int**, hat den Standardwert NULL.  
  
 [  **@frequency_relative_interval=**] *Frequency_relative_interval*  
 Das Datum des Verteilungstasks. Dieser Parameter wird verwendet, wenn *Frequency_type* festgelegt ist, um **32** (mit relativem Monatsintervall). *Frequency_relative_interval* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Erster|  
|**2**|Zweimal|  
|**4**|Dritter|  
|**8**|Vierter|  
|**16**|Letzter|  
  
 [  **@frequency_recurrence_factor=**] *Frequency_recurrence_factor*  
 Wie oft der Verteilungstask während des definierten wiederholt werden soll *Frequency_type*. *Frequency_recurrence_factor* ist **Int**, hat den Standardwert NULL.  
  
 [  **@frequency_subday=**] *Frequency_subday*  
 Die Häufigkeit für die erneute geplante Ausführung während des definierten Zeitraums. *Frequency_subday* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**1**|Einmal|  
|**2**|Zweimal|  
|**4**|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *Frequency_subday_interval*  
 Das Intervall für *frequency_subday*. *Frequency_subday_interval* ist **Int**, hat den Standardwert NULL.  
  
 [  **@active_start_time_of_day=**] *Active_start_time_of_day*  
 Die Tageszeit, zu der der Verteilungstask zum ersten Mal geplant ist. Dabei wird das Format HHMMSS verwendet. *Active_start_time_of_day* ist **Int**, hat den Standardwert NULL.  
  
 [  **@active_end_time_of_day=**] *Active_end_time_of_day*  
 Die Tageszeit, ab der der Verteilungstask nicht mehr geplant ist. Dabei wird das Format HHMMSS verwendet. *Active_end_time_of_day*ist **Int**, hat den Standardwert NULL.  
  
 [  **@active_start_date=**] *Active_start_date*  
 Das Datum, an dem der Verteilungstask zum ersten Mal geplant ist. Dabei wird das Format JJJJMMTT verwendet. *Active_start_date* ist **Int**, hat den Standardwert NULL.  
  
 [  **@active_end_date=**] *Active_end_date*  
 Das Datum, ab dem der Verteilungstask nicht mehr geplant ist. Dabei wird das Format JJJJMMTT verwendet. *Active_end_date*ist **Int**, hat den Standardwert NULL.  
  
 [  **@description=**] **"***Beschreibung***"**  
 Eine optionale Textbeschreibung. *Beschreibung* ist **nvarchar(255)**, hat den Standardwert NULL.  
  
 [  **@security_mode=**] *Security_mode*  
 Der implementierte Sicherheitsmodus. *Security_mode* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung|  
|**1**|Windows-Authentifizierung|  
  
 [ **@publisher**=] **"***Publisher***"**  
 Gibt einen Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger an. *Publisher* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  *Publisher* sollte nicht verwendet werden, beim Ändern von Artikeleigenschaften auf einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verleger.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_changesubscriber** wird für alle Replikationstypen verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_changesubscriber**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_addsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [Sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [Sp_helpserver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
