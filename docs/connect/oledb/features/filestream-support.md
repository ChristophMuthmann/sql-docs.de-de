---
title: FILESTREAM-Unterstützung | Microsoft Docs
description: FILESTREAM-Unterstützung in OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server [FILESTREAM support]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dc1a2d5e22e190eeed7bbdab27ee415f12552819
ms.sourcegitcommit: 8f1d1363e18e0c32ff250617ab6cb2da2147bf8e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/03/2018
---
# <a name="filestream-support"></a>FILESTREAM-Unterstützung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Die FILESTREAM-Funktion bietet eine Möglichkeit, große binäre Werte zu speichern und entweder über [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oder durch direkten Zugriff auf das Windows-Dateisystem darauf zuzugreifen. Ein großer Binärwert ist ein Wert, der größer als 2 Gigabyte (GB) ist. Weitere Informationen über die verbesserte FILESTREAM-Unterstützung finden Sie unter [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md).  
  
Wenn eine datenbankverbindung geöffnet wird, **@@TEXTSIZE**  wird auf-1 ("Unbegrenzt"), wird standardmäßig festgelegt werden.  
  
Es ist auch möglich, mit Windows-Dateisystem-APIs auf FILESTREAM-Spalten zuzugreifen und diese zu aktualisieren.  
  
Weitere Informationen finden Sie in folgenden Themen:  
  
-   [FILESTREAM-Unterstützung &#40;OLE DB&#41;](../../oledb/ole-db/filestream-support-ole-db.md)    
  
-   [ZUgreifen auf FILESTREAM-Daten mit OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>Abfragen von FILESTREAM-Spalten  
Schemarowsets in OLE DB geben nicht an, ob eine Spalte eine FILESTREAM-Spalte ist. ITableDefinition in OLE DB kann nicht zum Erstellen einer FILESTREAM-Spalte verwendet werden.    
  
Um FILESTREAM-Spalten zu erstellen oder zu erkennen, welche der vorhandenen Spalten FILESTREAM-Spalten sind, können Sie die **Is_filestream** Spalte die [sys.columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) -Katalogsicht angezeigt.  
  
Es folgt ein Beispiel:  
  
```sql  
-- Create a table with a FILESTREAM column.  
CREATE TABLE Bob_01 (GuidCol1 uniqueidentifier ROWGUIDCOL NOT NULL UNIQUE DEFAULT NEWID(), IntCol2 int, varbinaryCol3 varbinary(max) FILESTREAM);  
  
-- Find FILESTREAM columns.  
SELECT name FROM sys.columns WHERE is_filestream=1;  
  
-- Determine whether a column is a FILESTREAM column.  
SELECT is_filestream FROM sys.columns WHERE name = 'varbinaryCol3' AND object_id IN (SELECT object_id FROM sys.tables WHERE name='Bob_01');  
```  
  
## <a name="down-level-compatibility"></a>Kompabilität mit früheren Versionen  
Wenn Ihr Client kompiliert wurde, mithilfe von OLE DB-Treiber für SQL Server und die Anwendung eine Verbindung her, um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] über [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]), klicken Sie dann **varbinary(max)** Verhalten wird mit dem Verhalten kompatibel sein eingeführten [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Das heißt, die Maximalgröße der zurückgegebenen Daten ist auf 2 GB beschränkt. Für größere Ergebniswerte, 2 GB sind, werden abgeschnitten, und eine Warnung "Zeichenfolge rechts abgeschnitten" zurückgegeben. 
  
Wenn Datentypkompatibilität auf 80 festgelegt wird, ist das Clientverhalten mit dem Verhalten von Clients früherer Versionen konsistent.  
  
Für Clients, die SQLOLEDB oder andere Anbieter, die vor veröffentlicht wurden die [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], **varbinary(max)** zugeordnet, Image.  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Features](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
