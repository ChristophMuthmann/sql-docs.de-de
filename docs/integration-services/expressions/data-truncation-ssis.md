---
title: Abschneiden von Daten (SSIS) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- truncating data
- data truncation [Integration Services]
- expressions [Integration Services], data truncation
- truncate options [Integration Services]
ms.assetid: 02461e15-49ca-445b-abb3-5c369c283ec2
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0656e7f2d56caa0fcbffe24a42a2affe00089dc2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="data-truncation-ssis"></a>Abschneiden von Daten (SSIS)
  Bei der Konvertierung von Werten in andere Datentypen kann es passieren, dass Werte abgeschnitten werden.  
  
 Abschneiden kann auftreten beim:  
  
-   Übersetzen von Daten einer *DT_WSTR* -Zeichenfolge in eine *DT_STR* -Zeichenfolge mit der gleichen Länge, wenn die ursprüngliche Zeichenfolge Doppelbytezeichen enthält.  
  
-   Umwandeln einer ganzen Zahl aus einem *DT_I4* - in einen *DT_I2* -Wert. Dabei können signifikante Ziffern verloren gehen.  
  
-   Umwandeln einer ganzen Zahl ohne Vorzeichen in eine ganze Zahl mit Vorzeichen; dabei können signifikante Ziffern verloren gehen.  
  
-   Umwandeln einer reellen Zahl aus einem *DT_R8* - in einen *DT_R4* -Wert. Dabei können nicht signifikante Ziffern verloren gehen.  
  
-   Umwandeln einer ganzen Zahl aus einem *DT_I4* - in einen *DT_R4* -Wert. Dabei können nicht signifikante Ziffern verloren gehen.  
  
 Die Ausdrucksauswertung identifiziert explizite Umwandlungen, durch die Daten abgeschnitten werden könnten und gibt eine Warnung aus, wenn der Ausdruck analysiert wird. Beispielsweise werden Sie von der Ausdrucksauswertung gewarnt, falls eine Zeichenfolge mit 30 Zeichen in eine Zeichenfolge mit 20 Zeichen umgewandelt wird.  
  
 Ob Daten abgeschnitten werden, wird jedoch zur Laufzeit nicht überprüft. Sie erhalten in diesem Fall also zur Laufzeit keine Warnung. Die meisten Datenadapter und Transformationen unterstützen Fehlerausgaben, die mit der Disposition von Fehlerzeilen umgehen können.  
  
 Weitere Informationen zum Behandeln des Abschneidens von Daten finden Sie unter [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md)  
  
  
