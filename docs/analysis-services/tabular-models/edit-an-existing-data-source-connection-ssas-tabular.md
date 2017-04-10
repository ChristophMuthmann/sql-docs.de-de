---
title: "Bearbeiten einer vorhandenen Datenquellenverbindung (SSAS – tabellarisch) | Microsoft Docs"
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
f1_keywords: 
  - "sql13.asvs.bidtoolset.selexistconn.f1"
ms.assetid: 97e63f18-a01d-4c91-a411-e7e6d40a0647
caps.latest.revision: 13
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 13
---
# Bearbeiten einer vorhandenen Datenquellenverbindung (SSAS – tabellarisch)
  In diesem Thema wird beschrieben, wie Sie die Eigenschaften einer vorhandenen Datenquellenverbindung in einem tabellarischen Modell bearbeiten können.  
  
 Nachdem Sie eine Verbindung mit einer externen Datenquelle erstellt haben, können Sie diese Verbindung später wie folgt ändern:  
  
-   Sie können die Verbindungsinformationen, einschließlich der verwendeten Quelle (Datei, Feed oder Datenbank), die Verbindungseigenschaften oder andere anbieterspezifische Verbindungsoptionen ändern.  
  
-   Sie können Tabellen- und Spaltenzuordnungen ändern und Verweise auf Spalten löschen, die nicht mehr verwendet werden.  
  
-   Sie können die Tabellen, Sichten oder Spalten ändern, die aus der externen Datenquelle abgerufen werden.  
  
## Ändern einer Verbindung  
 In diesem Verfahren wird beschrieben, wie eine Datenquellenverbindung einer Datenbank geändert wird. Einige Optionen zum Arbeiten mit Datenquellen sind vom Datenquellentyp abhängig. Diese Unterschiede sollten jedoch leicht zu erkennen sein.  
  
#### So ändern Sie die von einer aktuellen Verbindung verwendete externe Datenquelle  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]im Menü **Modell** auf **Vorhandene Verbindungen**.  
  
2.  Wählen Sie die Datenquellenverbindung aus, die Sie ändern möchten, und klicken Sie dann auf **Bearbeiten**.  
  
3.  Klicken Sie im Dialogfeld **Verbindung bearbeiten** auf **Durchsuchen** , um eine andere Datenbank vom gleichen Typ, aber mit einem anderen Namen oder Speicherort, zu suchen.  
  
     Sobald Sie die Datenbankdatei ändern, wird eine Meldung angezeigt, die Sie darüber informiert, dass Sie die Tabellen speichern und aktualisieren müssen, um die neuen Daten anzuzeigen.  
  
4.  Klicken Sie auf **Speichern**und dann auf **Schließen**.  
  
5.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]auf das **Modell**, und klicken Sie dann auf **Verarbeiten**und **Alles verarbeiten**.  
  
     Die Tabellen werden mit der neuen Datenquelle, jedoch mit der ursprünglichen Datenauswahl, neu verarbeitet.  
  
    > [!NOTE]  
    >  Wenn die neue Datenquelle zusätzliche Tabellen enthält, die in der ursprünglichen Datenquelle nicht vorhanden waren, müssen Sie die geänderte Verbindung erneut öffnen und die Tabellen hinzufügen.  
  
## Bearbeiten von Tabellen- und Spaltenzuordnungen (Bindungen)  
 In diesem Verfahren wird beschrieben, wie die Zuordnungen bearbeitet werden, nachdem eine Datenquelle geändert wurde.  
  
#### So bearbeiten Sie Spaltenzuordnungen, wenn sich eine Datenquelle ändert  
  
1.  Wählen Sie im Modell-Designer eine Tabelle aus.  
  
2.  Klicken Sie im Menü **Tabelle** auf **Tabelleneigenschaften**.  
  
     Der Name der ausgewählten Tabelle wird im Feld **Tabellenname** angezeigt. Das Feld **Quellname** enthält den Namen der Tabelle in der externen Datenquelle. Wenn die Spalten in der Quelle und im Modell nicht identisch sind, können Sie zwischen den beiden Sätzen von Spaltennamen wechseln, indem Sie die Optionen **Quelle** oder **Modell**auswählen.  
  
3.  Um die Tabelle zu ändern, die als Datenquelle verwendet wird, wählen Sie für **Quellname**eine andere Tabelle als die derzeitige Tabelle aus.  
  
4.  Ändern Sie die Spaltenzuordnungen nach Bedarf:  
  
    1.  Um Spalten hinzuzufügen, die in der Quelle vorhanden sind, aber nicht im Modell, aktivieren Sie das Kontrollkästchen neben dem entsprechenden Spaltennamen.  
  
         Die tatsächlichen Daten werden bei der nächsten Aktualisierung in das Modell geladen.  
  
    2.  Wenn einige Spalten im Modell nicht mehr in der aktuellen Datenquelle verfügbar sind, wird im Infobereich eine Meldung angezeigt, in der die ungültigen Spalten aufgelistet sind. Weitere Schritte sind nicht erforderlich.  
  
5.  Klicken Sie auf **Speichern** , um die Änderungen auf das Modell anzuwenden.  
  
     Wenn Sie den aktuellen Satz von Tabelleneigenschaften speichern, werden Sie u. U. in einer Meldung darauf hingewiesen, dass die Tabellen verarbeitet werden müssen. Klicken Sie auf **Verarbeiten** , um aktualisierte Daten in das Modell zu laden.  
  
## Siehe auch  
 [Verarbeiten von Daten &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/process-data-ssas-tabular.md)   
 [Unterstützte Datenquellen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
  