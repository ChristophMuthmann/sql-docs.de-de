---
title: dm_server_memory_dumps (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_server_memory_dumps_TSQL
- dm_server_memory_dumps_TSQL
- dm_server_memory_dumps
- sys.dm_server_memory_dumps
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_memory_dumps dynamic management view
ms.assetid: 41782719-f54d-4e11-941a-c050c7576e23
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5d79c7817c44d87cc1a07ff13bd4c84acd450a33
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmservermemorydumps-transact-sql"></a>sys.dm_server_memory_dumps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Speicherabbilddatei generiert, indem Sie die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Verwenden Sie diese dynamische Verwaltungssicht, um potenzielle Probleme zu beheben.  
 
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Dateiname**|**nvarchar(256)**|Der Pfad und der Name der Speicherabbilddatei. Lässt keine NULL-Werte zu.|  
|**creation_time**|**datetimeoffset(7)**|Das Datum und die Uhrzeit, zu der die Datei erstellt wurde. Lässt keine NULL-Werte zu.|  
|**size_in_bytes**|**bigint**|Größe der Datei in Bytes. Lässt NULL-Werte zu.|  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Bei dem Speicherabbild (Dump) kann es sich um einen Minidump, einen Dump aller Threads oder um einen vollständigen Dump handeln. Die Dateien haben die Erweiterung ".mdmp".  
  
## <a name="security"></a>Sicherheit  
 Dumpdateien können vertrauliche Informationen enthalten. Zum Schutz vertraulicher Informationen können Sie eine Zugriffssteuerungsliste verwenden, um den Zugriff auf die Dateien einzuschränken oder die Dateien in einen Ordner mit eingeschränktem Zugriff zu kopieren. Bevor Sie Ihre Debugdateien beispielsweise an Microsoft Support Services senden, wird empfohlen, vertrauliche Informationen zu entfernen.  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung.  
  
  
