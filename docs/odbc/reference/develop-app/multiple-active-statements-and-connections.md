---
title: Mehrere aktive Anweisungen und Verbindungen | Microsoft Docs
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
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bff1b38ffb11cfd92b158e985dc6eaa45af9958c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="multiple-active-statements-and-connections"></a>Mehrere aktive Anweisungen und Verbindungen
Einige Treiber und DBMS begrenzen die Anzahl der Anweisungen und Verbindungen, die gleichzeitig aktiv sein können. Diese Werte können so klein wie eine sein. Weitere Informationen finden Sie unter der SQL_MAX_CONCURRENT_ACTIVITIES und SQL_MAX_DRIVER_CONNECTIONS Optionen in der [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) funktionsbeschreibung, und [Anweisung verarbeitet](../../../odbc/reference/develop-app/statement-handles.md) und [ Verbindungshandles](../../../odbc/reference/develop-app/connection-handles.md).
