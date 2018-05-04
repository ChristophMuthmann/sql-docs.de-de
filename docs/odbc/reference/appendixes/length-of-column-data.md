---
title: Länge der Spaltendaten | Microsoft Docs
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
- column data [ODBC]
- length of column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: c762c881-ebe0-4eac-84d5-f30281fc3eca
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e53cd64eaa0afb2ba042190b0649721c65979de7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="length-of-column-data"></a>Länge der Spaltendaten
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Die Cursorbibliothek erstellt einen Puffer in den Cache für jede an das Resultset mit gebundenen Längen-/Indikatorpuffers **SQLBindCol**. Er verwendet die Werte in diesen Puffern zum Erstellen einer **, in dem** -Klausel, wenn er emuliert positioniertes Update oder delete-Anweisungen. Diese Puffer aus dem Rowset Puffern aktualisiert, wenn er ruft Daten aus der Datenquelle und wann es positionierte Update-Anweisungen ausgeführt wird.  
  
 Wenn der C-Typ, der einen Datenpuffer SQL_C_CHAR oder sql_c_binary angegeben ist und der Längenindikator /-Wert SQL_NTS ist, wird die Länge der Zeichenfolge der Daten in die Längen-/Indikatorpuffers versetzt.  
  
> [!NOTE]  
>  Die Cursorbibliothek nicht seinem Cache nach einer Spalte aktualisiert, wenn **StrLen_or_IndPtr* im entsprechenden Rowset Puffer SQL_DATA_AT_EXEC oder das Ergebnis des Makros SQL_LEN_DATA_AT_EXEC ist.
