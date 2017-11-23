---
title: Katalogposition | Microsoft Docs
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
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog position
- catalog position [ODBC]
ms.assetid: 5bc5f64b-c75a-43d2-8745-102ec7a49000
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d4b219fe2f008c6e7f0e289211665a1dcf6f1bd1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="catalog-position"></a>Katalogposition
Die Position des einen Katalognamen in einen Bezeichner und wie sie vom Rest des Bezeichners getrennt ist, aus der Datenquelle mit Datenquelle variiert. Z. B. in einer Datenquelle Xbase der Name des Katalogs ist ein Verzeichnis und, in Microsoft® Windows® wird getrennt von den Tabellennamen (also einen Dateinamen) durch einen umgekehrten Schrägstrich (\\). Die folgende Abbildung veranschaulicht diese Bedingung.  
  
 ![Katalogposition: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 Der Katalog in einer SQL Server-Datenquelle ist eine Datenbank und wird aus dem Schema und Tabellennamen durch einen Punkt (.) getrennt.  
  
 ![Katalogposition: SQLServer](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 In einer Oracle-Datenquelle der Katalog wird auch die Datenbank jedoch folgt der Tabellenname, und getrennt von dem Schema und Tabellennamen durch ein at-Zeichen (@).  
  
 ![Katalogposition: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 Ruft eine Anwendung zur Ermittlung der Katalogtrennzeichen und den Speicherort der Name des Katalogs, **SQLGetInfo** mit den Optionen SQL_CATALOG_NAME_SEPARATOR und SQL_CATALOG_LOCATION. Interoperable Anwendungen ausführen können, sollten Bezeichner entsprechend der folgenden Werte erstellen.  
  
 Zitieren von Bezeichnern, die über mehrere Teile enthalten, müssen Anwendungen darauf achten, dass jeder Teil separat Angebot und nicht das Zeichen, das die Bezeichner trennt, in Anführungszeichen werden. Die folgende Anweisung hinzu, wählen Sie alle Zeilen und Spalten einer Tabelle Xbase des Katalogs (\XBASE\SALES\CORP) und Tabellennamen (Parts.dbf), jedoch nicht dem Katalogtrennzeichen z. B. in Anführungszeichen (\\):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 Die folgende Anweisung alle Zeilen und Spalten von einer Oracle-Tabelle auswählen (Sales) Katalog, Schema (geschäftlich), und Tabellennamen (Teile), aber nicht den Katalog in Anführungszeichen (@) oder Schema (.) als Trennzeichen:  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 Informationen über Bezeichner finden Sie im nächsten Abschnitt [Bezeichner in Anführungszeichen](../../../odbc/reference/develop-app/quoted-identifiers.md).
