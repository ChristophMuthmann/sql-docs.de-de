---
title: Hierarchien | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e3e50e89-f85d-485b-a271-1e0550520212
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5ce337737331ecf67332e4f012993a28d59715b0
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="hierarchies"></a>Hierarchien
  Hierarchien in Tabellenmodellen sind Metadaten, mit denen Beziehungen zwischen mindestens zwei Spalten in einer Tabelle definiert werden. Hierarchien können getrennt von anderen Spalten in der Feldliste eines Berichterstellungsclients angezeigt werden, damit Clientbenutzer einfacher darin navigieren und sie in einen Bericht aufnehmen können.  
  
##  <a name="bkmk_benefits"></a> Vorteile  
 Tabellen können Dutzende oder sogar Hunderte Spalten mit ungewöhnlichen Spaltennamen und ohne erkennbare Reihenfolge enthalten. Dies kann dazu führen, dass die Spalten in den Feldlisten von Berichterstellungsclients ungeordnet dargestellt werden, und es Benutzern erschweren, Daten zu finden und in einen Bericht einzuschließen. Hierarchien können eine übersichtliche und intuitive Ansicht einer andernfalls komplexen Datenstruktur bereitstellen.  
  
 Beispielsweise können Sie in einer Datumstabelle eine Kalenderhierarchie erstellen. Calendar Year wird als übergeordnetes Element oberster Ebene verwendet und verfügt über die untergeordneten Ebenen Month, Week und Day (Calendar Year->Month->Week->Day). In dieser Hierarchie wird eine logische Beziehung zwischen Kalenderjahr und Tag dargestellt. Anschließend kann ein Clientbenutzer das Kalenderjahr aus einer Feldliste auswählen, um alle Ebenen in eine PivotTable einzuschließen, oder die Hierarchie erweitern und nur bestimmte Ebenen auswählen, die in die PivotTable eingeschlossen werden sollen.  
  
 Da jede Ebene in einer Hierarchie eine Darstellung einer Spalte in einer Tabelle darstellt, kann die Ebene umbenannt werden. Das Umbenennen von Hierarchieebenen ist keine exklusive Hierarchiefunktion (da jede Spalte in einem Tabellenmodell umbenannt werden kann), erleichtert dem Benutzer jedoch das Auffinden und Einschließen von Ebenen in einen Bericht. Durch das Umbenennen einer Ebene wird die Spalte, auf die die Ebene verweist, nicht umbenannt. Die Ebene ist einfach besser zu identifizieren. Im Beispiel mit der Calendar Year-Hierarchie wurden in der Date-Tabelle der Datensicht die Spalten CalendarYear, CalendarMonth, CalendarWeek und CalendarDay in Calendar Year, Month, Week und Day umbenannt, damit sie leichter identifiziert werden können. Das Umbenennen von Ebenen bietet den zusätzlichen Vorteil, dass die Konsistenz von Berichten verbessert wird, da es weniger wahrscheinlich ist, dass Benutzer die Spaltennamen ändern müssen, um deren Lesbarkeit in PivotTables, Diagrammen usw. zu erhöhen.  
  
 Hierarchien können in Perspektiven aufgenommen werden. Eine Perspektive definiert sichtbare Teilmengen eines Modells, die fokussierte, unternehmensspezifische oder anwendungsspezifische Blickpunkte des Modells bereitstellen. Beispielsweise könnten Benutzer in einer Perspektive nur Zugriff auf eine anzeigbare Liste (Hierarchie) derjenigen Datenelemente erhalten, die für ihre spezifischen Berichterstellungsanforderungen erforderlich sind. Weitere Informationen finden Sie unter [Perspektiven](../../analysis-services/tabular-models/perspectives-ssas-tabular.md).  
  
 Hierarchien sollen nicht als Sicherheitsmechanismus verwendet werden, sondern als Tool zur Verbesserung der Benutzerfreundlichkeit. Die gesamte Sicherheit einer bestimmten Hierarchie wird vom zugrunde liegenden Modell geerbt. Hierarchien gewähren keinen Zugriff auf Modellobjekte, auf die ein Benutzer nicht bereits Zugriff hat. Die Sicherheit der Modelldatenbank muss geklärt werden, damit der Zugriff auf Objekte im Modell durch eine Hierarchie ermöglicht werden kann. Sicherheitsrollen können verwendet werden, um Modellmetadaten und Daten zu sichern. Weitere Informationen finden Sie unter [Rollen](../../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
##  <a name="bkmk_define"></a> Defining hierarchies  
 Hierarchien werden mit dem Modell-Designer in der Diagrammsicht erstellt und verwaltet. Das Erstellen und Verwalten von Hierarchien in der Datensicht des Modell-Designers wird nicht unterstützt. Um den Modell-Designer in der Diagrammsicht anzuzeigen, klicken Sie auf das Menü **Modell** , zeigen auf **Modellansicht**und klicken dann auf **Diagrammsicht**.  
  
 Um eine Hierarchie zu erstellen, klicken Sie mit der rechten Maustaste auf eine Spalte, die Sie als übergeordnete Ebene angeben möchten, und klicken Sie dann auf **Hierarchie erstellen**. Sie können eine beliebige Anzahl von Spalten (innerhalb einer einzelnen Tabelle) mithilfe einer Mehrfachauswahl einschließen oder später Spalten als untergeordnete Ebenen hinzufügen, indem Sie auf die Spalten klicken und sie in die übergeordnete Ebene ziehen. Bei der Auswahl mehrerer Spalten werden sie automatisch entsprechend ihrer Kardinalität angeordnet. Sie können die Reihenfolge ändern, indem Sie auf eine Spalte (Ebene) klicken und sie an eine andere Position ziehen, oder indem Sie die Navigationssteuerelemente Nach oben und Nach unten im Kontextmenü verwenden. Wenn Sie eine Spalte als untergeordnete Ebene hinzufügen, können Sie die automatische Erkennung nutzen, indem Sie die Spalte ziehen und auf der übergeordneten Ebene ablegen.  
  
 Eine Spalte kann in mehreren Hierarchien angezeigt werden. Hierarchien können keine spaltenfremden Objekte wie Measures oder KPIs enthalten. Eine Hierarchie kann auf Spalten aus nur einer Tabelle basieren. Wenn Sie ein Measure zusammen mit mindestens einer Spalte auswählen oder wenn Sie Spalten aus mehreren Tabellen auswählen, ist der Befehl **Hierarchie erstellen** im Kontextmenü deaktiviert. Zum Hinzufügen einer Spalte aus einer anderen Tabelle verwenden Sie die RELATED DAX-Funktion, um eine berechnete Spalte hinzuzufügen, die auf die Spalte der verknüpften Tabelle verweist. Die Funktion verwendet die folgende Syntax: `=RELATED(TableName[ColumnName])`. Weitere Informationen finden Sie im Thema zur RELATED-Funktion.  
  
 Neue Hierarchien erhalten standardmäßig den Namen hierarchy 1, hierarchy 2 usw. Sie sollten Hierarchienamen so ändern, dass die Über-/Unterordnungsbeziehung eindeutig zugeordnet werden kann, sodass sie für Benutzer besser zu identifizieren sind.  
  
 Nachdem Sie Hierarchien erstellt haben, können Sie deren Wirksamkeit mit der Funktion In Excel analysieren testen. Weitere Informationen finden Sie unter [in Excel analysieren](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
##  <a name="bkmk_related_tasks"></a> Verwandte Aufgaben  
  
|Task|Description|  
|----------|-----------------|  
|[Erstellen und Verwalten von Hierarchien](../../analysis-services/tabular-models/create-and-manage-hierarchies-ssas-tabular.md)|Beschreibt, wie Hierarchien mit dem Modell-Designer in der Diagrammsicht erstellt und verwaltet werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Designer für tabellarische Modelle](../../analysis-services/tabular-models/tabular-model-designer-ssas.md)   
 [Perspektiven](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
