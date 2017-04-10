---
title: "Ziel-Editor f&#252;r Rohdatendateien (Seite Spalten) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.rawfiledestinationcolumns.f1"
ms.assetid: 37f61d0b-1269-42ee-94ab-011cbaac63e9
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Ziel-Editor f&#252;r Rohdatendateien (Seite Spalten)
  Verwenden Sie den Ziel-Editor für Rohdatendateien zum Konfigurieren des Rohdatendatei-Ziels, um Rohdaten in eine Datei zu schreiben.  
  
 **Was möchten Sie tun?**  
  
-   [Öffnen des Ziel-Editors für Rohdatendateien](#open)  
  
-   [Festlegen der Optionen auf der Registerkarte "Verbindungs-Manager"](#connection)  
  
-   [Festlegen von Optionen auf der Registerkarte "Spalten"](#mapping)  
  
##  <a name="open"></a> Öffnen des Ziel-Editors für Rohdatendateien  
  
1.  Fügen Sie das Rohdatendatei-Ziel in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einem [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]-Paket hinzu.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Komponente, und klicken Sie anschließend auf **Bearbeiten**.  
  
##  <a name="connection"></a> Festlegen der Optionen auf der Registerkarte "Verbindungs-Manager"  
 **Zugriffsmodus**  
 Wählen Sie aus, wie der Dateiname angegeben wird. Wählen Sie **Dateiname** aus, um den Dateinamen und Pfad direkt einzugeben, oder **Dateiname aus Variable** , um eine Variable anzugeben, die den Dateinamen enthält.  
  
 **Dateiname** oder **Variablenname**  
 Geben Sie den Namen und Pfad der Rohdatendatei ein, oder wählen Sie die Variable aus, die den Dateinamen enthält.  
  
 **Schreiboption**  
 Wählen Sie die Methode aus, die zum Erstellen und Schreiben in die Datei verwendet wird.  
  
 **Generieren einer anfänglichen Rohdatendatei**  
 Klicken Sie auf die Schaltfläche, um eine leere Rohdatendatei zu generieren, die nur die Spalten (Nur-Metadatendatei) enthält, ohne dass das Paket ausgeführt werden muss. Sie können die Rohdatendatei-Quelle auf die Nur-Metadaten-Datei verweisen.  
  
 Wenn Sie auf die Schaltfläche klicken, wird eine Liste der Spalten angezeigt. Sie können auf "Abbrechen" klicken und die Spalten ändern, oder klicken Sie auf "OK", um das Erstellen der Datei fortzusetzen.  
  
##  <a name="mapping"></a> Festlegen von Optionen auf der Registerkarte "Spalten"  
 **Verfügbare Eingabespalten**  
 Wählen Sie mindestens eine Eingabespalte aus, die in die Rohdatendatei geschrieben werden soll.  
  
 **Eingabespalte**  
 Dieser Tabelle wird automatisch eine Eingabespalte hinzugefügt, wenn Sie sie unter **Verfügbare Eingabespalten** auswählen. Alternativ können Sie die Eingabespalte direkt in dieser Tabelle auswählen.  
  
 **Ausgabealias**  
 Geben Sie einen anderen Namen an, der für die Ausgabespalte verwendet werden soll.  
  
## Siehe auch  
 [Rohdatendatei-Ziel](../../integration-services/data-flow/raw-file-destination.md)  
  
  