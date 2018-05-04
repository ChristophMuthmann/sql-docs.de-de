---
title: BLOBs und OLE-Objekte | Microsoft Docs
description: BLOBs und OLE-Objekte
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-blobs
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- OLE DB Driver for SQL Server, BLOBs
- large data, OLE objects
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 81cbe599c0845d839975fc51c32d4b14b69ea321
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="blobs-and-ole-objects"></a>BLOBs und OLE-Objekte
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Der OLE DB-Treiber für SQL Server macht die **ISequentialStream** -Schnittstelle zur Unterstützung der Consumerzugriff auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **Ntext**, **Text**, **Bild** , **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, und Xml-Datentypen als binary large Objects (BLOBs). Die **lesen** Methode **ISequentialStream** ermöglicht dem Consumer, die viel Datenmengen in überschaubaren Abschnitten abzurufen.  
  
 Ein Beispiel für diese Funktion ist, finden Sie unter [Festlegen von großen Daten & #40; OLE DB & #41;](../../oledb/ole-db-how-to/set-large-data-ole-db.md).  
  
 Der OLE DB-Treiber für SQL Server können Sie eine vom Consumer implementierte **IStorage** Schnittstelle, wenn der Consumer den Schnittstellenzeiger in einem Accessor sorgt für datenänderungen gebundenen.  
  
 Für große Datenwerttypen, überprüft der OLE DB-Treiber für SQL Server für Annahmen über die typgroße in **IRowset** und DDL-Schnittstellen. Spalten mit **Varchar**, **Nvarchar**, und **Varbinary** Datentypen und die maximale Größe auf unlimited festgelegt dargestellt werden, als ISLONG über die Schemarowsets und mittels Schnittstellen, die Spaltendatentypen zurückgegeben.  
  
 Der OLE DB-Treiber für SQL Server macht die **varchar(max)**, **varbinary(max)** und **nvarchar(max)** bzw. als DBTYPE_STR, DBTYPE_BYTES bzw. DBTYPE_WSTR Typen.  
  
 Um mit diesen Typen zu arbeiten, stehen der Anwendung die folgenden Optionen zur Verfügung:  
  
-   Als den betreffenden Typ binden (DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR). Wenn der Puffer nicht groß ist erfolgt genügend abschneiden, wie dies in früheren Versionen (obwohl jetzt umfangreichere Werte verfügbar sind).  
  
-   Als den betreffenden Typ binden und zudem DBTYPE_BYREF angeben  
  
-   Als DBTYPE_IUNKNOWN binden und Streaming verwenden  
  
 Wenn die Bindung an DBTYPE_IUNKNOWN erfolgt, wird die Streamingfunktion ISequentialStream verwendet. Der OLE DB-Treiber für SQL Server unterstützt Binden von Ausgabeparametern als DBTYPE_IUNKNOWN für Datentypen an. Dies ist zur Unterstützung von Szenarien, in denen eine gespeicherte Prozedur diese Datentypen als Rückgabewerte zurückgibt, das als DBTYPE_IUNKNOWN an dem Client zurückgegeben wird.  
  
## <a name="storage-object-limitations"></a>Speicherobjekteinschränkungen  
  
-   Der OLE DB-Treiber für SQL Server kann nur ein einzelnes geöffnetes Speicherobjekt unterstützen. Versucht, mehr als ein Speicherobjekt zu öffnen (Abrufen eines Verweises auf mehr als einem **ISequentialStream** Schnittstellenzeiger) DBSTATUS_E_CANTCREATE zurückgegeben.  
  
-   In der OLE DB-Treiber für SQL Server ist der Standardwert der schreibgeschützten DBPROP_BLOCKINGSTORAGEOBJECTS nur-Lese Eigenschaft auf VARIANT_TRUE festgelegt. Wenn ein Speicherobjekt aktiv ist, werden daher einige Methoden (mit Ausnahme der Methoden in den Speicherobjekten) mit E_UNEXPECTED fehlschlagen.  
  
-   Die Länge der Daten eines von einem Consumer implementierten Speicherobjekts muss erfolgen bekannte an den OLE DB-Treiber für SQL Server aus der Erstellung der zeilenaccessor, der auf das Speicherobjekt verweist. Der Consumer muss einen Längenindikator in der zur Accessorerstellung verwendeten DBBINDING-Struktur binden.  
  
-   Wenn eine Zeile enthält mehr als einen großen Datenwert und DBPROP_ACCESSORDER nicht DBPROPVAL_AO_RANDOM, der Consumer muss entweder ein OLE DB-Treiber für SQL Server durch Cursor unterstütztes Rowset verwenden, um Zeilendaten abzurufen oder alle großen Datenwerte vor dem Abrufen von anderen verarbeiten Zeilenwerte. Wenn DBPROP_ACCESSORDER auf DBPROPVAL_AO_RANDOM lautet, speichert der OLE DB-Treiber für SQL Server alle Xml-Datentypen als binary large Objects (BLOBs), damit sie in beliebiger Reihenfolge zugegriffen werden kann.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Abrufen großer Datenmengen](../../oledb/ole-db-blobs/getting-large-data.md)  
  
-   [Festlegen großer Datenmengen](../../oledb/ole-db-blobs/setting-large-data.md)  
  
-   [Streamingunterstützung für BLOB-Ausgabeparameter](../../oledb/ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Programmierung](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)        
 [Verwenden von Datentypen mit umfangreichen Werten](../../oledb/features/using-large-value-types.md)  
  
  
