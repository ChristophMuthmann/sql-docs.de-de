---
title: 'Schritt 4a: Abrufen der Ergebnisse | Microsoft Docs'
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
- application process [ODBC], fetching results
- fetches [ODBC], fetching results
ms.assetid: 77d30142-c774-473c-96fb-b364bb92ac60
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96a6142cf8ea34f192d0bef5af4a4de0977551c3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="step-4a-fetch-the-results"></a>Schritt 4a: Abrufen der Ergebnisse
Der nächste Schritt besteht, die Ergebnisse abzurufen, wie in der folgenden Abbildung dargestellt.  
  
 ![Zeigt das Abrufen von Ergebnissen in einer ODBC-Anwendung](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 Wenn die Anweisung in "Schritt 3: Erstellen und Ausführen einer SQL-Anweisung" ausgeführt wurde eine **wählen** -Anweisung oder eine Katalogfunktion auf, ruft die Anwendung zuerst **SQLNumResultCols** bestimmt die Anzahl der Spalten im Resultset. Dieser Schritt ist nicht erforderlich, wenn die Anwendung bereits bekannt, die Anzahl der Resultsets Resultsetspalten ist, z. B. wenn die SQL-Anweisung in einer vertikalen oder benutzerdefinierten Anwendung hartcodiert wird.  
  
 Als Nächstes ruft die Anwendung ab, der Name, Datentyp, Genauigkeit und Skalierung jeder Resultsetspalte mit **SQLDescribeCol**. In diesem Fall ist dies nicht erforderlich für Anwendungen, z. B. vertikale und benutzerdefinierte Anwendungen, die diese Informationen bereits kennen. Die Anwendung übergibt diese Informationen **SQLBindCol**, die eine Anwendungsvariable bindet, auf eine Spalte im Resultset.  
  
 Die Anwendung jetzt ruft **SQLFetch** Abrufen der ersten Zeile der Daten, und legen die Daten aus dieser Zeile in der Variablen mit gebundenen **SQLBindCol**. Wenn lange Daten in der Zeile vorhanden sind, ruft er dann **SQLGetData** zum Abrufen dieser Daten. Rufen Sie die Anwendung weiterhin **SQLFetch** und **SQLGetData** weitere Daten ab. Nach dem Abrufen von Daten abgeschlossen wurde, ruft **SQLCloseCursor** Schließen des Cursors.  
  
 Eine vollständige Beschreibung der Ergebnisse abgerufen werden soll, finden Sie unter [Abrufen von Ergebnissen (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md) und [Abrufen von Ergebnissen (Erweitert)](../../../odbc/reference/develop-app/retrieving-results-advanced.md).  
  
 "Schritt 3: Erstellen und Ausführen einer SQL-Anweisung" zum Ausführen einer anderen Anweisung in derselben Transaktion; gibt die Anwendung jetzt zurück. oder auf "Schritt 5: Commit der Transaktion" einen commit oder Rollback der Transaktion fortgesetzt.
