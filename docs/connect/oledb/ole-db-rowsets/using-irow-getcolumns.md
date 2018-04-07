---
title: 'Mithilfe von IRow:: GetColumns | Microsoft Docs'
description: 'Zugriff auf alle Spalten in einer Zeile mithilfe von IRow:: GetColumns'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
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
- fetching rows
- IRow interface
- single row fetching [OLE DB Driver for SQL Server]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b18b256d859c85b846d81ae239003fec2aafc010
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="using-irowgetcolumns"></a>Verwenden von IRow::GetColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Die **IRow** Implementierung ermöglicht Vorwärtscursor sequenziellen Zugriff auf die Spalten. Sie können entweder alle Spalten in der Zeile mit einem einzigen Aufruf zugreifen **von IRow:: GetColumns** , oder rufen Sie **von IRow:: GetColumns** mehrere Male auf, jedes Mal, wenn Sie mehrere Spalten in der Zeile zugreifen.  
  
 Die verschiedenen Aufrufe von **von IRow:: GetColumns** sollten sich nicht überschneiden. Angenommen, wenn der erste Aufruf **von IRow:: GetColumns** Spalten 1, 2 und 3, der zweite Aufruf ruft **von IRow:: GetColumns** sollten für die Spalten 4, 5 und 6 aufrufen. Wenn spätere Aufrufe von **von IRow:: GetColumns** überlappen, ist das Statusflag (Dwstatus-Feld in der DBCOLUMNACCESS) auf DBSTATUS_E_UNAVAILABLE festgelegt.  
  
## <a name="see-also"></a>Siehe auch  
 [Abrufen einer einzelnen Zeile mit IRow](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
