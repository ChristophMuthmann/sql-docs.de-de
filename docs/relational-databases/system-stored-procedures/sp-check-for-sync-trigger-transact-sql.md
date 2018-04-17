---
title: Sp_check_for_sync_trigger (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- filter_TSQL
- sp_check_for_sync_trigger
helpviewer_keywords:
- sp_check_for_sync_trigger
ms.assetid: 54a1e2fd-c40a-43d4-ac64-baed28ae4637
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 38dfc81498173fe6024095889d06d222d4d98201
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spcheckforsynctrigger-transact-sql"></a>sp_check_for_sync_trigger (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Bestimmt, ob ein benutzerdefinierter Trigger oder eine benutzerdefinierte gespeicherte Prozedur im Kontext eines Replikationstriggers aufgerufen wird, der für sofort aktualisierbare Abonnements verwendet wird. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank oder auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_check_for_sync_trigger [ @tabid = ] 'tabid'   
    [ , [ @trigger_op = ] 'trigger_output_parameters' OUTPUT ]  
    [ , [ @fonpublisher = ] fonpublisher ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@tabid =** ] "*Tabid*"  
 Die Objekt-ID der Tabelle, die auf sofort aktualisierbare Trigger überprüft wird. *Tabid* ist **Int** hat keinen Standardwert.  
  
 [ **@trigger_op =** ] "*Trigger_output_parameters*" Ausgabe  
 Gibt an, ob der Ausgabeparameter den Typ von Trigger zurückgeben muss, mit dem er aufgerufen wird. *Trigger_output_parameters* ist **char(10)** und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Ins**|INSERT-Trigger|  
|**UPD**|UPDATE-Trigger|  
|**Del**|DELETE-Trigger|  
|NULL (Standard)||  
  
 [  **@fonpublisher =** ] *Fonpublisher*  
 Gibt die Position an, an der die gespeicherte Prozedur ausgeführt wird. *Fonpublisher* ist **Bit**, hat den Standardwert 0. Bei 0 findet die Ausführung auf dem Abonnenten und bei 1 auf dem Verleger statt.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 zeigt an, dass die gespeicherte Prozedur nicht im Kontext eines sofort aktualisierbaren Triggers aufgerufen wird. 1 gibt an, dass es im Kontext eines sofort aktualisierbaren Triggers aufgerufen wird, ist der Typ des Triggers zurückgegeben wird *@trigger_op*.  
  
## <a name="remarks"></a>Hinweise  
 **Sp_check_for_sync_trigger** wird bei Momentaufnahme- und Transaktionsreplikation verwendet.  
  
 **Sp_check_for_sync_trigger** wird verwendet, um die Koordination zwischen replikationstriggern und benutzerdefinierten Triggern. Diese gespeicherte Prozedur bestimmt, ob sie im Kontext eines Replikationstriggers aufgerufen wird. Beispielsweise können Sie die Prozedur aufrufen **Sp_check_for_sync_trigger** im Text eines benutzerdefinierten Triggers. Wenn **Sp_check_for_sync_trigger** gibt **0**, der benutzerdefinierte Trigger setzt die Verarbeitung fort. Wenn **Sp_check_for_sync_trigger** gibt **1**, der benutzerdefinierte Trigger beendet wird. So wird sichergestellt, dass der benutzerdefinierte Trigger nicht ausgelöst wird, wenn der Replikationstrigger die Tabelle aktualisiert.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird Code dargestellt, der in einem Trigger in der Abonnententabelle verwendet werden kann.  
  
```  
DECLARE @retcode int, @trigger_op char(10), @table_id int  
SELECT @table_id = object_id('tablename')  
EXEC @retcode = sp_check_for_sync_trigger @table_id, @trigger_op OUTPUT  
IF @retcode = 1  
RETURN  
```  
  
## <a name="example"></a>Beispiel  
 Der Code kann auch einem Trigger in einer Tabelle auf dem Verleger hinzugefügt werden; der Code ist ähnlich, aber der Aufruf von **Sp_check_for_sync_trigger** enthält einen zusätzlichen Parameter.  
  
```  
DECLARE @retcode int, @trigger_op char(10), @table_id int, @fonpublisher int  
SELECT @table_id = object_id('tablename')  
SELECT @fonpublisher = 1  
EXEC @retcode = sp_check_for_sync_trigger @table_id, @trigger_op OUTPUT, @fonpublisher  
IF @retcode = 1  
RETURN  
```  
  
## <a name="permissions"></a>Berechtigungen  
 **Sp_check_for_sync_trigger** gespeicherte Prozedur ausgeführt werden kann, von jedem Benutzer mit SELECT-Berechtigungen in der [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) -Systemsicht.  
  
## <a name="see-also"></a>Siehe auch  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
