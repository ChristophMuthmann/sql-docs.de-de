---
title: Genauigkeit für Datentyp Interval | Microsoft Docs
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
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- precision [ODBC]
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: eb73bd77-2e7e-4498-a266-4d7c990a0d56
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 73acf5a46768b11b0eb223327c1fa1bcf0e49f68
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="interval-data-type-precision"></a>Datentypgenauigkeit Intervall
Genauigkeit für ein Intervall-Datentyp schließt für anführenden Intervallwert, Genauigkeit, die Intervall-Genauigkeit und die Sekunden mit einfacher Genauigkeit.  
  
 Der führende Feld ein Intervall ist ein mit Vorzeichen versehene Zahl. Die maximale Anzahl von Ziffern für das führende Feld richtet sich nach einer Menge aufgerufen *für anführenden Intervallwert, Genauigkeit,* also ein Teil der Daten-Typdeklaration. Beispiel: die Deklaration: Intervall HOUR(5) auf MINUTE hat eine Genauigkeit für anführenden Intervallwert 5; dem Stundenfeld dauert die Werte von –99999 und 99999 angegeben. Die Genauigkeit für anführenden Intervallwert, die im Feld SQL_DESC_DATETIME_INTERVAL_PRECISION Deskriptordatensatz enthalten ist.  
  
 Die Liste der Felder, die Daten Intervalltyp aus besteht heißt *Intervall Genauigkeit*. Es ist keinen numerischen Wert wie der Begriff "Precision" impliziert. Beispielsweise ist die Intervall-Genauigkeit des Datentyps INTERVAL DAY TO ZWEITENS die Liste Tag, Stunde, MINUTE, Sekunde. Es gibt keine Deskriptorfeld, die diesen Wert enthält. die Genauigkeit Intervall kann immer durch den Intervalltyp der Daten ermittelt werden.  
  
 Alle Intervall-Datentyp, ein zweites Feld verfügt, hat eine *Genauigkeit in Millisekunden*. Dies ist die Anzahl der Dezimalstellen in den Bruchteil der Sekundenwert zulässig. Dies unterscheidet sich für andere Datentypen gibt an, in dem die Anzahl der Ziffern vor dem Dezimaltrennzeichen mit einfacher Genauigkeit. Die Sekunden Genauigkeit eines Datentyps Intervall ist die Anzahl der Ziffern nach dem Dezimaltrennzeichen an. Z. B. wenn die Sekunden Genauigkeit auf 6 festgelegt ist, würde die Zahl in das bruchteilfeld 123456 interpretiert werden als.123456 und die Anzahl 1230 als.001230 interpretiert werden würde. Für andere Datentypen wird dies als Skalierung bezeichnet. Intervall Sekunden Genauigkeit ist in der SQL_DESC_PRECISION-Feld des Deskriptors enthalten. Wenn die Genauigkeit der Sekundenbruchteil-Komponente des SQL-Intervallwert größer ist, was die C-Intervall-Struktur aufnehmen kann, ist er treiberdefinierten, ob die Sekundenbruchteile-Wert in der SQL-Intervall gerundet oder gekürzt, wenn für den C-konvertiert Intervall-Struktur.  
  
 Das Feld SQL_DESC_CONCISE_TYPE in einen Datentyp Intervall festgelegt ist, wird das SQL_DESC_TYPE-Feld als SQL_INTERVAL festgelegt und auf den Code für den Intervalltyp der Daten die SQL_DESC_DATETIME_INTERVAL_CODE festgelegt ist. Feld SQL_DESC_DATETIME_INTERVAL_PRECISION automatisch auf die führenden Intervall standardgenauigkeit von 2 festgelegt ist, und das SQL_DESC_PRECISION-Feld wird automatisch auf die Genauigkeit für die Sekunden von Intervall von 6 festgelegt. Wenn beide Werte ist nicht geeignet, sollte die Anwendung explizit das Deskriptorfeld durch einen Aufruf von festgelegt **SQLSetDescField**.
