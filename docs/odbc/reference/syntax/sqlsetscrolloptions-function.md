---
title: SQLSetScrollOptions Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLSetScrollOptions
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetScrollOptions
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC]
ms.assetid: 2a825ba7-7942-4c23-bcdb-c80dc12f8c86
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79ab0c408748fcbea30fdc2c792e433db8a4309d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetscrolloptions-function"></a>SQLSetScrollOptions-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: veraltet  
  
 **Zusammenfassung**  
 In ODBC 3.*.x*, die ODBC 2.0-Funktion **SQLSetScrollOptions** wurde ersetzt durch Aufrufe von **SQLGetInfo** und **SQLSetStmtAttr**.  
  
> [!NOTE]  
>  Weitere Informationen, was der Treiber-Manager diese Funktion einer ODBC 2. ordnet beim *.x* Anwendung arbeitet mit einer ODBC 3.*.x* -Treiber verwenden, finden Sie unter [veraltet Zuordnungsfunktionen](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität.  
  
> [!NOTE]  
>  Wenn der Treiber-Manager ordnet **SQLSetScrollOptions** für eine Anwendung mit dem Arbeiten mit einer ODBC 3.*.x* Treiber, der nicht unterstützt **SQLSetScrollOptions**, den Treiber -Manager setzt die SQL_ROWSET_SIZE setzen-Anweisungsoption nicht das SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut, zu der *RowsetSize* Argument in **SQLSetScrollOption**. Folglich **SQLSetScrollOptions** kann nicht von einer Anwendung verwendet werden, wenn mehrere Zeilen durch einen Aufruf zum Abrufen von **SQLFetch** oder **SQLFetchScroll**. Kann verwendet werden, nur dann, wenn durch einen Aufruf an das Abrufen mehrerer Zeilen **SQLExtendedFetch**.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die Anwendung auf einem 64-Bit-Betriebssystem ausgeführt wird, finden Sie unter [ODBC-64-Bit-Informationen](../../../odbc/reference/odbc-64-bit-information.md).  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
