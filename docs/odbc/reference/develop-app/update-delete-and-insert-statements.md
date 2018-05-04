---
title: Update-, DELETE- und INSERT-Anweisungen | Microsoft Docs
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
- updating data [ODBC], about updating data
- DELETE [ODBC]
- UPDATE [ODBC]
- INSERT [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 5004ea72-4c49-4064-9752-f7032ba7f133
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59e98d80962a059f885bd82ed8be465415a55774
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="update-delete-and-insert-statements"></a>Update-, DELETE- und INSERT-Anweisungen
SQL-basierte Anwendungen und nehmen Sie Änderungen an Tabellen durch Ausführen der **UPDATE**, **löschen**, und **einfügen** Anweisungen. Diese Anweisungen sind Teil der Konformitätsgrad des minimale SQL-Grammatik und von allen Treibern und Datenquellen unterstützt werden müssen.  
  
 Die Syntax dieser Anweisungen lautet:  
  
 **UPDATE***Tabellenname*  
  
 **Legen Sie** *Spaltenbezeichner* **=** {*Ausdruck* &#124; **NULL**}  
  
 [**,** *Spaltenbezeichner* **=** {*Ausdruck* &#124; **NULL**}]...  
  
 [**, In denen** *Suchbedingung*]  
  
 **DELETE FROM** *Tabellenname*[**, in denen** *Suchbedingung*]  
  
 **INSERT INTO** *Tabellenname*[**(*** Spaltenbezeichner* [**,** *Spaltenbezeichner*]... **)**]  
  
 {*-Abfragespezifikation* &#124;  **Werte (*** Wert einfügen* [**,** *Wert einfügen*]... **)**}  
  
 Beachten Sie, dass die *-Abfragespezifikation* Element gilt nur in der Kern- und erweiterte SQL-Grammatiken, und dass die *Ausdruck* und *Suchbedingung* Elemente steigern. im Kern- und erweiterte SQL-Grammatiken komplexer.  
  
 Andere SQL-Anweisungen, wie **UPDATE**, **löschen**, und **einfügen** Anweisungen sind, häufig teurer effizient, wenn sie Parameter verwenden. Beispielsweise kann die folgende Anweisung vorbereitet und wiederholt ausgeführt werden, um mehrere Zeilen in der Tabelle Orders einzufügen:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Diese Effizienz kann durch Übergeben von Arrays von Parameterwerten erhöht werden. Weitere Informationen zu Anweisungsparametern und Arrays von Parameterwerten finden Sie unter [Anweisungsparametern](../../../odbc/reference/develop-app/statement-parameters.md).
