---
title: Transaktionen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-transactions
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: 3b41e33a-c1ca-4b2a-9464-312b0ed3ca89
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c2a0bdf857a515cdff70cc04fc04294313b6e292
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="transactions"></a>Transaktionen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter implementiert die lokale Transaktion-Unterstützung. Der Consumer kann verteilte oder koordinierte Transaktionen mit Microsoft Distributed Transaction Coordinator (MS DTC) verwenden. Für Verbraucher, die Steuerung von Transaktionen, die mehrere Sitzungen umfasst die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter kann initiierte und von MS DTC verwaltete Transaktionen verknüpfen.  
  
 Wird standardmäßig die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter verwendet einen Autocommit-Transaktionsmodus, in dem jede diskrete Aktion in einer consumersitzung eine vollständige Transaktion für eine Instanz von umfasst [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter Autocommit-Modus ist lokal, und Autocommit-Transaktionen umfassen nie mehr als eine einzelne Sitzung.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter macht die **ITransactionLocal** -Schnittstelle, sodass des Consumers explizit und implizit starttransaktionen für eine einzelne Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützt keine geschachtelte lokale Transaktionen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Unterstützen lokaler Transaktionen](../../relational-databases/native-client-ole-db-transactions/supporting-local-transactions.md)  
  
-   [Unterstützen von verteilten Transaktionen](../../relational-databases/native-client-ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [Isolationsstufen &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
