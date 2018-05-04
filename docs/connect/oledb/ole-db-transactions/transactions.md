---
title: Transaktionen | Microsoft Docs
description: Transaktionen in OLE DB-Treiber für SQLServer
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
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 71ec6bbd3efb60c5a2dcc20f2496f038bd6b330a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="transactions"></a>Transaktionen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Der OLE DB-Treiber für SQL Server implementiert die lokale Transaktion-Unterstützung. Der Consumer kann verteilte oder koordinierte Transaktionen mit Microsoft Distributed Transaction Coordinator (MS DTC) verwenden. Für Verbraucher, die, die Steuerung von Transaktionen, die mehrere Sitzungen umfasst, können der OLE DB-Treiber für SQL Server initiierte und von MS DTC verwaltete Transaktionen verknüpfen.  
  
 Der OLE DB-Treiber für SQL Server verwendet standardmäßig ein, in dem jede diskrete Aktion in einer consumersitzung eine vollständige Transaktion für eine Instanz von umfasst Autocommit-Transaktionsmodus [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Der OLE DB-Treiber für SQL Server-Autocommit-Modus ist lokal, und Autocommit-Transaktionen umfassen nie mehr als eine einzelne Sitzung.  
  
 Der OLE DB-Treiber für SQL Server macht die **ITransactionLocal** -Schnittstelle, sodass des Consumers explizit und implizit starttransaktionen für eine einzelne Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Der OLE DB-Treiber für SQL Server unterstützt keine geschachtelte lokale Transaktionen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Unterstützen lokaler Transaktionen](../../oledb/ole-db-transactions/supporting-local-transactions.md)  
  
-   [Unterstützen von verteilten Transaktionen](../../oledb/ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [Isolationsstufen &#40;OLE DB&#41;](../../oledb/ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Programmierung](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
