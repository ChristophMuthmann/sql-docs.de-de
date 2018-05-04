---
title: Führen Sie die Metadaten | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 6d134515-e34d-4563-96d7-8ad7714818fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d41ebb87e7f30d0e7595310a972ea7dad2cf598
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="result-set-metadata"></a>Resultsetmetadaten
*Metadaten* sind Daten, die andere Daten beschreiben. Resultsetmetadaten beschreibt z. B. das Resultset, z. B. die Anzahl der Spalten im Resultset, die Datentypen der Spalten, deren Namen mit einfacher Genauigkeit, NULL-Zulässigkeit und usw. an.  
  
 Interoperable Anwendungen ausführen können, sollten immer die Metadaten der Spalten im Resultset überprüfen. Die Metadaten für eine Spalte in einem Resultset unterscheiden sich aus den Metadaten für die Spalte, wie Sie eine Katalogfunktion zurückgegeben. Nehmen wir beispielsweise an, dass eine aktualisierbare Spalte enthalten ist, in einem Resultset, die durch Verknüpfen von zwei Tabellen erstellt wurde. Während **SQLColumnPrivileges** kann darauf hinweisen, dass ein Benutzer kann die Spalte aktualisieren, die resultsetmetadaten möglicherweise nicht, wenn die Spalte auf der Seite "many" des Joins ist; vielen Datenquellen können auf der Seite "1" eines Joins, jedoch nicht auf Spalten aktualisieren, die " n-Seite. Sogar Datentypen können nicht angenommen, dass übereinstimmen, da die Datenquelle den Datentyp höher beim Erstellen des Resultsets ausgewählt Stufen kann.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Wie werden Metadaten verwendet?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol und SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
