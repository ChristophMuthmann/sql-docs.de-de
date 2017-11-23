---
title: "Internationale Unterstützung (Visual FoxPro-ODBC-Treiber) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- double-byte character sets [ODBC]
- FoxPro ODBC driver [ODBC], international support
- DBCS [ODBC]
- international support [ODBC]
- sort order [ODBC]
- collating sequences [ODBC]
- Visual FoxPro ODBC driver [ODBC], international support
ms.assetid: cd3fab32-13f1-4a86-abc4-5e18667669fc
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 06d85711cc234a8245e22b6b923b02641259eeef
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>Internationale Unterstützung (Visual FoxPro-ODBC-Treiber)
Microsoft Visual FoxPro-ODBC-Treiber unterstützt:  
  
-   Doppelbyte-Zeichensätze (DBCS)  
  
-   Mehrere für Sequenzen  
  
 Eine Sortierreihenfolge definiert die *Sortierreihenfolge* für Daten, die in einer Visual FoxPro-Tabelle oder einer Datenbank gespeichert. Standardmäßig ist der Treiber konfiguriert, um die Sortierreihenfolge Sequenzen zu verwenden, die die Sprachversion des Betriebssystems zu unterstützen.  
  
 Eine Liste der unterstützten Sortierreihenfolge Sequenzen, finden Sie unter [festgelegt COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
## <a name="locale"></a>Gebietsschema  
 Der Satz von Informationen, die eine bestimmte Sprache und Land/Region entspricht. Ein Gebietsschema gibt bestimmte Einstellungen wie z. B. Dezimaltrennzeichen, Datums- und Zeitformate und Sortierreihenfolge mit dem Zeichen an.  
  
## <a name="sort-order"></a>Sortierreihenfolge  
 Sortierreihenfolgen integrieren die Sortierungsregeln verschiedener *Gebietsschema*s, und Sie können die Daten in diesen Sprachen ordnungsgemäß sortiert. In der Visual FoxPro bestimmt die aktuelle Sortierreihenfolge die Ergebnisse des Ausdrucks Zeichenvergleiche und die Reihenfolge, in der die Datensätze in angezeigt werden, sortiert der Tabellen oder indizierten.
