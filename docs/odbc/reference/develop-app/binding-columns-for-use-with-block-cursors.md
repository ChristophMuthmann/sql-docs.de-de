---
title: "Binden von Spalten für die Verwendung mit Blockcursor | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- column-wise binding [ODBC]
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- cursors [ODBC], block
- binding columns [ODBC]
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 231beede-cdfa-4e28-8b10-2760b983250f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c527c2e89ab9acd0218a1b7f88112a81d537b780
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="binding-columns-for-use-with-block-cursors"></a>Binden von Spalten für die Verwendung mit Blockcursor
Da Blockcursor mehrere Zeilen zurückgeben, müssen Anwendungen, die sie verwenden ein Array von Variablen für die einzelnen Spalten anstelle einer einzelnen Variable binden. Diese Arrays werden zusammenfassend als bezeichnet den *Rowset Puffer*. Im folgenden sind die zwei Formate Bindung:  
  
-   Binden Sie ein Array für jede Spalte ein. Hierbei spricht *spaltenbezogene Bindungen* da jede Data-Struktur (Array) Daten für eine einzelne Spalte enthält.  
  
-   Definieren Sie eine Struktur zum Speichern der Daten für eine ganze Zeile und ein Array dieser Strukturen binden. Hierbei spricht *zeilenbezogene Bindungen* da jede Datenstruktur, die Daten für eine einzelne Zeile enthält.  
  
 Wie bei der Anwendung einzelne Variablen Spalten gebunden, ruft **SQLBindCol** Arrays an Spalten gebunden. Der einzige Unterschied ist, dass die Adressen übergebene Array Adressen, nicht einzelne Variablen Adressen. Die Anwendung legt die SQL_BIND_BY_COLUMN-Anweisungsattribut, um anzugeben, ob das spaltenweise oder zeilenweise Binden verwendet wird. Angibt, ob das spaltenweise oder zeilenweise Binden verwendet, ist weitgehend Anwendung Voreinstellung. Zeilenweise Bindung entspricht möglicherweise genauer die Anwendung Layout der Daten, in diesem Fall würden sie eine bessere Leistung bieten.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Spaltenweises Binden](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [Zeilenweises Binden](../../../odbc/reference/develop-app/row-wise-binding.md)
