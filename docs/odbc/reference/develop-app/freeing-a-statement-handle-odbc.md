---
title: Freigeben eines Anweisungshandles ODBC | Microsoft Docs
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
- statement handles [ODBC]
- handles [ODBC], statement
- freeing statement handles [ODBC]
ms.assetid: ee18e2f1-2690-4cc1-9e5c-e20244e5d480
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c0b56bfd04724c8506b5ba0fe7b5fd01a57a02e7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="freeing-a-statement-handle-odbc"></a>Freigeben eines Anweisungshandles ODBC
Wie bereits erwähnt, ist es effizienter, wiederverwenden Anweisungen als zum Löschen und neu zuzuordnen. Vor der Ausführung einer neuen SQL­Anweisung für eine Anweisung, sollten Anwendungen sicher sein, dass die aktuellen anweisungseinstellungen korrekt sind. Dazu zählen beispielsweise Anweisungsattribute, Parameterbindungen und Resultsetbindungen. Im allgemeinen Parametern und Resultsets für die alte SQL-Anweisung müssen entfernt werden soll (durch Aufrufen von **SQLFreeStmt** mit den Optionen SQL_RESET_PARAMS und SQL_UNBIND) und das Spoolobjekt für die neue SQL-Anweisung.  
  
 Wenn die Anwendung mit der Anweisung abgeschlossen ist, ruft er **SQLFreeHandle** um die Anweisung freizugeben. Nach der Freigabe der Anweisung, ist es ein anwendungsprogrammierungsfehler Fehler, die Anweisung Handle zu einem Aufruf von einer ODBC-Funktion zu verwenden. Dies hat sich nicht definierte, aber wahrscheinlich schwerwiegende Folgen.  
  
 Wenn **SQLFreeHandle** aufgerufen wird, wird der Treiberversionen, die die Struktur zum Speichern von Informationen über die Anweisung verwendet.  
  
 **SQLDisconnect** alle Anweisungen für eine Verbindung automatisch freigibt.
