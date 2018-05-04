---
title: Katalogfunktionen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], about catalog functions
- data dictionary [ODBC]
- catalog functions [ODBC]
- functions [ODBC], catalog functions
ms.assetid: 81ba9453-c085-47c0-b411-90ca6a5ee428
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 582b6d0912263d2eba76a7e357787c7c75ba0a75
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="catalog-functions"></a>Katalogfunktionen
Alle Datenbanken weisen eine Struktur, die beschreibt, wie Daten in der Datenbank gespeichert werden. Z. B. möglicherweise eine einfachen Auftrag Datenbank die Struktur, die in der folgenden Abbildung, in der die ID-Spalten, zum Verknüpfen der Tabellen verwendet werden angezeigt.  
  
 ![Zeigt die Struktur einer einfachen Datenbank](../../../odbc/reference/develop-app/media/pr19.gif "pr19")  
  
 Dieser Struktur, die zusammen mit anderen Informationen wie Rechte, befindet sich in einem Satz von Systemtabellen der Datenbank aufgerufen *Katalog* ist auch bekannt als ein *Datenwörterbuch*.  
  
 Eine Anwendung kann diese Struktur über Aufrufe von Ermitteln der *Katalogfunktionen*. Die Katalogfunktionen geben Informationen in Resultsets und sind in der Regel implementiert, über **wählen** Anweisungen für die Tabellen im Katalog. Beispielsweise könnte eine Anwendung ein Resultset mit Informationen über alle Tabellen im System oder alle Spalten in einer bestimmten Tabelle anfordern.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Verwendung von Katalogdaten](../../../odbc/reference/develop-app/uses-of-catalog-data.md)  
  
-   [Katalogfunktionen in ODBC](../../../odbc/reference/develop-app/catalog-functions-in-odbc.md)
