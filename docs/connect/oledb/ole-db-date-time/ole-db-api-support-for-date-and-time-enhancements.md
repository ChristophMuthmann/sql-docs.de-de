---
title: OLE DB-API-Unterstützung für Datum und Uhrzeit-Verbesserungen | Microsoft Docs
description: OLE DB-API-Unterstützung für Datum und Uhrzeit-Verbesserungen
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 3018a0a1c190578608811ca4ffff4ba28abf2bdc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>OLE DB-API-Unterstützung für Datum und Uhrzeit-Verbesserungen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Die folgenden OLE DB-APIs unterstützen die erweiterten Funktionen für Datum und Uhrzeit.  
  
|Funktion|Description|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|Ein Flag wird hinzugefügt, in der DBBINDING-Struktur, um Anwendungen zu unterscheiden zwischen ermöglichen **"DateTime"**, **datetime2**, und **Smalldatetime** Werte. Weitere Informationen finden Sie unter [Parameter und Rowsets Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IBCPSession::BCPColFmt|Weitere Informationen finden Sie unter [Massenkopieränderungen für erweiterte Datums- und Uhrzeittypen &#40;OLE DB-&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md).|  
|ICommandWithParameters::GetParameterInfo|Weitere Informationen finden Sie unter[Parameter und Rowsets Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|ICommandWithParameters:: SetParameterInfo|Weitere Informationen finden Sie unter[Parameter und Rowsets Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Weitere Informationen finden Sie unter[Parameter und Rowsets Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Weitere Informationen finden Sie unter[Parameter und Rowsets Metadata](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset::GetRowset|Einzelheiten zu den betroffenen Schemarowsets finden Sie[Datum und Uhrzeit und Schemarowsets](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md).|  
|IRowsetFastLoad|Diese Schnittstelle unterstützt ohne Änderungen die neuen Datums-/Uhrzeit-Typen.|  
|ITableDefinition::CreateTable|Weitere Informationen finden Sie unter [Datentypunterstützung für OLE DB-Datum und Uhrzeit-Verbesserungen](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>Siehe auch  
 [Datum und Uhrzeit-Verbesserungen & #40; OLE DB & #41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
