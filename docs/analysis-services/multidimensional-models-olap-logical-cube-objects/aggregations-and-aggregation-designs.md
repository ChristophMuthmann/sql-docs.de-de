---
title: Aggregationen und Aggregationsentwürfe | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 632c327685222260ea4648ceabf828b7d9a06591
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="aggregations-and-aggregation-designs"></a>Aggregations and Aggregation Designs
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Ein <xref:Microsoft.AnalysisServices.AggregationDesign>-Objekt definiert einen Satz von Aggregationsdefinitionen, die für mehrere Partitionen freigegeben werden können.  
  
 Ein <xref:Microsoft.AnalysisServices.Aggregation> -Objekt stellt die Zusammenfassung der Measuregruppendaten bei bestimmter Granularität der Dimensionen dar.  
  
 Ein einfaches <xref:Microsoft.AnalysisServices.Aggregation>-Objekt besteht aus: grundlegenden Informationen und Dimensionen. Grundlegende Informationen beinhalten den Namen der Aggregation, die ID, Anmerkungen und eine Beschreibung. Die Dimensionen sind eine Auflistung von <xref:Microsoft.AnalysisServices.AggregationDimension> Objekten, die die Liste der Granularitätsattribute der Dimension enthalten.  
  
 Aggregationen sind im Voraus berechnete Zusammenfassungen von Blattzellendaten. Mit Aggregationen kann die Abfrageantwortzeit verbessert werden, da die Antworten, bevor die Fragen gestellt werden, bereits vorbereitet sind. Wenn beispielsweise die Faktentabelle eines Data Warehouses hunderttausende von Zeilen enthält, kann die Beantwortung einer Abfrage, die den wöchentlichen Gesamtumsatz für eine bestimmte Produktlinie anfordert, viel Zeit in Anspruch nehmen, wenn alle Zeilen in der Faktentabelle erst gescannt und zur Abfragezeit zusammengefasst werden müssen, um die Antwort zu berechnen. Die Beantwortung erfolgt hingegen fast unmittelbar, wenn die zur Beantwortung dieser Abfrage benötigten zusammengefassten Daten im Voraus berechnet wurden. Die Vorausberechnung von zusammengefassten Daten erfolgt während der Verarbeitung und ist die Grundlage für die schnelle Antwortzeit der OLAP-Technologie.  
  
 Mithilfe von Cubes organisiert die OLAP-Technologie zusammengefasste Daten in mehrdimensionale Strukturen. Dimensionen und ihre Hierarchien von Attributen spiegeln die Abfragen wider, die für den Cube gestellt werden können. Aggregationen werden in einer mehrdimensionalen Struktur in Zellen mit Koordinaten gespeichert, die von den Dimensionen angegeben werden. Beispielsweise die Frage "Was waren die Umsätze von Produkt X im Jahr 1998 für die nordwestliche Region?" umfasst drei Dimensionen (Produkt, Zeit und Geografie) und ein Measure (Umsatz). Die Antwort ist der Wert in der Zelle, die im Cube die angegebenen Koordinaten (Product X, 1998, Northwest) besitzt; dies ist ein einzelner numerischer Wert.  
  
 Auf andere Fragen können mehrere Werte zurückgegeben werden. Ein Beispiel ist: "Wie lauten die Umsätze für Hardwareprodukte nach Quartal und nach Bezirk für das Jahr 1998?" Solche Abfragen geben Mengen von Zellen mit den Koordinaten zurück, die die angegebenen Bedingungen erfüllen. Die durch die Abfrage zurückgegebene Anzahl von Zellen hängt von der Anzahl der Elemente in der Hardware-Ebene der Product-Dimension, von den vier Quartalen des Jahres 1998 und von der Anzahl der Bezirke in der Geography-Dimension ab. Wenn alle zusammengefassten Daten in Aggregationen im Voraus berechnet wurden, hängt die Antwortzeit der Abfrage nur von der Zeit ab, die zum Extrahieren der angegebenen Zellen benötigt wird. Es sind keine Berechnungen oder Lesevorgänge für die Daten der Faktentabelle erforderlich.  
  
 Obwohl die Vorausberechnung aller möglichen Aggregationen in einem Cube die schnellstmögliche Antwortzeit für alle Abfragen bereitstellen kann, kann [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] jedoch einige aggregierte Werte einfach aus anderen vorausberechneten Aggregationen berechnen. Außerdem erfordert die Berechnung aller möglichen Aggregationen eine beträchtliche Verarbeitungszeit und viel Speicher. Es gibt also einen Zusammenhang zwischen Speicheranforderungen und dem Prozentsatz der möglichen, im Voraus berechneten Aggregationen. Werden keine Aggregationen vorausberechnet (0 %), werden die für einen Cube erforderliche Verarbeitungszeit und der erforderliche Speicherplatz minimiert. Die Abfrageantwortzeit kann jedoch langsam sein, da die zum Beantworten der einzelnen Abfragen erforderlichen Daten von den Blattzellen abgerufen und dann zur Abfragezeit aggregiert werden müssen. So kann z. B. das Zurückgeben einer einzelnen Zahl als Antwort auf die zuvor gestellte Frage ("Wie lauten die Umsätze von Produkt X im Jahr 1998 für den nordwestlichen Bezirk?") das Lesen tausender Datenzeilen erfordern, wobei jeweils der Wert jeder Zeile für das Sales-Measure extrahiert und die Summe berechnet werden muss. Darüber hinaus hängt die Zeit, die zum Abrufen der Daten erforderlich ist, davon ab, welcher Speichermodus für die Daten ausgewählt wurde – MOL, HOLAP oder ROLAP.  
  
## <a name="designing-aggregations"></a>Entwerfen von Aggregationen  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwendet einen hoch entwickelten Algorithmus, um Aggregationen für Vorausberechnungen auszuwählen, sodass andere Aggregationen schnell aus den im Voraus berechneten Werten ermittelt werden können. Wenn z. B. die Aggregationen für die Month-Ebene einer Time-Hierarchie im Voraus berechnet werden, erfordert die Berechnung für eine Quarter-Ebene nur das Zusammenfassen von drei Zahlen, was kaum Zeit in Anspruch nimmt. Dieses Verfahren spart Verarbeitungszeit und reduziert die Speicheranforderungen bei minimaler Auswirkung auf die Abfrageantwortzeit.  
  
 Der Aggregationsentwurfs-Assistent stellt Optionen bereit, mit denen Einschränkungen im Hinblick auf den Speicherplatz und den Prozentsatz für den Algorithmus angegeben werden können, sodass ein zufrieden stellender Kompromiss zwischen Abfrageantwortzeit und Speicheranforderungen erzielt wird. Der Algorithmus des Aggregationsentwurfs-Assistenten setzt jedoch voraus, dass alle möglichen Abfragen gleich wahrscheinlich sind. Der Verwendungsbasierte Optimierung-Assistent ermöglicht Ihnen das Anpassen des Aggregationsdesigns für eine Measuregruppe, indem die von Clientanwendungen gesendeten Abfragen analysiert werden. Mit dem Assistenten zum Optimieren der Aggregation eines Cubes können Sie die schnelle Antwortzeiten auf häufig gestellte Abfragen und weniger schnelle Antworten auf seltenere Abfragen ermöglichen, ohne den für den Cube benötigten Speicherplatz wesentlich zu beeinflussen.  
  
 Aggregationen werden mithilfe der Assistenten entworfen, sie werden jedoch dann berechnet, wenn die Partition, für die die Aggregationen entworfen werden, verarbeitet wird. Wenn die Struktur eines Cubes geändert wird, Daten den Quelltabellen eines Cubes hinzugefügt oder Daten in den Quelltabellen eines Cubes geändert werden, müssen nach der Aggregationserstellung die Aggregationen des Cubes normalerweise überprüft und der Cube erneut verarbeitet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Partition Speichermodi und Verarbeitung](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
  
