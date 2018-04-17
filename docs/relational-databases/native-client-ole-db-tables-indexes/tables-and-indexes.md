---
title: Tabellen und Indizes | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, indexes
- OLE DB, tables
- ITableDefinition interface
- tables [OLE DB]
- IIndexDefinition interface
- SQL Server Native Client OLE DB provider, tables
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: 4217c6d8-8cd2-43dc-b36f-3cfd8a58fabc
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ac3c3f79c946c3ddc01a3a39888133b995d3dccf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="tables-and-indexes"></a>Tabellen und Indizes
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter macht die **IIndexDefinition** und **ITableDefinition** Schnittstellen, ermöglicht es Consumern zu erstellen, ändern und Löschen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabellen und Indizes. Gültige Tabellen- und Indexdefinitionen hängen von der Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ab.  
  
 Die Möglichkeit, Tabellen und Indizes zu erstellen oder zu löschen, hängt von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Zugriffsrechten des Benutzers der Consumeranwendung ab. Das Löschen einer Tabelle kann durch das Vorhandensein von Beschränkungen der deklarativen referenziellen Integrität oder anderer Faktoren weiter eingeschränkt sein.  
  
 Die meisten Anwendungen, die für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden SQL-DMO statt dieser [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-anbieterschnittstellen. SQL-DMO steht für eine Auflistung von OLE-Automatisierungsobjekten, die alle administrativen Funktionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützen. Anwendungen, die auf mehrere OLE DB-Anbieter ausgerichtet sind, verwenden diese generischen OLE DB-Schnittstellen, die von den verschiedenen OLE DB-Anbietern unterstützt werden.  
  
 Im anbieterspezifischen Eigenschaftensatz DBPROPSET_SQLSERVERCOLUMN definiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die folgende Eigenschaft.  
  
|Eigenschafts-ID|Description|  
|-----------------|-----------------|  
|SSPROP_COL_COLLATIONNAME|Typ: VT_BSTR<br /><br /> R/W: Schreiben<br /><br /> Default: NULL<br /><br /> Beschreibung: Diese Eigenschaft dient nur in **ITableDefinition**. In dieser Eigenschaft angegebene Zeichenfolge verwendet wird, für die Erstellung einer [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)<br /><br /> verwendet.|  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Erstellen von SQL Server-Tabellen](../../relational-databases/native-client-ole-db-tables-indexes/creating-sql-server-tables.md)  
  
-   [Hinzufügen einer Spalte zu einer SQL Server-Tabelle](../../relational-databases/native-client-ole-db-tables-indexes/adding-a-column-to-a-sql-server-table.md)  
  
-   [Entfernen einer Spalte aus einer SQL Server-Tabelle](../../relational-databases/native-client-ole-db-tables-indexes/removing-a-column-from-a-sql-server-table.md)  
  
-   [Löschen einer SQL Server-Tabelle](../../relational-databases/native-client-ole-db-tables-indexes/dropping-a-sql-server-table.md)  
  
-   [Erstellen von SQL Server-Indizes](../../relational-databases/native-client-ole-db-tables-indexes/creating-sql-server-indexes.md)  
  
-   [Löschen eines SQL Server-Index](../../relational-databases/native-client-ole-db-tables-indexes/dropping-a-sql-server-index.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client & #40; OLE DB & #41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [DROP TABLE & #40; Transact-SQL & #41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
  
