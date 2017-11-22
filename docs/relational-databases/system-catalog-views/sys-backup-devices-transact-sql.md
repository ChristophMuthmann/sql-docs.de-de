---
title: Sys. backup_devices (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- backup_devices_TSQL
- backup_devices
- sys.backup_devices
- sys.backup_devices_TSQL
dev_langs: TSQL
helpviewer_keywords:
- backup devices [SQL Server], viewing information
- sys.backup_devices catalog view
ms.assetid: 457edaa4-aca1-4bd3-bf8d-734490b80fcd
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f034c59979d5c64ba464c2da0df52f7b711a53fc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysbackupdevices-transact-sql"></a>sys.backup_devices (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jede registrierte mit Sicherungsmedium **Sp_addumpdevice** oder in erstellte [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Name des Sicherungsmediums. Ist im Sicherungssatz eindeutig.|  
|**Typ**|**tinyint**|Typ des Sicherungsmediums:<br /><br /> 2 = Datenträger<br /><br /> 3 = Diskette (veraltet)<br /><br /> 5 = Band<br /><br /> 6 = Pipe (veraltet)<br /><br /> 7 = Virtuelles Medium (für die optionale Verwendung von Drittsicherungsanbietern)<br /><br /> In der Regel werden nur Datenträger (2) und Band (5) verwendet.|  
|**type_desc**|**nvarchar(60)**|Beschreibung des Sicherungsmediumtyps:<br /><br /> DISK<br /><br /> DISKETTE (veraltet)<br /><br /> TAPE<br /><br /> PIPE (veraltet)<br /><br /> VIRTUAL_DEVICE (für die optionale Verwendung von Sicherungsdrittanbietern)<br /><br /> In der Regel werden nur DISK und TAPE verwendet.|  
|**physical_name**|**nvarchar(260)**|Physischer Dateiname oder Pfad des Sicherungsmediums.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [Datenbanken und Dateikatalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
