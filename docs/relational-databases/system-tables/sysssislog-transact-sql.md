---
title: Sysssislog (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
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
- sysdtslog90_TSQL
- sysdtslog90
dev_langs:
- TSQL
helpviewer_keywords:
- sysssislog system table
ms.assetid: 7fa288a1-81e3-42a0-82f6-8a59019693d0
caps.latest.revision: 
author: spelluru
ms.author: spelluru
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 479c6158f7c26cde133fae66164dda89b9a39888
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysssislog-transact-sql"></a>sysssislog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält eine Zeile für jeden Protokollierungseintrag, der von Paketen oder deren Tasks und Containern zur Laufzeit generiert wird. Diese Tabelle wird in der MSDB-Datenbank erstellt, wenn Sie [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installieren. Wenn Sie die Protokollierung so konfigurieren, dass eine andere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank protokolliert wird, wird in der angegebenen Datenbank eine sysssislog-Tabelle mit diesem Format erstellt.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Schreibt Protokolleinträge in diese Tabelle **nur** Pakete beim Verwenden der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Protokollanbieter.  
  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|Der eindeutige Bezeichner des Protokollierungseintrags.|  
|Ereignis|**sysname**|Der Name des Ereignisses, das den Protokollierungseintrag generiert hat.|  
|computer|**nvarchar**|Der Computer, auf dem das Paket ausgeführt wurde, als der Protokollierungseintrag generiert wurde.|  
|Operator|**nvarchar**|Der Benutzername der Person, die das Paket ausgeführt hat, das den Protokollierungseintrag generiert hat.|  
|Quelle|**nvarchar**|Der Name der ausführbaren Datei im Paket, das den Protokolleintrag generiert hat.|  
|sourceid|**uniqueidentifier**|Die GUID der ausführbaren Datei im Paket, das den Protokolleintrag generiert hat.|  
|executionid|**uniqueidentifier**|GUID der Ausführungsinstanz der ausführbaren Datei, die den Protokollierungseintrag generiert hat.|  
|starttime|**datetime**|Der Zeitpunkt, zu dem die Paketausführung gestartet wurde.|  
|endtime|**datetime**|Der Zeitpunkt, zu dem das Paket abgeschlossen wurde.<br /><br /> Diese Funktion ist nicht implementiert. Der Wert in der Spalte endtime entspricht immer dem Wert in der Spalte starttime.|  
|datacode|**int**|Ein optionaler ganzzahliger Wert, der in der Regel das Ergebnis der Ausführung des Containers oder der Task angibt.|  
|databytes|**image**|Ein optionales Bytearray, das weitere Informationen enthält.|  
|message|**nvarchar**|Eine Beschreibung des Ereignisses sowie die mit dem Ereignis verknüpften Informationen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Integrationsservices &#40; SSIS &#41; Protokollierung](../../integration-services/performance/integration-services-ssis-logging.md)   
  
  
