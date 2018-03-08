---
title: Sp_changesubscriptiondtsinfo (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- sp_changesubscriptiondtsinfo
- sp_changesubscriptiondtsinfo_TSQL
helpviewer_keywords: sp_changesubscriptiondtsinfo
ms.assetid: 64fc085f-f81b-493b-b59a-ee6192d9736d
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6b551a265d30632f7ee96c86b78191388099c7d0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spchangesubscriptiondtsinfo-transact-sql"></a>sp_changesubscriptiondtsinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die DTS-Paketeigenschaften (Data Transformation Services) eines Abonnements. Diese gespeicherte Prozedur wird auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_changesubscriptiondtsinfo [ [ @job_id = ] job_id ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] 'dts_package_location' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@job_id=**] *Job_id*  
 Die Auftrags-ID des Verteilungs-Agents für das Pushabonnement. *Job_id* ist **varbinary(16)**, hat keinen Standardwert. Um die Verteilungsauftrags-ID zu suchen, führen Sie **Sp_helpsubscription** oder **Sp_helppullsubscription**.  
  
 [  **@dts_package_name** =] **"***Dts_package_name***"**  
 Gibt den Namen des DTS-Pakets an. *Dts_package_name* ist ein **Sysname**, hat den Standardwert NULL. Z. B. zum Angeben eines Pakets mit dem Namen **DTSPub_Package**, würden Sie angeben `@dts_package_name = N'DTSPub_Package'`.  
  
 [  **@dts_package_password** =] **"***Dts_package_password***"**  
 Gibt das Kennwort für das Paket an. *Dts_package_password* ist **Sysname** hat den Standardwert NULL, der gibt an, dass die Kennworteigenschaft bleiben unverändert.  
  
> [!NOTE]  
>  Ein DTS-Paket muss über ein Kennwort verfügen.  
  
 [  **@dts_package_location** =] **"***Dts_package_location***"**  
 Gibt den Paketspeicherort an. *Dts_package_location* ist ein **nvarchar(12)**, hat den Standardwert NULL, der angibt, dass der Speicherort des Pakets ist, verbleiben soll, nicht geändert. Der Speicherort des Pakets kann geändert werden, um **Verteiler** oder **Abonnenten**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_changesubscriptiondtsinfo** wird verwendet, für Momentaufnahme- und Transaktionsreplikation, die nur für Pushabonnements geeignet sind.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** festen Serverrolle **Db_owner** festen Datenbankrolle oder der Ersteller des Abonnements kann ausführen **Sp_changesubscriptiondtsinfo**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
