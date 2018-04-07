---
title: Unterstützung von Spalten mit geringer Dichte in OLE DB-Treiber für SQLServer | Microsoft Docs
description: Unterstützung von Spalten mit geringer Dichte in OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sparse columns, OLE DB Driver for SQL Server
- sparse columns, OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ffb8b7f18cf9c1653e5c77217f1d1dd339333fcf
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="sparse-columns-support-in-ole-db-driver-for-sql-server"></a>Unterstützung von Spalten mit geringer Dichte in OLE DB-Treiber für SQLServer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB-Treiber für SQL Server unterstützt Spalten mit geringer Dichte. Weitere Informationen zu Spalten mit geringer Dichte in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], finden Sie unter [Use Sparse Columns](../../../relational-databases/tables/use-sparse-columns.md) und [Verwenden von Spaltensätzen](../../../relational-databases/tables/use-column-sets.md).  
  
 Weitere Informationen zur Unterstützung der Spalte mit geringer Dichte in OLE DB-Treiber für SQL Server [zu Spalten mit geringer Dichte unterstützen &#40;OLE DB-&#41;](../../oledb/ole-db/sparse-columns-support-ole-db.md).  
  
 Informationen zu Beispielanwendungen, die diese Funktion veranschaulichen, finden Sie unter [Programmierbeispiele für SQL Server-Daten](http://msftdpprodsamples.codeplex.com/).  
  
## <a name="user-scenarios-for-sparse-columns-and-ole-db-driver-for-sql-server"></a>Benutzerszenarien für Spalten mit geringer Dichte und OLE DB-Treiber für SQLServer  
 In der folgenden Tabelle sind die gängigen Benutzerszenarien für OLE DB-Treiber für SQL Server-Benutzer mit Spalten mit geringer Dichte zusammengefasst:  
  
|Szenario|Verhalten|  
|--------------|--------------|  
|**Wählen Sie \* aus Tabelle** oder IOpenRowset:: OPENROWSET.|Gibt alle Spalten, die nicht Mitglied mit geringer Dichte sind **Column_set**, zuzüglich einer XML-Spalte, die die Werte aller nicht-Null-Spalten enthält, die Elemente mit geringer Dichte **Column_set**.|  
|Verweisen auf eine Spalte über den Namen|Die Spalte kann verwiesen werden, unabhängig von deren Status für die Spalte mit geringer Dichte oder **Column_set** Mitgliedschaft.|  
|Zugriff **Column_set** -Elementspalten über eine berechnete XML-Spalte.|Spalten, die Elemente mit geringer Dichte **Column_set** zugegriffen werden kann, durch Auswählen der **Column_set** anhand des Namens und können Werte eingefügt und aktualisiert durch Aktualisieren der XML-Code in der **Column_set** Spalte.<br /><br /> Der Wert muss dem Schema für **Column_set** Spalten.|  
|Abrufen von Metadaten für alle Spalten in einer Tabelle über das DBSCHEMA_COLUMNS-Schemarowset ohne spaltenbeschränkung (OLE DB).|Gibt eine Zeile für alle Spalten, die nicht Mitglied einer **Column_set**. Wenn die Tabelle mit geringer Dichte **Column_set**, wird eine Zeile dafür zurückgegeben werden.<br /><br /> Beachten Sie, dass dies keine Metadaten für Spalten zurückgibt, die Elemente einer **Column_set**.|  
|Abrufen von Metadaten für alle Spalten, unabhängig von geringer Dichte oder Zugehörigkeit in einem **Column_set**. Hier könnte eine sehr große Anzahl an Zeilen zurückgegeben werden.|Rufen Sie IDBSchemaRowset:: GetRowset für das DBSCHEMA_COLUMNS_EXTENDED-Schemarowset ein.|  
|Abrufen von Metadaten nur für Spalten, die Elemente einer **Column_set**. Hier könnte eine sehr große Anzahl an Zeilen zurückgegeben werden.|Rufen Sie IDBSchemaRowset:: GetRowset für das DBSCHEMA_SPARSE_COLUMN_SET-Schemarowset ein.|  
|Bestimmen, ob eine Spalte eine geringe Dichte aufweist|Betrachten Sie die SS_IS_SPARSE-Spalte des DBSCHEMA_COLUMNS-Schemarowsets (OLE DB).|  
|Bestimmen Sie, ob eine Spalte ist eine **Column_set**.|Betrachten Sie die SS_IS_COLUMN_SET-Spalte des DBSCHEMA_COLUMNS-Schemarowsets. Oder Lesen Sie *DwFlags* zurückgegebenes IColumnsInfo:: GetColumnInfo oder DBCOLUMNFLAGS im von IColumnsRowset:: GetColumnsRowset zurückgegebenen Rowset. Für **Column_set** Spalten DBCOLUMNFLAGS_SS_ISCOLUMNSET festgelegt.|  
|Importieren und Exportieren von Spalten mit geringer Dichte über BCP für eine Tabelle ohne **Column_set**.|Keine Änderung im Verhalten unterscheidet sich von früheren Versionen des OLE DB-Treiber für SQL Server.|  
|Importieren und Exportieren von Spalten mit geringer Dichte über BCP für eine Tabelle mit einer **Column_set**.|Die **Column_set** importiert und exportiert, auf die gleiche Weise wie XML; d. h. als **varbinary(max)** Wenn gebunden als Binär oder als **nvarchar(max)** Wenn als eine gebunden**Char** oder **Wchar** Typ.<br /><br /> Spalten, die Elemente mit geringer Dichte **Column_set** werden nicht exportiert werden, als unterschiedliche Spalten; sie sind nur im Wert des exportiert die **Column_set**.|  
|**Queryout** -Verhalten für BCP.|Keine Änderung bei der Behandlung explizit benannter Spalten aus früheren Versionen von OLE DB-Treiber für SQL Server.<br /><br /> In Szenarien, die das Importieren und Exportieren zwischen Tabellen mit unterschiedlichen Schemas umfassen, ist möglicherweise eine besondere Behandlung erforderlich.<br /><br /> Weitere Informationen über BCP finden Sie unter „Massenkopierunterstützung (BCP) für Spalten mit geringer Dichte” weiter unten in diesem Thema.|  
  
## <a name="down-level-client-behavior"></a>Downlevelclient-Verhalten  
 Downlevelclients geben Metadaten nur für Spalten, die nicht Mitglied mit geringer Dichte sind zurück **Column_set** für SQLColumns und DBSCHMA_COLUMNS.
  
 Downlevelclients können auf Spalten, die Elemente mit geringer Dichte zugreifen **Column_set** anhand des Namens, und die **Column_set** Spalte als XML-Spalte für zugegriffen werden [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Clients.  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>Massenkopierunterstützung (BCP) für Spalten mit geringer Dichte  
 Es gibt keine Änderungen an der BCP-API in der OLE DB für die Spalten mit geringer Dichte oder **Column_set** Funktionen.  
  
 Wenn eine Tabelle hat eine **Column_set**, Spalten mit geringer Dichte nicht als unterschiedliche Spalten behandelt. Die Werte aller Spalten mit geringer Dichte sind im Wert des enthalten die **Column_set**, dem auf die gleiche Weise wie eine XML-Spalte exportiert wird, also als **varbinary(max)** Wenn gebunden als Binär oder als  **nvarchar(max)** wenn er als ein **Char** oder **Wchar** Typ). Beim Import der **Column_set** Wert muss das Schema der entsprechen den **Column_set**.  
  
 Für **Queryout** Vorgänge, erfolgt keine Änderung der Art und Weise, die explizit verwiesen wird Spalten behandelt werden. **COLUMN_SET** Spalten weisen das gleiche Verhalten wie XML-Spalten und geringe Dichte hat keine Auswirkung auf die Handhabung von Namen von Spalten mit geringer Dichte.  
  
 Jedoch wenn **Queryout** wird verwendet, für das Exportieren und Sie Spalten mit geringer Dichte, die Elemente der Spaltensatz mit geringer Dichte nach Name verweisen, Sie können keine keinen direkten Import in eine Tabelle mit gleicher Struktur ausführen. Dies ist, da BCP Metadaten konsistent mit verwendet werden, eine **wählen \***  Vorgang für den Import und nicht zuordnen kann **Column_set** -Elementspalten diesen Metadaten. So importieren Sie **Column_set** -Elementspalten einzeln zu definieren, eine Ansicht für die Tabelle, die auf den gewünschten verweist **Column_set** Spalten, und Sie müssen den Importvorgang mithilfe der Sicht ausführen.  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Programmierung](../../oledb/oledb-driver-for-sql-server-programming.md)  
  
  
