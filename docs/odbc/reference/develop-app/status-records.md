---
title: Statusdatensätze | Microsoft Docs
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
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 4a987f69-158f-4cc4-a31b-2b7dd8dcbb87
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b8a5cc55bacf76b8bf7d0e9b35a4e7a4daa9439
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="status-records"></a>Statusdatensätze
Die Felder in den statusdatensätzen enthalten Informationen über bestimmte Fehler oder Warnungen, die von der Treiber-Manager, Treiber oder eine Datenquelle, einschließlich der SQLSTATE, systemeigener Fehlernummer, diagnosemeldung, Spaltennummer und Zeilennummer zurückgegeben. Statusdatensätze können erstellt werden, nur, wenn die Funktion SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA oder SQL_STILL_EXECUTING zurückgibt. Eine vollständige Liste der Felder in den statusdatensätzen finden Sie unter der [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) funktionsbeschreibung.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Sequenz der Statusdatensätze](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [Diagnosemeldungen](../../../odbc/reference/develop-app/diagnostic-messages.md)
