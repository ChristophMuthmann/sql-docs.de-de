---
title: Durchsuchen von Daten in einer Datenquellensicht (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4d509e2f4f23218eb5ea7a104e33160deab69cef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="explore-data-in-a-data-source-view-analysis-services"></a>Durchsuchen von Daten in einer Datenquellensicht (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Sie können das Dialogfeld **Daten durchsuchen** im Datenquellensicht-Designer von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] verwenden, um Daten für eine Tabelle, eine Sicht oder eine benannte Abfrage in einer Datenquellensicht (data source view; DSV) zu durchsuchen. Wenn Sie die Daten im Datenquellensicht-Designer durchsuchen, können Sie den Inhalt jeder Datenspalte in einer ausgewählten Tabelle, Sicht oder benannten Abfrage anzeigen. Das Anzeigen des tatsächlichen Inhalts hilft Ihnen, zu bestimmen, ob alle Spalten benötigt werden, ob benannte Berechnungen erforderlich sind, um Benutzerfreundlichkeit und Zweckmäßigkeit zu erhöhen, und ob vorhandene benannte Berechnungen oder benannte Abfragen die erwarteten Werte zurückgeben.  
  
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
  
  
