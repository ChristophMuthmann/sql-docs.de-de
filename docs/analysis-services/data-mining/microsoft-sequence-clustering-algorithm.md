---
title: Microsoft Sequence Clustering-Algorithmus | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clusters [Analysis Services]
- algorithms [data mining]
- sequence clustering algorithms [Analysis Services]
- sequence [Analysis Services]
ms.assetid: ae779a1f-0adb-4857-afbd-a15543dff299
caps.latest.revision: "49"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 181b95753ac004aef4da9134ce46347c4cffa304
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="microsoft-sequence-clustering-algorithm"></a>Microsoft Sequence Clustering-Algorithmus
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering-Algorithmus ist ein eindeutiger Algorithmus, der mit dem Cluster Sequenzanalyse kombiniert. Mithilfe dieses Algorithmus können Sie Daten zu Ereignissen untersuchen, die durch *Sequenzen*verknüpft werden können. Der Algorithmus ermittelt die am häufigsten vorkommenden Sequenzen und führt dann ein Clustering identischer Sequenzen durch. Die folgenden Beispiele veranschaulichen die Arten von Sequenzen, die Sie als Daten für Machine Learning erfassen können, um Aufschluss über häufige Probleme oder Geschäftsszenarios zu erhalten:  
  
-   Clickstreams oder Klickpfade, die erstellt werden, wenn Benutzer navigieren oder eine Website durchsuchen  
  
-   Protokolle, in denen Ereignisse aufgeführt sind, die einem Vorfall vorausgehen, z.B. Festplattenfehler oder Serverdeadlocks  
  
-   Transaktionsdatensätze, die die Reihenfolge beschreiben, in der der Kunde seinem Onlineeinkaufswagen Waren hinzufügt  
  
-   Datensätze, die die Interaktionen von Kunden (oder Patienten) innerhalb von Zeiträumen verfolgen, um Dienstkündigungen oder andere schlechte Ergebnisse vorherzusagen  
  
 Dieser Algorithmus ähnelt dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Clustering-Algorithmus in vielerlei Hinsicht. Anstatt jedoch nach Clustern mit Fällen zu suchen, die ähnliche Attribute enthalten, sucht der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering-Algorithmus nach Clustern mit Fällen, die ähnliche Pfade in einer Sequenz enthalten.  
  
## <a name="example"></a>Beispiel  
 Die [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] Website sammelt Informationen darüber, welche Seiten die Benutzer besuchen Sie Website und die Reihenfolge, in der Seiten besucht werden. Da die Firma die Möglichkeit der Onlinebestellung bietet, müssen sich die Kunden bei der Site anmelden. Dadurch erhält die Firma Informationen zum Klickverhalten jedes einzelnen Kundenprofils. Mithilfe des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering-Algorithmus kann die Firma diese Daten verarbeiten und so Gruppen oder Cluster von Kunden ermitteln, die ähnliche Klickmuster oder -sequenzen aufweisen. Die Firma kann dann anhand dieser Cluster die Bewegungen der Benutzer auf der Website analysieren und diejenigen Seiten identifizieren, die am engsten mit dem Verkauf eines bestimmten Produkts verbunden sind. Außerdem lässt sich vorhersagen, welche Seiten mit der höchsten Wahrscheinlichkeit als Nächstes besucht werden.  
  
## <a name="how-the-algorithm-works"></a>Funktionsweise des Algorithmus  
 Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering-Algorithmus ist ein hybrider Algorithmus, der Clustering-Techniken mit Markov-Kettenanalysen verbindet, um Cluster und deren Sequenzen zu identifizieren.  Eines der Kennzeichen des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering-Algorithmus besteht in der Verwendung von Sequenzdaten. Diese Daten repräsentieren in der Regel eine Reihe von Ereignissen oder Statusübergängen in einem Dataset, wie z. B. eine Reihe von Produktkäufen oder Webklickfolgen eines bestimmten Benutzers. Um zu bestimmen, welche Sequenzen als Eingaben für das Clustering am besten geeignet sind, überprüft der Algorithmus alle Übergangswahrscheinlichkeiten und misst die Differenzen oder Abstände zwischen allen im Dataset möglichen Sequenzen. Nachdem der Algorithmus eine Liste der möglichen Sequenzen erstellt hat, verwendet er die Sequenzinformationen als Eingabe für das Clustering mit Erwartungsmaximierung (EM).  
  
 Eine ausführliche Beschreibung der Implementierung finden Sie unter [Microsoft Sequence Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
## <a name="data-required-for-sequence-clustering-models"></a>Anforderungen für Sequenzclustermodelle  
 Wenn Sie Daten für das Training von Sequenzclustermodellen aufbereiten, müssen Sie sich mit den Anforderungen des jeweiligen Algorithmus, dessen Anforderungen an die Daten und der Verwendung der Daten vertraut machen.  
  
 Für Sequenzclustermodelle gelten folgende Anforderungen:  
  
-   **Eine einzelne Schlüsselspalte:** Für ein Sequenzclustermodell ist ein Schlüssel erforderlich, der Datensätze identifiziert.  
  
-   **Eine Sequenzspalte** : Für Sequenzdaten muss das Modell über eine geschachtelte Tabelle verfügen, die eine Sequenz-ID-Spalte enthält. Die Sequenz-ID kann ein beliebiger sortierbarer Datentyp sein. Sie können beispielsweise eine Webseiten-ID, eine Ganzzahl oder eine Textzeichenfolge verwenden, solange die Spalte die Ereignisse in einer Sequenz identifiziert. Für jede Sequenz ist nur ein Sequenzbezeichner zulässig, und jedes Modell darf nur einen Sequenztyp enthalten.  
  
-   **Optionale nicht sequenzielle Attribute** : Der Algorithmus unterstützt das Hinzufügen anderer Attribute, die nicht mit dem Sequenzieren verknüpft sind. Diese Attribute können geschachtelte Spalten einschließen.  
  
 In dem zuvor erwähnten Beispiel der Website von [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] kann ein Sequenzclustermodell beispielsweise Auftragsinformationen als Falltabelle, demografische Daten über den Kunden des entsprechenden Auftrags als nicht sequenzielle Attribute und eine geschachtelte Tabelle mit der Sequenz, in der der Kunde die Website durchsucht hat oder Artikel in einen Einkaufswagen gelegt hat, als Sequenzinformationen beinhalten.  
  
 Ausführliche Informationen zu den in Sequenzclustermodellen unterstützten Inhaltstypen und Datentypen finden Sie im Abschnitt über Anforderungen unter [Technische Referenz für den Microsoft Sequence Clustering-Algorithmus](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
## <a name="viewing-a-sequence-clustering-model"></a>Anzeigen eines Sequenzclustermodells  
 Das von diesem Algorithmus erstellte Miningmodell enthält Beschreibungen der in den Daten am häufigsten vorkommenden Sequenzen. Zum Durchsuchen des Modells können Sie den **Microsoft Sequenzcluster-Viewer**verwenden. Wenn Sie ein Sequenzclustermodell anzeigen, zeigt Ihnen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cluster, die mehrere Übergänge enthalten. Sie können auch entsprechende statistische Daten anzeigen. Weitere Informationen finden Sie unter [Durchsuchen eines Modells mit dem Microsoft Sequenzcluster-Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md).  
  
 Wenn Sie detailliertere Informationen möchten, können Sie das Modell im [Microsoft Generic Content Tree Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)durchsuchen. Der für das Modell gespeicherte Inhalt umfasst die Verteilung der Werte an jedem Knoten, die Wahrscheinlichkeit jedes Clusters und Details zu den Übergängen. Weitere Informationen finden Sie unter [Mingingmodellinhalt von Sequence Clustering-Modellen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
## <a name="creating-predictions"></a>Erstellen von Vorhersagen  
 Nachdem das Modell trainiert wurde, werden die Ergebnisse als Mustersatz gespeichert. Anhand der Beschreibungen der häufigsten Sequenzen der Daten können Sie den wahrscheinlich nächsten Schritt in einer neuen Sequenz vorhersagen. Da der Algorithmus jedoch andere Spalten einschließt, eignet sich das entstandene Modell auch zum Identifizieren von Beziehungen zwischen Sequenzdaten und Eingaben, die nicht sequenziell sind. Wenn Sie dem Modell beispielsweise demografische Daten hinzufügen, können Sie Vorhersagen für bestimmte Gruppen von Kunden machen. Vorhersageabfragen können angepasst werden, um eine variable Anzahl von Vorhersagen oder aussagekräftige statistische Daten zurückzugeben.  
  
 Informationen zum Erstellen von Abfragen für ein Data Mining-Modell finden Sie unter [Data Mining-Abfragen](../../analysis-services/data-mining/data-mining-queries.md). Beispiele zur Verwendung von Abfragen in Verbindung mit einem Sequenzclustermodell finden Sie unter [Sequenz Clustering-Modellabfragebeispiele](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md).  
  
## <a name="remarks"></a>Hinweise  
  
-   Unterstützt nicht die Verwendung von PMML (Predictive Model Markup Language) zum Erstellen von Miningmodellen.  
  
-   Unterstützt Drillthrough.  
  
-   Unterstützt die Verwendung von OLAP-Miningmodellen und die Erstellung von Data Mining-Dimensionen.  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Microsoft Sequence Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [Sequence Clustering-Abfragebeispiele](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [Durchsuchen eines Modells mit dem Microsoft Sequence Cluster-Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
  
