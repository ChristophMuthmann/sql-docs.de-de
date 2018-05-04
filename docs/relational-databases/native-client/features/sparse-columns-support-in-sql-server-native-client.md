---
title: Spalten mit geringer Dichte-Unterstützung in SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|features
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sparse columns, ODBC
- sparse columns, SQL Server Native Client
- sparse columns, OLE DB
ms.assetid: aee5ed81-7e23-42e4-92d3-2da7844d9bc3
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5f9cf56b4ee1a7e3108607912ecba9a05d0815e4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sparse-columns-support-in-sql-server-native-client"></a>Unterstützung für Spalten mit geringer Dichte in SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client unterstützt Sparsespalten. Weitere Informationen zu Spalten mit geringer Dichte in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], finden Sie unter [Use Sparse Columns](../../../relational-databases/tables/use-sparse-columns.md) und [Verwenden von Spaltensätzen](../../../relational-databases/tables/use-column-sets.md).  
  
 Weitere Informationen zu Spalten mit geringer Dichte zu unterstützen, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client finden Sie unter [zu Spalten mit geringer Dichte unterstützen &#40;ODBC&#41; ](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md) und [zu Spalten mit geringer Dichte unterstützen &#40;OLE DB-&#41; ](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md) .  
  
 Informationen zu Beispielanwendungen, die diese Funktion veranschaulichen, finden Sie unter [Programmierbeispiele für SQL Server-Daten](http://msftdpprodsamples.codeplex.com/).  
  
## <a name="user-scenarios-for-sparse-columns-and-sql-server-native-client"></a>Benutzerszenarien für Spalten mit geringer Dichte und SQL Server Native Client  
 In der folgenden Tabelle sind die gängigen Benutzerszenarien für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Benutzer mit Sparsespalten zusammengefasst:  
  
|Szenario|Verhalten|  
|--------------|--------------|  
|**Wählen Sie \* aus Tabelle** oder IOpenRowset:: OPENROWSET.|Gibt alle Spalten, die nicht Mitglied mit geringer Dichte sind **Column_set**, zuzüglich einer XML-Spalte, die die Werte aller nicht-Null-Spalten enthält, die Elemente mit geringer Dichte **Column_set**.|  
|Verweisen auf eine Spalte über den Namen|Die Spalte kann verwiesen werden, unabhängig von deren Status für die Spalte mit geringer Dichte oder **Column_set** Mitgliedschaft.|  
|Zugriff **Column_set** -Elementspalten über eine berechnete XML-Spalte.|Spalten, die Elemente mit geringer Dichte **Column_set** zugegriffen werden kann, durch Auswählen der **Column_set** anhand des Namens und können Werte eingefügt und aktualisiert durch Aktualisieren der XML-Code in der **Column_set** Spalte.<br /><br /> Der Wert muss dem Schema für **Column_set** Spalten.|  
|Abrufen von Metadaten für alle Spalten in einer Tabelle über SQLColumns mit einem spaltensuchmuster NULL oder "%" (ODBC) oder über das DBSCHEMA_COLUMNS-Schemarowset ohne spaltenbeschränkung (OLE DB).|Gibt eine Zeile für alle Spalten, die nicht Mitglied einer **Column_set**. Wenn die Tabelle mit geringer Dichte **Column_set**, wird eine Zeile dafür zurückgegeben werden.<br /><br /> Beachten Sie, dass dies keine Metadaten für Spalten zurückgibt, die Elemente einer **Column_set**.|  
|Abrufen von Metadaten für alle Spalten, unabhängig von geringer Dichte oder Zugehörigkeit in einem **Column_set**. Hier könnte eine sehr große Anzahl an Zeilen zurückgegeben werden.|Legen Sie das Deskriptorfeld SQL_SOPT_SS_NAME_SCOPE auf SQL_SS_NAME_SCOPE_EXTENDED und rufen [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) (ODBC).<br /><br /> Rufen Sie IDBSchemaRowset:: GetRowset für das DBSCHEMA_COLUMNS_EXTENDED-Schemarowset (OLE DB).<br /><br /> Dieses Szenario ist in einer Anwendung, die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client einer früheren Version als [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] verwendet, nicht möglich. Eine solche Anwendung könnte jedoch Systemsichten direkt Abfragen.|  
|Abrufen von Metadaten nur für Spalten, die Elemente einer **Column_set**. Hier könnte eine sehr große Anzahl an Zeilen zurückgegeben werden.|Legen Sie das Deskriptorfeld SQL_SOPT_SS_NAME_SCOPE auf SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET und Aufrufen von SQLColumns (ODBC).<br /><br /> Rufen Sie IDBSchemaRowset:: GetRowset für das DBSCHEMA_SPARSE_COLUMN_SET-Schemarowset (OLE DB).<br /><br /> Dieses Szenario ist in einer Anwendung, die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client einer früheren Version als [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] verwendet, nicht möglich. Eine solche Anwendung könnte jedoch Systemsichten abfragen.|  
|Bestimmen, ob eine Spalte eine geringe Dichte aufweist|Wenden Sie sich an die SS_IS_SPARSE-Spalte des Resultsets SQLColumns (ODBC).<br /><br /> Betrachten Sie die SS_IS_SPARSE-Spalte des DBSCHEMA_COLUMNS-Schemarowsets (OLE DB).<br /><br /> Dieses Szenario ist in einer Anwendung, die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client einer früheren Version als [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] verwendet, nicht möglich. Eine solche Anwendung könnte jedoch Systemsichten abfragen.|  
|Bestimmen Sie, ob eine Spalte ist eine **Column_set**.|Wenden Sie sich an die SS_IS_COLUMN_SET-Spalte des Resultsets SQLColumns. Oder sehen Sie sich das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-spezifische SQL_CA_SS_IS_COLUMN_SET-Spaltenattribut (ODBC) an.<br /><br /> Betrachten Sie die SS_IS_COLUMN_SET-Spalte des DBSCHEMA_COLUMNS-Schemarowsets. Oder Lesen Sie *DwFlags* zurückgegebenes IColumnsInfo:: GetColumnInfo oder DBCOLUMNFLAGS im von IColumnsRowset:: GetColumnsRowset zurückgegebenen Rowset. Für **Column_set** Spalten DBCOLUMNFLAGS_SS_ISCOLUMNSET festgelegt (OLE DB).<br /><br /> Dieses Szenario ist in einer Anwendung, die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client einer früheren Version als [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] verwendet, nicht möglich. Eine solche Anwendung könnte jedoch Systemsichten abfragen.|  
|Importieren und Exportieren von Spalten mit geringer Dichte über BCP für eine Tabelle ohne **Column_set**.|Keine Änderung im Verhalten im Vergleich zu vorherigen Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|Importieren und Exportieren von Spalten mit geringer Dichte über BCP für eine Tabelle mit einer **Column_set**.|Die **Column_set** importiert und exportiert, auf die gleiche Weise wie XML; d. h. als **varbinary(max)** Wenn gebunden als Binär oder als **nvarchar(max)** Wenn als eine gebunden**Char** oder **Wchar** Typ.<br /><br /> Spalten, die Elemente mit geringer Dichte **Column_set** werden nicht exportiert werden, als unterschiedliche Spalten; sie sind nur im Wert des exportiert die **Column_set**.|  
|**Queryout** -Verhalten für BCP.|Keine Änderung in der Behandlung explizit benannter Spalten im Vergleich zu vorherigen Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.<br /><br /> In Szenarien, die das Importieren und Exportieren zwischen Tabellen mit unterschiedlichen Schemas umfassen, ist möglicherweise eine besondere Behandlung erforderlich.<br /><br /> Weitere Informationen über BCP finden Sie unter „Massenkopierunterstützung (BCP) für Spalten mit geringer Dichte” weiter unten in diesem Thema.|  
  
## <a name="down-level-client-behavior"></a>Downlevelclient-Verhalten  
 Downlevelclients geben Metadaten nur für Spalten, die nicht Mitglied mit geringer Dichte sind zurück **Column_set** für SQLColumns und DBSCHMA_COLUMNS. Die zusätzlichen OLE DB-Schemarowsets in eingeführte [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client ist nicht verfügbar, auch die Änderungen SQLColumns in ODBC über SQL_SOPT_SS_NAME_SCOPE.  
  
 Downlevelclients können auf Spalten, die Elemente mit geringer Dichte zugreifen **Column_set** anhand des Namens, und die **Column_set** Spalte als XML-Spalte für zugegriffen werden [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Clients.  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>Massenkopierunterstützung (BCP) für Spalten mit geringer Dichte  
 Es gibt keine Änderungen an der BCP-API in ODBC- oder OLE DB für die Spalten mit geringer Dichte oder **Column_set** Funktionen.  
  
 Wenn eine Tabelle hat eine **Column_set**, Spalten mit geringer Dichte nicht als unterschiedliche Spalten behandelt. Die Werte aller Spalten mit geringer Dichte sind im Wert des enthalten die **Column_set**, dem auf die gleiche Weise wie eine XML-Spalte exportiert wird, also als **varbinary(max)** Wenn gebunden als Binär oder als  **nvarchar(max)** wenn er als ein **Char** oder **Wchar** Typ). Beim Import der **Column_set** Wert muss das Schema der entsprechen den **Column_set**.  
  
 Für **Queryout** Vorgänge, erfolgt keine Änderung der Art und Weise, die explizit verwiesen wird Spalten behandelt werden. **COLUMN_SET** Spalten weisen das gleiche Verhalten wie XML-Spalten und geringe Dichte hat keine Auswirkung auf die Handhabung von Namen von Spalten mit geringer Dichte.  
  
 Jedoch wenn **Queryout** wird verwendet, für das Exportieren und Sie Spalten mit geringer Dichte, die Elemente der Spaltensatz mit geringer Dichte nach Name verweisen, Sie können keine keinen direkten Import in eine Tabelle mit gleicher Struktur ausführen. Dies ist, da BCP Metadaten konsistent mit verwendet werden, eine **wählen \***  Vorgang für den Import und nicht zuordnen kann **Column_set** -Elementspalten diesen Metadaten. So importieren Sie **Column_set** -Elementspalten einzeln zu definieren, eine Ansicht für die Tabelle, die auf den gewünschten verweist **Column_set** Spalten, und Sie müssen den Importvorgang mithilfe der Sicht ausführen.  
  
## <a name="see-also"></a>Siehe auch  
 [Programmierung für SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
