---
title: "Statusdatensätze | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 4a987f69-158f-4cc4-a31b-2b7dd8dcbb87
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ab82d285a57c147a27cb248e1e28b1bd9c6d0241
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="status-records"></a>Statusdatensätze
Die Felder in den statusdatensätzen enthalten Informationen über bestimmte Fehler oder Warnungen, die von der Treiber-Manager, Treiber oder eine Datenquelle, einschließlich der SQLSTATE, systemeigener Fehlernummer, diagnosemeldung, Spaltennummer und Zeilennummer zurückgegeben. Statusdatensätze können erstellt werden, nur, wenn die Funktion SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA oder SQL_STILL_EXECUTING zurückgibt. Eine vollständige Liste der Felder in den statusdatensätzen finden Sie unter der [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) funktionsbeschreibung.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Sequenz der Statusdatensätze](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [Diagnosemeldungen](../../../odbc/reference/develop-app/diagnostic-messages.md)
