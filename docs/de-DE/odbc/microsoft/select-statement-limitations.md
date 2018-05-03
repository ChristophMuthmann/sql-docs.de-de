---
title: SELECT-Anweisung Einschränkungen | Microsoft Docs
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
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e27e435fea1aeb864eb20ac478a72860394b8f6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="select-statement-limitations"></a>Einschränkungen der SELECT-Anweisung
Eine Aggregatfunktion Spalte kann nicht mit einem nicht-Aggregatspalte in einer SELECT-Anweisung kombiniert werden.  
  
 Die Auswahlliste einer SELECT-Anweisung, die eine GROUP BY-Klausel verfügt, können nur Ausdrücke aus der GROUP BY-Klausel oder Funktionen festlegen.  
  
 Die Verwendung von ein Sternchen (Wählen Sie alle Spalten) in einer SELECT-Anweisung mit einer GROUP BY-Klausel wird nicht unterstützt. Die Namen der Spalten ausgewählt werden, müssen angegeben werden.  
  
 Die Verwendung eines vertikalen Balkens in einer SELECT-Anweisung wird nicht unterstützt. Verwenden Sie einen Parameter in der SELECT-Anweisung, wenn Sie müssen zum Verweisen auf einen Datenwert, der einen vertikalen Balken enthält.  
  
 Wenn Sie einen Spaltenalias in einer SELECT-Anweisung verwenden, muss das Wort "as" den Alias vorangestellt sein. Z. B. "SELECT col1 als einer von b." Ohne die "als" wird die Anweisung einen Fehler zurück.  
  
 Wenn ein falsche Spaltennamen in einer SELECT-Anweisung eingegeben wird, wird ein SQLSTATE 07001-Fehler "Falsche Anzahl von Parametern," zurückgegeben statt eines Fehlers SQLSTATE S0022 "Spalte nicht gefunden."  
  
 Wenn der Microsoft Excel-Treiber verwendet wird, wenn eine leere Zeichenfolge in eine Spalte eingefügt wird, wird die leere Zeichenfolge in NULL konvertiert. eine gesuchte SELECT-Anweisung, die mit einer leeren Zeichenfolge in die WHERE-Klausel für die betreffende Spalte nicht erfolgreich ausgeführt wird.
