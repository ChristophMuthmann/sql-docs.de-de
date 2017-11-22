---
title: Umgebung, Verbindungs- und Anweisungsattribute | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- environment attributes [ODBC]
- connection attributes [ODBC]
- statement attributes [ODBC]
ms.assetid: 9e15b276-3b7a-428a-b72f-a3ddfe1ba1ce
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 933e51d6ae61f734f2e849e91837dcf5404728f1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="environment-connection-and-statement-attributes"></a>Umgebung, Verbindungs- und Anweisungsattribute
ODBC definiert eine Reihe von Attributen, die Umgebungen, Verbindungen und Anweisungen zugeordnet sind.  
  
 Umgebung Attribute beeinflussen die gesamte Umgebung, z. B., ob Verbindungspooling aktiviert ist. Umgebung Attribute werden festgelegt, mit **SQLSetEnvAttr** und mit abgerufene **SQLGetEnvAttr**.  
  
 Verbindungsattribute beeinflussen jede Verbindung einzeln, z. B. wie lange ein Treiber beim Versuch, die für die Verbindung mit einer Datenquelle, bevor ein Timeout auftritt, warten soll. Weitere Verbindungsattribute gesetzt werden, mit **SQLSetConnectAttr** und mit abgerufene **SQLGetConnectAttr**. Weitere Informationen zu Verbindungsattributen finden Sie unter [Verbindungsattribute](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Anweisungsattribute beeinflussen jede Anweisung einzeln, z. B., ob eine Anweisung asynchron ausgeführt werden soll. Anweisungsattribute werden mit festgelegt **SQLSetStmtAttr** und mit abgerufene **SQLGetStmtAttr**. Einige Anweisungsattribute sind nur-Lese Attribute und können nicht festgelegt werden. Beispielsweise ist das SQL_ATTR_ROW_NUMBER-Anweisungsattribut, die verwendet wird, um die Anzahl der aktuellen Zeile im Cursor abzurufen, schreibgeschützt. Weitere Informationen zu Anweisungsattribute, finden Sie unter [Anweisungsattribute](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Zusätzlich zu den Attributen, die von ODBC definiert werden kann ein Treiber eigene Verbindungs- und Anweisungsattribute definieren. Treiberdefinierten Attribute müssen registriert sein, mit der Open Group, um sicherzustellen, dass zwei Treiber Lieferanten verschiedene, proprietäre Attribute keine den gleichen ganzzahligen Wert zuweisen. Weitere Informationen finden Sie unter [Treiber-spezifische Datentypen, Deskriptor Typen Informationstypen, Diagnosetypen und Attribute](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Eine vollständige Liste von Attributen finden Sie unter [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), und [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md). Die meisten Attribute werden auch in der Beschreibung der ODBC-Funktion beschrieben, die sie betreffen.
