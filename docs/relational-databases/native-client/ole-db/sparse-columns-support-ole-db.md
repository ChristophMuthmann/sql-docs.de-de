---
title: "Unterstützung für Spalten mit geringer Dichte (OLE DB) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 918574b3-c62e-4937-9e5f-37310dedc8f9
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 83781fb2194f5ef94ea7a73a8c32017ceb25424a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="sparse-columns-support-ole-db"></a>Unterstützung für Spalten mit geringer Dichte (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Dieses Thema enthält Informationen über [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Unterstützung für Spalten mit geringer Dichte. Weitere Informationen zu Sparsespalten finden Sie unter [Sparse Columns Support in SQL Server Native Client](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md). Ein Beispiel finden Sie unter [Anzeigen von Spalten- und Katalogmetadaten für Spalten mit geringer Dichte &#40; OLE DB &#41;](../../../relational-databases/native-client-ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md).  
  
## <a name="ole-db-statement-metadata"></a>OLE DB-Anweisungsmetadaten  
 Beginnend mit [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], ein neuer DBCOLUMNFLAGS-Flagwert, DBCOLUMNFLAGS_SS_ISCOLUMNSET, verfügbar ist. Dieser Wert sollte für Spalten festgelegt werden, die **column_set** -Werte sind. Das DBCOLUMNFLAGS-Flag kann abgerufen werden, über die *DwFlags* Parameter IColumnsInfo:: GetColumnsInfo und die DBCOLUMN_FLAGS-Spalte des Rowsets IColumnsRowset:: GetColumnsRowset zurückgegebenes.  
  
## <a name="ole-db-catalog-metadata"></a>OLE DB-Katalogmetadaten  
 Zwei zusätzliche [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-spezifische Spalten wurden zu DBSCHEMA_COLUMNS hinzugefügt.  
  
|Spaltenname|Datentyp|Wert/Kommentare|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|Wenn die Spalte eine Sparsespalte ist, weist sie den Wert VARIANT_TRUE auf, andernfalls den Wert VARIANT_FALSE.|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|Wenn die Spalte die **column_set** -Sparsespalte ist, weist sie den Wert VARIANT_TRUE auf, andernfalls den Wert VARIANT_FALSE.|  
  
 Zwei zusätzliche Schemarowsets wurden ebenfalls hinzugefügt. Diese Rowsets verfügen über die gleiche Struktur wie DBSCHEMA_COLUMNS, geben aber andere Inhalte zurück. DBSCHEMA_COLUMNS_EXTENDED gibt alle Spalten zurück, unabhängig davon, ob sie Elemente von **column_set** sind. DBSCHEMA_SPARSE_COLUMN_SET gibt nur Spalten zurück, die Elemente des Sparse-**column_set** sind.  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>OLE DB DataTypeCompatibility-Verhalten  
 Verhalten bei **DataTypeCompatibility = 80** (in der Verbindungszeichenfolge) ist konsistent mit einem [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] -Client wie folgt:  
  
-   Die neuen Schemarowsets sind nicht sichtbar, und es gibt keine Zeilen für sie im Rowset der Schemarowsets.  
  
-   Neue Spalten im COLUMNS-Rowset sind nicht sichtbar.  
  
-   DBCOLUMNFLAGS_SS_ISCOLUMNSET wird nicht für **column_set** -Spalten festgelegt.  
  
-   DBCOMPUTEMODE_NOTCOMPUTED wird für **column_set** -Spalten festgelegt.  
  
## <a name="ole-db-support-for-sparse-columns"></a>OLE DB-Unterstützung für Spalten mit geringer Dichte  
 Die folgenden OLE DB-Schnittstellen wurden in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client geändert, um Sparsespalten zu unterstützen:  
  
|Typ oder Elementfunktion|Description|  
|-----------------------------|-----------------|  
|IColumnsInfo::GetColumnsInfo|Ein neuer DBCOLUMNFLAGS-Flagwert, DBCOLUMNFLAGS_SS_ISCOLUMNSET, wird für **column_set** -Spalten in *dwFlags*festgelegt.<br /><br /> DBCOLUMNFLAGS_WRITE wird für **column_set** -Spalten festgelegt.|  
|IColumsRowset::GetColumnsRowset|Ein neuer DBCOLUMNFLAGS-Flagwert, DBCOLUMNFLAGS_SS_ISCOLUMNSET, wird für **column_set** -Spalten in DBCOLUMN_FLAGS festgelegt.<br /><br /> DBCOLUMN_COMPUTEMODE wird für **column_set** -Spalten auf DBCOMPUTEMODE_DYNAMIC festgelegt.|  
|IDBSchemaRowset::GetSchemaRowset|DBSCHEMA_COLUMNS gibt zwei neue Spalten zurück: SS_IS_COLUMN_SET und SS_IS_SPARSE.<br /><br /> DBSCHEMA_COLUMNS gibt nur Spalten zurück, die keine Elemente eines **column_set**sind.<br /><br /> Zwei neue Schemarowsets wurden hinzugefügt: DBSCHEMA_COLUMNS_EXTENDED gibt alle Spalten zurück, unabhängig davon, ob sie eine geringe Dichte aufweisen oder Elemente von **column_set** sind. DBSCHEMA_SPARSE_COLUMN_SET gibt nur Spalten zurück, die Elemente eines **column_set**sind. Diese neuen Rowsets verfügen über die gleichen Spalten und die Einschränkungen wie DBSCHEMA_COLUMNS.|  
|IDBSchemaRowset::GetSchemas|IDBSchemaRowset:: GetSchemas schließt die GUIDs für die neuen Rowsets DBSCHEMA_COLUMNS_EXTENDED und DBSCHEMA_SPARSE_COLUMN_SET in der Liste verfügbarer Schemarowsets.|  
|ICommand::Execute|Wenn **wählen \* aus** *Tabelle* wird verwendet, werden alle Spalten, die keine Elemente mit geringer Dichte zurückgegeben **Column_set**, zuzüglich einer XML-Spalte, die Werte aller enthält nicht-Null-Spalten, die Elemente mit geringer Dichte **Column_set**, falls vorhanden.|  
|IOpenRowset::OpenRowset|IOpenRowset:: OPENROWSET gibt ein Rowset mit den gleichen Spalten als ICommand:: Execute, mit einem **wählen \***  Abfrage in der gleichen Tabelle.|  
|ITableDefinition|Es gibt keine Änderungen an dieser Schnittstelle für Sparsespalten oder für **column_set** -Spalten. Anwendungen, die Schemaänderungen vornehmen müssen, müssen das entsprechende [!INCLUDE[tsql](../../../includes/tsql-md.md)] direkt ausführen.|  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
