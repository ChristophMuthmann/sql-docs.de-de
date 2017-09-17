---
title: "INDEXERSTELLUNG für Paradox | Microsoft Docs"
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
- CREATE INDEX [ODBC]
- Paradox driver [ODBC], create index
ms.assetid: 6472bd69-b931-4bc2-a9bf-f1873ed4cdfe
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 058677892aa1a3266b1cd93a5ff015ed0a14bcb9
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="create-index-for-paradox"></a>INDEX für Paradox erstellen
Die Syntax der CREATE INDEX-Anweisung für den Paradox ODBC-Treiber lautet:  
  
 **Erstellen Sie** [**UNIQUE**] **INDEX** *Indexname*  
  
 **ON** *Tabellenname*  
  
 **(** *Spaltenbezeichner* [**ASC**]  
  
 [**,** *Spaltenbezeichner* [**ASC**]...] **)**  
  
 Paradox ODBC-Treiber unterstützt nicht die **"DESC"** Schlüsselwort in der ODBC-SQL-Grammatik für die CREATE INDEX-Anweisung. Die *Tabellenname* -Argument kann den vollständigen Pfad der Tabelle angeben.  
  
 Wenn das Schlüsselwort **UNIQUE** angegeben ist, erstellt der Paradox ODBC-Treiber einen eindeutigen Index. Der erste eindeutige Index wird als primären Index erstellt. Dies ist eine Paradox primären Schlüsseldatei mit dem Namen *Tabellenname*. PX. Primäre Indizes gelten die folgenden Einschränkungen:  
  
-   Der Primärindex muss erstellt werden, bevor die Tabelle keine Zeilen hinzugefügt werden.  
  
-   Nach der ersten "n" Spalten in einer Tabelle muss ein primärer Index definiert werden.  
  
-   Pro Tabelle ist nur eine primärer Index zulässig.  
  
-   Eine Tabelle kann nicht vom Treiber Paradox aktualisiert werden, wenn ein primärer Index nicht für die Tabelle definiert ist. (Beachten Sie, dass dies nicht "true" für eine leere Tabelle ist die aktualisiert werden können, selbst wenn ein eindeutiger Index für die Tabelle nicht definiert ist.)  
  
-   Die *Indexname* Argument für einen primären Index muss den Namen der Tabelle nach Bedarf Paradox identisch sein.  
  
 Wenn das Schlüsselwort **UNIQUE** wird weggelassen, wird der Paradox ODBC-Treiber einen nichteindeutiger Index erstellt. Dies umfasst zwei Paradox sekundären Indexdateien mit dem Namen *Tabellenname*. X* nn * und *Tabellenname*. Y*nn*, wobei * nn * ist die Nummer der Spalte in der Tabelle. Nicht eindeutige Indizes gelten die folgenden Einschränkungen:  
  
-   Ein nichteindeutiger Index für eine Tabelle erstellt werden kann, muss ein primärer Index für diese Tabelle vorhanden sein.  
  
-   Für Paradox 3. *x*, *Indexname* Argument für jeden Index als primären Index (eindeutige oder nicht eindeutig) muss den Namen der Spalte identisch sein. Für 4 Paradox. *x* und 5.* X*, der Namen des solchen Index werden kann, braucht jedoch den Namen der Spalte identisch sein.  
  
-   Für ein nichteindeutiger Index kann nur eine Spalte angegeben werden.  
  
 Spalten können nicht hinzugefügt werden, nachdem ein Index für eine Tabelle definiert wurde. Wenn die erste Spalte der Argumentliste einer CREATE TABLE-Anweisung ein Index erstellt wird, kann keine zweite Spalte in der Argumentliste enthalten.  
  
 Verwenden Sie z. B. die Verkaufsauftragsnummer und Zahlenspalten als eindeutiger Index für die Tabelle SO_LINES Zeile, die Anweisung ein:  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 Die Spalte für den Teil als ein nicht eindeutiger Index für die Tabelle SO_LINES verwenden möchten, verwenden Sie die Anweisung aus:  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 Beachten Sie, dass wenn zwei CREATE INDEX-Anweisungen ausgeführt werden, die erste Anweisung immer einen primären Index mit dem gleichen Namen wie die Tabelle erstellen wird und die zweite Anweisung wird immer einen nichteindeutiger Index mit dem gleichen Namen wie die Spalte erstellt. Diese Indizes werden auf diese Weise benannt werden, auch wenn andere Namen in der CREATE INDEX-Anweisungen eingegeben werden und auch wenn der Index eindeutig in der zweiten CREATE INDEX-Anweisung mit der Bezeichnung.  
  
> [!NOTE]  
>  Wenn Sie Paradox Treiber verwenden, ohne die Implementierung von Borland Database Engine, nur lesen und Anfügen sind Anweisungen zulässig.
