---
title: Value-Argumenten Muster | Microsoft Docs
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
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], pattern value
- pattern value arguments [ODBC]
ms.assetid: 1d3f0ea6-87af-4836-807f-955e7df2b5df
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4959b329f855028cedc99f7c43ef889754baecda
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="pattern-value-arguments"></a>Muster Value-Argumenten
Einige Argumente im Katalog-Funktionen, wie die *TableName* Argument in **SQLTables**, Suchmustern akzeptieren. Diese Argumente akzeptieren Suchmustern Wenn SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_FALSE; festgelegt ist Sie sind Bezeichner Argumente, die einem Suchmuster nicht akzeptieren, wenn dieses Attribut auf SQL_TRUE festgelegt ist.  
  
 Die Suchzeichenfolge für die Muster sind:  
  
-   Ein Unterstrich (_), der einem beliebigen einzelnes Zeichen darstellt.  
  
-   Ein Prozentzeichen (%), die eine beliebige Sequenz von NULL oder mehr Zeichen darstellt.  
  
-   Ein Escape-Zeichen, die treiberspezifische und wird verwendet, um die Unterstriche enthalten Prozent anmeldet, und das Escape-Zeichen als Literale. Wenn das Escape-Zeichen ein nicht spezieller vorausgeht, besitzt das Escape-Zeichen keine besondere Bedeutung. Wenn das Escape-Zeichen ein Sonderzeichen voransteht, versieht er Sonderzeichen enthalten. Z. B. "\a" als zwei Zeichen behandelt werden würde "\\" und "a", aber "\\%" als einzelnes Zeichen "%" nicht spezieller behandelt werden würde.  
  
 Das Escapezeichen wird abgerufen, mit der Option SQL_SEARCH_PATTERN_ESCAPE **SQLGetInfo**. Es muss alle Unterstrich, Prozentzeichen oder Escape-Zeichen in einem Argument, das Suchmuster, sodass dieses Zeichen als Literal enthalten akzeptiert voranstellen. Beispiele sind in der folgenden Tabelle gezeigt.  
  
|Suchmuster|Description|  
|--------------------|-----------------|  
|EIN % %|Alle Bezeichner, die mit dem Buchstaben A|  
|ABC_|Alle vier Zeichen Bezeichner ABC ab|  
|ABC\\_|Der Bezeichner ABC_, vorausgesetzt das Escape-Zeichen ist ein umgekehrter Schrägstrich (\\)|  
|\\\\%|Alle Bezeichner ab, die mit einem umgekehrten Schrägstrich (\\), vorausgesetzt das Escape-Zeichen ist ein umgekehrter Schrägstrich|  
  
 Spezielle muss darauf geachtet werden als Escapesequenz für Muster der Suchzeichenfolge in-Argumente, die Suchmustern akzeptieren. Dies gilt insbesondere für das Unterstrich-Zeichen, der häufig in Bezeichnern verwendet wird. Ein häufiger Fehler in Anwendungen ist zum Abrufen eines Werts aus einem Katalogfunktion und den Wert an eine Suche Pattern-Argument in einen anderen Katalogfunktion übergeben. Nehmen wir beispielsweise an eine Anwendung ruft den Namen der Tabelle, aus dem Ergebnis MY_TABLE legen Sie für **SQLTables** und übergibt Sie diese Option, um **SQLColumns** zum Abrufen einer Liste der Spalten im MY_TABLE. Anstatt die Spalten für MY_TABLE abrufen, erhalten die Anwendung die Spalten für alle Tabellen, die dem Suchmuster MY_TABLE, z. B. MY_TABLE, MY1TABLE MY2TABLE und So weiter entsprechen.  
  
> [!NOTE]  
>  ODBC-2. *x* Treiber unterstützen keine Suchmuster in der *CatalogName* Argument in **SQLTables**. ODBC 3.*.x* Treiber akzeptiert Suchmustern in diesem Argument aus, wenn die SQL_ATTR_ ODBC_VERSION Umgebung-Attribut auf SQL_OV_ODBC3 festgelegt ist; sie akzeptieren keine Suchmustern in diesem Argument, wenn er auf SQL_OV_ODBC2 festgelegt ist.  
  
 Einen null-Zeiger an eine Suche Pattern-Argument übergeben schränkt die Suche für dieses Argument nicht; d. h. sind ein null-Zeiger und die Suche Muster% (Zeichen) Äquivalent. Jedoch eine leere Muster suchen – d. h. ein gültiger Zeiger auf eine Zeichenfolge der Länge 0 (null) – entspricht, nur die leere Zeichenfolge ("").
