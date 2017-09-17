---
title: Wie Metadaten verwendet wird? | Microsoft-Dokumentation
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
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4723b48732065ccc2f307d9eeef46f8b35574c2d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="how-is-metadata-used"></a>Wie Metadaten verwendet wird?
Anwendungen erfordern Metadaten für die meisten Resultsetvorgänge. Die Anwendung verwendet z. B. den Datentyp einer Spalte, um zu bestimmen, welche Art von Variable an diese Spalte gebunden werden soll. Er verwendet die Bytelänge einer Zeichenspalte, um zu bestimmen, wie viel Speicherplatz, Daten aus dieser Spalte angezeigt werden muss. Wie eine Anwendung die Metadaten für eine Spalte bestimmt, hängt vom Typ der Anwendung ab.  
  
 Vertikale Anwendungen funktionieren mit vordefinierten Tabellen und führen vordefinierte Vorgänge für diese Tabellen. Da die resultsetmetadaten für solche Anwendungen definiert ist, bevor die Anwendung überhaupt geschrieben und wird durch den Entwickler der Anwendung gesteuert wird, kann es der Anwendung fest programmiert sein. Wenn beispielsweise eine OrderID-Spalte in der Datenquelle als 4-Byte-Ganzzahl definiert ist, kann die Anwendung stets eine 4-Byte-Ganzzahl an diese Spalte binden. Wenn Metadaten in der Anwendung hartcodiert sind, bedeutet eine Änderung an den von der Anwendung verwendeten Tabelle im Allgemeinen eine Änderung am Anwendungscode. Dies ist ein Problem selten auf, da solche Änderungen in der Regel als Teil einer neuen Version der Anwendung vorgenommen werden.  
  
 Wie vertikale Anwendungen benutzerdefinierte Anwendungen in der Regel mit vordefinierten Datentabellen arbeiten und führen vordefinierte Vorgänge für diese Tabellen. Beispielsweise könnte eine Anwendung geschrieben werden, zum Übertragen von Daten zwischen drei verschiedenen Datenquellen; die übertragenen Daten ist i. d. r. bezeichnet, wenn die Anwendung geschrieben wird. Daher sind tendenziell benutzerdefinierte Anwendungen auch hartcodierte Metadaten aufweisen.  
  
 Allgemeiner Anwendungen, insbesondere solche, die ad-hoc-Abfragen unterstützen, fast nie kennen, die Metadaten des Resultsets, die sie erstellen. Aus diesem Grund müssen sie die Metadaten zur Laufzeit mithilfe der Funktionen ermitteln **SQLNumResultCols**, **SQLDescribeCol**, und **SQLColAttribute**, die in beschriebenen der im nächsten Abschnitt [SQLDescribeCol und SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md).  
  
 Alle Anwendungen, unabhängig von ihrem Typ können hartcodieren Metadaten für die durch die Katalogfunktionen zurückgegebenen Resultsets. Diese Resultsets werden im Abschnitt "Referenz" dieses Handbuchs definiert.
