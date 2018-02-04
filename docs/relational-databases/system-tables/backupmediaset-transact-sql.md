---
title: Backupmediaset (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- backupmediaset
- backupmediaset_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], backupmediaset system table
- backupmediaset system table
ms.assetid: d9c18a93-cab9-4db8-ae09-c6bd8145ab8f
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 334c7cbcb3afb00685049aafbb2c0a290ba97a2a
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="backupmediaset-transact-sql"></a>backupmediaset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden Sicherungsmediensatz. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
 
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|Eindeutige Mediensatz-ID zurück. Identität, Primärschlüssel.|  
|**media_uuid**|**uniqueidentifier**|UUID des Mediensatzes. Alle [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Mediensätze haben eine UUID.<br /><br /> Für frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]jedoch, wenn ein Mediensatz nur eine Medienfamilie enthält die **Media_uuid** Spalte kann NULL sein (**Media_family_count** 1).|  
|**media_family_count**|**tinyint**|Die Anzahl der Medienfamilien im Mediensatz. Kann den Wert NULL haben.|  
|**name**|**nvarchar(128)**|Name des Mediensatzes. Kann den Wert NULL haben.<br /><br /> Weitere Informationen finden Sie unter MEDIANAME und MEDIADESCRIPTION in [BACKUP &#40; Transact-SQL &#41; ](../../t-sql/statements/backup-transact-sql.md).|  
|**description**|**nvarchar(255)**|Textbeschreibung des Mediensatzes. Kann den Wert NULL haben.<br /><br /> Weitere Informationen finden Sie unter MEDIANAME und MEDIADESCRIPTION in [BACKUP &#40; Transact-SQL &#41; ](../../t-sql/statements/backup-transact-sql.md).|  
|**software_name**|**nvarchar(128)**|Name der Sicherungssoftware, mit der die Medienbezeichnung geschrieben wurde. Kann den Wert NULL haben.|  
|**software_vendor_id**|**int**|ID des Softwareanbieters, der die Sicherungsmedienbezeichnung geschrieben hat. Kann den Wert NULL haben.<br /><br /> Der Wert für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hexadezimal 0 x 1200 ist.|  
|**MTF_major_version**|**tinyint**|Hauptversionsnummer von MTF ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Tape Format), das zum Generieren dieses Mediensatzes verwendet wurde. Kann den Wert NULL haben.|  
|**mirror_count**|**tinyint**|Anzahl der Spiegel im Mediensatz.|  
|**is_password_protected**|**bit**|Gibt an, ob der Mediensatz kennwortgeschützt ist:<br /><br /> 0 = Nicht geschützt<br /><br /> 1 = Geschützt|  
|**is_compressed**|**bit**|Gibt an, ob die Sicherung komprimiert ist:<br /><br /> 0 = nicht komprimiert<br /><br /> 1 = komprimiert<br /><br /> Während einer **Msdb** ein Upgrade ausführen, wird dieser Wert auf NULL festgelegt. Dies gibt eine nicht komprimierte Sicherung an.|  
|**is_encrypted**|**Bit**|Gibt an, ob die Sicherung verschlüsselt ist:<br /><br /> 0 = nicht verschlüsselt<br /><br /> 1 = Verschlüsselt.|  
  
## <a name="remarks"></a>Hinweise  
 RESTORE VERIFYONLY FROM *Backup_device* WITH LOADHISTORY füllt die Spalten von der **Backupmediaset** Tabelle mit den entsprechenden Werten aus dem mediensatzheader.  
  
 Um die Anzahl der Zeilen in dieser Tabelle und in anderen Tabellen sicherungs- und Verlaufstabellen zu verringern, führen Sie die [Sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) gespeicherte Prozedur.  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern und Wiederherstellen von Tabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [System Tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
