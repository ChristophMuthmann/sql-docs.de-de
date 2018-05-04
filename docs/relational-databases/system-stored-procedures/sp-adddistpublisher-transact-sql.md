---
title: Sp_adddistpublisher (Transact-SQL) | Microsoft Docs
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
- sp_adddistpublisher
- sp_adddistpublisher_TSQL
helpviewer_keywords:
- sp_adddistpublisher
ms.assetid: 04e15011-a902-4074-b38c-3ec2fc73b838
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3ca0d66f6b5a4df2e0d4f4fa79d9eb882159c431
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spadddistpublisher-transact-sql"></a>sp_adddistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Konfiguriert einen Verleger so, dass er eine angegebene Verteilungsdatenbank verwendet. Diese gespeicherte Prozedur wird auf dem Verteiler für jede Datenbank ausgeführt. Beachten Sie, dass die gespeicherten Prozeduren [Sp_adddistributor &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) und [Sp_adddistributiondb &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) muss vor der Verwendung dieser gespeicherten ausgeführt wurden die Prozedur.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_adddistpublisher [ @publisher= ] 'publisher'   
        , [ @distribution_db= ] 'distribution_db'   
    [ , [ @security_mode= ] security_mode ]   
    [ , [ @login= ] 'login' ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @working_directory= ] 'working_directory' ]   
    [ , [ @trusted= ] 'trusted' ]   
    [ , [ @encrypted_password= ] encrypted_password ]   
    [ , [ @thirdparty_flag = ] thirdparty_flag ]  
    [ , [ @publisher_type = ] 'publisher_type' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publisher=**] **'***publisher***'**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@distribution_db=**] **"***Distribution_db***"**  
 Ist der Name der Verteilungsdatenbank. *Distributor_db* ist **Sysname**, hat keinen Standardwert. Dieser Parameter wird von Replikations-Agents zum Herstellen einer Verbindung zum Verleger verwendet.  
  
 [  **@security_mode=**] *Security_mode*  
 Der implementierte Sicherheitsmodus. Dieser Parameter wird nur von Replikations-Agents verwendet, um eine Verbindung mit dem Verleger für Abonnements mit verzögertem Update oder mit einem Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger herzustellen. *Security_mode* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**0**|Replikations-Agents auf dem Verteiler verwenden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung zum Herstellen einer Verbindung mit dem Verleger.|  
|**1** (Standard)|Replikations-Agents auf dem Verteiler verwenden die Windows-Authentifizierung beim Herstellen einer Verbindung zum Verleger.|  
  
 [  **@login=**] **"***Anmeldung***"**  
 Die Anmeldung ist. Dieser Parameter ist erforderlich, wenn *Security_mode* ist **0**. *login* ist vom Datentyp **sysname**und hat den Standardwert NULL. Dieser Parameter wird von Replikations-Agents zum Herstellen einer Verbindung zum Verleger verwendet.  
  
 [  **@password=**] **"***Kennwort***"**]  
 Ist das Kennwort. *Kennwort* ist **Sysname**, hat den Standardwert NULL. Dieser Parameter wird von Replikations-Agents zum Herstellen einer Verbindung zum Verleger verwendet.  
  
> [!IMPORTANT]  
>  Verwenden Sie kein leeres Kennwort. Verwenden Sie ein sicheres Kennwort.  
  
 [  **@working_directory=**] **"***Working_directory***"**  
 Der Name des Arbeitsverzeichnisses, das zum Speichern von Daten- und Schemadateien für die Veröffentlichung verwendet wird. *Working_directory* ist **nvarchar(255)**, und der Standardwert ist der Ordner ReplData für diese Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], z. B. 'c:\Programme\Microsoft SQL Server\MSSQL\MSSQ.1\ReplData'. Dieser Name sollte im UNC-Format angegeben werden.  
  
 [  **@trusted=**] **"***vertrauenswürdigen***"**  
 Dieser Parameter wurde als veraltet markiert und steht nur aus Gründen der Abwärtskompatibilität zur Verfügung. *vertrauenswürdige* ist **nvarchar(5)**, Einstellung auf einen anderen Wert als **"false"** führt zu einem Fehler.  
  
 [  **@encrypted_password=**] *Encrypted_password*  
 Festlegen von *Encrypted_password* wird nicht mehr unterstützt. Beim Festlegen dieser **Bit** Parameter **1** führt zu einem Fehler.  
  
 [  **@thirdparty_flag =**] *Thirdparty_flag*  
 Gibt an, ob der Verleger ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger ist. *Thirdparty_flag* ist **Bit**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**0** (Standardwert)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank.|  
|**1**|Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank.|  
  
 [ **@publisher_type**=] **"***Publisher_type***"**  
 Gibt den Verlegertyp an, wann der Verleger kein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger ist. *Publisher_type* ist vom Datentyp Sysname und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**<br /><br /> (Standard)|Gibt einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger an.|  
|**ORACLE**|Gibt einen standardmäßigen Oracle-Verleger an.|  
|**ORACLE-GATEWAY**|Gibt einen Oracle Gateway-Verleger an.|  
  
 Weitere Informationen zu den Unterschieden zwischen einem Oracle-Verleger und einem Oracle-Gatewayverleger finden Sie unter [Konfigurieren eines Oracle-Verlegers](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_adddistpublisher** wird von Momentaufnahme-, Transaktions- und Mergereplikation verwendet.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistpublisher-tran_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** -Serverrolle kann ausführen **Sp_adddistpublisher**.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren der Veröffentlichung und der Verteilung](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [Sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Verteilung konfigurieren](../../relational-databases/replication/configure-distribution.md)  
  
  
