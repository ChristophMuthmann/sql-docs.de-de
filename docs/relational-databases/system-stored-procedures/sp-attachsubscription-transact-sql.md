---
title: Sp_attachsubscription (Transact-SQL) | Microsoft Docs
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
- sp_attachsubscription
- sp_attachsubscription_TSQL
helpviewer_keywords:
- sp_attachsubscription
ms.assetid: b9bbda36-a46a-4327-a01e-9cd632e4791b
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7104db0241fe6d68137f5290f82e33f5dd3984ae
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spattachsubscription-transact-sql"></a>sp_attachsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt eine vorhandene Abonnementdatenbank an einen beliebigen Abonnenten an. Diese gespeicherte Prozedur wird beim neuen Abonnenten für die master-Datenbank ausgeführt.  
  
> [!IMPORTANT]  
>  Diese Funktion wurde als veraltet markiert und wird in einer zukünftigen Version entfernt. Diese Funktion sollte bei neuen Entwicklungen nicht verwendet werden. Für Mergeveröffentlichungen, die mithilfe von parametrisierten Filtern partitioniert werden, ist es empfehlenswert, die neuen Funktionen von partitionierten Momentaufnahmen zu verwenden. Diese vereinfachen die Initialisierung zahlreicher Abonnements. Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md). Für nicht partitionierte Veröffentlichungen können Sie ein Abonnement mit einer Sicherung initialisieren. Weitere Informationen finden Sie unter [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)initialisiert wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_attachsubscription [ @dbname = ] 'dbname'  
        , [ @filename = ] 'filename'  
    [ , [ @subscriber_security_mode = ] 'subscriber_security_mode' ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @distributor_security_mode = ] distributor_security_mode ]   
    [ , [ @distributor_login = ] 'distributor_login' ]   
    [ , [ @distributor_password = ] 'distributor_password' ]   
    [ , [ @publisher_security_mode = ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @db_master_key_password = ] 'db_master_key_password' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@dbname=** ] **'***dbname***'**  
 Die Zeichenfolge, die die Ziel-Abonnementdatenbank namentlich angibt. *Dbname* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@filename=** ] **"***Filename***"**  
 Der Name und physische Speicherort der primären MDF-Datei (**master** Datendatei). *FileName* ist **nvarchar(260)**, hat keinen Standardwert.  
  
 [  **@subscriber_security_mode=** ] **"***Subscriber_security_mode***"**  
 Der Sicherheitsmodus des Abonnenten, der beim Herstellen der Verbindung mit einem Abonnenten verwendet werden soll. *Subscriber_security_mode* ist **Int**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Die Windows-Authentifizierung muss verwendet werden. Wenn *Subscriber_security_mode* nicht **1** (Windows-Authentifizierung), wird ein Fehler zurückgegeben.  
  
 [  **@subscriber_login=** ] **"***Subscriber_login***"**  
 Der Anmeldename des Abonnenten, der beim Synchronisieren zum Herstellen der Verbindung mit einem Abonnenten verwendet wird. *Subscriber_login* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Dieser Parameter wurde als veraltet markiert und wird nur aus Gründen der Abwärtskompatibilität von Skripts beibehalten. Wenn *Subscriber_security_mode* nicht **1** und *Subscriber_login* wird angegeben, wird ein Fehler zurückgegeben.  
  
 [  **@subscriber_password=** ] **"***Subscriber_password***"**  
 Das Kennwort des Abonnenten. *Subscriber_password* ist **Sysname**, hat den Standardwert NULL.  
  
> [!NOTE]  
>  Dieser Parameter wurde als veraltet markiert und wird nur aus Gründen der Abwärtskompatibilität von Skripts beibehalten. Wenn *Subscriber_security_mode* nicht **1** und *Subscriber_password* wird angegeben, wird ein Fehler zurückgegeben.  
  
 [  **@distributor_security_mode=** ] *Distributor_security_mode*  
 Der Sicherheitsmodus, der beim Synchronisieren zum Herstellen der Verbindung mit einem Verteiler verwendet wird. *Distributor_security_mode* ist **Int**, hat den Standardwert **0**. **0** gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung. **1** gibt die Windows-Authentifizierung. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@distributor_login=** ] **"***Distributor_login***"**  
 Der Verteileranmeldename, der beim Synchronisieren zum Herstellen der Verbindung mit einem Verteiler verwendet wird. *Distributor_login* ist erforderlich, wenn *Distributor_security_mode* festgelegt ist, um **0**. *Distributor_login* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@distributor_password=** ] **"***Distributor_password***"**  
 Das Verteilerkennwort. *Distributor_password* ist erforderlich, wenn *Distributor_security_mode* festgelegt ist, um **0**. *Distributor_password* ist **Sysname**, hat den Standardwert NULL. Der Wert der *Distributor_password* muss weniger als 120 Unicode-Zeichen umfassen.  
  
> [!IMPORTANT]  
>  Verwenden Sie kein leeres Kennwort. Verwenden Sie ein sicheres Kennwort. Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
 [  **@publisher_security_mode=** ] *Publisher_security_mode*  
 Der Sicherheitsmodus, der beim Synchronisieren zum Herstellen der Verbindung mit einem Verleger verwendet wird. *Publisher_security_mode* ist **Int**, hat den Standardwert **1**. Wenn **0**, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung. Wenn **1**, gibt die Windows-Authentifizierung. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@publisher_login=** ] **"***Publisher_login***"**  
 Der Anmeldename, der beim Synchronisieren zum Herstellen der Verbindung mit einem Verleger verwendet wird. *Publisher_login* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@publisher_password=** ] **"***Publisher_password***"**  
 Das Kennwort, das beim Herstellen der Verbindung mit dem Verleger verwendet wird. *Publisher_password* ist **Sysname**, hat den Standardwert NULL. Der Wert der *Publisher_password* muss weniger als 120 Unicode-Zeichen umfassen.  
  
> [!IMPORTANT]  
>  Verwenden Sie kein leeres Kennwort. Verwenden Sie ein sicheres Kennwort. Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
 [  **@job_login=** ] **"***Job_login***"**  
 Der Anmeldename für das Windows-Konto, unter dem der Agent ausgeführt wird. *Job_login* ist **nvarchar(257)**, hat keinen Standardwert. Das Windows-Konto wird stets für Agent-Verbindungen mit dem Verteiler verwendet.  
  
 [  **@job_password=** ] **"***Job_password***"**  
 Das Kennwort für das Windows-Konto, unter dem der Agent ausgeführt wird. *Job_password* ist **Sysname**, hat keinen Standardwert. Der Wert der *Job_password* muss weniger als 120 Unicode-Zeichen umfassen.  
  
> [!IMPORTANT]  
>  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
 [  **@db_master_key_password=** ] **"***Db_master_key_password***"**  
 Das Kennwort eines benutzerdefinierten Datenbank-Hauptschlüssels. *Db_master_key_password* ist **nvarchar(524)**, hat den Standardwert NULL. Wenn *Db_master_key_password* nicht angegeben wird, eine vorhandene Datenbank-Hauptschlüssel gelöscht und neu erstellt werden.  
  
> [!IMPORTANT]  
>  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_attachsubscription** wird für Momentaufnahme-, Transaktions- und Mergereplikation verwendet.  
  
 Ein Abonnement kann nicht an die Veröffentlichung angefügt werden, wenn die Aufbewahrungsdauer der Veröffentlichung abgelaufen ist. Wenn ein Abonnement mit einer abgelaufenen Aufbewahrungsdauer angegeben wird, tritt ein Fehler auf, wenn das Abonnement angefügt wird oder wenn es erstmalig synchronisiert wird. Veröffentlichungen mit einer Aufbewahrungsdauer von **0** (laufen nie ab) werden ignoriert.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_attachsubscription**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
