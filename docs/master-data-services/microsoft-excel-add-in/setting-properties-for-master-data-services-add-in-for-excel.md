---
title: "Festlegen von Eigenschaften f&#252;r das Master Data Services-Add-In f&#252;r Microsoft Excel | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cab1c662-5d40-4c16-9f5c-36ff9608810b
caps.latest.revision: 8
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 8
---
# Festlegen von Eigenschaften f&#252;r das Master Data Services-Add-In f&#252;r Microsoft Excel
  Die Einstellungen des Master Data Services-Add-Ins für Excel bestimmen, wie Daten aus MDS in das Excel-Add-In geladen werden und wie Daten aus dem Excel-Add-In in MDS veröffentlicht werden.  
  
 Öffnen Sie **Excel**, klicken Sie auf das Menü **Masterdaten** und anschließend auf **Einstellungen**, um die Einstellungen für das Excel-Add-In vorzunehmen. Jeder mit Zugriff auf Excel kann diese Einstellungen ändern. Die Einstellungen gelten für den Computer, auf dem Excel geöffnet ist.  
  
## Einstellungen für das Excel-Add-In  
  
||||  
|-|-|-|  
|Registerkarte und Abschnitt|Einstellung|Description|  
|Einstellungen: Veröffentlichen|Dialogfeld **Veröffentlichen und mit Anmerkung versehen** beim Veröffentlichen anzeigen|Verwenden Sie diese Option, um das Dialogfeld **Veröffentlichen und mit Anmerkung versehen** anzuzeigen, nachdem Sie auf **Veröffentlichen**geklickt haben, um eine einzelne Anmerkung für alle Änderungen einzugeben oder eine Anmerkung für jede Änderung einzugeben.<br /><br /> Deaktivieren Sie die Option, um anzugeben, dass der Veröffentlichungsprozess ohne Anzeige des Dialogfelds **Veröffentlichen und mit Anmerkung versehen** initiiert wird. Sie erhalten keine Gelegenheit, eine Anmerkung einzugeben.|  
|Einstellungen: Version|Versionsauswahl|Wählen Sie die Version der Masterdaten aus, die in das Excel-Add-In geladen werden. Mögliche Werte sind:<br /><br /> **Keine** – die Version ist standardmäßig auf keine Version festgelegt<br /><br /> **Älteste** – standardmäßig ist die älteste Version festgelegt, oder **Neueste** – standardmäßig ist die neueste Version festgelegt.|  
|Einstellungen: Protokollierung|Ausführliche Protokollierung aktivieren|Aktivieren Sie die Protokollierung für das Laden von Masterdaten aus MDS in das Excel-Add-In, sodass das Ergebnis jedes Befehls im Dienst protokolliert wird.|  
|Einstellungen: Telemetrie|Telemetriedatensammlung aktivieren|Aktivieren Sie die Telemetrie, um die Qualität, Zuverlässigkeit und Leistung des Excel-Add-Ins für [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] zu verbessern.|  
|Einstellungen: Batchverarbeitungsgröße|Anzahl der zu ladenden Zellen|Wählen Sie eine Zahl aus, um anzugeben, wie viele Tausende von Zellen in einem Batch geladen werden, der vom MDS-Server in Excel geladen wird. Der Standardwert lautet 50.000 Zellen.|  
|Einstellungen: Batchverarbeitungsgröße|Anzahl der zu veröffentlichenden Zellen|Wählen Sie eine Zahl aus, um anzugeben, wie viele Tausende von Zellen in einem Batch veröffentlicht werden, der von Excel an den Server zurückgegeben wird. Der Standardwert lautet 50.000 Zellen.|  
|Einstellungen: Zur Liste sicherer Server hinzugefügte Server|Auswahl aufheben|Klicken Sie, um die Liste der Verbindungen zu löschen, die als sicher gekennzeichnet wurden, als die zugeordnete Shortcutabfragedatei geöffnet wurde.|  
|Daten: Filter|Filterwarnung für große Datasets anzeigen|Klicken Sie, um eine Warnung anzuzeigen, wenn das Dataset, das aus MDS in Excel geladen wird, die maximale Anzahl der Zeilen oder Spalten überschreitet.|  
|Daten: Filter|Maximale Zeilenanzahl|Wählen Sie den Schwellenwert für die Anzahl der zu ladenden Zeilen aus, bei dessen Überschreitung eine Filterwarnung ausgegeben wird.|  
|Daten: Filter|Maximale Spaltenanzahl|Wählen Sie den Schwellenwert für die Anzahl der zu ladenden Spalten aus, bei dessen Überschreitung eine Filterwarnung ausgegeben wird.|  
|Daten: Zellenformat|Zellenfarbe ändern bei: Geänderte Attributwerte|Klicken Sie, um anzugeben, dass die Farbe einer Zelle geändert wird, wenn sich der Attributwert in dieser Zelle ändert, während Sie die Excel-Add-In-Tabelle mit neuen Daten aus dem MDS-Repository aktualisieren.|  
|Daten: Zellenformat|Zellenfarbe ändern bei: Elemente werden hinzugefügt|Klicken Sie, um anzugeben, dass die Farbe der Zellen einer Zeile geändert wird, wenn der Zeile ein neues Element hinzugefügt wird, während Sie die Excel-Add-In-Tabelle mit neuen Daten aus dem MDS-Repository aktualisieren.|  
|Daten: Zellenformat|Anzeigeformat|Wählen Sie das bevorzugte Format für die Anzeige der Werte domänenbasierter Attribute. Die Optionen sind Code {Name}, Code und Name {Code}.|  
  
  