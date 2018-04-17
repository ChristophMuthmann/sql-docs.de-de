---
title: Ebene 1 Schnittstelle Konformität | Microsoft Docs
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
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- level 1 interface conformance levels [ODBC]
ms.assetid: ee3f5c08-0583-4f3b-8354-ef71b6086a7e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: faae1bf56dd28f83fa3fec5c340bcf67c302def3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="level-1-interface-conformance"></a>Ebene 1 Schnittstelle Konformität
Der Konformitätsgrad des Ebene-1-Schnittstelle enthält die Schnittstelle Konformität Ebene Kernfunktionalität sowie auf zusätzliche Funktionen, z. B. Transaktionen, die in der Regel in eine relationale OLTP-DBMS verfügbar sind. Ein Ebene-1-Schnittstelle – konforme-Treiber ermöglicht die Anwendung, zusätzlich zu den Funktionen in der zentrale Schnittstelle Konformitätsgrad gehen:  
  
|||  
|-|-|  
|101|Geben Sie das Schema der Datenbank Tabellen und Sichten (mit einem zweiteiligen Namen). (Weitere Informationen finden Sie unter der dreiteilige Namensgebung 201 in Funktion [Ebene 2 Schnittstelle Konformität](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|102|Rufen Sie "true" asynchrone Ausführung der ODBC-Funktionen, auf dem entsprechende ODBC-Funktionen synchrone oder alle asynchronen für eine gegebene Verbindung sind.|  
|103|Bildlauffähige Cursor verwenden und so die dadurch Zugriff auf ein Resultset in Methoden außer Vorwärtscursor, durch den Aufruf **SQLFetchScroll** mit der *FetchOrientation* Argument als SQL_FETCH_NEXT. (Die SQL_FETCH_BOOKMARK *FetchOrientation* ist im Feature 204 [Ebene 2 Schnittstelle Konformität](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|104|Abrufen von Primärschlüsseln von Tabellen, durch den Aufruf **SQLPrimaryKeys**.|  
|105|Verwenden von gespeicherten Prozeduren, durch die ODBC-Escapesequenz für Prozeduraufrufen und Abfragen von Datenwörterbuch zu gespeicherten Prozeduren, durch den Aufruf **SQLProcedureColumns** und **SQLProcedures**. (Der Prozess, mit dem Prozeduren erstellt und in der Datenquelle gespeichert werden, außerhalb des Bereichs dieses Dokuments ist.)|  
|106|Verbinden mit einer Datenquelle, indem Sie interaktiv Durchsuchen der verfügbaren Server durch den Aufruf **SQLBrowseConnect**.|  
|107|Verwenden Sie ODBC-Funktionen anstelle von SQL-Anweisungen, um bestimmte Datenbankvorgänge durchzuführen: **SQLSetPos** mit SQL_POSITION und SQL_REFRESH.|  
|108|Zugreifen auf den Inhalt der mehrere Resultsets, die durch Aufrufen von Batches und gespeicherte Prozeduren generiert **SQLMoreResults**.|  
|109|Begrenzen von Transaktionen, die Aufteilung auf verschiedene ODBC-Funktionen mit "true" Unteilbarkeit und die Möglichkeit zum Angeben der SQL_ROLLBACK in **SQLEndTran**.|
