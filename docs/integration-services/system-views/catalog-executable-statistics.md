---
title: catalog.executable_statistics | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 3dda28d6-10d8-4294-9b5e-a6048c07faf9
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efd64e5612f10b3521849ff2da6103d2975f4830
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="catalogexecutablestatistics"></a>catalog.executable_statistics
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt eine Zeile für jede ausführbare Datei an, die ausgeführt wird, einschließlich der einzelnen Iterationen einer ausführbaren Datei.  
  
 Eine ausführbare Datei ist ein Task oder ein Container, den Sie der Ablaufsteuerung eines Pakets hinzufügen.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|Statistics_id|bigint|Eindeutige ID der Daten.|  
|Execution_id|bigint|Eindeutige ID für die Instanz der Ausführung.<br /><br /> Die catalog.executions-Sicht enthält weitere Informationen zu Ausführungen. Weitere Informationen finden Sie unter [catalog.executions (SSISDB Database)](../../integration-services/system-views/catalog-executions-ssisdb-database.md) (catalog.executions [SSISDB-Datenbank]).|  
|Executable_id|bigint|Eindeutige ID für die Paketkomponente.<br /><br /> Die catalog.executables-Sicht enthält weitere Informationen zu ausführbaren Dateien. Weitere Informationen finden Sie unter [catalog.executables](../../integration-services/system-views/catalog-executables.md).|  
|Execution_path|nvarchar(max)|Der vollständige Ausführungspfad der Paketkomponente, einschließlich der einzelnen Iterationen der Komponente.|  
|Start_time|datetimeoffset(7)|Der Zeitpunkt, zu dem die ausführbare Datei in die Phase vor der Ausführung eintritt.|  
|End_time|datetimeoffset(7)|Der Zeitpunkt, zu dem die ausführbare Datei in die Phase nach der Ausführung eintritt.|  
|Execution_duration|int|Der Zeitraum, über den sich die ausführbare Datei in der Ausführung befunden hat. Der Wert ist in Millisekunden angegeben.|  
|Execution_result|smallint|Folgende Werte sind möglich:<br /><br /> 0 (Erfolg)<br /><br /> 1 (Fehler)<br /><br /> 2 (Abschluss)<br /><br /> 3 (Abgebrochen)|  
|Execution_value|sql_variant|Der von der Ausführung zurückgegebene Wert. Dies ist ein benutzerdefinierter Wert.|  
  
## <a name="permissions"></a>Berechtigungen  
 Die Sicht erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für die Instanz der Ausführung.  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin** .  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
  
