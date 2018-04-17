---
title: Löschen von Zeilen durch Lesezeichen mit SQLBulkOperations | Microsoft Docs
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
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 017286f36c7747e02f1c120d56d38ae47a6e2008
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>Löschen von Zeilen durch Lesezeichen mit SQLBulkOperations
Beim Löschen einer Zeile von Lesezeichen, **SQLBulkOperations** macht die Datenquelle, die eine oder mehrere ausgewählte Zeilen der Tabelle zu löschen. Die Zeilen werden durch das Lesezeichen in einer Lesezeichenspalte gebundenen identifiziert.  
  
 So löschen Sie Zeilen durch Lesezeichen mit **SQLBulkOperations**, die Anwendung bewirkt Folgendes:  
  
1.  Ruft ab und speichert die Textmarken aller Zeilen gelöscht werden soll. Wenn mehrere Lesezeichen vorhanden ist, und spaltenbezogene Bindungen verwendet wird, werden die Lesezeichen in einem Array gespeichert. Wenn mehrere Lesezeichen vorhanden ist, und die zeilenweise Bindung verwendet wird, werden Lesezeichen in einem Array von Zeilenstrukturen gespeichert.  
  
2.  Legt das SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut auf die Anzahl von Lesezeichen und bindet den Puffer mit der Lesezeichenwert, oder das Array von Lesezeichen, um die Spalte 0.  
  
3.  Aufrufe **SQLBulkOperations** mit *Vorgang* SQL_DELETE_BY_BOOKMARK festgelegt.
