---
title: Katalogfunktionen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- catalog functions [ODBC], about catalog functions
- data dictionary [ODBC]
- catalog functions [ODBC]
- functions [ODBC], catalog functions
ms.assetid: 81ba9453-c085-47c0-b411-90ca6a5ee428
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 497676e6b87b6603d4bc6cb1615bb1b133c7acd4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="catalog-functions"></a>Katalogfunktionen
Alle Datenbanken weisen eine Struktur, die beschreibt, wie Daten in der Datenbank gespeichert werden. Z. B. möglicherweise eine einfachen Auftrag Datenbank die Struktur, die in der folgenden Abbildung, in der die ID-Spalten, zum Verknüpfen der Tabellen verwendet werden angezeigt.  
  
 ![Zeigt die Struktur einer einfachen Datenbank](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 Dieser Struktur, die zusammen mit anderen Informationen wie Rechte, befindet sich in einem Satz von Systemtabellen der Datenbank aufgerufen *Katalog* ist auch bekannt als ein *Datenwörterbuch*.  
  
 Eine Anwendung kann diese Struktur über Aufrufe von Ermitteln der *Katalogfunktionen*. Die Katalogfunktionen geben Informationen in Resultsets und sind in der Regel implementiert, über **wählen** Anweisungen für die Tabellen im Katalog. Beispielsweise könnte eine Anwendung ein Resultset mit Informationen über alle Tabellen im System oder alle Spalten in einer bestimmten Tabelle anfordern.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Der Katalogdaten verwendet](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [In ODBC-Katalogfunktionen](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)

