---
title: Isolationsstufen (OLE DB) | Microsoft Docs
description: Isolationsstufen (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 03612c759cd25eb280573fa172ef86691f58dc19
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="isolation-levels-ole-db"></a>Isolationsstufen (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Clients können Transaktionsisolationsstufen für eine Verbindung steuern. Wird verwendet um Transaktionsisolationsstufen zu steuern, die OLE DB-Treiber für SQL Server-Consumer aus:  
  
-   DBPROPSET_SESSION-Eigenschaft DBPROP_SESS_AUTOCOMMITISOLEVELS für den OLE DB-Treiber für SQL Server Standard Autocommit-Modus.  
  
     Der OLE DB-Treiber für SQL Server-Standard für die Stufe ist DBPROPVAL_TI_READCOMMITTED.  
  
-   Die *IsoLevel* Parameter von der **ITransactionLocal:: StartTransaction** Methode für lokale Manualcommit-Transaktionen.  
  
-   Die *IsoLevel* Parameter von der **ITransactionDispenser:: BeginTransaction** Methode für die MS DTC koordinierte verteilte Transaktionen.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] lässt schreibgeschützten Zugriff auf die Dirty Read-Isolationsstufe zu. Alle anderen Stufen schränken Parallelität ein, indem sie Sperren für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Objekte anwenden. Da der Client größere Parallelitätsstufen benötigt, wendet [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] größere Einschränkungen auf gleichzeitigem Zugriff auf Daten an. Um das höchste Maß an gleichzeitigen Zugriff auf Daten zu gewährleisten, sollte der OLE DB-Treiber für SQL Server-Consumer seine Anforderungen für spezielle Parallelitätsstufen auf intelligente Weise steuern.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] hat Momentaufnahmeisolationsstufe eingeführt. Weitere Informationen finden Sie unter [arbeiten mit Snapshot-Isolation](../../oledb/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Transaktionen](../../oledb/ole-db-transactions/transactions.md)  
  
  
