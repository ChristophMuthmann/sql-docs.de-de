---
title: UTF-16-Unterstützung in OLE DB-Treiber für SQLServer | Microsoft Docs
description: UTF-16-Unterstützung in OLE DB-Treiber für SQLServer
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
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
manager: craigg
ms.openlocfilehash: f88dea7bbc4fbd2ea6307647e1cbce47b07a0558
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>UTF-16-Unterstützung in OLE DB-Treiber für SQLServer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Ab [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], wenn Sie beim Binden eines Spaltenergebnisses oder Ausgabeparameters einen Puffer fester Länge angeben und die **Wchar** Zeichen, die in den Puffer geschrieben werden, bevor das abschließende Zeichen ein hoher Ersatzzeichencodepunkt ist ein Ersatzzeichenpaars, und wenn das nächste **Wchar** Zeichen ist ein niedriger Ersatzzeichencodepunkt, OLE DB-Treiber für SQL Server wird nicht die hoher Ersatzzeichencodepunkt hinzugefügt, in den Puffer.  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Features](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
