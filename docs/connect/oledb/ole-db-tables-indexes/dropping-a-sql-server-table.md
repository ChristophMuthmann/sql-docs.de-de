---
title: Löschen einer SQL Server-Tabelle | Microsoft Docs
description: Löschen einer SQL Server-Tabelle, die mithilfe von OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- deleting tables
- OLE DB Driver for SQL Server, tables
- removing tables
- dropping tables
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bd9dd493a114475e9f0ca5c14cd32a9418931b9b
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="dropping-a-sql-server-table"></a>Löschen einer SQL Server-Tabelle
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Der OLE DB-Treiber für SQL Server macht die **dropTable** Function zum Entfernen einer [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabelle aus einer Datenbank.  
  
 Geben Sie den Tabellennamen als Unicode-Zeichenfolge in der *PwszName* Mitglied der *uName* -Vereinigung der *pTableID* Parameter. Die *eKind* Mitglied *pTableID* muss DBKIND_NAME sein.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellen und Indizes](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
