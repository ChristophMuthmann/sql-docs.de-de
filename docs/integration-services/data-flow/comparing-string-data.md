---
title: Vergleichen von Zeichenfolgendaten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- comparing string data
- comparison options [Integration Services]
- locales [Integration Services]
- converting string data
- string comparisons
ms.assetid: 93aeb5bd-e208-46b7-8979-dea2dcd37d4c
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 56adf456b22be6675f02c7ee6919428263156938
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="comparing-string-data"></a>Vergleichen von Zeichenfolgendaten
  Zeichenfolgendaten sind ein wichtiger Bestandteil vieler Transformationen, die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]ausgeführt werden, und Zeichenfolgenvergleiche werden auch bei der Auswertung von Ausdrücken in Variablen und Eigenschaftsausdrücken verwendet. Beispielsweise vergleicht die Transformation zum Sortieren Werte in einem Dataset, um Daten in auf- und absteigender Reihenfolge zu sortieren.  
  
## <a name="configuring-transformations-for-string-comparisons"></a>Konfigurieren von Transformationen für Zeichenfolgenvergleiche  
 Die Transformation zum Sortieren, die Transformation für das Aggregieren, die Transformation für Fuzzygruppierung und die Transformation für Fuzzysuche können angepasst werden, um die Methode zum Vergleichen von Zeichenfolgen auf Spaltenebene zu ändern. Beispielsweise können Sie angeben, dass beim Vergleichen die Groß-/Kleinschreibung ignoriert wird. Das heißt, Groß- und Kleinbuchstaben werden als identische Zeichen behandelt.  
  
 Die folgenden Transformationen verwenden Ausdrücke, die Zeichenfolgenvergleiche einschließen können.  
  
-   Die Transformation für bedingtes Teilen kann Zeichenfolgenvergleiche in Ausdrücken verwenden, um zu bestimmen, welche Ausgabe an die Datenzeile gesendet werden soll. Weitere Informationen finden Sie unter [Conditional Split Transformation](../../integration-services/data-flow/transformations/conditional-split-transformation.md).  
  
-   Die Transformation für abgeleitete Spalten kann Zeichenfolgenausdrücke in Ausdrücken verwenden, um neue Spaltenwerte zu generieren. Weitere Informationen finden Sie unter [Derived Column Transformation](../../integration-services/data-flow/transformations/derived-column-transformation.md).  
  
 Variablen, Variablenzuordnungen und Rangfolgeneinschränkungen verwenden ebenfalls Ausdrücke, die Zeichenfolgenausdrücke einschließen können. Weitere Informationen zu Ausdrücken finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
## <a name="processing-during-string-comparison"></a>Verarbeiten während des Zeichenfolgenvergleichs  
 Abhängig von den Daten und der Konfiguration der Transformation wird möglicherweise die folgende Verarbeitung während des Vergleichs von Zeichenfolgendaten ausgeführt:  
  
-   Konvertieren von Daten in das Unicode-Format. Falls die Quelldaten noch nicht das Unicode-Format haben, werden die Daten vor dem Vergleich automatisch in Unicode konvertiert.  
  
-   Verwenden des Gebietsschemas, um gebietsschemaspezifische Regeln zum Interpretieren von Datum, Uhrzeit, Dezimaldaten und Sortierreihenfolge anzuwenden.  
  
-   Anwenden von Vergleichsoptionen auf Spaltenebene, um die Unterscheidung von Vergleichen zu ändern.  
  
## <a name="converting-string-data-to-unicode"></a>Konvertieren von Zeichenfolgendaten in das Unicode-Format  
 Abhängig von den Vorgängen, die die Transformation ausführt, und der Konfiguration der Transformation werden Zeichenfolgendaten möglicherweise in den DT_WSTR-Datentyp konvertiert. Hierbei handelt es sich um eine Unicode-Darstellung von Zeichenfolgendaten.  
  
 Zeichenfolgendaten mit dem DT_STR-Datentyp werden mithilfe der Codepage der Spalte in Unicode konvertiert. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] unterstützt Codepages auf Spaltenebene, und jede Spalte kann mithilfe einer anderen Codepage konvertiert werden.  
  
 In den meisten Fällen kann [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] die richtige Codepage anhand der Datenquelle identifizieren. Beispielsweise können Sie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Sortierung auf Datenbank- und Spaltenebene festlegen. Die Codepage wird von einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sortierung abgeleitet, wobei es sich entweder um eine Windows- oder eine SQL-Sortierung handelt.  
  
 Angenommen, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt eine unerwartete Codepage bereit oder das Paket greift auf eine Datenquelle mithilfe eines Anbieters zu, der nicht ausreichend Informationen bereitstellt, um die richtige Codepage zu bestimmen. In diesem Fall können Sie in der OLE DB-Quelle und im OLE DB-Ziel eine Standardcodepage angeben. Die Standardcodepages werden anstelle der Codepages von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendet.  
  
 Dateien weisen keine Codepages auf. Stattdessen enthalten der Verbindungs-Manager für Flatfiles und der Verbindungs-Manager für mehrere Flatfiles, mit denen ein Paket eine Verbindung mit einer Dateidaten herstellt, eine Eigenschaft zum Angeben der Codepage der Datei. Die Codepage kann nicht auf Spaltenebene, sondern nur auf Dateiebene festgelegt werden.  
  
## <a name="setting-locale"></a>Festlegen des Gebietsschemas  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendet die Codepage nicht, um gebietsschemaspezifische Regeln zum Sortieren von Daten oder zum Interpretieren von Datum, Uhrzeit und Dezimaldaten abzuleiten. Stattdessen liest die Transformation das Gebietsschema, das mit der LocaleId-Eigenschaft in der Datenflusskomponente, dem Datenflusstask, dem Container oder dem Paket festgelegt wird. Standardmäßig wird das Gebietsschema einer Transformation vom Datenflusstask geerbt, der es wiederum vom Paket erbt. Falls der Datenflusstask ein Container wie z. B. der For-Schleifencontainer ist, erbt er das Gebietsschema vom Container.  
  
 Sie können auch ein Gebietsschema für einen Verbindungs-Manager für Flatfiles und einen Verbindungs-Manager für mehrere Flatfiles angeben.  
  
## <a name="setting-comparison-options"></a>Festlegen von Vergleichsoptionen  
 Das Gebietsschema stellt die grundlegenden Regeln zum Vergleichen von Zeichenfolgendaten bereit. Beispielsweise gibt das Gebietsschema die Sortierposition jedes Buchstabens im Alphabet an. Diese Regeln sind jedoch möglicherweise für die Vergleiche mancher Transformationen nicht ausreichend. Deshalb unterstützt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] erweiterte Vergleichsoptionen, die über die Vergleichsregeln eines Gebietsschemas hinausgehen. Diese Vergleichsoptionen werden auf Spaltenebene festgelegt. Beispielsweise können Sie mit einer der Vergleichsoptionen Zeichen ohne Zwischenraum ignorieren. Dadurch werden diakritische Zeichen wie z. B. Akzente ignoriert, sodass "a" und "á" für Vergleichszwecke identisch sind.  
  
 In der folgenden Tabelle werden die Vergleichsoptionen und eine Sortiermethode beschrieben.  
  
|Vergleichsoption|Description|  
|-----------------------|-----------------|  
|Groß-/Kleinschreibung ignorieren|Gibt an, ob beim Vergleichen zwischen Groß- und Kleinbuchstaben unterschieden wird. Falls diese Option festgelegt ist, ignoriert der Zeichenfolgenvergleich die Groß-/Kleinschreibung. Beispielsweise ist dann "ABC" mit "abc" identisch.|  
|Kanatyp ignorieren|Gibt an, ob beim Vergleichen zwischen den beiden Typen japanischer Kanazeichen unterschieden wird: Hiragana und Katakana. Falls diese Option festgelegt ist, ignoriert der Zeichenfolgenvergleich den Kanatyp.|  
|Zeichenbreite ignorieren|Gibt an, ob beim Vergleichen zwischen einem Single-Byte-Zeichen und demselben Zeichen als Double-Byte-Zeichen unterschieden wird. Wenn diese Option festgelegt ist, werden die Single-Byte- und die Double-Byte-Darstellung desselben Zeichens als identisch behandelt.|  
|Zeichen ohne Zwischenraum ignorieren|Gibt an, ob beim Vergleichen zwischen Zeichen mit Zwischenraum und diakritischen Zeichen unterschieden wird. Falls diese Option festgelegt ist, ignoriert der Zeichenfolgenvergleich diakritische Zeichen. Beispielsweise ist dann "å" mit "a" identisch.|  
|Symbole ignorieren|Gibt an, ob beim Vergleichen zwischen Buchstaben und Symbolen wie z. B. Leerzeichen, Satzzeichen, Währungssymbolen und mathematischen Symbolen unterschieden wird. Falls diese Option festgelegt ist, ignoriert der Zeichenfolgenvergleich Symbole. Beispielsweise ist " New York" dann identisch mit "New York", und "*ABC" ist identisch mit "ABC"'.|  
|Interpunktion als Symbole sortieren|Gibt an, ob beim Vergleichen alle Interpunktionssymbole außer dem Bindestrich und dem Apostroph vor den alphanumerischen Zeichen sortiert werden. Falls diese Option festgelegt ist, wird z. B. ".ABC" vor "ABC" sortiert.|  
  
 Die Transformation zum Sortieren, die Transformation für das Aggregieren, die Transformation für Fuzzygruppierung und die Transformation für Fuzzysuche schließen diese Optionen zum Vergleichen von Daten ein.  
  
 Das **FullySensitive** -Vergleichsflag wird im Dialogfeld **Erweiterter Editor** für die Transformation für Fuzzygruppierung und die Transformation für Fuzzysuche angezeigt. Wenn Sie das **FullySensitive** -Vergleichsflag auswählen, gelten alle Vergleichsoptionen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server Integration Services-Datentypen](../../integration-services/data-flow/integration-services-data-types.md)   
 [Schnelle Analyse](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95)   
 [Standardanalyse](http://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)  
  
  
