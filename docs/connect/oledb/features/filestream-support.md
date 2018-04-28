---
title: FILESTREAM-Unterstützung | Microsoft Docs
description: FILESTREAM-Unterstützung in OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
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
- FILESTREAM [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server [FILESTREAM support]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e08cf05033ff7815784aef4d08fb65f8e61d299
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="filestream-support"></a>FILESTREAM-Unterstützung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Beginnend mit [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], OLE DB-Treiber für SQL Server unterstützt die verbesserte FILESTREAM-Funktion. Beispiele finden Sie in [Filestream und OLE DB-](../../oledb/ole-db-how-to/filestream/filestream-and-ole-db.md).  

Die FILESTREAM-Funktion bietet eine Möglichkeit, große binäre Werte zu speichern und entweder über [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oder durch direkten Zugriff auf das Windows-Dateisystem darauf zuzugreifen. Ein großer Binärwert ist ein Wert, der größer als 2 Gigabyte (GB) ist. Weitere Informationen über die verbesserte FILESTREAM-Unterstützung finden Sie unter [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md).  
  
Wenn eine datenbankverbindung geöffnet wird, **@@TEXTSIZE**  wird auf-1 ("Unbegrenzt"), wird standardmäßig festgelegt werden.  
  
Es ist auch möglich, mit Windows-Dateisystem-APIs auf FILESTREAM-Spalten zuzugreifen und diese zu aktualisieren.  
  
Weitere Informationen finden Sie unter [zugreifen auf FILESTREAM-Daten mit OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
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
  
## <a name="comments"></a>Kommentare
- Zum Senden und Empfangen von **varbinary(max)** Werte, die größer als 2 GB sind, eine Anwendung verwendet **DBTYPE_IUNKNOWN** in Parameter- und ergebnisbindungen. Für Parameter muss der Anbieter aufrufen IUnknown:: QueryInterface für ISequentialStream und Ergebnisse, die einer ISequentialStream-Schnittstelle zurückgibt.  

-  Für OLE DB wird die Option ISequentialStream Werte zur Überprüfung gelockert werden. Beim *wType* ist **DBTYPE_IUNKNOWN** in der **DBBINDING** Struktur längenüberprüfung kann entweder durch das weglassen deaktiviert **DBPART_LENGTH** von *DwPart* oder durch Festlegen der Länge der Daten (Offset *ObLength* im Datenpuffer) auf ~ 0. In diesem Fall überprüft der Provider die Länge des Werts nicht und fordert alle Daten an (oder gibt sie zurück), die über den Datenstrom zur Verfügung stehen. Diese Änderung wird auf alle LOB-Typen (Large Object) und auf XML angewendet, allerdings nur, wenn eine Verbindung zu [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]-Servern (oder höher) besteht. Auf diese Weise erhalten Entwickler eine höhere Flexibilität, während sie die Konsistenz und Abwärtskompatibilität für vorhandene Anwendungen und Downlevelserver beibehalten.  Diese Änderung wirkt sich auf alle Schnittstellen, die Daten, die hauptsächlich IRowset:: GetData ICommand:: Execute und IRowsetFastLoad:: InsertRow übertragen.
 

## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Features](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
