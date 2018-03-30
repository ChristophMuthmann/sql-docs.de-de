---
title: ICommandWithParameters | Microsoft Docs
description: ICommandWithParameters-Schnittstelle
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9d810ea13512537572bf39fbda938b6b59d64db7
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Verbesserungen am Anfang des Datenbank-Engine mit [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] ICommandWithParameters:: GetParameterInfo genauere Beschreibungen der erwarteten Ergebnisse abrufen können. Diese genaueren Ergebnisse unterscheidet sich möglicherweise von der Rückgabewerte CommandWithParameters::GetParameterInfo in früheren Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [Metadatenermittlung](../../oledb/features/metadata-discovery.md).  
  
 Ab [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], beim Aufrufen von ICommandWithParameters:: SetParameterInfo, der an übergebene Wert den *PwszName* Parameter muss ein gültiger Bezeichner sein. Weitere Informationen finden Sie unter [Datenbankbezeichner](../../../relational-databases/databases/database-identifiers.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Schnittstellen &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
