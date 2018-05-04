---
title: Anweisungshandles | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f844a4a783ccdbb2281857e440ce09d965a0c738
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="statement-handles"></a>Anweisungshandles
Ein *Anweisung* ist am einfachsten als betrachtet eine SQL-Anweisung, wie z. B. **wählen \* aus Mitarbeiter**. Eine Anweisung ist jedoch mehr als nur eine SQL-Anweisung: er besteht aus der alle Informationen, die SQL-Anweisung, wie z. B. alle Resultsets, die von der Anweisung erstellt und in der Ausführung der Anweisung verwendeten Parametern zugeordnet. Eine Anweisung muss auch nicht zu eine Anwendung definierte SQL-Anweisung verfügen. Z. B. wenn ein Katalog-Funktion wie **SQLTables** wird ausgeführt für eine Anweisung, die es führt einer vordefinierte SQL-Anweisung, die eine Liste der Tabellennamen zurückgibt.  
  
 Jede Anweisung wird durch ein Anweisungshandle identifiziert. Eine Anweisung bezieht sich auf eine einzelne Verbindung, und kann mehrere Anweisungen für diese Verbindung. Einige Treiber zu begrenzen die Anzahl der aktiven Anweisungen, die sie unterstützen; die SQL_MAX_CONCURRENT_ACTIVITIES option **SQLGetInfo** gibt an, wie viele aktive Anweisungen, die ein Treiber über eine einzelne Verbindung unterstützt. Eine Anweisung definiert *active* Wenn ausstehende Ergebnisse bestehen, Ergebnisse gegangenem ein Resultset oder die Anzahl der betroffenen Zeilen ein **einfügen**, **UPDATE**, oder **Löschen** -Anweisung oder die Daten mit mehreren Aufrufen an gesendet wird **SQLPutData**.  
  
 Innerhalb eines Codeabschnitts, die ODBC (der Treiber-Manager oder eines Treibers) implementiert, identifiziert das Anweisungshandle eine Struktur, die Anweisungsinformationen, z. B. enthält:  
  
-   Die Anweisung Zustand  
  
-   Die aktuelle auf Anweisungsebene-Diagnose  
  
-   Die Adressen von der Anwendungsvariablen an die Anweisung Parameter gebunden und Resultsetspalten  
  
-   Die aktuellen Einstellungen der einzelnen Anweisungsattribut  
  
 Anweisungshandles werden in den meisten ODBC-Funktionen verwendet. Sie werden vor allem, in der Funktionen verwendet, Parameter gebunden und Resultsetspalten (**SQLBindParameter** und **SQLBindCol**), Vorbereiten und Ausführen von Anweisungen (**SQLPrepare** **SQLExecute**, und **SQLExecDirect**), Abrufen von Metadaten (**SQLColAttribute** und **SQLDescribeCol**), Abrufen von Daten Ergebnisse (**SQLFetch**), und rufen Sie die Diagnose (**SQLGetDiagField** und **SQLGetDiagRec**). Sie werden auch in Katalogfunktionen verwendet (**SQLColumns**, **SQLTables**usw.) und eine Reihe weiterer Funktionen.  
  
 Anweisungshandles zugeordnet **SQLAllocHandle** und mit freigegebenen **SQLFreeHandle**.
