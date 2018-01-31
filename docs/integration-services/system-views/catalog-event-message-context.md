---
title: catalog.event_message_context | Microsoft-Dokumentation
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
ms.assetid: 273a54f8-b107-4f36-9461-2b475644760d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 593931ad7aa343229cfac934cd2ce2648bdddb99
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="catalogeventmessagecontext"></a>catalog.event_message_context
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Zeigt Informationen zu den Bedingungen an, die Ausführungsereignismeldungen für Ausführungen auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Server zugeordnet sind.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|Context_id|BIGINT|Eindeutige ID für den Fehlerkontext.|  
|Event_message_id|BIGINT|Eindeutige ID für die Meldung, auf die sich der Kontext bezieht.|  
|Context_depth|ssNoversion|Je höher der Wert für die Tiefe, desto weiter entfernt vom Fehler befindet sich der Kontext. Wenn ein Fehler auftritt, startet die Kontexttiefe bei 1. Der Wert 0 gibt den Status des Pakets vor Beginn der Ausführung an.|  
|Package_path|Nvarchar(max)|Der Paketpfad für die Kontextquelle.|  
|Context_type|SMALLINT|Der Typ des Objekts, das als Quelle des Kontexts dient. Eine Liste der Kontexttypen finden Sie im Abschnitt **Hinweise**.|  
|Context_source_name|Nvarchar(4000)|Der Name des Objekts, das als Quelle des Kontexts dient.|  
|Context_source_id|Nvarchar(38)|Die eindeutige ID des Objekts, das als Quelle des Kontexts dient.|  
|Property_name|Nvarchar(4000)|Der Name der Eigenschaft, die der Quelle des Kontexts zugeordnet ist.|  
|Property_value|Sql_variant|Der Eigenschaftswert, der der Quelle des Kontexts zugeordnet ist.|  
  
## <a name="remarks"></a>Remarks  
 In der folgenden Tabelle sind die Kontexttypen aufgeführt.  
  
||||  
|-|-|-|  
|Wert des Kontexttyps|Typname|Description|  
|10|Task|Status einer Aufgabe beim Auftreten eines Fehlers.|  
|20|Pipeline|Fehler in einer Pipelinekomponente: Quelle, Ziel oder Transformationskomponente.|  
|30|Sequenz|Status einer Sequenz.|  
|40|For-Schleife|Status einer For-Schleife.|  
|50|Foreach-Schleife|Status einer Foreach-Schleife|  
|60|Paket|Status des Pakets beim Auftreten eines Fehlers.|  
|70|Variable|Variablenwert|  
|80|Ziel-Editor für Dimensionsverarbeitung|Eigenschaften eines Verbindungs-Managers.|  
  
## <a name="permissions"></a>Berechtigungen  
 Diese Sicht erfordert eine der folgenden Berechtigungen:  
  
-   READ-Berechtigung für den Vorgang  
  
-   Mitgliedschaft in der Datenbankrolle **ssis_admin** .  
  
-   Mitgliedschaft in der Serverrolle **sysadmin**  
  
  
