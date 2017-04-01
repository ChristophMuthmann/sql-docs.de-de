---
title: "Durchsuchen von Daten in einer Datenquellensicht (Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Durchsuchen von Daten [Analysis Services]"
  - "Datenquellensichten (Analysis Services), Durchsuchen von Daten"
  - "Anzeigen von Quelldaten"
ms.assetid: 2c922c35-fbcb-45b2-96b1-c7a846d8b419
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 34
---
# Durchsuchen von Daten in einer Datenquellensicht (Analysis Services)
  Sie können das Dialogfeld **Daten durchsuchen** im Datenquellensicht-Designer von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] verwenden, um Daten für eine Tabelle, eine Sicht oder eine benannte Abfrage in einer Datenquellensicht (data source view; DSV) zu durchsuchen. Wenn Sie die Daten im Datenquellensicht-Designer durchsuchen, können Sie den Inhalt jeder Datenspalte in einer ausgewählten Tabelle, Sicht oder benannten Abfrage anzeigen. Das Anzeigen des tatsächlichen Inhalts hilft Ihnen, zu bestimmen, ob alle Spalten benötigt werden, ob benannte Berechnungen erforderlich sind, um Benutzerfreundlichkeit und Zweckmäßigkeit zu erhöhen, und ob vorhandene benannte Berechnungen oder benannte Abfragen die erwarteten Werte zurückgeben.  
  
 Zum Anzeigen von Daten müssen Sie über eine aktive Verbindung mit der Datenquelle bzw. den Datenquellen für das ausgewählte Objekt in der Datenquellensicht verfügen. Alle benannten Berechnungen in einer Tabelle werden ebenfalls in der Abfrage gesendet.  
  
 Die in einem tabellarischen Format zurückgegebenen Daten, die sortiert und kopiert werden können. Klicken Sie auf die Spaltenüberschriften, um die Zeilen nach dieser Spalte erneut zu sortieren. Sie können auch Daten im Raster hervorheben und STRG+C drücken, um die Auswahl in die Zwischenablage zu kopieren.  
  
 Sie können zudem die Stichprobenmethode und die Anzahl für die Stichprobe steuern. Standardmäßig werden die obersten 5000 Zeilen zurückgegeben.  
  
## So durchsuchen Sie Daten oder ändern Stichprobenoptionen  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das Projekt, oder stellen Sie eine Verbindung mit der Datenbank her, das bzw. die die Datenquellensicht enthält, in der Sie Daten durchsuchen möchten.  
  
2.  Erweitern Sie im Projektmappen-Explorer den Ordner **Datenquellensichten**, und doppelklicken Sie anschließend auf die Datenquellensicht.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Tabelle, Sicht oder benannte Abfrage, die die anzuzeigenden Daten enthält, und klicken Sie anschließend auf **Daten durchsuchen**.  
  
     Die Datenquelle, die der Tabelle, Sicht oder benannten Abfrage in der Datenquellensicht zugrunde liegt, sind Abfragen, und das Ergebnis wird auf der Registerkarte **\<Objektname>-Tabelle durchsuchen** angezeigt.  
  
4.  Klicken Sie auf der Symbolleiste **\<Objektname>-Tabelle durchsuchen** auf das Symbol **Stichprobenoptionen**.  
  
     Das Dialogfeld **Optionen zum Durchsuchen von Daten** wird geöffnet. In diesem Dialogfeld können Sie die Stichprobenmethode (mehr oder weniger Datensätze als die Standardstichprobengröße von 5000 Zeilen) oder die Anzahl für die Stichprobe angeben.  
  
5.  Klicken Sie nach Bedarf auf **OK** oder **Abbrechen** .  
  
6.  Wenn Sie eine neue Stichprobe der Daten nehmen möchten, klicken Sie auf der Symbolleiste **\<Objektname>-Tabelle durchsuchen** auf **Neue Datenstichproben**.  
  
## Siehe auch  
 [Datenquellsichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  