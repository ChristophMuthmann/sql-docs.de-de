---
title: Anweisungsparametern | Microsoft Docs
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
helpviewer_keywords: statement parameters [ODBC]
ms.assetid: 58d5b166-2578-4699-a560-1f1e6d86c49a
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 08d2365291bf6c402ead138d6182c83de5f27896
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="statement-parameters"></a>Anweisungsparametern
Ein *Parameter* ist eine Variable in einer SQL­Anweisung. Angenommen Sie, dass eine Parts-Tabelle Spalten PartID, Beschreibung und Price verfügt. Ein Teil ohne Parameter hinzufügen, müsste z. B. eine SQL-Anweisung erstellen:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 Obwohl diese Anweisung einen neuen Auftrag einfügt, ist es keine geeignete Lösung für eine Anwendung, da die einzufügenden Werte in der Anwendung fest programmiert werden können. Eine Alternative besteht darin, erstellen Sie die SQL-Anweisung zur Laufzeit mithilfe der Werte eingefügt werden. Dies ist auch keine geeignete Lösung, wegen der Komplexität der Erstellen von Anweisungen zur Laufzeit. Die beste Lösung besteht darin ersetzt die Elemente der **Werte** -Klausel mit Fragezeichen (?), oder *parametermarkierungen*:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Die Parametermarkierungen werden dann an Anwendungsvariablen gebunden. Um eine neue Zeile hinzuzufügen, muss die Anwendung nur die Werte der Variablen festlegen, und führen Sie die Anweisung. Der Treiber ruft dann die aktuellen Werte der Variablen ab und sendet sie an die Datenquelle. Wenn die Anweisung mehrmals ausgeführt wird, kann die Anwendung den Prozess noch effizienter gestalten durch Vorbereiten der Anweisung.  
  
 Die Anweisung, die oben gezeigte möglicherweise hartcodierte in einer Anwendung eine neue Zeile eingefügt. Parametermarkierungen sind jedoch nicht auf die vertikale Anwendungen beschränkt. Für jede Anwendung vereinfachen sie das Erstellen von SQL-Anweisungen zur Laufzeit durch das Vermeiden von Konvertierungen in und aus Text ist schwierig. Ist beispielsweise nur angezeigte Teil-ID wahrscheinlich in der Anwendung als eine ganze Zahl gespeichert. Wenn die SQL-Anweisung ohne parametermarkierungen erstellt wird, die Anwendung muss Teil-ID in Text konvertieren, und die Datenquelle muss die Umstellung zurück auf eine ganze Zahl. Mithilfe einer parametermarkierung kann die Anwendung Teil-ID an den Treiber als ganze Zahl, schicken, in der Regel er an die Datenquelle als eine ganze Zahl senden kann. Dies spart zwei Konvertierungen. Für lange Datenwerte ist dies sehr wichtig, da die Textformen solcher Werte häufig einer SQL-Anweisung die zulässige Länge überschritten.  
  
 Parameter sind nur an bestimmten Stellen in der SQL-Anweisungen gültig. Z. B. in der select-Liste nicht zulässig sind (die Liste der Spalten von zurückgegeben werden sollen eine **wählen** Anweisung), noch dürfen sie als beide Operanden des binären Operators z. B. das Gleichheitszeichen (=), da es unmöglich, wären Bestimmen Sie den Parametertyp an. Im Allgemeinen sind die Parameter gültig ist nur in Anweisungen (Data Manipulation Language, DML) und nicht in Anweisungen (Data Definition Language, Datendefinitionssprache). Weitere Informationen finden Sie unter [Parametermarkierungen](../../../odbc/reference/appendixes/parameter-markers.md) in Anhang C: SQL-Grammatik.  
  
 Wenn die SQL-Anweisung für eine Prozedur, die benannte Parameter aufruft, kann verwendet werden. Benannte Parameter werden durch ihren Namen, nicht anhand ihrer Position in der SQL-Anweisung identifiziert. Sie können durch einen Aufruf von gebunden werden **SQLBindParameter**, jedoch der Parameter wird nicht von durch SQL_DESC_NAME-Felds den IPD (Implementierung Parameterdeskriptor) identifiziert die *ParameterNumber* Argument **SQLBindParameter**. Sie können auch durch Aufrufen von gebunden **SQLSetDescField** oder **SQLSetDescRec**. Weitere Informationen zu benannten Parametern finden Sie unter [Bindungsparameter von Namen (Parameter genannt)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)weiter unten in diesem Abschnitt. Weitere Informationen zu Deskriptoren, finden Sie unter [Deskriptoren](../../../odbc/reference/develop-app/descriptors.md).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Binden von Parametern](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [Festlegen von Parameterwerten](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [Senden von Long-Daten](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [Abrufen von Ausgabeparametern von SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [Prozedurparameter](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [Arrays für Parameterwerte](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
