---
title: DDL-Anweisungen | Microsoft Docs
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
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], DDL statements
- DDL statements [ODBC]
ms.assetid: 96ac9859-5976-4b06-ae1f-2fec3231e266
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61605252563150f4bb957eda14a95c5745650656
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="ddl-statements"></a>DDL-Anweisungen
Anweisungen von Data Definition Language (DDL) unterschiedlich enormen DBMS. ODBC-SQL definiert-Anweisungen für die am häufigsten verwendeten Definition Datenoperationen: Erstellen und Löschen von Tabellen, Indizes und Ansichten; Ändern von Tabellen; erteilen und Widerrufen von Berechtigungen. Alle anderen DDL-Anweisungen sind Daten datenquellenspezifischen. Daher können interoperable Anwendungen ausführen können nicht einige DDL-Vorgänge ausführen. Im Allgemeinen, dies ist kein Problem, da solche Vorgänge sind tendenziell hoch DBMS-spezifische und sich am besten eignen Links der proprietäre Software für die Verwaltung mit den meisten DBMS geliefert, oder das Setup-Programm mit dem Treiber geliefert.  
  
 Ein weiteres Problem in Datendefinition ist dieses Datentyps enormen zwischen DBMS variieren. Statt standard Datentypnamen definieren und erzwingen Treiber in DBMS-spezifische Namen umwandeln, **SQLGetTypeInfo** bietet eine Möglichkeit für Anwendungen, um den Typnamen für DBMS-spezifische Daten zu ermitteln. Interoperable Anwendungen ausführen können sollten diese Namen in SQL-Anweisungen verwenden, erstellen und Ändern von Tabellen. die Namen in [Anhang C: SQL-Grammatik](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), und [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md), sind lediglich Beispiele.
