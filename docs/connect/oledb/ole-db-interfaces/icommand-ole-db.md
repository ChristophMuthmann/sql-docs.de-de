---
title: ICommand (OLE DB) | Microsoft Docs
description: ICommand-Schnittstelle (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ICommand [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0773739177de393b44aedec96b907a39fe37e04c
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Dieser Artikel beschreibt die OLE DB-Verhalten, die speziell für OLE DB-Treiber für SQL Server ist.  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 Das Einfügen von Daten, die größer als die Größe einer Spalte sind, führt in der Regel zu einem Fehler. In bestimmten Situationen wird zwar S_OK zurückgegeben, der *dwStatus* wird jedoch auf DBSTATUS_S_TRUNCATED festgelegt. Es im Allgemeinen tritt auf beim Einfügen von Daten mit Parametern, in denen die Spalte nicht groß genug zum Speichern der Daten ist, und **ICommandWithParameters:: SetParameterInfo** wurde nicht aufgerufen wurde.  
  
## <a name="see-also"></a>Siehe auch  
 [Schnittstellen & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)
  
  
