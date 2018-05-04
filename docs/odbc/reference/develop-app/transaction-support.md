---
title: Transaktionsunterstützung | Microsoft Docs
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
- transactions [ODBC], degree of support
ms.assetid: d56e1458-8da2-4d73-a777-09e045c30a33
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f3e62cd93f3823a2205ed2c2721ed95749f7a1a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="transaction-support"></a>Transaktionsunterstützung.
Der Grad an Unterstützung für Transaktionen wird Treiber definiert. ODBC soll für einen Einzelbenutzer oder desktop-Datenbank implementiert werden, die keine Notwendigkeit, mehrere Updates auf dessen Daten zu verwalten ist. Darüber hinaus sind einige Datenbanken, die Transaktionen unterstützen nur für die Anweisungen (Data Manipulation Language, DML) von SQL Server; Es sind Einschränkungen oder spezielle Transaktionssemantik im Hinblick auf die Verwendung der Windows-Verwaltungsinstrumentation (Data Definition Language, Datendefinitionssprache), wenn eine Transaktion aktiv ist. Möglicherweise gibt es also transaktionsunterstützung für mehrere gleichzeitige Aktualisierungen an Tabellen jedoch nicht für die Anzahl und die Definition von Tabellen während einer Transaktion ändern.  
  
 Eine Anwendung bestimmt, ob Transaktionen unterstützt werden, ob DDL kann, in einer Transaktion und alle Spezialeffekte aufgenommen werden der DDL in einer Transaktion, einschließlich der durch den Aufruf **SQLGetInfo** mit der Option SQL_TXN_CAPABLE. Weitere Informationen finden Sie unter der [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) funktionsbeschreibung.  
  
 Wenn der Treiber werden keine Transaktionen unterstützt, aber die Anwendung die Möglichkeit, die hat (unter Verwendung einer API als ODBC) zum Sperren und Entsperren von Daten, können Anwendungen transaktionsunterstützung durch Sperren und entsperren Datensätze und Tabellen nach Bedarf erreichen. Zum Implementieren der Konto-Transfer-Beispiel würde die Anwendung sperren die Einträge für beide Konten, kopieren Sie die aktuellen Werte soll das erste Konto, das zweite Konto Guthaben und entsperren Datensätze. Wenn alle Schritte fehlgeschlagen ist, würde die Anwendung die Konten, die mit der Kopien zurückgesetzt.  
  
 Auch Datenquellen, die Transaktionen unterstützen möglicherweise nicht mehr als eine Transaktion zu einem Zeitpunkt innerhalb einer bestimmten Umgebung zu unterstützen. -Anwendungen rufen **SQLGetInfo** mit der Option SQL_MULTIPLE_ACTIVE_TXN, um zu bestimmen, ob eine Datenquelle gleichzeitige aktive Transaktionen auf mehr als eine Verbindung in der gleichen Umgebung unterstützen kann. Da eine Transaktion pro Verbindung vorhanden ist, ist dies nur interessant, Anwendungen, die mehrere Verbindungen mit derselben Datenquelle haben.
