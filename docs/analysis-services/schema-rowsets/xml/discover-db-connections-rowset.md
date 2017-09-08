---
title: DISCOVER_DB_CONNECTIONS-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_DB_CONNECTIONS rowset
ms.assetid: 12a51a4e-5f3d-4449-9d94-7836fea1bc8b
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a592cffbf5d8fe19d37fc48989d9c2776df81a4e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="discoverdbconnections-rowset"></a>DISCOVER_DB_CONNECTIONS-Rowset
  Stellt Informationen zur Ressourcenauslastung und Aktivität der zurzeit geöffneten Verbindungen vom Server in einer Datenbank bereit.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_DB_CONNECTIONS** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CONNECTION_CATALOG_NAME**|**DBTYPE_WSTR**||Der Name der Datenbank, mit der zurzeit eine Verbindung besteht.|  
|**CONNECTION_ID**|**DBTYPE_I4**||Eine eindeutige Zahl, die die Verbindung identifiziert.|  
|**CONNECTION_IDLE_TIME_MS**|**DBTYPE_I8**||Die Leerlaufzeit in Millisekunden seit dem Start der Verbindung.|  
|**CONNECTION_IN_USE**|**DBTYPE_I4**||Gibt an, ob die Verbindung aktiv ist (1) oder sich im Leerlauf befindet (0).|  
|**CONNECTION_LAST_COMMAND_END_TIME**|**DBTYPE_DBTIMESTAMP**||UTC-Datum und -Zeit des Servers, zu denen der letzte Befehl seine Ausführung beendet hat.|  
|**CONNECTION_LAST_COMMAND_START_TIME**|**DBTYPE_DBTIMESTAMP**||UTC-Datum und -Zeit des Servers, zu denen der letzte Befehl seine Ausführung initiiert hat.|  
|**CONNECTION_SERVER_NAME**|**DBTYPE_WSTR**||Der Name des Servers, mit dem zurzeit eine Verbindung besteht.|  
|**CONNECTION_SPID**|**DBTYPE_I4**||Die Sitzungs-ID.|  
|**CONNECTION_START_TIME**|**DBTYPE_DBTIMESTAMP**||UTC-Datum und -Zeit des Servers, zu denen die Verbindung initiiert wurde.|  
|**CONNECTION_USAGE_TIME_MS**|**DBTYPE_I8**||Die Aktivitätszeit der Verbindung in Millisekunden seit dem Start der Verbindung.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
> [!IMPORTANT]  
>  Das **DISCOVER_DB_CONNECTIONS** -Rowset zeigt nur Informationen an, wenn der Dienst mit der relationalen Datenquelle verbunden ist.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DISCOVER_DB_CONNECTIONS** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|CONNECTION_ID|DBTYPE_I4|Optional.|  
|CONNECTION_IN_USE|DBTYPE_I4|Optional.|  
|CONNECTION_SERVER_NAME|DBTYPE_WSTR|Optional.|  
|CONNECTION_CATALOG_NAME|DBTYPE_WSTR|Erforderlich.|  
|CONNECTION_SPID|DBTYPE_I4|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis-Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
