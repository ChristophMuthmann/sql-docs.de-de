---
title: "Internationale Unterstützung (Visual FoxPro-ODBC-Treiber) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
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
ms.openlocfilehash: 7f99c63f641ecdb6338f8028cc7438021e32e2ae
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
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
