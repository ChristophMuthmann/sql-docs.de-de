---
title: Erstellen eines Rowsets mit IOpenRowset | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c78658537d6af6bd08423aa2be3add03bdaba7b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Erstellen eines Rowsets mit 'IopenRowset'
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützt die **IOpenRowset:: OPENROWSET** Methode mit den folgenden Einschränkungen:  
  
-   Eine Basistabelle oder Sicht muss angegeben werden in einer Datenbank-ID (DBID) Struktur, die die *pTableID* -Parameter zeigt.  
  
-   Die DBID *eKind* Element muss dbkind_name.  
  
-   Die DBID *uName* Member muss den Namen einer vorhandenen Basistabelle oder einer Sicht als Unicode-Zeichenfolge angeben.  
  
-   Die *pIndexID* Parameter **OpenRowset** muss NULL sein.  
  
 Das Resultset von **IOpenRowset:: OPENROWSET** enthält ein einzelnes Rowset. Resultsets, die ein einzelnes Rowset enthalten können unterstützt werden, indem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Cursor. Die Cursorunterstützung ermöglicht dem Entwickler die Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Parallelitätsmechanismen.  
  
## <a name="see-also"></a>Siehe auch  
 [Rowsets](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
