---
title: 'Mithilfe von IRow:: GetColumns | Microsoft Docs'
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7f4f66d36796de8c4dbb0c39b169314be9bdc473
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="using-irowgetcolumns"></a>Verwenden von IRow::GetColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die **IRow** Implementierung ermöglicht Vorwärtscursor sequenziellen Zugriff auf die Spalten. Sie können entweder alle Spalten in der Zeile mit einem einzigen Aufruf zugreifen **von IRow:: GetColumns** , oder rufen Sie **von IRow:: GetColumns** mehrere Male auf, jedes Mal, wenn Sie mehrere Spalten in der Zeile zugreifen.  
  
 Die verschiedenen Aufrufe von **von IRow:: GetColumns** sollten sich nicht überschneiden. Angenommen, wenn der erste Aufruf **von IRow:: GetColumns** Spalten 1, 2 und 3, der zweite Aufruf ruft **von IRow:: GetColumns** sollten für die Spalten 4, 5 und 6 aufrufen. Wenn spätere Aufrufe von **von IRow:: GetColumns** überlappen, ist das Statusflag (Dwstatus-Feld in der DBCOLUMNACCESS) auf DBSTATUS_E_UNAVAILABLE festgelegt.  
  
## <a name="see-also"></a>Siehe auch  
 [Abrufen einer einzelnen Zeile mit IRow](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
