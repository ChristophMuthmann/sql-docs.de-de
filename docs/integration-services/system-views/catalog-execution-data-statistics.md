---
title: catalog.execution_data_statistics | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 6f51407e-0e4e-4b44-af33-db14c9d40ded
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a5463b9da862b8ebeb3f9f769da7a22dde6867b6
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="catalogexecutiondatastatistics"></a>catalog.execution_data_statistics
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In dieser Sicht wird eine Zeile angezeigt, sobald eine Datenflusskomponente Daten für eine bestimmte Paketausführung an eine Downstreamkomponente sendet. Anhand der Informationen in dieser Sicht kann der Datendurchsatz für eine Komponente berechnet werden.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|data_stats_id|**bigint**|Eindeutiger Bezeichner (ID) der Daten.|  
|execution_id|**bigint**|Eindeutige ID für die Instanz der Ausführung.|  
|package_name|**nvarchar(260)**|Der Name des ersten Pakets, das während der Ausführung gestartet wurde.|  
|task_name|**nvarchar(4000)**|Der Name des Datenflusstask.|  
|dataflow_path_id_string|**nvarchar(4000)**|Die Identifikationszeichenfolge des Datenflusspfads.|  
|dataflow_path_name|**nvarchar(4000)**|Der Name des Datenflusspfads.|  
|source_component_name|**nvarchar(4000)**|Der Namen der Datenflusskomponente, die die Daten gesendet hat.|  
|destination_component_name|**nvarchar(4000)**|Der Namen der Datenflusskomponente, die die Daten empfangen hat.|  
|rows_sent|**bigint**|Die Anzahl der Zeilen, die von der Quellkomponente gesendet wurden.|  
|created_time|**datatimeoffset(7)**|Die Zeit, zu der die Werte abgerufen wurden.|  
|execution_path|**nvarchar(max)**|Der Ausführungspfad der Komponente.|  
  
## <a name="remarks"></a>Remarks  
  
-   Wenn eine Komponente mehrere Ausgaben hat, wird für jede Ausgabe eine Zeile hinzugefügt.  
  
-   Standardmäßig werden beim Starten einer Ausführung keine Informationen über die Anzahl der gesendeten Zeilen protokolliert.  
  
-   Um diese Daten für eine bestimmte Paketausführung anzuzeigen, legen Sie den Protokolliergrad auf **Ausführlich** fest. Weitere Informationen finden Sie unter [Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für die Instanz der Ausführung  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin**  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
> [!NOTE]  
>  Wenn Sie über die Berechtigung verfügen, einen Vorgang auf dem Server auszuführen, verfügen Sie auch über die Berechtigung, Informationen zu dem Vorgang anzuzeigen. Sicherheit auf Zeilenebene wird erzwungen. Es werden nur Zeilen angezeigt, zu deren Anzeige Sie berechtigt sind.  
  
  
