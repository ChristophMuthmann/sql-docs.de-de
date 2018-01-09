---
title: SQLProcedures | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 23a0c1de61959b3a69766b6554f4c20694dea208
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="sqlprocedures"></a>'SQLProcedures'
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Alle gespeicherten Prozeduren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geben einen Wert zurück. **SQLProcedures** gibt SQL_PT_FUNCTION für die Resultsetspalte PROCEDURE_TYPE aus.  
  
 **SQLProcedures** gibt SQL_SUCCESS zurück, unabhängig davon, ob Werte für die Parameter *CatalogName, SchemaName* oder *ProcName* vorhanden sind. **SQLFetch** gibt SQL_NO_DATA zurück, wenn in diesen Parametern ungültige Werte verwendet werden.  
  
 **SQLProcedures** kann in einem statischen Servercursor ausgeführt werden. Wenn versucht wird, **SQLProcedures** in einem aktualisierbaren (dynamischen oder Keyset-)Cursor auszuführen, gibt der Cursor SQL_SUCCESS_WITH_INFO zurück. Das bedeutet, dass der Cursortyp geändert wurde.  
  
 **SQLProcedures** gibt Informationen zu allen Prozeduren zurück, deren Name *ProcName* entspricht und die vom aktuellen Benutzer ausgeführt werden können bzw. für die der Benutzer die VIEW DEFINITION-Berechtigung erhalten hat.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLProcedures-Funktion](http://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
