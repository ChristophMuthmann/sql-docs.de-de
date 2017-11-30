---
title: Sp_helpdevice (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
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
- sp_helpdevice
- sp_helpdevice_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpdevice
ms.assetid: 1a5eafa7-384e-4691-ba05-978eb73bbefb
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a39dcc6cd75837017826fdcf9b37ff7d6a3598c9
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpdevice-transact-sql"></a>sp_helpdevice (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Meldet Informationen zu Microsoft® SQL Server™-Sicherungsmedien.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Wir empfehlen die Verwendung der [backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md) stattdessen die Katalogsicht  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpdevice [ [ @devname = ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@devname =** ] **"***Namen***"**  
 Der Name des Sicherungsmediums, für das Informationen gemeldet werden. Der Wert von *name* ist immer **sysname**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Gerätename**|**sysname**|Logischer Medienname.|  
|**physical_name**|**nvarchar(260)**|Physischer Dateiname.|  
|**Beschreibung**|**nvarchar(255)**|Beschreibung des Mediums.|  
|**status**|**int**|Eine Nummer, die der Statusbeschreibung in der **description** -Spalte entspricht.|  
|**CntrlType**|**smallint**|Controllertyp des Mediums:<br /><br /> 2 = Datenträgermedium<br /><br /> 5 = Bandmedium|  
|**Größe**|**int**|Mediengröße in Seiten von je 2 KB.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn *name* angegeben wird, zeigt **sp_helpdevice** Informationen zu dem angegebenen Sicherungsmedium an. Wenn *name* nicht angegeben wird, zeigt **sp_helpdevice** Informationen zu allen Sicherungsmedien in der **sys.backup_devices** -Katalogsicht an.  
  
 Sicherungsmedien werden dem System mithilfe von **sp_addumpdevice**hinzugefügt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgende Beispiel werden Informationen zu allen Sicherungsmedien in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXEC sp_helpdevice;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [Datenbankmodul gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
