---
title: ICommand (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ICommand [SQL Server Native Client]
ms.assetid: 5e24b3a0-0658-44fc-b653-f4c52f9eb328
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 483c45ea2761a87e15a258ceca793dd09e1173f5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In diesem Thema wird erläutert, OLE DB-Verhalten die jeweilige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 Das Einfügen von Daten, die größer als die Größe einer Spalte sind, führt in der Regel zu einem Fehler. In bestimmten Situationen wird zwar S_OK zurückgegeben, der *dwStatus* wird jedoch auf DBSTATUS_S_TRUNCATED festgelegt. Dieser Fall tritt im Allgemeinen ein, wenn Daten mit Parametern eingefügt werden, die Spalte jedoch zum Speichern der Daten nicht groß genug ist und **ICommandWithParameters::SetParameterInfo** nicht aufgerufen wurde.  
  
## <a name="see-also"></a>Siehe auch  
 [Schnittstellen & #40; OLE DB & #41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
