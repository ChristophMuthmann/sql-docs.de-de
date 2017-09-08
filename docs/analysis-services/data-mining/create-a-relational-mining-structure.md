---
title: Erstellen Sie eine relationale Miningstruktur | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], data mining
- data mining [Analysis Services], structure
- mining structures [Analysis Services], creating
- relational mining models [Analysis Services]
- OLAP mining models [Analysis Services]
ms.assetid: 5547d639-377d-4ca7-88fc-ce1f9e2babc5
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 82fa652f76c1818ef6538b379723e7f91c8482ab
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-relational-mining-structure"></a>Erstellen einer relationalen Miningstruktur
  Die meisten Data Mining-Modelle basieren auf relationalen Datenquellen. Die Vorteile, ein relationales Data Mining-Modell zu erstellen, bestehen darin, dass Sie Ad-hoc-Daten zusammenstellen sowie ein Modell trainieren und aktualisieren können, ohne dass die Komplexität gegeben ist, die beim Erstellen eines Cubes vorliegt.  
  
 Eine relationale Miningstruktur kann Daten aus ungleichartigen Quellen abrufen. Die Rohdaten können in Tabellen, Dateien oder relationalen Datenbanksystemen gespeichert werden, so lange die Daten als Teil der Datenquellensicht definiert werden können. Sie sollten z. B. eine relationale Miningstruktur verwenden, wenn die Daten in Excel, einem SQL Server Data Warehouse, einer SQL Server-Berichtsdatenbank oder aber in externen Quellen enthalten sind, auf die über die OLE DB- oder ODBC-Anbieter zugegriffen wird.  
  
 Dieses Thema bietet eine Übersicht darüber, wie der Data Mining-Assistent verwendet wird, um eine relationale Miningstruktur zu erstellen.  
  
 [Anforderungen](#BKMK_Relational_Structure)  
  
 [Prozess zum Erstellen einer relationalen Miningstruktur](#BKMK_Relational_Structure)  
  
 [So wählen Sie Datenquellen aus](#BKMK_ChooseRelData)  
  
 [So geben Sie Inhaltstyp und Datentyp an](#bkmk_ContentDataType)  
  
 [Warum und wie wird ein Dataset mit zurückgehaltenen Daten erstellt?](#bkmk_Holdout)  
  
 [Warum und wie wird Drillthrough aktiviert?](#BKMK_DrillThru)  
  
## <a name="requirements"></a>Anforderungen  
 Zunächst müssen Sie über eine vorhandene Datenquelle verfügen. Sie können mithilfe des Datenquellen-Designers eine Datenquelle einrichten, wenn diese nicht bereits vorhanden ist. Weitere Informationen finden Sie unter [Erstellen einer Datenquelle &#40;SSAS – mehrdimensional&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md).  
  
 Verwenden Sie danach den Datenquellensicht-Assistenten, um die erforderlichen Daten in einer einzelnen Datenquellensicht zusammenzustellen. Weitere Informationen darüber, wie Sie Daten mit Datenquellensichten auswählen, transformieren, filtern oder verwalten können, finden Sie unter [Datenquellsichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
##  <a name="BKMK_Relational_Structure"></a> Übersicht über den Prozess  
 Starten Sie den Data Mining-Assistenten, indem Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Knoten **Miningstrukturen** klicken und dann **Neue Miningstruktur hinzufügen**auswählen. Der Assistent führt Sie beim Erstellen der Struktur eines neuen relationalen Miningmodells durch folgende Schritte:  
  
1.  **Definitionsmethode auswählen**: Hier wählen Sie einen Datenquellentyp aus. Zudem wählen Sie **Aus relationaler Datenbank oder Data Warehouse**.  
  
2.  **Data Mining-Struktur erstellen**: Bestimmen Sie, ob Sie nur eine Struktur oder eine Struktur mit einem Miningmodell erstellen.  
  
     Sie wählen auch einen entsprechenden Algorithmus für das ursprüngliche Modell aus. Hilfestellung bei der Auswahl des besten Algorithmus für bestimmte Tasks finden Sie unter [Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
3.  **Datenquellensicht auswählen**: Wählen Sie eine Datenquellensicht aus, die beim Training des Modells verwendet werden soll. Die Datenquellensicht kann auch für Tests verwendete Daten oder nicht verknüpfte Daten enthalten. Sie wählen aus, welche Daten tatsächlich in der Struktur und im Modell verwendet werden. Sie können zu einem späteren Zeitpunkt auch Filter für die Daten anwenden.  
  
4.  **Tabellentypen angeben**: Wählen Sie die Tabelle aus, die die für die Analyse verwendeten Fälle enthält. Besonders bei den Datasets, die zur Erstellung von Market Basket-Modellen verwendet werden, können Sie auch eine verknüpfte Tabelle einbinden, um diese als geschachtelte Tabelle zu verwenden.  
  
     Für jede Tabelle müssen Sie den entsprechenden Schlüssel angeben, damit der Algorithmus weiß, wie ein eindeutiger Datensatz identifiziert wird. Außerdem müssen Sie die verknüpften Datensätze angeben, wenn Sie eine geschachtelte Tabelle hinzugefügt haben.  
  
     Weitere Informationen finden Sie unter [Mining Structure Columns](../../analysis-services/data-mining/mining-structure-columns.md).  
  
5.  **Trainingsdaten angeben**: Auf dieser Seite wählen Sie die *Falltabelle*aus, welche die Tabelle darstellt, die die wichtigsten Daten für die Analyse enthält.  
  
     Besonders bei jenen Datasets, die zur Erstellung von Market Basket-Modellen verwendet werden, können Sie auch eine verknüpfte Tabelle einbinden. Die Werte in dieser geschachtelten Tabelle werden als mehrfache Werte betrachtet, die sich alle auf eine einzelne Zeile (oder auf einen einzelnen Fall) in der Haupttabelle beziehen.  
  
6.  **Inhalt und Datentyp der Spalten angeben**: Für jede Spalte, die Sie in der Struktur verwenden, müssen Sie sowohl einen *Datentyp* als auch einen *Inhaltstyp*auswählen.  
  
     Der Assistent erkennt automatisch mögliche Datentypen. Sie müssen jedoch den vom Assistenten empfohlenen Datentyp nicht verwenden. Selbst wenn die Daten z. B. Zahlen enthalten, können diese für Kategoriedaten eventuell repräsentativ sein. Die von Ihnen als Schlüssel angegebenen Spalten werden automatisch dem richtigen Datentyp für den entsprechenden Modelltyp zugewiesen. Weitere Informationen finden Sie unter [Miningmodellspalten](../../analysis-services/data-mining/mining-model-columns.md) und [Datentypen &#40;Data Mining&#41;](../../analysis-services/data-mining/data-types-data-mining.md).  
  
     Der *Inhaltstyp* , den Sie für jede im Modell verwendete Spalte auswählen, teilt den Algorithmus mit, wie die Daten verarbeitet werden sollen.  
  
     Sie können sich z. B. dafür entscheiden, Zahlen zu diskretisieren anstatt sie als kontinuierliche Werte zu verwenden. Sie können auch beim Algorithmus anfragen, dass dieser den besten Inhaltstyp für die Spalte automatisch erkennt. Weitere Informationen finden Sie unter [Inhaltstypen &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
7.  **Testsatz erstellen**: Auf dieser Seite können Sie dem Assistenten mitteilen, wie viele Daten zum Testen des Modells verwendet werden sollen. Wenn die Daten mehrere Modelle unterstützen, empfiehlt es sich, ein zurückgehaltenes Dataset zu erstellen, sodass alle Modelle basierend auf den gleichen Daten getestet werden können.  
  
     Weitere Informationen finden Sie unter [Tests und Überprüfung &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md).  
  
8.  **Assistenten abschließen**: Auf dieser Seite geben Sie einen Namen für die neue Miningstruktur und das zugeordnete Miningmodell an und speichern die Struktur und das Modell.  
  
     Sie können außerdem einige wichtige Optionen je nach Modelltyp festlegen. Sie können z. B. Drillthrough für die Struktur aktivieren.  
  
     Zu diesem Zeitpunkt sind die Miningstruktur und das zugeordnete Modell nur Metadaten. Sie müssen beide verarbeiten, um Ergebnisse zu erhalten.  
  
##  <a name="BKMK_ChooseRelData"></a> So werden relationale Daten ausgewählt  
 Relationale Miningstrukturen können auf Daten basieren, die durch eine OLE DB-Datenquelle zur Verfügung gestellt werden. Wenn die Quelldaten in mehreren Tabellen enthalten sind, können Sie eine Datenquellensicht verwenden, um die von Ihnen benötigten Tabellen und Spalten an einem Ort zusammenzuführen.  
  
 Wenn die Tabellen 1:n-Beziehungen enthalten, haben Sie z. B. mehrere Kaufdatensätze für jeden Kunden, den Sie analysieren möchten. Sie können Tabellen hinzufügen und dann eine Tabelle als Falltabelle verwenden, wodurch Sie Daten für die zahlreichen Seiten der Beziehung als geschachtelte Tabelle verknüpfen können.  
  
 Die Daten in einer Miningstruktur werden von sämtlichen Komponenten abgeleitet, die in einer vorhandenen Datenquellensicht enthalten sind. Sie können Daten innerhalb der Datenquellensicht nach Bedarf ändern. Dabei können Sie Beziehungen oder abgeleitete Spalten hinzufügen, die in den zugrunde liegenden relationalen Daten unter Umständen nicht vorhanden sind. Sie können auch benannte Berechnungen oder Aggregationen innerhalb der Datenquellensicht erstellen. Diese Funktionen sind äußerst praktisch, wenn Sie keinen Einfluss auf die Anordnung der Daten in der Datenquelle haben oder wenn Sie mit unterschiedlichen Aggregationen der Daten für die Data Mining-Modelle experimentieren möchten.  
  
 Sie müssen nicht alle verfügbaren Daten verwenden. Sie können auswählen, welche Spalten Sie in die Miningstruktur einbinden möchten. Alle Modelle, die auf dieser Struktur basieren, können dann jene Spalten verwenden. Alternativ können Sie bestimmte Spalten für ein bestimmtes Modell als **Ignore** kennzeichnen. Sie können es den Benutzern eines Data Mining-Modells ermöglichen, ein Drilldown für die Ergebnisse des Miningmodells auszuführen, um die zusätzlichen Spalten der Miningstruktur anzuzeigen, die selbst nicht im Miningmodell enthalten sind.  
  
##  <a name="bkmk_ContentDataType"></a> So geben Sie Inhaltstyp und Datentyp an  
 Der Datentyp entspricht in großem Umfang den Datentypen, die Sie in SQL Server oder anderen Anwendungsschnittstellen spezifizieren: Datumsangaben und Uhrzeiten, Zahlen zu verschiedenen Größen, boolesche Werte, Text und andere diskrete Daten.  
  
 Inhaltstypen sind jedoch wichtig für Data Mining und wirken sich auf das Ergebnis der Analyse aus. Der Inhaltstyp teilt dem Algorithmus mit, was dieser mit den Daten tun soll: Sollen Zahlen in einer kontinuierlichen Skala verarbeitet oder klassifiziert werden? Wie viele potenziellen Werte sind vorhanden? Ist jeder Wert eindeutig? Wenn der Wert ein Schlüssel ist, welche Art von Schlüssel ist dieser dann? Gibt er Datums-/Uhrzeitwert, eine Sequenz oder eine andere Art von Schlüssel an?  
  
 Beachten Sie, dass die Auswahl des Datentyps die Auswahl der Inhaltstypen einschränken kann. Sie können z. B. keine Werte diskretisieren, die nicht numerisch sind. Wenn Sie den von Ihnen gewünschten Inhaltstyp nicht sehen können, so können Sie auf **Zurück** klicken, um zur Datentypseite zurückzukehren und es mit einem anderen Datentyp zu versuchen.  
  
 Sie müssen nicht darauf achten, ob Sie den Inhaltstyp falsch abrufen. Es ist sehr einfach, ein neues Modell zu erstellen und den Inhaltstyp innerhalb des Modells zu ändern, solange der neue Inhaltstyp vom in der Miningstruktur festgelegten Datentyp unterstützt wird. Eine übliche Vorgehensweise besteht darin, mehrere Modelle mit unterschiedlichen Inhaltstypen entweder als Experiment zu erstellen oder die Anforderungen eines anderen Algorithmus zu erfüllen.  
  
 Wenn die Daten z. B. eine Einkommensspalte enthalten, können Sie beim Verwenden des Microsoft Decision Trees-Algorithmus zwei verschiedene Modelle erstellen und die Spalte abwechselnd entweder mit fortlaufenden Nummern oder als diskrete Bereiche konfigurieren. Wenn Sie jedoch mit dem Microsoft Naive Bayes-Algorithmus ein Modell hinzufügen, sind Sie gezwungen, die Spalte ausschließlich in diskretisierte Werte zu ändern, da dieser Algorithmus keine fortlaufenden Nummern unterstützt.  
  
##  <a name="bkmk_Holdout"></a> Warum und wie werden Daten in Trainings- und Testsätze aufgeteilt?  
 Gegen Ende der Assistentenunterstützung müssen Sie sich entscheiden, ob die Daten in Trainings- oder Testsätze partitioniert werden. Die Möglichkeit, einen willkürlich entnommenen Anteil der Daten für den Test bereitzustellen, ist sehr vorteilhaft. Dadurch wird sichergestellt, dass für die Verwendung aller mit der neuen Miningstruktur verknüpften Miningmodelle ein konsistenter Satz an Testdaten zur Verfügung steht.  
  
> [!WARNING]  
>  Beachten Sie, dass diese Option nicht für alle Modelltypen verfügbar ist. Wenn Sie z. B. ein Planungsmodell erstellen, können Sie keine zurückgehaltenen Daten verwenden, da der Zeitreihenalgorithmus es erforderlich macht, dass in den Daten keine Lücken vorhanden sind. Eine Liste der Modelltypen, die Datasets für zurückgehaltene Daten unterstützen, finden Sie unter [Trainings- und Testdatasets](../../analysis-services/data-mining/training-and-testing-data-sets.md).  
  
 Um ein Dataset für zurückgehaltene Daten zu erstellen, geben Sie den Prozentsatz der Daten an, den Sie für Tests verwenden möchten. Alle verbleibenden Daten werden zu Trainingszwecken verwendet. Optional können Sie die maximale Anzahl von Fällen festlegen, die für Tests verwendet werden soll. Oder Sie legen einen Ausgangswert fest, der beim Starten des zufälligen Auswahlprozesses verwendet werden soll.  
  
 Die Definition des Testsatzes für zurückgehaltene Daten wird zusammen mit der Miningstruktur gespeichert. Dadurch steht, wenn Sie basierend auf der Struktur ein neues Modell erstellen, das Testdataset für die Bewertung der Genauigkeit des Modells immer zur Verfügung. Wenn Sie den Cache der Miningstruktur löschen, werden die Informationen darüber, welche Fälle für Trainings- und welche für Testzwecke verwendet werden, ebenfalls gelöscht.  
  
##  <a name="BKMK_DrillThru"></a> Warum und wie wird Drillthrough aktiviert?  
 Fast am Ende der Assistentenunterstützung haben Sie die Möglichkeit, *Drillthrough*zu aktivieren. Obwohl sie wichtig ist, kann diese Möglichkeit leicht übersehen werden. Mithilfe von Drillthrough können Sie Quelldaten in der Miningstruktur anzeigen, indem Sie das Miningmodell abfragen.  
  
 Warum ist dies nützlich? Es sei gegeben, dass Sie die Ergebnisse eines Clusteringmodells anzeigen und die Kunden ansehen möchten, die in einen bestimmten Cluster eingefügt werden. Mit Drillthrough können Sie Details wie etwa Kontaktinformationen anzeigen.  
  
> [!WARNING]  
>  Damit Sie Drillthrough verwenden können, müssen Sie es aktivieren, wenn Sie die Miningstruktur erstellen. Sie können zu einem späteren Zeitpunkt Drillthrough für Modelle aktivieren, indem Sie eine Eigenschaft für das Modell festlegen. Die Miningstrukturen machen es jedoch erforderlich, dass diese Option am Anfang festgelegt wird. Weitere Informationen finden Sie unter [Drillthroughabfragen &#40;Data Mining&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Designer](../../analysis-services/data-mining/data-mining-designer.md)   
 [Datamining-Assistenten &#40; Analysis Services – Datamining &#41;](../../analysis-services/data-mining/data-mining-wizard-analysis-services-data-mining.md)   
 [Miningmodelleigenschaften](../../analysis-services/data-mining/mining-model-properties.md)   
 [Eigenschaften für Miningstrukturen und Strukturspalten](../../analysis-services/data-mining/properties-for-mining-structure-and-structure-columns.md)   
 [Tasks und Anweisungen für Miningstrukturen](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
