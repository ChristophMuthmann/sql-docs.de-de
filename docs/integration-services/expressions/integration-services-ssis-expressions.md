---
title: "Integration Services-Ausdrücke (SSIS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- packages [Integration Services], expressions
- Integration Services packages, expressions
- SQL Server Integration Services packages, expressions
- expressions [Integration Services], packages
- SSIS packages, expressions
ms.assetid: 26d2e242-7f60-4fa9-a70d-548a80eee667
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7dedaa6d36fb0618b6124b1d2b1014c32fb2f44c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="integration-services-ssis-expressions"></a>Integration Services-Ausdrücke (SSIS)
  Ein Ausdruck ist eine Kombination aus Symbolen (Bezeichner, Literale, Funktionen und Operatoren), die einen einzelnen Datenwert ergeben. Einfache Ausdrücke können aus einer einzelnen Konstante, Variable oder Funktion bestehen. Meist sind Ausdrücke jedoch komplex, verwenden mehrere Operatoren und Funktionen und verweisen auf mehrere Spalten und Variablen. In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]können Ausdrücke zum Definieren von Bedingungen für CASE-Anweisungen, Erstellen und Aktualisieren von Werten in Datenspalten, Zuweisen von Werten zu Variablen, Aktualisieren oder Auffüllen von Eigenschaften zur Laufzeit, Definieren von Einschränkungen in Rangfolgeneinschränkungen sowie zum Bereitstellen von Ausdrücken für den For-Schleifencontainer verwendet werden.  
  
 Ausdrücke basieren auf einer Ausdruckssprache und der Ausdrucksauswertung. Die Ausdrucksauswertung analysiert Ausdrücke und ermittelt, ob sich Ausdrücke an die Regeln der Ausdruckssprache halten. Weitere Informationen zur Ausdruckssyntax und zu unterstützten Literalen und Bezeichnern finden Sie in den folgenden Themen.  
  
-   [Syntax &#40;SSIS&#41;](../../integration-services/expressions/syntax-ssis.md)  
  
-   [Literale &#40;SSIS&#41;](../../integration-services/expressions/numeric-string-and-boolean-literals.md)  
  
-   [Bezeichner &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md)  
  
## <a name="components-that-use-expressions"></a>Komponenten, die Ausdrücke verwenden  
 In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] können für die folgenden Elemente Ausdrücke verwendet werden:  
  
-   Die Transformation für bedingtes Teilen, die eine auf Ausdrücken basierende Entscheidungsstruktur implementiert, um Datenzeilen an verschiedene Ziele weiterzuleiten. In einer Transformation für bedingtes Teilen verwendete Ausdrücke müssen zu **true** oder **false**ausgewertet werden. Beispielsweise können die Zeilen, die die Bedingung im Ausdruck "Column1 > Column2" erfüllen, an eine andere Ausgabe weitergeleitet werden.  
  
-   Die Transformation für abgeleitete Spalte, die mithilfe von Ausdrücken erstellte Werte verwendet, um neue Spalten in einem Datenfluss aufzufüllen, oder um vorhandene Spalten zu aktualisieren. Beispielsweise kann der Ausdruck Column1 + " ABC" verwendet werden, um einen Wert zu aktualisieren, oder um mit der verketteten Zeichenfolge einen neuen Wert zu erstellen.  
  
-   Variablen, deren Wert mit einem Ausdruck festgelegt werden kann. Die Variable GETDATE() legt z. B. den Wert der Variablen auf das aktuelle Datum fest.  
  
-   Rangfolgeneinschränkungen, bei denen mithilfe von Ausdrücken die Bedingungen angegeben werden können, die festlegen, ob der eingeschränkte Task oder Container eines Pakets ausgeführt wird. In einer Rangfolgeneinschränkung verwendete Ausdrücke müssen zu **true** oder **false**ausgewertet werden. Der Ausdruck @A > @B z.B. vergleicht zwei benutzerdefinierte Variablen, um zu bestimmen, ob der eingeschränkte Task ausgeführt wird.  
  
-   For-Schleifen-Container, bei denen mithilfe von Ausdrücken Initialisierungs-, Auswertungs- und Inkrementanweisungen erstellt werden können, die von der Schleifenstruktur verwendet werden. Der Ausdruck @Counter = 1 z.B. initialisiert den Schleifenzähler.  
  
 Ausdrücke können auch zum Aktualisieren der Werte von Paketeigenschaften, Containern wie dem For- und dem Foreach-Schleifencontainer, Tasks, Verbindungs-Managern auf Paket- und Projektebene, Protokollanbietern und Foreach-Enumeratoren verwendet werden. Mithilfe eines Eigenschaftsausdrucks kann z.B. die Zeichenfolge „Localhost.AdventureWorks“ der ConnectionName-Eigenschaft des Tasks „SQL ausführen“ zugewiesen werden. Weitere Informationen finden Sie unter [Verwenden von Eigenschaftsausdrücken in Paketen](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
## <a name="icon-markers-for-expressions"></a>Symbolmarker für Ausdrücke  
 In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]wird ein spezieller Symbolmarker neben Verbindungs-Managern, Variablen und Tasks angezeigt, für die Ausdrücke festgelegt sind. Die **HasExpressions** -Eigenschaft ist für alle SSIS-Objekte verfügbar, die Ausdrücke unterstützen, mit Ausnahme von Variablen. Mit der Eigenschaft können Sie bequem ermitteln, welche Objekte über Ausdrücke verfügen.  
  
## <a name="expression-builder"></a>Ausdrucks-Generator  
 Der Ausdrucks-Generator ist ein grafisches Tool zum Erstellen von Ausdrücken. Dieser ist in den Dialogfeldern **Transformations-Editor für bedingtes Teilen**, **Transformations-Editor für abgeleitete Spalte** und **Ausdrucks-Generator** verfügbar, es handelt sich um ein grafisches Tool zum Erstellen von Ausdrücken.  
  
 Der Ausdrucks-Generator stellt Ordner bereit, die paketspezifische Elemente enthalten, sowie Ordner, die die von der Ausdruckssprache bereitgestellten Funktionen, Typumwandlungen und Operatoren enthalten. Paketspezifische Elemente umfassen Systemvariablen und benutzerdefinierte Variablen. In den Dialogfeldern **Transformations-Editor für bedingtes Teilen** und **Transformations-Editor für abgeleitete Spalte** können Sie auch Datenspalten anzeigen. Sie können Elemente aus den Ordnern in die Spalten **Bedingung** oder **Ausdruck** ziehen, um die Ausdrücke für die Transformationen zu erstellen, oder Sie können Ausdrücke direkt in die Spalten eingeben. Der Ausdrucks-Generator fügt erforderliche Syntaxelemente, wie z. B. das @-Präfix bei Variablennamen, automatisch hinzu.  
  
> [!NOTE]  
>  Die Namen von benutzerdefinierten und Systemvariablen unterscheiden nach Groß-/Kleinschreibung.  
  
 Variablen verfügen über einen Gültigkeitsbereich, und im Ordner **Variablen** im Ausdrucks-Generator werden nur die Variablen aufgeführt, die im Gültigkeitsbereich enthalten sind und verwendet werden können. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Verwenden eines Ausdrucks in einer Datenflusskomponente](http://msdn.microsoft.com/library/9181b998-d24a-41fb-bb3c-14eee34f910d)  
  
## <a name="related-content"></a>Verwandte Inhalte  
 Technischer Artikel, [SSIS Expression Examples](http://go.microsoft.com/fwlink/?LinkId=220761), auf social.technet.microsoft.com  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
