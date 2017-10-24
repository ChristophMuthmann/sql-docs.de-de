---
title: Lektion 9 Perspektiven erstellen | Microsoft Docs
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 55b0f0d0-1cdf-4876-9c3d-d0c848be3f5d
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 993cf02a47240c0a74667f6220c6b2dd5d6df86c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-8-create-perspectives"></a>Lektion 8: Erstellen von Perspektiven
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In dieser Lektion erstellen Sie eine Perspektive mit dem Namen Internet Sales. Eine Perspektive definiert eine sichtbare Teilmenge eines Modells, die fokussierte, unternehmensspezifische oder anwendungsspezifische Blickpunkte bereitstellt. Wenn ein Benutzer auf ein Modell mithilfe einer Perspektive herstellt, sehen sie nur die Modellobjekte (Tabellen, Spalten, Measures, Hierarchien und KPIs), als in der Perspektive definierten Felder.  
  
Die Internet Sales-Perspektive in dieser Lektion erstellten wird die DimCustomer-Tabellenobjekt. Wenn Sie eine Perspektive erstellen, die bestimmte Objekte aus der Sicht ausschließt, ist dieses Objekt immer noch im Modell vorhanden. Es ist jedoch in keiner Feldliste eines Berichterstellungsdiensts sichtbar. In berechneten Spalten und Measures können Berechnungen mit ausgeschlossenen Objektdaten ausgeführt werden, unabhängig davon, ob die Spalten und Measures in einer Perspektive enthalten sind.  
  
In dieser Lektion wird beschrieben, wie Sie Perspektiven erstellen und sich mit den Erstellungstools der Tabellenmodelle vertraut machen. Wenn Sie später dieses Modell aus, um zusätzliche Tabellen einzufügen erweitern, können Sie weitere Perspektiven, um verschiedene Blickpunkte des Modells, z. B. Inventur- und Sales definieren erstellen. Weitere Informationen finden Sie unter [Perspektiven](../analysis-services/tabular-models/perspectives-ssas-tabular.md).  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **5 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 7: Erstellen von Key Performance Indicators](../analysis-services/lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Erstellen von Perspektiven  
  
#### <a name="to-create-an-internet-sales-perspective"></a>So erstellen Sie eine Internet Sales-Perspektive  
  
1.  Klicken Sie auf die **Modell** Menü > **Perspektiven** > **erstellen und verwalten**.  
  
2.  Klicken Sie im Dialogfeld **Perspektiven** auf **Neue Perspektive**.  
  
3.  Doppelklicken Sie auf die **neue Perspektive** Spaltenüberschrift, und klicken Sie dann umbenennen **Internetverkäufe**.  
  
4.  Wählen Sie alle Tabellen *außer* **DimCustomer**.  
  
    ![als-tabellarische-lesson8-Perspektiven](../analysis-services/media/as-tabular-lesson8-perspectives.png)
  
    In einer späteren Lektion verwenden analysieren in Excel-Funktion Sie zum Testen dieser Perspektive. Der Excel-PivotTable-Feldliste enthält jede Tabelle außer der DimCustomer-Tabelle.  

## <a name="whats-next"></a>Wie geht es weiter?
Wechseln Sie zur nächsten Lektion: [Lektion 9: Erstellen von Hierarchien](../analysis-services/lesson-9-create-hierarchies.md).
  
  
  
  

