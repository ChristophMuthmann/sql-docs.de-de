---
title: Daten und C-Zeichenfolgen Zeichen | Microsoft Docs
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
- data buffers [ODBC], length
- data buffers [ODBC], character data
- buffers [ODBC], C strings
- buffers [ODBC], character data
- character data and buffers [ODBC]
- length of data buffers [ODBC]
- data buffers [ODBC], C strings
- buffers [ODBC], length
- C strings and buffers [ODBC]
ms.assetid: 3a141cb4-229d-4027-9349-615cb2995e36
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d8bdba6134e53a7e3913c0255fe709a8a891eeae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="character-data-and-c-strings"></a>Zeichendaten und C-Zeichenfolgen
Eingabeparameter, die Zeichendaten mit variabler Länge (z. B. Spaltennamen, dynamische Parameter und zeichenfolgenattributwerten) verweisen, haben einen zugeordnete Length-Parameter. Wenn Sie Zeichenfolgen mit Null-Zeichen, wie in C, wird von die Anwendung beendet wird, stellt er entweder die Länge in Bytes der Zeichenfolge (nicht einschließlich der Null-Terminator) oder SQL_NTS (Null-Terminated String) als Argument bereit. Ein nicht negativer Längenargument gibt die tatsächliche Länge der Zeichenfolge zugeordnet. Der Length-Argument möglicherweise 0 an eine Zeichenfolge der Länge 0 (null), die von einer NULL-Wert unterscheidet. Der negative Wert SQL_NTS weist den Treiber auf die Länge der Zeichenfolge zu bestimmen, indem die Suche nach Null-Abschlusszeichen.  
  
 Wenn Zeichendaten vom Treiber an die Anwendung zurückgegeben werden, muss die Treiber immer Null-es beendet werden. Dies ermöglicht es der Anwendung die Wahl, ob die Daten als Zeichenfolge oder ein Array von Zeichen behandelt. Ist die Anwendungspuffer nicht groß genug für alle Zeichendaten zurück, der Treiber verkürzt sie auf den Bytelänge des Puffers abzüglich der Anzahl der Bytes, die Null-Abschlusszeichen erforderlich, Null-beendet die abgeschnittenen Daten und speichert ihn in der Puffer. Daher müssen Anwendungen immer zusätzlichen Speicherplatz für das Null-Terminierung Zeichen im Puffer zum Abrufen von Zeichendaten reservieren. Beispielsweise ist ein 51-Byte-Puffer zum Abrufen der Daten 50 Zeichen erforderlich.  
  
 Besondere Sorgfalt geboten von der Anwendung und der Treiber beim Senden und Abrufen von long Zeichendaten in Teilen mit **SQLPutData** oder **SQLGetData**. Wenn die Daten als eine Reihe von Null endende Zeichenfolgen übergeben werden, müssen die Null-Terminierung Zeichen an diesen Zeichenfolgen entfernt werden, bevor die Daten, die zusammengesetzt werden können.  
  
 Eine Anzahl von ODBC-Programmierer muss Zeichendaten und C-Zeichenfolgen verwechselt werden. Ist dies der Fall ein Artefakt mit der Programmiersprache C beim ODBC-Funktionen definieren. Wenn eine ODBC-Treiber oder die Anwendung eine andere Sprache verwendet – Beachten Sie, dass ODBC sprachunabhängige – diese Verwirrung ist weniger wahrscheinlich, dass Sie auftreten.  
  
 Wenn C-Zeichenfolgen zum Speichern von Zeichendaten verwendet werden, wird die Null-Abschlusszeichen wird nicht als Teil der Daten und nicht als Teil seiner Bytelänge. Beispielsweise kann die Zeichen Daten "ABC" als C-Zeichenfolge "ABC\0" oder das Array von Zeichen {"A", "B", "C"} gespeichert werden. Die Bytelänge der Daten ist 3, unabhängig davon, ob er als Zeichenfolge oder ein Array von Zeichen behandelt wird.  
  
 Obwohl Anwendungen und-Treiber häufig C-Zeichenfolgen (nullterminierte Arrays von Zeichen) verwenden, um Zeichendaten aufzunehmen, besteht keine zwingend vorgeschrieben. In C können Zeichendaten auch als ein Array von Zeichen (ohne Null-Terminierung) und die Bytelänge eingelesenen Längen-/Indikatorpuffers separat behandelt werden.  
  
 Da Zeichendaten in einen nicht-Null endendes Array aufnehmen können, und die Bytelänge separat übergeben, ist es möglich, die Null-Zeichen in Zeichendaten eingebettet werden sollen. Allerdings in diesem Fall ist das Verhalten der ODBC-Funktionen nicht definiert, und es treiberspezifische ist, gibt an, ob ein Treiber ordnungsgemäß verarbeitet. Daher sollte interoperable Anwendungen immer Zeichendaten verarbeiten, die eingebettete Null-Zeichen als binäre Daten enthalten kann.
