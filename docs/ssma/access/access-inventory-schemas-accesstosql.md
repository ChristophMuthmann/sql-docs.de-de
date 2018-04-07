---
title: Zugriff auf Lager Schemas (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- columns table
- databases table
- exported metadata
- exporting, schemas of exported metadata
- foreign keys table
- forms table
- indexes, table
- inventory schemas
- macros table
- modules table
- queries table
- reference, inventory schemas
- reports table
- schemas of exported metadata
- schemas, exported metadata
- SSMA_Access_InventoryColumns
- SSMA_Access_InventoryDatabases
- SSMA_Access_InventoryForeignKeys
- SSMA_Access_InventoryForms
- SSMA_Access_InventoryIndexes
- SSMA_Access_InventoryMacros
- SSMA_Access_InventoryModules
- SSMA_Access_InventoryQueries
- SSMA_Access_InventoryReports
- SSMA_Access_InventoryTables
- tables, inventory
ms.assetid: fdd3cff2-4d62-4395-8acf-71ea8f17f524
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d68215dd768a2fbd4e6723d7ca98ef9a5c96c72d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="access-inventory-schemas-accesstosql"></a>Access-Inventur-Schemas (AccessToSQL)
In den folgenden Abschnitten wird beschrieben, die Tabellen, die von SSMA erstellt werden, wenn Sie zu Access-Schemas exportieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="databases"></a>Datenbanken  
Datenbank-Metadaten in exportiert wird die **SSMA_Access_InventoryDatabases** Tabelle. Diese Tabelle enthält die folgenden Spalten:  
  
|Spaltenname|Datentyp|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Eine GUID, die jede Datenbank eindeutig identifiziert. Diese Spalte wird auch der Primärschlüssel für die Tabelle.|  
|**DatabaseName**|**nvarchar(4000)**|Der Name der Access-Datenbank.|  
|**ExportTime**|**datetime**|Datum und Uhrzeit der Erstellung dieser Metadaten von SSMA.|  
|**FilePath**|**nvarchar(4000)**|Der vollständige Pfad und Name der Access-Datenbank.|  
|**FileSize**|**bigint**|Die Größe der Access-Datenbank in KB.|  
|**FileOwner**|**nvarchar(4000)**|Das Windows-Konto, das als Besitzer der Access-Datenbank angegeben ist.|  
|**DateCreated**|**datetime**|Das Datum und Uhrzeit der Erstellung die Access-Datenbank.|  
|**DateModified**|**datetime**|Das Datum und Uhrzeit der letzten die Access-Datenbank Änderung.|  
|**TablesCount**|**int**|Die Anzahl der Tabellen in der Access-Datenbank.|  
|**QueriesCount**|**int**|Die Anzahl der Abfragen in der Access-Datenbank.|  
|**FormsCount**|**int**|Die Anzahl der Formulare in der Access-Datenbank.|  
|**ModulesCount**|**int**|Die Anzahl der Module in der Access-Datenbank.|  
|**ReportsCount**|**int**|Die Anzahl der Berichte in der Access-Datenbank.|  
|**MacrosCount**|**int**|Die Anzahl der Makros in der Access-Datenbank.|  
|**AccessVersion**|**nvarchar(4000)**|Die Access-Version der Datenbank.|  
|**Sortierung**|**nvarchar(4000)**|Die Sortierung der Access-Datenbank. Sortierungen bestimmen, wie eine Datenbank sortiert und vergleicht Zeichenfolgen.|  
|**JetVersion**|**nvarchar(4000)**|Die Version der Jet-Datenbank-Engine. Access-Datenbanken verwenden Sie das zugrunde liegende Jet-Datenbankmodul.|  
|**IsUpdatable**|**bit**|Gibt an, ob die Datenbank aktualisiert werden kann. Wenn der Wert 1 ist, kann die Datenbank aktualisiert werden. Wenn der Wert 0 ist, ist die Datenbank schreibgeschützt.|  
|**QueryTimeout**|**int**|Konfigurierte ODBC-Wert für das Abfragetimeout für die Datenbank, in Sekunden. Der Standardwert ist 60 Sekunden.|  
  
## <a name="tables"></a>Tabellen  
Tabellenmetadaten ist exportiert der **SSMA_Access_InventoryTables** Tabelle. Diese Tabelle enthält die folgenden Spalten:  
  
|Spaltenname|Datentyp|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifiziert die Datenbank, die diese Tabelle enthält.|  
|**TableId**|**uniqueidentifier**|Eine GUID, die die Tabelle eindeutig identifiziert. Diese Spalte wird auch der Primärschlüssel für die Tabelle.|  
|**TableName**|**nvarchar(4000)**|Der Name der Tabelle.|  
|**RowsCount**|**int**|Anzahl der Zeilen in der Tabelle.|  
|**ValidationRule**|**nvarchar(4000)**|Die Regel, die gültigen Eingaben für die Tabelle definiert. Wenn es wurde keine Gültigkeitsprüfungsregel vorhanden ist, wird das Feld eine leere Zeichenfolge enthalten.|  
|**LinkedTable**|**nvarchar(4000)**|Eine andere Tabelle, sofern vorhanden, die mit der Tabelle verknüpft ist. Ermöglicht das Verknüpfen von Tabellen Hinzufügungen, löschungen und Updates für die andere Tabelle mithilfe dieser Tabelle.|  
|**ExternalSource**|**nvarchar(4000)**|Die Datenquelle ist ggf., die der Tabelle zugeordnet. Wenn eine Tabelle verknüpft ist, muss es sich um eine externe Datenquelle, die in diesem Feld angegeben.|  
  
## <a name="columns"></a>Spalten  
Spaltenmetadaten ist exportiert der **SSMA_Access_InventoryColumns** Tabelle. Diese Tabelle enthält die folgenden Spalten:  
  
|Spaltenname|Datentyp|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifiziert die Datenbank, die diese Spalte enthält.|  
|**TableId**|**uniqueidentifier**|Identifiziert die Tabelle, die diese Spalte enthält.|  
|**ColumnId**|**int**|Eine ganze Zahl erhöht die Spalte angibt. **ColumnId** ist der Primärschlüssel für die Tabelle.|  
|**ColumnName**|**nvarchar(4000)**|Name der Spalte.|  
|**IsNullable**|**bit**|Gibt an, ob die Spalte null-Werte enthalten kann. Wenn der Wert 1 ist, kann die Spalte null-Werte enthalten. Wenn der Wert 0 ist, kann nicht in die Spalte null-Werte enthalten. Beachten Sie, dass die Validierungsregel auch verwendet werden kann, um zu verhindern, dass null-Werte.|  
|**DataType**|**nvarchar(4000)**|Der Access-Datentyp der Spalte, wie z. B. **Text** oder **lang**.|  
|**IsAutoIncrement**|**bit**|Gibt an, ob ganzzahligen Werten in die Spalte automatisch inkrementiert wird. Wenn der Wert 1 ist, werden die ganzen Zahlen automatisch inkrementiert.|  
|**Ordinal**|**smallint**|Die Reihenfolge der Spalte in der Tabelle, beginnend mit 0 (null).|  
|**DefaultValue**|**nvarchar(4000)**|Der Standardwert für die Spalte.|  
|**ValidationRule**|**nvarchar(4000)**|Die Regel, die zum Überprüfen der Daten, die hinzugefügt oder aktualisiert werden, in der Spalte verwendet wird.|  
  
## <a name="indexes"></a>Indizes  
Indexmetadaten werden exportiert, um die **SSMA_Access_InventoryIndexes** Tabelle. Diese Tabelle enthält die folgenden Spalten:  
  
|Spaltenname|Datentyp|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifiziert die Datenbank, die diesen Index enthält.|  
|**TableId**|**uniqueidentifier**|Identifiziert die Tabelle, die diesen Index enthält.|  
|**IndexId**|**int**|Inkrementelle eine ganze Zahl, die den Index angibt. Diese Spalte ist der Primärschlüssel für die Tabelle.|  
|**IndexName**|**nvarchar(4000)**|Der Name des Index.|  
|**ColumnsIncluded**|**nvarchar(4000)**|Listet die Spalten, die im Index enthalten sind. Die Spaltennamen werden durch ein Semikolon getrennt.|  
|**IsUnique**|**bit**|Gibt an, ob jedes Element im Index eindeutig sein muss. Für einen mehrspaltigen Index muss die Kombination der Werte eindeutig sein. Wenn der Wert 1 ist, wird der Index eindeutige Werte erzwungen.|  
|**IsPK**|**bit**|Gibt an, ob der Index automatisch als Teil der Definition des primären Schlüssels erstellt wurde.|  
|**IsClustered**|**bit**|Gibt an, ob der Index gruppiert ist. Ein gruppierter Index sortiert die physische Speicherung von Daten. Eine Tabelle kann nur ein gruppierten Index haben.|  
  
## <a name="foreign-keys"></a>Fremdschlüssel  
Foreign Key-Metadaten ist exportiert der **SSMA_Access_InventoryForeignKeys** Tabelle. Diese Tabelle enthält die folgenden Spalten:  
  
|Spaltenname|Datentyp|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifiziert die Datenbank, die diese Fremdschlüssel enthält.|  
|**TableId**|**uniqueidentifier**|Identifiziert die Tabelle, die diese Fremdschlüssel enthält.|  
|**ForeignKeyId**|**int**|Inkrementelle eine ganze Zahl, die den Fremdschlüssel identifiziert. Diese Spalte ist der Primärschlüssel für die Tabelle.|  
|**ForeignKeyName**|**nvarchar(4000)**|Der Name des Index.|  
|**ReferencedTableId**|**uniqueidentifier**|Identifiziert die Tabelle, die die Quellspalten enthält.|  
|**SourceColumns**|**nvarchar(4000)**|Listet die foreign Key-Spalte oder Spalten.|  
|**ReferencedColumns**|**nvarchar(4000)**|Listet die Primärschlüsselspalte oder Spalten, die vom Fremdschlüssel verwiesen werden.|  
|**IsCascadeForUpdate**|**bit**|Gibt an, dass alle Zeilen, die auf dieses Schlüsselwerts zu verweisen, wenn der Primärschlüsselwert aktualisiert wird, auch aktualisiert werden.|  
|**IsCascadeForDelete**|**bit**|Gibt an, wenn der Primärschlüsselwert gelöscht wird, werden alle Zeilen, die auf dieses Schlüsselwerts verweisen ebenfalls gelöscht.|  
|**IsEnforced**|**bit**|Gibt an, dass die foreign Key-Einschränkung erzwungen wird.|  
  
## <a name="queries"></a>Abfragen  
Abfragemetadaten ist exportiert der **SSMA_Access_InventoryQueries** Tabelle. Diese Tabelle enthält die folgenden Spalten:  
  
|Spaltenname|Datentyp|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifiziert die Datenbank, die diese Abfrage enthält.|  
|**QueryId**|**int**|Inkrementelle eine ganze Zahl, die die Abfrage identifiziert. Diese Spalte ist der Primärschlüssel für die Tabelle.|  
|**QueryName**|**nvarchar(4000)**|Der Name der Abfrage.|  
|**QueryText**|**nvarchar(4000)**|Code der SQL-Abfrage, z. B. eine SELECT-Anweisung.|  
|**IsUpdateable**|**bit**|Gibt an, ob die Abfrage aktualisierbar oder schreibgeschützt ist.|  
|**QueryType**|**nvarchar(4000)**|Gibt den Typ der Abfrage, z. B. **wählen** oder **SetOperation**.|  
|**ExternalSource**|**nvarchar(4000)**|Wenn die Abfrage eine externen Datenquelle verweist, ist dies die von der Abfrage verwendeten Verbindungszeichenfolge.|  
  
## <a name="forms"></a>Formulare  
In von Formularmetadaten exportiert wird die **SSMA_Access_InventoryForms** Tabelle. Diese Tabelle enthält die folgenden Spalten:  
  
|Spaltenname|Datentyp|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifiziert die Datenbank, die dieses Formular enthält.|  
|**FormId**|**int**|Inkrementelle eine ganze Zahl, die das Formular identifiziert. Diese Spalte ist der Primärschlüssel für die Tabelle.|  
|**FormName**|**nvarchar(4000)**|Der Name des Formulars.|  
  
## <a name="macros"></a>Makros  
Makro-Metadaten werden exportiert, auf die **SSMA_Access_InventoryMacros** Tabelle. Diese Tabelle enthält die folgenden Spalten:  
  
|Spaltenname|Datentyp|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifiziert die Datenbank, die das Makro enthält.|  
|**MacroId**|**int**|Inkrementelle eine ganze Zahl, die das Makro identifiziert. Diese Spalte ist der Primärschlüssel für die Tabelle.|  
|**MacroName**|**nvarchar(4000)**|Der Name des Makros.|  
  
## <a name="reports"></a>Berichte  
Berichtsmetadaten ist exportiert der **SSMA_Access_InventoryReports** Tabelle. Diese Tabelle enthält die folgenden Spalten:  
  
|Spaltenname|Datentyp|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifiziert die Datenbank mit dem Bericht.|  
|**ReportId**|**int**|Inkrementelle eine ganze Zahl, die den Bericht bezeichnet. Diese Spalte ist der Primärschlüssel für die Tabelle.|  
|**Berichtsname**|**nvarchar(4000)**|Der Berichtsname.|  
  
## <a name="modules"></a>Module  
Metadaten des Moduls ist exportiert der **SSMA_Access_InventoryModules** Tabelle. Diese Tabelle enthält die folgenden Spalten:  
  
|Spaltenname|Datentyp|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifiziert die Datenbank, die das Modul enthält.|  
|**ModuleId**|**int**|Inkrementelle eine ganze Zahl, die das Modul identifiziert. Diese Spalte ist der Primärschlüssel für die Tabelle.|  
|**ModuleName**|**nvarchar(4000)**|Der Name des Moduls.|  
  
## <a name="see-also"></a>Siehe auch  
[Exporting an Access Inventory (Exportieren eines Access-Inventars)](http://msdn.microsoft.com/en-us/7e1941fb-3d14-4265-aff6-c77a4026d0ed)  
  
