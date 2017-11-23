---
title: "Große benutzerdefinierte CLR-Typen | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: large CLR user-defined types
ms.assetid: b65eb61d-ccf6-49c0-98e7-9a4ef4b2f790
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6f3bd1277849a00ae27b5227acbccf05e2a674d8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="large-clr-user-defined-types"></a>Große benutzerdefinierte CLR-Typen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  In SQL Server 2005 waren benutzerdefinierte Typen (User-Defined Types, UDTs) in der Common Language Runtime (CLR) auf eine Größe von 8.000 Bytes beschränkt. Diese Einschränkung wurde aufgehoben [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] und höheren Versionen. CLR-UDTs werden jetzt auf eine ähnliche Weise wie große Objekttypen (LOB) behandelt. UDTs mit genau oder weniger als 8.000 Byte verhalten sich also genau wie in SQL Server 2005. Größere UDTs werden aber unterstützt und zeigen ihre Größe als "unbegrenzt" an.  
  
 Weitere Informationen finden Sie unter [Large CLR User-Defined Datentypen &#40; OLE DB &#41;](../../../relational-databases/native-client/ole-db/large-clr-user-defined-types-ole-db.md) und [Large CLR User-Defined Datentypen &#40; ODBC &#41;](../../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="use-cases"></a>Einsatzgebiete  
 Für ODBC umfasst die Unterstützung großer UDTs die Möglichkeit zum Versenden von UDT-Werten in Teilen als Data-at-Execution-Parameter. Dies erfolgt mithilfe von SQLPutData.  
  
 Für OLE DB-Unterstützung für große UDTs die Möglichkeit zum Stream UDT-Werte zu und von dem Server mithilfe von ISequentialStream-Bindung.  
  
 UDTs kleiner oder gleich 8.000 Byte verhalten sich wie in SQL Server 2005. Für OLE DB können Sie immer noch kleine UDTs streamen, mithilfe von ISequentialStream-Bindung.  
  
 Manchmal muss systemeigener Code den Inhalt von CLR-UDTs verstehen, muss aber keine verwalteten Objekte instanziieren. In diesem Fall können Sie die benutzerdefinierte Serialisierung verwenden, um UDT-Werte auf dem Server in ein für die Clients bekanntes Format zu konvertieren.  
  
 Bei Anwendungen, die über einen vorhandenen Datenzugriffscode verfügen, können Sie das CLR-UDT-Verhalten auf dem Client nutzen, indem Sie UDTs über systemeigene APIs abrufen und sie mithilfe von C++ CLI Interop in Anwendungen des gemischten Modus instanziieren.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client-Features](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
