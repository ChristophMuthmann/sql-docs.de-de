---
title: SQLSpecialColumns | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLSpecialColumns function
ms.assetid: dffe02ed-8f79-4c9a-af34-98130bbe5462
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ff6889d81489b0009d4c48b5194d772abaec014
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sqlspecialcolumns"></a>'SQLSpecialColumns'
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Bei Anforderung von zeilenbezeichnern (*IdentifierType* SQL_BEST_ROWID), **SQLSpecialColumns** gibt ein leeres Resultset (keine Datenzeilen) zurück, für alle Bereich außer SQL_SCOPE_CURROW angeforderten. Das generierte Resultset gibt an, dass die Spalten nur innerhalb dieses Bereichs gültig sind.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt keine Pseudospalten für Bezeichner. Die **SQLSpecialColumns** Resultset identifiziert alle Spalten als SQL_PC_NOT_PSEUDO.  
  
 **SQLSpecialColumns** kann in einem statischen Cursor ausgeführt werden. Der Versuch auszuführen **SQLSpecialColumns** in einem aktualisierbaren (keysetgesteuerten oder dynamischen) gibt SQL_SUCCESS_WITH_INFO, dass der Cursortyp geändert wurde.  
  
## <a name="sqlspecialcolumns-support-for-enhanced-date-and-time-features"></a>SQLSpecialColumns-Unterstützung für erweiterte Funktionen zu Datum und Uhrzeit  
 Weitere Informationen zu den Werten für die Spalten DATA_TYPE, TYPE_NAME, COLUMN_SIZE, BUFFER_LENGTH und DECIMAL_DIGTS für Datum/Uhrzeit-Typen zurückgegeben wird, finden Sie unter [Katalogmetadaten](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Weitere allgemeine Informationen finden Sie unter [Datum und Uhrzeit-Verbesserungen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlspecialcolumns-support-for-large-clr-udts"></a>SQLSpecialColumns -Unterstützung für große CLR-UDTs  
 **SQLSpecialColumns** unterstützt große CLR-benutzerdefinierte Typen (UDTs). Weitere Informationen finden Sie unter [Large CLR User-Defined Datentypen &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLSpecialColumns-Funktion](http://go.microsoft.com/fwlink/?LinkId=59371)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
