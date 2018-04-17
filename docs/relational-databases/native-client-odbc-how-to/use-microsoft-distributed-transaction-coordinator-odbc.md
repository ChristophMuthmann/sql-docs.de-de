---
title: Verwenden Sie Microsoft Distributed Transaction Coordinator (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-how-to
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MS DTC, using
ms.assetid: 12a275e1-8c7e-436d-8a4e-b7bee853b35c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: fc4ad990a8ccb3a30e03deac03bb19e323199748
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="use-microsoft-distributed-transaction-coordinator-odbc"></a>Verwenden von Microsoft Distributed Transaction Coordinator (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
### <a name="to-update-two-or-more-sql-servers-by-using-ms-dtc"></a>So aktualisieren Sie zwei oder mehr SQL Server mit MS DTC  
  
1.  Stellen Sie mit der MS DTC OLE-Funktion DtcGetTransactionManager eine Verbindung mit MS DTC her. Informationen zu MS DTC finden Sie unter Microsoft Distributed Transaction Coordinator.  
  
2.  Rufen Sie SQLDriverConnect einmal für jede Microsoft® SQL Server™-Verbindung auf, die Sie einrichten möchten.  
  
3.  Rufen Sie die MS DTC OLE-Funktion ITransactionDispenser::BeginTransaction auf, um eine MS DTC-Transaktion zu starten und ein Transaction-Objekt zu erhalten, das diese Transaktion repräsentiert.  
  
4.  Rufen Sie [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) mindestens einmal für jede ODBC-Verbindung auf, die Sie in der MS DTC-Transaktion auflisten möchten. Der zweite [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)-Parameter muss SQL_ATTR_ENLIST_IN_DTC lauten, und der dritte Parameter muss das Transaktionsobjekt (aus Schritt 3) sein.  
  
5.  Rufen Sie [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399) einmal für jeden SQL Server auf, den Sie aktualisieren möchten.  
  
6.  Rufen Sie MS DTC OLE-Funktion ITransaction::Commit auf, um ein Commit für die MS DTC-Transaktion auszuführen. Das Transaction-Objekt ist nicht mehr gültig.  
  
 Um eine Reihe von MS DTC-Transaktionen auszuführen, wiederholen Sie die Schritte 3 bis 6.  
  
 Um den Verweis auf das Transaction-Objekt freizugeben, rufen Sie die MS DTC OLE-Funktion ITransaction::Return auf.  
  
 Wenn Sie eine ODBC-Verbindung mit einer MS DTC-Transaktion und dieselbe Verbindung dann mit einer lokalen SQL Server-Transaktion verwenden möchten, rufen Sie [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) mit SQL_DTC_DONE auf.  
  
> [!NOTE]  
>  Sie können [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) und [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399) auch nacheinander für jeden SQL Server aufrufen, statt sie gemäß dem Vorschlag in den Schritten 4 und 5 aufzurufen.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Transaktionen & #40; ODBC & #41;](http://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
  
