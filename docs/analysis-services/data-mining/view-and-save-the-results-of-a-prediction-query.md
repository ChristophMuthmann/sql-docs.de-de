---
title: Anzeigen und speichern Sie die Ergebnisse einer Vorhersageabfrage | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- prediction queries [Analysis Services]
- viewing prediction query results
- displaying prediction query results
- Mining Model Prediction [Analysis Services], viewing results
ms.assetid: abba4d24-3619-44c1-8279-88f27ad627d3
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8d0d16a2a5717514aa7d8faff1a1611bd74ef7a2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="view-and-save-the-results-of-a-prediction-query"></a>Anzeigen und Speichern der Ergebnisse einer Vorhersageabfrage
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Nachdem Sie in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mit dem Generator für Vorhersageabfragen eine Abfrage definiert haben, können Sie die Abfrage ausführen und die Abfrageergebnisse anzeigen, indem Sie zur Abfrageergebnissicht wechseln.  
  
 Sie können die Ergebnisse einer Vorhersageabfrage in einer Tabelle in jeder Datenquelle speichern, die in einem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt definiert ist. Sie können dabei entweder eine neue Tabelle erstellen oder die Abfrageergebnisse in einer bereits vorhandenen Tabelle speichern. Wenn Sie die Ergebnisse in einer vorhandenen Tabelle speichern, können Sie entweder die aktuell in der Tabelle gespeicherten Daten überschreiben lassen. Ansonsten werden die Abfrageergebnisse an die vorhandenen Daten in der Tabelle angehängt.  
  
### <a name="run-a-query-and-view-the-results"></a>Ausführen von Abfragen und Anzeigen von Ergebnissen  
  
1.  Klicken Sie auf der Symbolleiste der Registerkarte **Miningmodellvorhersage** im Data Mining-Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf **Ergebnis** .  
  
     Die Abfrageergebnissicht wird geöffnet, und die Abfrage wird ausgeführt. Die Ergebnisse werden im Viewer in einem Raster angezeigt.  
  
### <a name="save-the-results-of-a-prediction-query-to-a-table"></a>Speichern der Ergebnisse einer Vorhersageabfrage in einer Tabelle  
  
1.  Klicken Sie auf der Symbolleiste der Registerkarte **Miningmodellvorhersage** im Data Mining-Designer auf **Abfrageergebnis speichern**.  
  
     Das Dialogfeld **Ergebnis der Data Mining-Abfrage speichern** wird geöffnet.  
  
2.  Wählen Sie aus der **Datenquelle** -Liste eine Datenquelle aus, oder klicken Sie auf **Neu** , um eine neue Datenquelle zu erstellen.  
  
3.  Geben Sie im Feld **Tabellenname** den Namen der Tabelle ein. Wenn die Tabelle bereits vorhanden ist, können Sie das Kontrollkästchen **Überschreiben, falls vorhanden** aktivieren, um den bisherigen Inhalt der Tabelle mit den Abfrageergebnissen zu überschreiben. Wenn der Inhalt der Tabelle nicht überschrieben werden soll, dürfen Sie dieses Kontrollkästchen nicht aktivieren. Die neuen Abfrageergebnisse werden dann an die in der Tabelle vorhandenen Daten angehängt.  
  
4.  Wählen Sie unter **Zur Datenquellensicht hinzufügen** , wenn Sie die Tabelle zu einer Datenquellensicht hinzufügen wollen.  
  
5.  Klicken Sie auf **Speichern**.  
  
    > [!WARNING]  
    >  Wenn das Ziel keine hierarchischen Rowsets unterstützt, können Sie den Ergebnissen das FALTTENED-Schlüsselwort hinzufügen, um es als flache Tabelle zu speichern.  
  
  
