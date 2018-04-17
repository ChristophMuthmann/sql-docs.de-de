---
title: FILESTREAM-Unterstützung | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: native-client|features
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], SQL Server Native Client
- SQL Server Native Client [FILESTREAM support]
ms.assetid: 1ad3400d-7fcd-40c9-87ae-f5afc61e0374
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf5a3a4c62b8ba11aecd5b62f38bec9913816402
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="filestream-support"></a>FILESTREAM-Unterstützung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Die FILESTREAM-Funktion bietet eine Möglichkeit, große binäre Werte zu speichern und entweder über [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oder durch direkten Zugriff auf das Windows-Dateisystem darauf zuzugreifen. Ein großer Binärwert ist ein Wert, der größer als 2 Gigabyte (GB) ist. Weitere Informationen über die verbesserte FILESTREAM-Unterstützung finden Sie unter [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md).  
  
 Wenn eine datenbankverbindung geöffnet wird, **@@TEXTSIZE**  wird auf-1 ("Unbegrenzt"), wird standardmäßig festgelegt werden.  
  
 Es ist auch möglich, mit Windows-Dateisystem-APIs auf FILESTREAM-Spalten zuzugreifen und diese zu aktualisieren.  
  
 Weitere Informationen finden Sie in folgenden Themen:  
  
-   [FILESTREAM-Unterstützung &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [FILESTREAM-Unterstützung &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [ZUgreifen auf FILESTREAM-Daten mit OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>Abfragen von FILESTREAM-Spalten  
 Schemarowsets in OLE DB geben nicht an, ob eine Spalte eine FILESTREAM-Spalte ist. ITableDefinition in OLE DB kann nicht zum Erstellen einer FILESTREAM-Spalte verwendet werden.  
  
 Katalogfunktionen z. B. SQLColumns in ODBC meldet, ob eine Spalte eine FILESTREAM-Spalte ist nicht auf.  
  
 Um FILESTREAM-Spalten zu erstellen oder zu erkennen, welche der vorhandenen Spalten FILESTREAM-Spalten sind, können Sie die **Is_filestream** Spalte die [sys.columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) -Katalogsicht angezeigt.  
  
 Es folgt ein Beispiel:  
  
```  
-- Create a table with a FILESTREAM column.  
CREATE TABLE Bob_01 (GuidCol1 uniqueidentifier ROWGUIDCOL NOT NULL UNIQUE DEFAULT NEWID(), IntCol2 int, varbinaryCol3 varbinary(max) FILESTREAM);  
  
-- Find FILESTREAM columns.  
SELECT name FROM sys.columns WHERE is_filestream=1;  
  
-- Determine whether a column is a FILESTREAM column.  
SELECT is_filestream FROM sys.columns WHERE name = 'varbinaryCol3' AND object_id IN (SELECT object_id FROM sys.tables WHERE name='Bob_01');  
```  
  
## <a name="down-level-compatibility"></a>Kompabilität mit früheren Versionen  
 Wenn Ihr Client kompiliert wurde, mit der Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, die enthalten war [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], und die Anwendung eine Verbindung mit [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], **varbinary(max)** Verhalten wird mit kompatibelsein[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Das heißt, die Maximalgröße der zurückgegebenen Daten ist auf 2 GB beschränkt. Für größere Ergebniswerte, 2 GB sind, werden abgeschnitten, und eine Warnung "Zeichenfolge rechts abgeschnitten" zurückgegeben.  
  
 Wenn Datentypkompatibilität auf 80 festgelegt wird, ist das Clientverhalten mit dem Verhalten von Clients früherer Versionen konsistent.  
  
 Für Clients, die SQLOLEDB oder andere Anbieter, die vor veröffentlicht wurden die [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Version des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client **varbinary(max)** zugeordnet, Image.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client-Features](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
