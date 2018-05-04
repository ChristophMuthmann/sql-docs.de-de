---
title: ISSAsynchStatus (OLE DB) | Microsoft Docs
description: ISSAsynchStatus (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
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
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 6c6ce6c399798206fc9f66af68bd1cf2ffea718a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **ISSAsynchStatus** Schnittstelle verfügbar macht, Unterstützung für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] asynchrone Vorgänge. Es ist eine optionale Schnittstelle, die von der OLE DB-Kernschnittstelle erbt **IDBAsynchStatus**. Neben den von **IDBAsynchStatus** geerbten Methoden **Abort** und **GetStatus**stellt **ISSAsynchStatus** eine neue Methode bereit, die verwendet wird, um zu warten, bis ein asynchroner Vorgang abgeschlossen ist oder ein Timeout auftritt.  
  
|Methode|Description|  
|------------|-----------------|  
|[ISSAsynchStatus::Abort &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-abort-ole-db.md)|Bricht einen asynchron ausgeführten Vorgang ab.|  
|[Issasynchstatus:: GetStatus &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|Gibt den Status eines asynchron ausgeführten Vorgangs zurück.|  
|[Issasynchstatus:: Waitforasynchcompletion &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|Wartet, bis der asynchron ausgeführte Vorgang abgeschlossen ist oder ein Timeout auftritt.|  
  
## <a name="remarks"></a>Hinweise  
 Die **ISSAsynchStatus** -Implementierung der **ISSAsynchStatus::GetStatus** -Methode ist mit der **IDBAsynchStatus::GetStatus** -Methode identisch, gibt jedoch anstelle von DB_E_CANCELED E_UNEXPECTED zurück, wenn die Initialisierung eines Datenquellenobjekts abgebrochen wird (wenngleich **ISSAsynchStatus::WaitForAsynchCompletion** DB_E_CANCELED zurückgibt). Es ist zurückzuführen, dass das Datenquellenobjekt den gewöhnlichen Status aufweist, die nach einem Abbruchvorgang nicht ist, sodass weitere Initialisierungsvorgänge durchgeführt werden können.  
  
 Die folgenden Methoden unterstützen die Verwendung der asynchronen Ausführung in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   **ICommand:: Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>Siehe auch  
 [Schnittstellen & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [Ausführen asynchroner Vorgänge](../../oledb/features/performing-asynchronous-operations.md)  
  
  
