---
title: SQLGetConnectOption Funktion | Microsoft Docs
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
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectOption
helpviewer_keywords:
- SQLGetConnectOption function [ODBC]
ms.assetid: 59cde899-7957-4b5e-8677-f34d3b859bfd
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 079ab02fdc7ff44012c5c2a13a0fd369577ace0f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: veraltet  
  
 **Zusammenfassung**  
 In ODBC 3.*.x*, die ODBC 2.*.x* Funktion **SQLGetConnectOption** wurde ersetzt durch **SQLGetConnectAttr**. Weitere Informationen finden Sie unter [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md).  
  
> [!NOTE]  
>  Weitere Informationen, was der Treiber-Manager diese Funktion einer ODBC 2. ordnet beim *.x* Anwendung arbeitet mit einer ODBC 3.*.x* -Treiber verwenden, finden Sie unter [veraltet Zuordnungsfunktionen](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)in Anhang G: Treiber Richtlinien für die Abwärtskompatibilität.  
  
> [!NOTE]  
>  Das Attribut SQL_ASYNC_DBC_FUNCTION_ENABLE in ODBC 3.8 eingeführt wird nicht von **SQLGetConnectOption**. Anwendungen, die den asynchronen Vorgang für ein Verbindungshandle verwenden müssen verwenden **SQLGetConnectAttr**.  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
