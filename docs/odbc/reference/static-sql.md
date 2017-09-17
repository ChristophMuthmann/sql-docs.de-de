---
title: Statische SQL | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- static SQL [ODBC]
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- SQL statements [ODBC], static SQL
- embedded SQL [ODBC]
- SQL [ODBC], static SQL
ms.assetid: 667d92ec-fed9-4028-81d4-bb9ba867356a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1675f70b67f5c600aada546f8caf8eb8b99df99a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="static-sql"></a>Statische SQL-Anweisungen
Embedded SQL in angezeigten [Embedded SQL-Beispiel](../../odbc/reference/embedded-sql-example.md) wird als statische SQL bezeichnet. Es ist statisches SQL aufgerufen wird, da die SQL-Anweisungen in der Anwendung statisch sind. d. h., sie nicht jedes Mal ändern, die das Programm ausgeführt wird. Wie im vorherigen Abschnitt beschrieben wird, werden diese Anweisungen kompiliert, wenn der Rest des Programms kompiliert wird.  
  
 Statische SQL funktioniert gut in vielen Situationen und kann in jeder Anwendung, die für die Datenzugriff kann, zur Entwurfszeit Programm bestimmt werden verwendet werden. Z. B. eine Order-Eintrag-Programm verwendet immer dieselbe Anweisung zum Einfügen einer neuen Bestellung und eine Airline-Reservierung-System verwendet immer dieselbe Anweisung so ändern Sie den Status von einem Arbeitsplatz von verfügbar in reserviert. Alle diese Anweisungen würde durch die Verwendung von Hostvariablen verallgemeinert werden; unterschiedliche Werte in einem Verkaufsauftrag eingefügt werden können, und anderen Arbeitsplätze reserviert werden können. Da solche Anweisungen in der Anwendung fest programmiert sein können, haben diese Programme den Vorteil, den die Anweisungen analysiert, überprüft und zum Zeitpunkt der Kompilierung nur einmal optimiert werden müssen. Dies führt dazu, dass Code relativ schnell.
