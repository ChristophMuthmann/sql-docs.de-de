---
title: Rolle der Treiber-Manager | Microsoft Docs
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
- diagnostic information [ODBC], SqlGetDiagField
- diagnostic information [ODBC], driver manager error checking
- SQLGetDiagField function [ODBC], driver manager
- SQLGetDiagRec function [ODBC], driver manager
- ODBC driver manager [ODBC]
- diagnostic information [ODBC], SqlGetDiagRec
- driver manager [ODBC], error checking
ms.assetid: 7b861c82-357e-4590-8074-45136e9ed15e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0a6e0b002c34e8bf35f4f2c9b42dd7b47293ac9b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="role-of-the-driver-manager"></a>Rolle des Treiber-Managers
Der Treiber-Manager bestimmt die endgültige Reihenfolge in den statusdatensätzen zurückgegeben, die sie generiert. Insbesondere wird bestimmt, welcher Datensatz, hat den höchsten Rang, und zuerst zurückgegeben werden soll. Der Treiber ist verantwortlich für die Anordnung von statusdatensätzen, die sie generiert. Wenn durch den Treiber-Manager und der Treiber Statusdatensätze zurückgesendet werden, ist der Treiber-Manager für ihre Anordnung verantwortlich. Weitere Informationen finden Sie unter [Sequenz Statusdatensätze](../../../odbc/reference/develop-app/sequence-of-status-records.md).  
  
 Der Treiber-Manager wird so viel fehlerüberprüfung wie möglich. Dies spart Treiber aus, für die gleichen Fehler überprüfen. Wenn ein Funktionsargument eine diskrete Anzahl von Werten, z. B. akzeptiert z. B. *Vorgang* in **SQLSetPos**, der Treiber-Manager überprüft, dass der angegebene Wert gültig ist.  
  
 In den folgenden Abschnitten wird beschrieben, die Typen von Bedingungen, die vom Treiber-Manager überprüft. Sie dürfen nicht vollständig sein; für eine vollständige Liste der SQLSTATEs der Treiber-Manager zurückgibt, finden Sie im Abschnitt "Diagnose" für jede Funktion. die Beschreibung der einzelnen Kontrollkästchen vom Treiber-Manager vorgenommen beginnt mit den Buchstaben "(DM)." Siehe auch die Statustabellen der Übergang in [Anhang B: ODBC-Übergang-Statustabellen](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md); Fehler in Klammern angezeigt werden vom Treiber-Manager erkannt.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Überprüfungen des Argumentwerts](../../../odbc/reference/develop-app/argument-value-checks.md)  
  
-   [Überprüfungen des Statusübergangs](../../../odbc/reference/develop-app/state-transition-checks.md)  
  
-   [Überprüfungen auf allgemeine Fehler](../../../odbc/reference/develop-app/general-error-checks.md)  
  
-   [Fehler des Treiber-Managers und Überprüfungen der Warnung](../../../odbc/reference/develop-app/driver-manager-error-and-warning-checks.md)
