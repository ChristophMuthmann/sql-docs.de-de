---
title: Verwenden der OUTPUT-Klausel mit OLE DB in SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-provider
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 53deeb99-c088-4fde-844b-b2d91d6de1eb
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5ab1101c5cb3bcddb5603fa83b3efd91b02cc592
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-the-output-clause-with-ole-db-in-sql-server-native-client"></a>Verwenden der OUTPUT-Klausel mit OLE DB in SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Wenn Sie in einem INSERT-, UPDATE-, DELETE- oder MERGE-Befehl eine OUTPUT-Klausel verwenden, ist die Anzahl der betroffenen Zeilen nicht verfügbar. Die Anwendung muss die Anzahl von Zeilen im Rowset zählen, die von der OUTPUT-Klausel zurückgegeben werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eine SQL Server Native Client OLE DB-Anbieteranwendung](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
