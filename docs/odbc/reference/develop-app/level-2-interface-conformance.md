---
title: Ebene 2 Schnittstelle Konformität | Microsoft Docs
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
- interface conformance levels [ODBC]
- level 2 interface conformance levels [ODBC]
- conformance levels [ODBC], interface
ms.assetid: 2dc87840-f2fe-43dd-9d7b-bd95523081d9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a8696cfd70ea355dd8ade721b2bb660019506a7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="level-2-interface-conformance"></a>Ebene 2 Schnittstelle Konformität
Der Konformitätsgrad des Level 2-Schnittstelle enthält die Funktionen der Ebene 1 Benutzeroberfläche Konformitätsgrad – sowie die folgenden Features:  
  
|||  
|-|-|  
|201|Verwenden Sie dreiteilige Namen von Tabellen und Sichten. (Weitere Informationen finden Sie unter der zweiteiligen Benennungskonvention Unterstützungsfunktion 101 in [Ebene 1 Schnittstelle Konformität](../../../odbc/reference/develop-app/level-1-interface-conformance.md).)|  
|202|Beschreiben Sie dynamische Parameter – durch den Aufruf **SQLDescribeParam**.|  
|203|Verwenden Sie nicht nur Eingabeparameter jedoch auch Ausgabe und Eingabe/Ausgabe-Parameter, und die Ergebniswerte von gespeicherten Prozeduren.|  
|204|Verwenden von Lesezeichen, einschließlich Abrufen von Lesezeichen, durch den Aufruf **SQLDescribeCol** und **SQLColAttribute** für die Spalte die Zahl 0; Abrufen von Zeilen basierend auf einem Lesezeichen durch Aufrufen von **SQLFetchScroll** mit der *FetchOrientation* Argument festgelegt SQL_FETCH_BOOKMARK; zu aktualisieren, löschen und Abrufen von Lesezeichen-Vorgängen, durch den Aufruf **SQLBulkOperations** mit der *Vorgang* Argument SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK oder SQL_FETCH_BY_BOOKMARK festgelegt.|  
|205|Erweiterte Informationen über das Datenwörterbuch durch den Aufruf abgerufen **SQLColumnPrivileges**, **SQLForeignKeys**, und **SQLTablePrivileges**.|  
|206|Verwenden Sie ODBC-Funktionen anstelle von SQL-Anweisungen, um zusätzliche Datenbankvorgänge, durch den Aufruf ausführen **SQLBulkOperations** mit SQL_ADD, oder **SQLSetPos** mit SQL_DELETE oder SQL_UPDATE auf. (Unterstützung für Aufrufe von **SQLSetPos** mit der *LockType* Argument auf SQL_LOCK_EXCLUSIVE oder SQL_LOCK_UNLOCK festgelegt, ist nicht Teil der Übereinstimmungsebenen, jedoch ist ein optionales Feature.)|  
|207|Aktivieren Sie die asynchrone Ausführung der ODBC-Funktionen für angegebene einzelne Anweisungen.|  
|208|Abrufen der SQL_ROWVER Zeile identifizieren-Spalte mit Tabellen, durch Aufrufen **SQLSpecialColumns**. (Weitere Informationen finden Sie auf die Unterstützung für **SQLSpecialColumns** mit der *IdentifierType* Argument festgelegt wird, um SQL_BEST_ROWID als feature in 20 [Core Schnittstelle Konformität](../../../odbc/reference/develop-app/core-interface-conformance.md) .)|  
|209|Das SQL_ATTR_CONCURRENCY-Anweisungsattribut auf mindestens ein Wert als SQL_CONCUR_READ_ONLY festgelegt.|  
|210|Die Fähigkeit zum Timeout anmeldeanforderung und SQL-Abfragen (SQL_ATTR_LOGIN_TIMEOUT und SQL_ATTR_QUERY_TIMEOUT).|  
|211|Die Fähigkeit, die Standardisolationsstufe zu ändern; die Fähigkeit zum Ausführen von Transaktionen mit der "serializable" Maß an Isolation.|
