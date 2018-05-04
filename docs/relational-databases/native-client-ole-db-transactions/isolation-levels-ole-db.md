---
title: Isolationsstufen (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: d70ee72c-6e2a-4bcd-9456-4a697a866361
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: cbaf0204f27582697e924d919bc2338f9e3acde0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="isolation-levels-ole-db"></a>Isolationsstufen (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Clients können Transaktionsisolationsstufen für eine Verbindung steuern. Isolationsstufe der Transaktion, steuern die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter Consumer verwendet:  
  
-   DBPROPSET_SESSION-Eigenschaft DBPROP_SESS_AUTOCOMMITISOLEVELS für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter standardmäßigen Autocommitmodus.  
  
     Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter-Standardeinstellung für die Stufe ist DBPROPVAL_TI_READCOMMITTED.  
  
-   Die *IsoLevel* Parameter von der **ITransactionLocal:: StartTransaction** Methode für lokale Manualcommit-Transaktionen.  
  
-   Die *IsoLevel* Parameter von der **ITransactionDispenser:: BeginTransaction** Methode für die MS DTC koordinierte verteilte Transaktionen.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lässt schreibgeschützten Zugriff auf die Dirty Read-Isolationsstufe zu. Alle anderen Stufen schränken Parallelität ein, indem sie Sperren für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Objekte anwenden. Da der Client größere Parallelitätsstufen benötigt, wendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] größere Einschränkungen auf gleichzeitigem Zugriff auf Daten an. Verwalten Sie das höchste Maß an gleichzeitigen Zugriff auf Daten, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Consumer der Native Client OLE DB-Anbieter muss seine Anforderungen für spezielle Parallelitätsstufen auf intelligente Weise steuern.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] hat Momentaufnahmeisolationsstufe eingeführt. Weitere Informationen finden Sie unter [arbeiten mit Snapshot-Isolation](../../relational-databases/native-client/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Transaktionen](../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
