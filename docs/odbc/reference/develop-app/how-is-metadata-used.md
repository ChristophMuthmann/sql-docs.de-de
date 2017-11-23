---
title: Wie Metadaten verwendet wird? | Microsoft-Dokumentation
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
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6cb8bb35eb0e53415465b3ea003341d74e248bda
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="how-is-metadata-used"></a>Wie Metadaten verwendet wird?
Anwendungen erfordern Metadaten für die meisten Resultsetvorgänge. Die Anwendung verwendet z. B. den Datentyp einer Spalte, um zu bestimmen, welche Art von Variable an diese Spalte gebunden werden soll. Er verwendet die Bytelänge einer Zeichenspalte, um zu bestimmen, wie viel Speicherplatz, Daten aus dieser Spalte angezeigt werden muss. Wie eine Anwendung die Metadaten für eine Spalte bestimmt, hängt vom Typ der Anwendung ab.  
  
 Vertikale Anwendungen funktionieren mit vordefinierten Tabellen und führen vordefinierte Vorgänge für diese Tabellen. Da die resultsetmetadaten für solche Anwendungen definiert ist, bevor die Anwendung überhaupt geschrieben und wird durch den Entwickler der Anwendung gesteuert wird, kann es der Anwendung fest programmiert sein. Wenn beispielsweise eine OrderID-Spalte in der Datenquelle als 4-Byte-Ganzzahl definiert ist, kann die Anwendung stets eine 4-Byte-Ganzzahl an diese Spalte binden. Wenn Metadaten in der Anwendung hartcodiert sind, bedeutet eine Änderung an den von der Anwendung verwendeten Tabelle im Allgemeinen eine Änderung am Anwendungscode. Dies ist ein Problem selten auf, da solche Änderungen in der Regel als Teil einer neuen Version der Anwendung vorgenommen werden.  
  
 Wie vertikale Anwendungen benutzerdefinierte Anwendungen in der Regel mit vordefinierten Datentabellen arbeiten und führen vordefinierte Vorgänge für diese Tabellen. Beispielsweise könnte eine Anwendung geschrieben werden, zum Übertragen von Daten zwischen drei verschiedenen Datenquellen; die übertragenen Daten ist i. d. r. bezeichnet, wenn die Anwendung geschrieben wird. Daher sind tendenziell benutzerdefinierte Anwendungen auch hartcodierte Metadaten aufweisen.  
  
 Allgemeiner Anwendungen, insbesondere solche, die ad-hoc-Abfragen unterstützen, fast nie kennen, die Metadaten des Resultsets, die sie erstellen. Aus diesem Grund müssen sie die Metadaten zur Laufzeit mithilfe der Funktionen ermitteln **SQLNumResultCols**, **SQLDescribeCol**, und **SQLColAttribute**, die in beschriebenen der im nächsten Abschnitt [SQLDescribeCol und SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md).  
  
 Alle Anwendungen, unabhängig von ihrem Typ können hartcodieren Metadaten für die durch die Katalogfunktionen zurückgegebenen Resultsets. Diese Resultsets werden im Abschnitt "Referenz" dieses Handbuchs definiert.
