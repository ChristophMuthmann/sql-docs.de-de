---
title: BLOBs und OLE-Objekte | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-blobs
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: 767fa2f6-9cd2-436f-add5-e760bed29a58
caps.latest.revision: "43"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 03eb28507a7fa0fdc2bf8df55dbb39356f24109c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="blobs-and-ole-objects"></a>BLOBs und OLE-Objekte
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter macht die **ISequentialStream** -Schnittstelle zur Unterstützung der Consumerzugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Ntext**, **Text**, **Image**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, und Xml-Datentypen als binary large Objects (BLOBs). Die **lesen** Methode **ISequentialStream** ermöglicht dem Consumer, die viel Datenmengen in überschaubaren Abschnitten abzurufen.  
  
 Ein Beispiel für diese Funktion ist, finden Sie unter [Festlegen von großen Daten &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md).  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter können Sie eine vom Consumer implementierte **IStorage** Schnittstelle, wenn der Consumer den Schnittstellenzeiger in einem Accessor sorgt für datenänderungen gebundenen.  
  
 Bei Datentypen mit umfangreichen Werten die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter überprüft Annahmen über die typgroße in **IRowset** und DDL-Schnittstellen. Spalten mit **Varchar**, **Nvarchar**, und **Varbinary** Datentypen mit max. Größe auf unlimited festgelegt werden, als ISLONG dargestellt werden, über die Schemarowsets und Schnittstellen, die Spaltendatentypen.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter macht die **varchar(max)**, **varbinary(max)** und **nvarchar(max)** bzw. als DBTYPE_STR, DBTYPE_BYTES bzw. DBTYPE_WSTR Typen.  
  
 Um mit diesen Typen zu arbeiten, hat eine Anwendung die folgenden Optionen:  
  
-   Als den betreffenden Typ binden (DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR). Wenn der Puffer nicht groß genug ist, werden Daten abgeschnitten, wie dies auch in früheren Versionen der Fall war (obwohl jetzt umfangreichere Werte verfügbar sind).  
  
-   Als den betreffenden Typ binden und zudem DBTYPE_BYREF angeben  
  
-   Als DBTYPE_IUNKNOWN binden und Streaming verwenden  
  
 Wenn die Bindung an DBTYPE_IUNKNOWN erfolgt, wird die Streamingfunktion ISequentialStream verwendet. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützt Binden von Ausgabeparametern als DBTYPE_IUNKNOWN für Datentypen in Szenarien nützlich, eine gespeicherte Prozedur, in denen diese Daten zurückgibt, Typen als Rückgabewerte der verfügbar gemacht werden als DBTYPE_IUNKNOWN an den Client.  
  
## <a name="storage-object-limitations"></a>Speicherobjekteinschränkungen  
  
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter kann nur ein einzelnes geöffnetes Speicherobjekt unterstützen. Versucht, mehr als ein Speicherobjekt zu öffnen (Abrufen eines Verweises auf mehr als einem **ISequentialStream** Schnittstellenzeiger) DBSTATUS_E_CANTCREATE zurückgegeben.  
  
-   In der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter, der Standardwert der schreibgeschützten DBPROP_BLOCKINGSTORAGEOBJECTS-Eigenschaft schreibgeschützt ist, den Wert VARIANT_TRUE auf. Das zeigt an, dass einige Methoden (solche, die sich nicht in den Speicherobjekten befinden) mit E_UNEXPECTED fehlschlagen, wenn ein Speicherobjekt aktiv ist.  
  
-   Die Länge der Daten eines von einem Consumer implementierten Speicherobjekts muss bekannt gemacht werden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter aus der Erstellung der zeilenaccessor, der auf das Speicherobjekt verweist. Der Consumer muss einen Längenindikator in der zur Accessorerstellung verwendeten DBBINDING-Struktur binden.  
  
-   Wenn eine Zeile mehr als einen großen Datenwert enthält und DBPROP_ACCESSORDER nicht DBPROPVAL_AO_RANDOM, muss der Consumer entweder ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter durch Cursor unterstütztes Rowset um Zeilendaten abzurufen oder alle großen Datenwerte vor dem Abrufen weiterer Zeilenwerte verarbeiten. Wenn DBPROP_ACCESSORDER auf DBPROPVAL_AO_RANDOM, lautet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter alle Xml-Datentypen als binary large Objects (BLOBs) zwischenspeichert, sodass in beliebiger Reihenfolge zugegriffen werden kann.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Abrufen großer Datenmengen](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [Festlegen großer Datenmengen](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [Streamingunterstützung für BLOB-Ausgabeparameter](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client &#40; OLE DB &#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [Verwenden von Datentypen mit umfangreichen Werten](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
