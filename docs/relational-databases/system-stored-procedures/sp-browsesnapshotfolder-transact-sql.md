---
title: Sp_browsesnapshotfolder (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_browsesnapshotfolder
- sp_browsesnapshotfolder_TSQL
helpviewer_keywords:
- sp_browsesnapshotfolder
ms.assetid: 0872edf2-4038-4bc1-a68d-05ebfad434d2
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 90371326d42ab34fcf5d20b92d5a19f479ab1b6b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spbrowsesnapshotfolder-transact-sql"></a>sp_browsesnapshotfolder (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den vollständigen Pfad für die letzte Momentaufnahme zurück, die für eine Veröffentlichung generiert wurde. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_browsesnapshotfolder [@publication= ] 'publication'  
    { [ , [ @subscriber = ] 'subscriber' ]  
 [ , [ @subscriber_db = ] 'subscriber_db' ] }  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publication=**] **'***publication***'**  
 Der Name der Veröffentlichung, die den Artikel enthält. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@subscriber=**] **"***Abonnenten***"**  
 Der Name des Abonnenten. *Abonnenten* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@subscriber_db=**] **"***Subscriber_db***"**  
 Ist der Name der Abonnementdatenbank. *Subscriber_db* ist **Sysname**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar(512)**|Vollständiger Pfad zum Momentaufnahmeverzeichnis.|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_browsesnapshotfolder** wird bei Momentaufnahme- und Transaktionsreplikation verwendet.  
  
 Wenn die *Abonnenten* und *Subscriber_db* Felder Wert NULL aufweisen, die gespeicherte Prozedur gibt den momentaufnahmeordner der die neueste Momentaufnahme, die sie für die Veröffentlichung finden kann. Wenn die *Abonnenten* und *Subscriber_db* Felder angegeben werden, wird die gespeicherte Prozedur gibt den momentaufnahmeordner für das angegebene Abonnement zurück. Wenn keine Momentaufnahme für die Veröffentlichung generiert wurde, wird ein leeres Resultset zurückgegeben.  
  
 Wenn die Veröffentlichung so eingerichtet ist, dass sie Momentaufnahmedateien sowohl im Arbeitsverzeichnis als auch im Momentaufnahmeordner des Verlegers generiert, dann enthält das Resultset zwei Zeilen. Die erste Zeile enthält den Veröffentlichungsmomentaufnahmeordner, und die zweite Zeile enthält das Verlegerarbeitsverzeichnis. **Sp_browsesnapshotfolder** eignet sich zum Ermitteln des Verzeichnisses, in dem momentaufnahmedateien generiert werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_browsesnapshotfolder**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
