---
title: Puffer | Microsoft Docs
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
- input buffers [ODBC]
- length/indicator buffers [ODBC]
- output buffers [ODBC]
- buffers [ODBC], about buffers
- application buffers [ODBC]
- buffers [ODBC]
ms.assetid: 42c5226c-cb40-4d1e-809f-2ea50ce6bd55
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0d63aa103ac71aa89d245f6b8e4770b2c4943f2a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="buffers"></a>Puffer
Ein Puffer ist jedem Teil einer Anwendung Arbeitsspeicher verwendet, um Daten zwischen der Anwendung und den Treiber übergeben. Beispielsweise Anwendungspuffer können zugeordnet werden, oder *gebunden* Resultsetspalten mit **SQLBindCol**. Wie jede Zeile abgerufen wird, werden die Daten für jede Spalte in diesen Puffern zurückgegeben. *Geben Sie Puffer* dienen zum Übergeben von Daten aus der Anwendung an den Treiber; *Ausgabepuffer* werden verwendet, um Daten aus dem Treiber an die Anwendung zurückgegeben.  
  
> [!NOTE]  
>  Wenn eine ODBC-Funktion SQL_ERROR zurückgibt, sind den Inhalt der Ausgabeargumente der Funktion nicht definiert.  
  
 Diese Erläuterung bezieht sich auf selbst in erster Linie mit Puffern unbestimmt-Typs. Die Adressen der diese Puffer werden als Argumente des Typs SQLPOINTER, wie z. B. die *TargetValuePtr* Argument in **SQLBindCol**. Allerdings einige der Elemente, die hier erläutert, wie z. B. die Argumente, mit der Puffer, gelten auch für Argumente verwendet, um Zeichenfolgen an den Treiber übergeben, z. B. die *TableName* Argument in **SQLTables**.  
  
 Diese Puffer sind in der Regel einander paarweise zugeordnet. *Datenpuffer* werden verwendet, um die Daten selbst zu übergeben, während er sich *Längenindikator/Puffer* werden verwendet, um die Länge der Daten in den Datenpuffer oder ein spezieller Wert z. B. SQL_NULL_DATA gibt an, dass die Daten NULL übergeben. Die Länge der Daten in einen Datenpuffer unterscheidet sich von der Länge des Datenpuffers selbst. Die folgende Abbildung zeigt die Beziehung zwischen den Datenpuffer und Längen-/Indikatorpuffers.  
  
 ![Datenpuffer und Länge&#47;Indikatorpuffers](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 Ein Längen-/Indikatorpuffers ist erforderlich, wenn der Datenpuffer Daten, z. B. Zeichen- oder Binärdaten variabler Länge enthält. Enthält der Datenpuffer Daten fester Länge, z. B. eine ganze Zahl oder Datum Struktur ist ein Längen-/Indikatorpuffers musste nur Indikatorwerte übergeben werden, da die Länge der Daten bereits bekannt ist. Wenn eine Anwendung ein Längen-/Indikatorpuffers mit Daten fester Länge verwendet, ignoriert der Treiber alle Längen darin übergeben.  
  
 Die Länge des Datenpuffers und die darin enthaltenen Daten wird in Bytes, im Gegensatz zu Zeichen gemessen. Diese Unterscheidung ist bedeutungslos für Programme, die ANSI-Zeichenfolgen verwenden, da die Länge in Bytes und Zeichen identisch sind.  
  
 Wenn Datenpuffer eine treiberdefinierten Deskriptorfeld, eine Diagnose Feld oder ein Attribut darstellt, sollte die Anwendung an den Treiber-Manager den Charakter das Funktionsargument angeben, der den Wert für das Feld oder das Attribut angibt. Die Anwendung wird durch Festlegen der Length-Argument in einem beliebigen Funktionsaufruf, die das Feld oder ein Attribut auf einen der folgenden Werte festgelegt. (Dasselbe gilt für Funktionen, die die Werte des Felds oder Attributs, mit der Ausnahme, die das Argument auf die Werte verweist, die für die Einstellung-Funktion in das Argument selbst abzurufen.)  
  
-   Wenn das Funktionsargument, die der Wert für das Feld oder ein Attribut gibt einen Zeiger auf eine Zeichenfolge ist die *Länge* -Argument gibt die Länge der Zeichenfolge oder SQL_NTS.  
  
-   Wenn das Funktionsargument, die der Wert für das Feld oder ein Attribut gibt einen Zeiger auf einen Puffer, der binäre ist, platziert die Anwendung das Ergebnis der SQL_LEN_BINARY_ATTR (*Länge*) Makro in den *Länge* Argument. Dies setzt einen negativen Wert in der *Länge* Argument.  
  
-   Wenn das Funktionsargument, die der Wert für das Feld oder ein Attribut gibt einen Zeiger auf einen anderen Wert als eine Zeichenfolge oder eine binäre Zeichenfolge ist die *Länge* Arguments müssen den Wert SQL_IS_POINTER.  
  
-   Wenn das Funktionsargument, die der Wert für das Feld oder ein Attribut gibt einen Wert fester Länge enthält die *Länge* Argument ist SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT oder SQL_ISI_USMALLINT, nach Bedarf.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Verzögerte Puffer](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [Zuweisen und Freigeben von Puffern](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [Verwenden von Datenpuffern](../../../odbc/reference/develop-app/using-data-buffers.md)
