---
title: UTF-16-Unterstützung in OLE DB-Treiber für SQLServer | Microsoft Docs
description: UTF-16-Unterstützung in OLE DB-Treiber für SQLServer
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a0f710e6f567f789771a80677beb24d24b1c8f5d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>UTF-16-Unterstützung in OLE DB-Treiber für SQLServer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Ab [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], wenn Sie beim Binden eines Spaltenergebnisses oder Ausgabeparameters einen Puffer fester Länge angeben und die **Wchar** Zeichen, die in den Puffer geschrieben werden, bevor das abschließende Zeichen ein hoher Ersatzzeichencodepunkt ist ein Ersatzzeichenpaars, und wenn das nächste **Wchar** Zeichen ist ein niedriger Ersatzzeichencodepunkt, OLE DB-Treiber für SQL Server wird nicht die hoher Ersatzzeichencodepunkt hinzugefügt, in den Puffer.  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Features](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
