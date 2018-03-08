---
title: Analysis Services Tutorial Lektion 8 erstellen Perspektiven | Microsoft Docs
description: Beschreibt, wie Perspektiven in Analysis Services Tutorial-Projekt zu erstellen.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: 3b28d60cd5e1fc4050e72cd4ac56b2db882cbafa
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="create-perspectives"></a>Erstellen von Perspektiven

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In dieser Lektion erstellen Sie eine Internet Sales-Perspektive. Eine Perspektive definiert eine sichtbare Teilmenge eines Modells, die fokussierte, unternehmensspezifische oder anwendungsspezifische Blickpunkte bereitstellt. Wenn ein Benutzer auf ein Modell mithilfe einer Perspektive herstellt, sehen sie nur die Modellobjekte (Tabellen, Spalten, Measures, Hierarchien und KPIs), als in der Perspektive definierten Felder. Weitere Informationen finden Sie unter [Perspektiven](../tabular-models/perspectives-ssas-tabular.md).
  
Die Internet Sales-Perspektive, die Sie in dieser Lektion erstellen schließt das Objekt der DimCustomer-Tabelle. Wenn Sie eine Perspektive, die bestimmte Objekte aus der Sicht ausschließt erstellen, ist dieses Objekt immer noch im Modell vorhanden. Allerdings ist es nicht in einer Feldliste von berichtserstellungsclients angezeigt. In berechneten Spalten und Measures können Berechnungen mit ausgeschlossenen Objektdaten ausgeführt werden, unabhängig davon, ob die Spalten und Measures in einer Perspektive enthalten sind.  
  
In dieser Lektion wird beschrieben, wie Sie Perspektiven erstellen und sich mit den Erstellungstools der Tabellenmodelle vertraut machen. Wenn Sie später dieses Modell aus, um zusätzliche Tabellen einzufügen erweitern, können Sie weitere Perspektiven, um verschiedene Blickpunkte des Modells, z. B. Inventur- und Sales definieren erstellen.  
  
Geschätzte Zeit zum Abschließen dieser Lektion: **fünf Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  

Dieser Artikel ist Teil eines Lernprogramms zur tabellenmodellierung, das in Reihenfolge absolviert werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 7: Erstellen von Key Performance Indicators](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Erstellen von Perspektiven  
  
#### <a name="to-create-an-internet-sales-perspective"></a>So erstellen Sie eine Internet Sales-Perspektive  
  
1.  Klicken Sie auf die **Modell** Menü > **Perspektiven** > **erstellen und verwalten**.  
  
2.  Klicken Sie im Dialogfeld **Perspektiven** auf **Neue Perspektive**.  
  
3.  Doppelklicken Sie auf die **neue Perspektive** Spaltenüberschrift, und klicken Sie dann umbenennen **Internetverkäufe**.  
  
4.  Wählen Sie die Tabellen *außer* **DimCustomer**.  
  
    ![as-lesson8-perspectives](../tutorial-tabular-1400/media/as-lesson8-perspectives.png)
  
    In einer späteren Lektion verwenden Sie Funktion in Excel analysieren dieser Perspektive zu testen. Der Excel-PivotTable-Feldliste enthält jede Tabelle außer der DimCustomer-Tabelle.  

## <a name="whats-next"></a>Wie geht es weiter?

[Lektion 9: Erstellen von Hierarchien](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md).
  
  
  
  
