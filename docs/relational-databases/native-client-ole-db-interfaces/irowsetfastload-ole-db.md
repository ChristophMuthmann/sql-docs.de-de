---
title: IRowsetFastLoad (OLE DB) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-interfaces
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: COM
helpviewer_keywords: IRowsetFastLoad interface
ms.assetid: d19a7097-48d9-409a-aff9-277891b7aca7
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2c2dc8ba7de032f9f9dbdb21d51b22e7347a68fc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die **IRowsetFastLoad** Schnittstelle verfügbar macht, Unterstützung für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] speicherbasierte Massenkopiervorgänge. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB-Anbieters verwenden die Schnittstelle zum schnellen Hinzufügen von Daten zu einem vorhandenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle.  
  
 Wenn Sie SSPROP_ENABLEFASTLOAD für eine Sitzung auf VARIANT_TRUE festlegen, können Sie keine Daten aus Rowsets lesen, die danach von dieser Sitzung zurückgegeben werden. Wenn SSPROP_ENABLEFASTLOAD auf VARIANT_TRUE festgelegt ist, werden alle in der Sitzung erstellten Rowsets vom Typ IRowsetFastLoad. IRowsetFastLoad-Rowsets unterstützen nicht die Funktionalität zum Abrufen. aus diesem Grund können keine Daten aus diesen Rowsets nicht gelesen werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Methode|Description|  
|------------|-----------------|  
|[IRowsetFastLoad:: Commit &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md)|Markiert das Ende eines Batches eingefügter Zeilen und schreibt die Zeilen in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle.|  
|[IRowsetFastLoad:: InsertRow &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)|Fügt dem Rowset für das Massenkopieren eine Zeile hinzu.|  
  
## <a name="see-also"></a>Siehe auch  
 [Schnittstellen &#40; OLE DB &#41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [Massenimport von Daten mithilfe von IRowsetFastLoad &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [Senden von BLOB-Daten an SQLServer mit IROWSETFASTLOAD und ISEQUENTIALSTREAM &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
