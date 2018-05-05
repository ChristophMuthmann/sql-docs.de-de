---
title: Verwendungen von Katalogdaten | Microsoft Docs
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
- catalog data [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], using catalog data
ms.assetid: d5915d0c-eec3-4382-850e-bd863763c99a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4d510a0f7e0d0c401e0f8ea8a8c346a917f05c3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="uses-of-catalog-data"></a>Der Katalogdaten verwendet
Anwendungen verwenden die Katalogdaten in einer Vielzahl von Möglichkeiten. Es folgen einige häufige Verwendungsmöglichkeiten:  
  
-   **Erstellen von SQL-Anweisungen zur Laufzeit.** Vertikale Anwendungen, z. B. eine Anwendung enthalten hartcodierten SQL-Anweisungen. Die Tabellen und Spalten, die von der Anwendung verwendet werden, sind voraus, fest, ebenso wie die Anweisungen, die Zugriff auf diese Tabellen. Eine Anwendung enthält beispielsweise in der Regel einen einzelnen parametrisierten **einfügen** -Anweisung für das System neue Bestellungen hinzugefügt.  
  
     Allgemeine Anwendungen, z. B. einem Tabellenkalkulationsprogramm, die Verwendung von ODBC zum Abrufen von Daten, erstellen häufig SQL-Anweisungen zur Laufzeit basierend auf Benutzereingaben. Eine solche Anwendung konnte erfordern, dass der Benutzer zur Eingabe der Namen der Tabellen und Spalten verwendet. Es wäre jedoch einfacher, für den Benutzer, wenn die Anwendung angezeigt, die Listen von Tabellen und Spalten aus denen der Benutzer die Auswahl vornehmen kann. Um diese Listen zu erstellen, würde die Anwendung Aufrufen der **SQLTables** und **SQLColumns** Katalogfunktionen.  
  
-   **Erstellen von SQL-Anweisungen während der Entwicklung.** Entwicklungsumgebungen Anwendung können in der Regel der Programmierer Datenbankabfragen beim Entwickeln einer Anwendung zu erstellen. Die Abfragen werden dann im zu erstellenden Anwendung hartcodiert.  
  
     Solche Umgebungen können auch **SQLTables** und **SQLColumns** Listen erstellen über die konnte der Programmierer Auswahl ändern. Diese Umgebungen können auch **SQLPrimaryKeys** und **SQLForeignKeys** automatisch ermitteln und Anzeigen von Beziehungen zwischen ausgewählten Tabellen und verwenden **SQLStatistics** zu bestimmen und indizierte Felder markieren, sodass Programmierer effizientere Abfragen erstellen kann.  
  
-   **Cursor zu konstruieren.** Eine Anwendung, die Treiber oder die Middleware, die einen bildlauffähigen Cursor-Modul bietet können **SQLSpecialColumns** um zu bestimmen, welche Spalte oder Spalten eine Zeile eindeutig identifiziert. Das Programm erstellen konnte eine *Keyset* , die die Werte dieser Spalten für jede Zeile, die abgerufen wurde. Wenn die Anwendung wieder in die Zeile ein Bildlauf durchgeführt, würden sie diese Werte dann verwenden, zum Abrufen der neuesten Daten für die Zeile. Weitere Informationen zu bildlauffähige Cursor und Keysets, finden Sie unter [bildlauffähige Cursor](../../../odbc/reference/develop-app/scrollable-cursors.md).
