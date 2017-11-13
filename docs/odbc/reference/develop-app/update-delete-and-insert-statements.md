---
title: Update-, DELETE- und INSERT-Anweisungen | Microsoft Docs
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
- updating data [ODBC], about updating data
- DELETE [ODBC]
- UPDATE [ODBC]
- INSERT [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 5004ea72-4c49-4064-9752-f7032ba7f133
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b150288c113b1aebf92abedbd6f7eabd0b4b7d24
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="update-delete-and-insert-statements"></a>Update-, DELETE- und INSERT-Anweisungen
SQL-basierte Anwendungen und nehmen Sie Änderungen an Tabellen durch Ausführen der **UPDATE**, **löschen**, und **einfügen** Anweisungen. Diese Anweisungen sind Teil der Konformitätsgrad des minimale SQL-Grammatik und von allen Treibern und Datenquellen unterstützt werden müssen.  
  
 Die Syntax dieser Anweisungen lautet:  
  
 **UPDATE***Tabellenname*   
  
 **Legen Sie** *Spaltenbezeichner*  **=**  {*Ausdruck* &#124; **NULL**}  
  
 [**,** *Spaltenbezeichner*  **=**  {*Ausdruck* &#124; **NULL**}]...  
  
 [**, In denen** *Suchbedingung*]  
  
 **DELETE FROM** *Tabellenname*[**, in denen** *Suchbedingung*]  
  
 **INSERT INTO** *Tabellenname*[**(***Spaltenbezeichner* [**,** *Spaltenbezeichner-*] ... **)**]  
  
 {*-Abfragespezifikation* &#124; **Werte (***Wert einfügen* [**,** *Wert einfügen*]... **)**}  
  
 Beachten Sie, dass die *-Abfragespezifikation* Element gilt nur in der Kern- und erweiterte SQL-Grammatiken, und dass die *Ausdruck* und *Suchbedingung* Elemente steigern. im Kern- und erweiterte SQL-Grammatiken komplexer.  
  
 Andere SQL-Anweisungen, wie **UPDATE**, **löschen**, und **einfügen** Anweisungen sind, häufig teurer effizient, wenn sie Parameter verwenden. Beispielsweise kann die folgende Anweisung vorbereitet und wiederholt ausgeführt werden, um mehrere Zeilen in der Tabelle Orders einzufügen:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Diese Effizienz kann durch Übergeben von Arrays von Parameterwerten erhöht werden. Weitere Informationen zu Anweisungsparametern und Arrays von Parameterwerten finden Sie unter [Anweisungsparametern](../../../odbc/reference/develop-app/statement-parameters.md).

