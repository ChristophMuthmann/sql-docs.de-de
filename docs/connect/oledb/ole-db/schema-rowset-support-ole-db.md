---
title: Schemarowset-Unterstützung (OLE DB) | Microsoft Docs
description: Schemarowset-Unterstützung (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- OLE DB Driver for SQL Server, schema rowsets
- rowsets [OLE DB], schema
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3409a7a2d8ed7a047b2c2e5dcdf1a421084333ca
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="schema-rowset-support-ole-db"></a>Schemarowset-Unterstützung (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Der OLE DB-Treiber für SQL Server unterstützt auch zurückgegebene Schemainformationen von einem verknüpften Server, bei der Verarbeitung von [!INCLUDE[tsql](../../../includes/tsql-md.md)] verteilte Abfragen.  
  
> [!NOTE]  
>  Obwohl [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Synonyme unterstützt, werden Metadaten für Synonyme ist nicht vom OLE DB-Treiber für SQL Server zurückgegeben.  
  
 Die folgenden Tabellen enthalten die Schemarowsets und die Einschränkungsspalten vom OLE DB-Treiber für SQL Server unterstützt.  
  
|Schemarowset|Einschränkungsspalten|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMN_PRIVILEGES|Alle Einschränkungen werden unterstützt.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|DBSCHEMA_COLUMNS|Alle Einschränkungen werden unterstützt.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME<br /><br /> Die folgenden zusätzlichen Spalten gelten für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:<br /><br /> COLUMN_LCID, die Gebietsschema-ID der Sortierung. COLUMN_LCID ist der gleiche Wert wie eine Windows-LCID.<br /><br /> COLUMN_COMPFLAGS definiert, welche Vergleiche für die Sortierung unterstützt werden. Das Datenformat ist das Gleiche wie DBPROB_FINDCOMPAREOPS.<br /><br /> COLUMN_SORTID, das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Sortierungsformat für die Sortierung.<br /><br /> COLUMN_TDSCOLLATION, die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Sortierung für die Spalte.<br /><br /> IS_COMPUTED, mit dem Wert VARIANT_TRUE, wenn es sich um eine berechnete Spalte handelt, andernfalls VARIANT_FALSE.|  
|DBSCHEMA_FOREIGN_KEYS|Alle Einschränkungen werden unterstützt.<br /><br /> PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|DBSCHEMA_INDEXES|Einschränkungen 1, 2, 3 und 5 werden unterstützt.<br /><br /> TABLE_CATALOG TABLE_SCHEMA INDEX_NAME TABLE_NAME|  
|DBSCHEMA_PRIMARY_KEYS|Alle Einschränkungen werden unterstützt.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_PROCEDURE_PARAMETERS|Alle Einschränkungen werden unterstützt.<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|DBSCHEMA_PROCEDURES|Einschränkungen 1, 2 und 3 werden unterstützt.<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME<br /><br /> DBSCHEMA_PROCEDURES gibt nur Prozeduren zurück, die vom aktuellen Benutzer ausgeführt werden können bzw. für die der Benutzer die VIEW DEFINITION-Berechtigung erhalten hat.|  
|DBSCHEMA_PROVIDER_TYPES|Alle Einschränkungen werden unterstützt.<br /><br /> DATA_TYPE BEST_MATCH|  
|DBSCHEMA_SCHEMATA|Alle Einschränkungen werden unterstützt.<br /><br /> CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|DBSCHEMA_STATISTICS|Alle Einschränkungen werden unterstützt.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_TABLE_CONSTRAINTS|Alle Einschränkungen werden unterstützt.<br /><br /> CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|DBSCHEMA_TABLE_PRIVILEGES|Alle Einschränkungen werden unterstützt.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|DBSCHEMA_TABLES|Alle Einschränkungen werden unterstützt.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|DBSCHEMA_TABLES_INFO|Alle Einschränkungen werden unterstützt.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Unterstützung für verteilte Abfragen in Schemarowsets](../../oledb/ole-db/schema-rowsets-distributed-query-support.md)  
  
 [LINKEDSERVERS-Rowset &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQLServer &#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)   
 [Verwenden von benutzerdefinierten Typen](../../oledb/features/using-user-defined-types.md)  
  
  
