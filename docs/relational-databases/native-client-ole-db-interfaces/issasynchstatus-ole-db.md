---
title: ISSAsynchStatus (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSAsynchStatus interface
ms.assetid: c643f09f-9ccc-4d8b-9243-3cde86c2bd46
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8e5a756b55d3a426e18f8b224659d42669ab89ac
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **ISSAsynchStatus** unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asynchrone Vorgänge. Hierbei handelt es sich um eine optionale Schnittstelle, die von der OLE DB-Kernschnittstelle **IDBAsynchStatus**erbt. Neben den von **IDBAsynchStatus** geerbten Methoden **Abort** und **GetStatus**stellt **ISSAsynchStatus** eine neue Methode bereit, die verwendet wird, um zu warten, bis ein asynchroner Vorgang abgeschlossen ist oder ein Timeout auftritt.  
  
|Methode|Description|  
|------------|-----------------|  
|[ISSAsynchStatus::Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md)|Bricht einen asynchron ausgeführten Vorgang ab.|  
|[Issasynchstatus:: GetStatus &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|Gibt den Status eines asynchron ausgeführten Vorgangs zurück.|  
|[Issasynchstatus:: Waitforasynchcompletion &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|Wartet, bis der asynchron ausgeführte Vorgang abgeschlossen ist oder ein Timeout auftritt.|  
  
## <a name="remarks"></a>Hinweise  
 Die **ISSAsynchStatus** -Implementierung der **ISSAsynchStatus::GetStatus** -Methode ist mit der **IDBAsynchStatus::GetStatus** -Methode identisch, gibt jedoch anstelle von DB_E_CANCELED E_UNEXPECTED zurück, wenn die Initialisierung eines Datenquellenobjekts abgebrochen wird (wenngleich **ISSAsynchStatus::WaitForAsynchCompletion** DB_E_CANCELED zurückgibt). Dies ist darauf zurückzuführen, dass das Datenquellenobjekt nach einem Abbruchvorgang nicht mehr den gewöhnlichen Status aufweist, sodass weitere Initialisierungsvorgänge durchgeführt werden können.  
  
 Die folgenden Methoden unterstützen die Verwendung der asynchronen Ausführung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   **ICommand:: Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>Siehe auch  
 [Schnittstellen & #40; OLE DB & #41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [Ausführen asynchroner Vorgänge](../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
  
  
