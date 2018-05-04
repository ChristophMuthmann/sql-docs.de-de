---
title: Arbeiten mit der RollupChildren-Funktion (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7316f209c3653dd81eb6d2052428d0e6306b4c0f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-manipulation---rollupchildren-function"></a>Datenbearbeitung für MDX - RollupChildren-Funktion
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Die MDX-Funktion (Multidimensional Expressions) [RollupChildren](../../../mdx/rollupchildren-mdx.md) führt einen Rollup der untergeordneten Elemente eines Elements aus, wobei auf jedes untergeordnete Element ein anderer unärer Operator angewendet wird. Der Wert des Rollups wird als Zahl zurückgegeben. Der unäre Operator kann durch eine Elementeigenschaft des untergeordneten Elements bereitgestellt werden, oder der Operator kann ein Zeichenfolgenausdruck sein, der direkt an die Funktion übergeben wird.  
  
## <a name="rollupchildren-function-examples"></a>Beispiele zur RollupChildren-Funktion  
 Die Verwendung der **RollupChildren** -Funktion in MDX-Anweisungen (Multidimensional Expressions) ist einfach zu erklären, die Funktion kann jedoch weit reichende Folgen für MDX-Abfragen haben.  
  
 Der Einfluss der **RollupChildren** -Funktion wird in MDX-Abfragen ersichtlich, die zum Durchführen einer selektiven Analyse der vorhandenen Cubedaten entworfen wurden. Die folgende Tabelle enthält beispielsweise eine Liste untergeordneter Elemente des übergeordneten Elements „Nettoumsatz“, wobei die unären Operatoren (durch die **UNARY_OPERATOR** -Elementeigenschaft dargestellt) in Klammern angegeben sind.  
  
|Übergeordnetes Element|Untergeordnetes Element|  
|-------------------|------------------|  
|Nettoumsatz|Domestic Sales (+)<br /><br /> Domestic Returns (-)<br /><br /> Foreign Sales (+)<br /><br /> Foreign Returns (-)|  
  
 Das übergeordnete Element Net Sales stellt derzeit die Gesamtsumme der in- und ausländischen Bruttoumsatzwerte bereit, wobei in- und ausländische Rücknahmen im Rahmen des Rollups subtrahiert werden.  
  
 Sie möchten jedoch eine schnelle und einfache Vorhersage des in- und ausländischen Bruttoumsatzes plus 10 % bereitstellen, wobei die in- und ausländischen Rücknahmen ignoriert werden. Zum Berechnen dieses Wertes können Sie die **RollupChildren** -Funktion auf eine der beiden folgenden Arten verwenden: mit einer benutzerdefinierten Elementeigenschaft oder mit der **IIf** -Funktion.  
  
### <a name="using-a-custom-member-property"></a>Verwenden einer benutzerdefinierten Elementeigenschaft  
 Wenn die Rollupberechnung häufig ausgeführt werden soll, besteht die Möglichkeit, eine Elementeigenschaft zu erstellen, in der der Operator gespeichert ist, der für jedes untergeordnete Element für eine bestimmte Funktion verwendet werden soll. Die folgende Tabelle zeigt gültige unäre Operatoren an und beschreibt das erwartete Ergebnis.  
  
|Operator|Ergebnis|  
|--------------|------------|  
|+|Gesamt = Gesamt + aktuelles untergeordnetes Element|  
|-|Gesamt = Gesamt - aktuelles untergeordnetes Element|  
|*|Gesamt = Gesamt * aktuelles untergeordnetes Element|  
|/|Gesamt = Gesamt / aktuelles untergeordnetes Element|  
|~|Untergeordnetes Element wird im Rollup nicht verwendet. Der Wert des untergeordneten Elements wird ignoriert.|  
  
 Beispielsweise könnte eine Elementeigenschaft mit dem Namen **SALES_OPERATOR** erstellt werden, die folgenden unären Operatoren könnten ihr zugewiesen werden (siehe nächste Tabelle).  
  
|Übergeordnetes Element|Untergeordnetes Element|  
|-------------------|------------------|  
|Nettoumsatz|Domestic Sales (+)<br /><br /> Domestic Returns (~)<br /><br /> Foreign Sales (+)<br /><br /> Foreign Returns (~)|  
  
 Mit dieser neuen Elementeigenschaft führt die folgende MDX-Anweisung die Schätzung des Bruttoumsatzes schnell und effizient aus (wobei in- und ausländische Rücknahmen ignoriert werden):  
  
```  
RollupChildren([Net Sales], [Net Sales].CurrentMember.Properties("SALES_OPERATOR")) * 1.1  
```  
  
 Beim Aufrufen der Funktion wird der Wert jedes untergeordneten Elements mithilfe des Operators, der in der Elementeigenschaft gespeichert ist, auf das Gesamtergebnis angewendet. Die Elemente für in- und ausländische Rücknahmen werden ignoriert, und der von der **RollupChildren** -Funktion zurückgegebene Rollupgesamtwert wird mit 1,1 multipliziert.  
  
### <a name="using-the-iif-function"></a>Verwenden der IIf-Funktion  
 Wenn die Beispieloperation nicht häufig verwendet wird oder nur für eine einzelne MDX-Abfrage gültig ist, kann die [IIf](../../../mdx/iif-mdx.md) -Funktion zusammen mit der **RollupChildren** -Funktion verwendet werden, um dasselbe Ergebnis bereitzustellen. Die folgende MDX-Abfrage stellt dasselbe Ergebnis wie das vorherige MDX-Abfragebeispiel bereit, jedoch ohne die Verwendung einer benutzerdefinierten Elementeigenschaft:  
  
```  
RollupChildren([Net Sales], IIf([Net Sales].CurrentMember.Properties("UNARY_OPERATOR") = "-", "~", [Net Sales].CurrentMember.Properties("UNARY_OPERATOR))) * 1.1  
```  
  
 Die MDX-Anweisung wertet den unären Operator des untergeordneten Elements aus. Wird der unäre Operator zur Subtraktion verwendet (wie dies bei den Elementen der in- und ausländischen Rücknahmen der Fall ist), wird der unäre Tildeoperator (~) durch die **IIf** -Funktion ersetzt. Andernfalls verwendet die **IIf** -Funktion den unären Operator des untergeordneten Elements. Schließlich wird der zurückgegebene Rollupgesamtwert mit 1,1 multipliziert, um die Vorhersage der in- und ausländischen Bruttoumsätze bereitzustellen.  
  
## <a name="see-also"></a>Siehe auch  
 [Bearbeiten von Daten & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  
