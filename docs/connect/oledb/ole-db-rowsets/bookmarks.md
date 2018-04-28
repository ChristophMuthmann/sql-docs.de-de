---
title: Lesezeichen | Microsoft Docs
description: Lesezeichen im OLE DB-Treiber für SQLServer
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bookmarks [OLE DB]
- OLE DB Driver for SQL Server, bookmarks
- rowsets [OLE DB], bookmarks
- OLE DB rowsets, bookmarks
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c0ac349e10f056bd97968579988a7b9f202b16a0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="bookmarks"></a>Lesezeichen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Lesezeichen ermöglichen es Consumern, schnell zu einer Zeile zurück. Mit Lesezeichen können Consumer auf der Grundlage des Lesezeichenwerts beliebig auf Zeilen zugreifen. Die Lesezeichenspalte ist die Spalte 0 (null) im Rowset. Der Consumer legt den Wert des Felds dwFlag der Bindungsstruktur auf DBCOLUMNSINFO_ISBOOKMARK fest, um anzugeben, dass die Spalte als Lesezeichen verwendet wird. Der Consumer legt zudem die Rowseteigenschaft DBPROP_BOOKMARKS auf VARIANT_TRUE fest. Mit dieser Spalte 0 werden können, die im Rowset vorhanden sind. Die **IRowsetLocate:: GetRowsAt** Methode wird dann zum Abrufen von Zeilen, beginnend mit der Zeile, die als in einem Lesezeichen als Offset angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Rowsets](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
