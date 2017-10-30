---
title: Filteroperatoren (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27914c8b-8951-4b7d-914d-1cbf528dd248
caps.latest.revision: 11
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 0d83ee33afcd50635a163a56f977e77fc6e6c68a
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="filter-operators-master-data-services"></a>Filteroperatoren (Master Data Services)
  Wenn sie eine Liste von Elementen filtern, sind die folgenden Operatoren verfügbar.  
  
> [!NOTE]  
>  Wenn Sie nach mehreren Kriterien filtern, müssen alle Kriterien den Wert "true" haben, um Ergebnisse zurückzugeben. Zum Beispiel SquareFeet = 2000 **AND** Division <> 123.  
  
## <a name="filter-operators"></a>Filteroperatoren  
  
|Steuerelementname|Description|  
|------------------|-----------------|  
|**Ist gleich**|Gibt Attributwerte zurück, die den angegebenen Kriterien genau entsprechen. Um nach **Mountain-100**zu filtern, müssen Sie z.B. **Mountain-100**eingeben.|  
|**Ist nicht gleich**|Gibt Attributwerte zurück, die keine genaue Übereinstimmung mit den angegebenen Kriterien aufweisen. Die Filterkriterien müssen dem Attributwert, den Sie aus den Ergebnissen ausschließen möchten, genau entsprechen. Um Ergebnisse auszuschließen, die mit **Mountain-100**übereinstimmen, müssen Sie z.B. **Mountain-100**eingeben.<br /><br /> <br /><br /> Hinweis: Wenn eine Filteranwendung mit einer „Ist nicht gleich“-Klausel auf ein Attribut angewendet wird, wird ein Element, dessen Attribut nicht NULL ist, die Filterbedingung übergeben und zurückgegeben werden, wenn in Ihren Datenbankeinstellungen SET ANSI_NULLS auf ON festgelegt ist. Um dieses Verhalten zu beenden, legen Sie SET ANSI_NULLS in den Datenbankeinstellungen auf OFF fest. Wenn SET ANSI_NULLS auf OFF festgelegt ist, werden alle Datenvergleiche mit einem NULL-Wert als TRUE ausgewertet, falls der Datenwert NULL ist. Dies hat zur Folge, dass das Element die "Ist nicht gleich"-Klausel nicht besteht. Weitere Informationen finden Sie unter [SET ANSI_NULLS &#40;Transact-SQL&#41;](../t-sql/statements/set-ansi-nulls-transact-sql.md).|  
|**Ist wie**|Verwendet den LIKE-Operator aus Transact-SQL zum Filtern von Ergebnissen. Weitere Informationen finden Sie unter [LIKE &#40;Transact-SQL&#41;](../t-sql/language-elements/like-transact-sql.md) in der SQL Server-Onlinedokumentation.|  
|**Ist nicht wie**|Verwendet den NOT-Operator aus Transact-SQL zum Filtern von Ergebnissen. Weitere Informationen finden Sie unter [NOT &#40;Transact-SQL&#41;](../t-sql/language-elements/not-transact-sql.md) in der SQL Server-Onlinedokumentation.|  
|**Ist größer als**|Gibt Attributwerte zurück, die größer als die angegebenen Kriterien sind. Um Attributwerte zurückzugeben, die mit einem Buchstaben größer als **F**beginnen, geben Sie z. B. **F**ein.|  
|**Ist kleiner als**|Gibt Attributwerte zurück, die kleiner als die angegebenen Kriterien sind. Um Attributwerte zurückzugeben, die mit einem Buchstaben kleiner als **F**beginnen, geben Sie z. B. **F**ein.|  
|**Ist größer als oder gleich**|Gibt Attributwerte zurück, die größer oder gleich den angegebenen Kriterien sind. Um Attributwerte zurückzugeben, die mit der Zahl **3** oder einer höheren Zahl beginnen, geben Sie z. B. **3**ein.|  
|**Ist kleiner als oder gleich**|Gibt Attributwerte zurück, die kleiner oder gleich den angegebenen Kriterien sind. Um Attributwerte zurückzugeben, die mit der Zahl **3** oder einer kleineren Zahl beginnen, geben Sie z. B. **3**ein.|  
|**Stimmt überein**|Verwendet einen Fuzzysuchindex zum Filtern von Ergebnissen.<br /><br /> Geben Sie im Feld **Ähnlichkeitsgrad** an, wie genau die Abweichung der Attributwerte von den angegebenen Filterkriterien (mit einem Standardwert von „30 %“) sein muss.<br /><br /> Wählen Sie eine der folgenden Möglichkeiten im Listenfeld **Algorithmus** aus.<br /><br /> **Levenshtein**: Eine Distanz auf Grundlage der Anzahl von Bearbeitungen (beispielsweise Hinzufügungen oder Löschungen), die benötigt wird, um von einer Zeichenfolge zur nächsten zu gelangen. Dies ist die Standardeinstellung. Erfordert keine zusätzlichen Parameter.<br /><br /> **Jaccard**: Ein Index, der sich am besten eignet, wenn versucht wird, mehrere Zeichenfolgen abzugleichen. Diese Suche unterstützt einen zusätzlichen Parameter der Kapselungsvorspannung (siehe unten).<br /><br /> **Jaro-Winkler**: Eine Distanz, die sich am besten für die Suche von doppelten Personennamen eignet. Diese Methode gibt mehr Ergebnisse zurück als jede andere Methode. Unterstützt keine Kapselungsvorspannung.<br /><br /> **Längste gemeinsame Teilsequenz**: Funktioniert auf Grundlage einer Teilsequenz, in der die Buchstaben eines Musters in einer Reihenfolge angezeigt werden, obwohl sie getrennt werden können (beispielsweise ist „MSR“ eine Teilsequenz von „MeiSteR“). Diese Suche unterstützt einen zusätzlichen Parameter der Kapselungsvorspannung (siehe unten).<br /><br /> <br /><br /> Hinweis: Fügen Sie für den **Jaccard** - oder den **Längste gemeinsame Teilsequenz** -Algorithmus einen **Verzerrungswert für den Einschluss**hinzu. Dies ist ein Längenschwellenwert, der in einem dezimalen Prozentsatz zwischen "0" und "1" bereitgestellt wird, mit dem Standard "0,62". Ein niedrigerer Schwellenwert vergrößert die Anzahl der möglichen zurückgegebenen Übereinstimmungen.|  
|**Stimmt nicht überein**|Verwendet einen Fuzzysuchindex zum Filtern von Ergebnissen. Geben Sie im Feld **Ähnlichkeitsgrad** an, wie genau die Abweichung der Attributwerte von den angegebenen Filterkriterien sein muss.|  
|**Enthält Muster**|Verwendet reguläre Ausdrücke von .NET Framework, um Ergebnisse nach einem angegebenen Muster zu filtern. Weitere Informationen zu regulären Ausdrücken finden Sie unter [Sprachelemente für reguläre Ausdrücke](http://go.microsoft.com/fwlink/?LinkId=164401) in der MSDN Library.|  
|**Enthält kein Muster**|Verwendet reguläre Ausdrücke von .NET Framework zum Filtern von Ergebnissen, die einem angegebenen Muster nicht entsprechen. Weitere Informationen zu regulären Ausdrücken finden Sie unter [Sprachelemente für reguläre Ausdrücke](http://go.microsoft.com/fwlink/?LinkId=164401) in der MSDN Library.|  
|**Ist NULL**|Gibt Attributwerte zurück, die NULL lauten. Das Feld **Kriterien** wird deaktiviert, wenn Sie den **Ist NULL** -Operator auswählen.|  
|**Ist nicht NULL**|Gibt Attributwerte zurück, die nicht NULL lauten. Das Feld **Kriterien** wird deaktiviert, wenn Sie den **Ist nicht NULL** -Operator auswählen.|  
  
  

