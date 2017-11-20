---
title: execution_data_taps | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 54226c01-5b8f-4730-8a5f-1da2613f9689
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bc949b9b6111c65d6faa43a118efd03068630fe0
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexecutiondatataps"></a>catalog.execution_data_taps
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt Informationen für jede in einer Ausführung definierte Datenabzweigung an.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|data_tap_id|**bigint**|Eindeutiger Bezeichner (ID) der Datenabzweigung.|  
|execution_id|**bigint**|Der eindeutige Bezeichner (ID) für die Instanz der Ausführung.|  
|package_path|**nvarchar(max)**|Der Paketpfad für den Datenflusstask, in dem Daten abgerufen werden.|  
|dataflow_path_id_string|**nvarchar(4000)**|Die Identifikationszeichenfolge des Datenflusspfads.|  
|dataflow_task_guid|**uniqueidentifier**|Eindeutiger Bezeichner (ID) des Datenflusstasks.|  
|max_rows|**int**|Die Anzahl an zu erfassenden Zeilen. Wenn dieser Wert nicht angegeben ist, werden alle Zeilen erfasst.|  
|filename|**nvarchar(4000)**|Der Name der Datendumpdatei. Weitere Informationen finden Sie unter [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).|  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für die Instanz der Ausführung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
> [!NOTE]  
>  Wenn Sie über die Berechtigung verfügen, einen Vorgang auf dem Server auszuführen, verfügen Sie auch über die Berechtigung, Informationen zu dem Vorgang anzuzeigen. Sicherheit auf Zeilenebene wird erzwungen. Es werden nur Zeilen angezeigt, zu deren Anzeige Sie berechtigt sind.  
  
## <a name="see-also"></a>Siehe auch  
 [Generieren von Dumpdateien für die Paketausführung](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  

