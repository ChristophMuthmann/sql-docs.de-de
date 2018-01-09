---
title: Durchsuchen von Daten in einer Datenquellensicht (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
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
- exploring data [Analysis Services]
- data source views [Analysis Services], exploring data
- viewing source data
ms.assetid: 2c922c35-fbcb-45b2-96b1-c7a846d8b419
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0245eee4ac1b2b874145fa29f9b659b057977f16
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="explore-data-in-a-data-source-view-analysis-services"></a>Durchsuchen von Daten in einer Datenquellensicht (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Sie können die **Daten durchsuchen** im Datenquellensicht-Designers im Dialogfeld [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] zum Durchsuchen von Daten für eine Tabelle, Sicht oder benannten Abfrage in einer Datenquelle anzeigen (DSV). Wenn Sie die Daten im Datenquellensicht-Designer durchsuchen, können Sie den Inhalt jeder Datenspalte in einer ausgewählten Tabelle, Sicht oder benannten Abfrage anzeigen. Das Anzeigen des tatsächlichen Inhalts hilft Ihnen, zu bestimmen, ob alle Spalten benötigt werden, ob benannte Berechnungen erforderlich sind, um Benutzerfreundlichkeit und Zweckmäßigkeit zu erhöhen, und ob vorhandene benannte Berechnungen oder benannte Abfragen die erwarteten Werte zurückgeben.  
  
 Zum Anzeigen von Daten müssen Sie über eine aktive Verbindung mit der Datenquelle bzw. den Datenquellen für das ausgewählte Objekt in der Datenquellensicht verfügen. Alle benannten Berechnungen in einer Tabelle werden ebenfalls in der Abfrage gesendet.  
  
 Die in einem tabellarischen Format zurückgegebenen Daten, die sortiert und kopiert werden können. Klicken Sie auf die Spaltenüberschriften, um die Zeilen nach dieser Spalte erneut zu sortieren. Sie können auch Daten im Raster hervorheben und STRG+C drücken, um die Auswahl in die Zwischenablage zu kopieren.  
  
 Sie können zudem die Stichprobenmethode und die Anzahl für die Stichprobe steuern. Standardmäßig werden die obersten 5000 Zeilen zurückgegeben.  
  
## <a name="to-browse-data-or-change-sampling-options"></a>So durchsuchen Sie Daten oder ändern Stichprobenoptionen  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das Projekt, oder stellen Sie eine Verbindung mit der Datenbank her, das bzw. die die Datenquellensicht enthält, in der Sie Daten durchsuchen möchten.  
  
2.  Erweitern Sie im Projektmappen-Explorer den Ordner **Datenquellensichten** , und doppelklicken Sie anschließend auf die Datenquellensicht.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Tabelle, Sicht oder benannte Abfrage, die die anzuzeigenden Daten enthält, und klicken Sie anschließend auf **Daten durchsuchen**.  
  
     Die Datenquelle zugrunde liegenden der Tabelle, Sicht oder benannten Abfrage in der Datenquellensicht handelt es sich Abfragen und die Ergebnisse werden in der **Durchsuchen \<Objektname > Tabelle** Registerkarte.  
  
4.  Auf der **Durchsuchen \<Objektname > Tabelle** -Symbolleiste klicken Sie auf die **Samplingoptionen** Symbol.  
  
     Das Dialogfeld **Optionen zum Durchsuchen von Daten** wird geöffnet. In diesem Dialogfeld können Sie die Stichprobenmethode (mehr oder weniger Datensätze als die Standardstichprobengröße von 5000 Zeilen) oder die Anzahl für die Stichprobe angeben.  
  
5.  Klicken Sie nach Bedarf auf **OK** oder **Abbrechen** .  
  
6.  Um die Daten neu berechnen, klicken Sie auf **Resample Daten** auf die **Durchsuchen \<Objektname > Tabelle** Symbolleiste.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenquellsichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
