---
title: Interoperabilität | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC]
- interoperability [ODBC], about interoperability
ms.assetid: 43b7c849-9d59-4002-9977-9e2c8730b859
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e7bbec995af3475208afa328c163dbbd42f0e46
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="interoperability"></a>Interoperabilität
*Interoperabilität* ist die Fähigkeit einer Anwendung mit vielen verschiedenen DBMS verwendet werden kann. Die Notwendigkeit zum Schreiben von generischen und interoperabler Anwendungen war eines der wichtigsten Faktoren, die zur Entwicklung von ODBC. Interoperabilität ist jedoch kein einfaches Pfad gefolgt von "nicht kompatibel", "vollständig interoperable." Der Pfad über viele Verzweigungen verfügt, und jedes erfordert eine vor-und Nachteile zwischen Funktionen, Geschwindigkeit, Codekomplexität und Entwicklungszeit.  
  
 Der Prozess des Schreibens einer interoperablen Anwendung führt mehrere Schritte:  
  
1.  Entscheiden, ob die Anwendung ODBC verwendet werden.  
  
2.  Wählen ein Maß an Interoperabilität und entscheiden, welche vor-und Nachteile zum Erreichen dieser Ebene erforderlich sind.  
  
3.  Interoperable Code schreiben, und es vollständig wie möglich zu testen.  
  
 Beachten Sie, dass die Interoperabilität in erster Linie für die Domäne der Autor der Anwendung ist. Treiber dienen zum Arbeiten mit einer einzelnen DBMS sind und per Definition sind nicht interoperabel. Sie spielen eine Rolle an der Interoperabilität von ordnungsgemäß implementieren und das Verfügbarmachen von ODBC über eine einzelne DBMS.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Ist ODBC die Antwort?](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [Auswählen einer Ebene der Interoperabilität](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [Ermitteln der Ziel-DBMS und Zieltreiber](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [Erwägen der zu verwendenden Datenbankfunktionen](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [Länge des Produktzyklus](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [Schreiben einer interoperablen Anwendung](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [Testen von interoperablen Anwendungen](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
