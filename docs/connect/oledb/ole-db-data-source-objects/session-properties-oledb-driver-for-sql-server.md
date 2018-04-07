---
title: Eigenschaften von leistungssitzungen - OLE DB-Treiber für SQLServer | Microsoft Docs
description: Eigenschaften von leistungssitzungen - OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- OLE DB Driver for SQL Server, sessions
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8bc378d8b4ea414077e6d34f8f19720f27629460
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="session-properties---ole-db-driver-for-sql-server"></a>Eigenschaften von leistungssitzungen - OLE DB-Treiber für SQLServer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Der OLE DB-Treiber für SQL Server interpretiert OLE DB-Sitzungseigenschaften wie folgt aus.  
  
|Eigenschafts-ID|Description|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|Der OLE DB-Treiber für SQL Server unterstützt alle Autocommit Isolationsstufen von Transaktionen mit Ausnahme der chaosstufe DBPROPVAL_TI_CHAOS.|  
  
 Im anbieterspezifischen Eigenschaftensatz DBPROPSET_SQLSERVERSESSION definiert der OLE DB-Treiber für SQL Server die folgende zusätzliche Sitzungseigenschaft.  
  
|Eigenschafts-ID|Description|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|Typ: VT_BOOL<br /><br /> R/w: Lesen/Schreiben<br /><br /> Standard: VARIANT_FALSE<br /><br /> Beschreibung: In CATALOG-Einschränkung zugelassene Bezeichner in Anführungszeichen.<br /><br /> VARIANT_TRUE: Bezeichner in Anführungszeichen werden für eine CATALOG-Einschränkung für die Schemarowsets erkannt, die Unterstützung für verteilte Abfragen bieten.<br /><br /> VARIANT_FALSE: Bezeichner in Anführungszeichen werden nicht für eine CATALOG-Einschränkung für die Schemarowsets erkannt, die Unterstützung für verteilte Abfragen bieten.<br /><br /> Weitere Informationen zu Schemarowsets dar, die Unterstützung für verteilte Abfragen bieten, finden Sie unter [Unterstützung von verteilten Abfragen in Schemarowsets](../../oledb/ole-db/schema-rowsets-distributed-query-support.md).|  
|SSPROP_ALLOWNATIVEVARIANT|Typ: VT_BOOL<br /><br /> R/W: Lesen/Schreiben<br /><br /> Standard: VARIANT_FALSE<br /><br /> Beschreibung: Bestimmt, ob die Daten als DBTYPE_VARIANT oder DBTYPE_SQLVARIANT abgerufen werden.<br /><br /> VARIANT_TRUE: Der Spaltentyp wird als DBTYPE_SQLVARIANT zurückgegeben. In diesem Fall enthält der Puffer die SSVARIANT-Struktur.<br /><br /> VARIANT_FALSE: Der Spaltentyp wird als DBTYPE_VARIANT zurückgegeben und der Puffer enthält die VARIANT-Struktur.|  
|SSPROP_ASYNCH_BULKCOPY|Zur Verwendung des asynchronen Modus legen Sie die anbieterspezifische Sitzungseigenschaft SSPROP_ASYNCH_BULKCOPY vor dem Aufrufen der BCPExec-Methode auf VARIANT_TRUE fest. Diese Eigenschaft ist im DBPROPSET_SQLSERVERSESSION-Eigenschaftensatz verfügbar.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datenquellenobjekte & #40; OLE DB & #41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
