---
title: IDBProperties (OLE DB) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-interfaces
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0d49300aef1bc7fcc84937059f5644ad6369c22e
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2018
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Dank der OLE DB-Standardspezifikation können Anbieter VT_EMPTY für **DBPROPINFO::vValues**angeben. Allerdings [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB immer VT_EMPTY zurückgegeben, wenn Sie aufrufen **GetPropertyInfo** mit **DBPROPSET_ROWSETALL** Rowseteigenschaften abgerufen werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Schnittstellen &#40; OLE DB &#41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
