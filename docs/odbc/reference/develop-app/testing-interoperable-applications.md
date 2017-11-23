---
title: Testen von interoperablen Anwendungen | Microsoft Docs
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
- interoperability [ODBC], testing interoperable applications
- testing interoperable applications [ODBC]
ms.assetid: 489083cb-8430-40be-9ef2-d75b9a2eea88
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1722688afbda2ecbc8a71d05cc8f9bb4bc330345
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="testing-interoperable-applications"></a>Testen von interoperablen Anwendungen ausführen können
Testen von interoperablen Anwendungen ist bestenfalls eine zeitaufwändig Geschäfts- und im schlimmsten Fall nicht möglich, da die neuen Treiber ständig auf dem Markt angezeigt werden. Ein akzeptablen Grad an Tests ist jedoch möglich. Anwendungen mit begrenzten "oder" niedrig Interoperabilität müssen nur für diese Treiber getestet werden soll, die sie unterstützen garantiert werden. Sie müssen jedoch vollständig für diese Treiber getestet werden.  
  
 Äußerst interoperable Anwendungen können nicht für alle Treiber praktisch getestet werden soll. Am besten geeignet, die meisten Anwendungsentwickler können ist vollständig für eine kleine Anzahl von Treibern und cursorily für weitere Tests. Getestete Treiber sollte die am häufigsten verwendeten Treiber für die am häufigsten verwendeten DBMS in der Anwendung Markt enthalten; der Markt allen DBMS abdeckt, sollten die Treiber für Desktops und Server DBMS getestet werden.  
  
 Eines der Probleme beim Testen der ODBC-Anwendungen ist die Anzahl der beteiligten Komponenten: die Anwendung selbst, der Treiber-Manager, den Treiber, die DBMS, und möglicherweise Netzwerksoftware oder -Gateways. Anwendungen leichter können zum Nachverfolgen von Fehlern durch das Bereitstellen von Fehlermeldungen, die von ODBC-Funktionen über die zurückgegebene **SQLGetDiagField** und **SQLGetDiagRec**. Diese Nachrichten Identifizieren der Hersteller und die Komponente, in denen Fehler auftreten. Weitere Informationen finden Sie unter [Diagnose](../../../odbc/reference/develop-app/diagnostics.md).
