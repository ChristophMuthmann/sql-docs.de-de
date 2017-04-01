---
title: "Ziel-Editor f&#252;r Rohdatendateien (Seite Verbindungs-Manager) | Microsoft Docs"
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
  - "sql13.dts.designer.rawfiledestinationconnectionmanager.f1"
ms.assetid: a0ec9643-3b44-4467-b855-f45ae4794f7f
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Ziel-Editor f&#252;r Rohdatendateien (Seite Verbindungs-Manager)
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
 Klicken Sie auf die Schaltfläche, um eine leere Rohdatendatei zu generieren, die nur die Spalten (Nur-Metadatendatei) enthält, ohne dass das Paket ausgeführt werden muss. Die Datei enthält die Spalten, die Sie auf der Seite **Spalten** von **Ziel-Editor für Rohdatendateien**ausgewählt haben. Sie können die Rohdatendatei-Quelle auf diese Nur-Metadaten-Datei verweisen.  
  
 Wenn Sie auf **Anfängliche Rohdatendatei generieren**klicken, wird ein Meldungsfeld angezeigt. Klicken Sie auf **OK** , um die Erstellung der Datei fortzusetzen. Klicken Sie auf **Abbrechen** , um eine andere Liste von Spalten auf der Seite **Spalten** auszuwählen.  
  
##  <a name="mapping"></a> Festlegen von Optionen auf der Registerkarte "Spalten"  
 **Verfügbare Eingabespalten**  
 Wählen Sie mindestens eine Eingabespalte aus, die in die Rohdatendatei geschrieben werden soll.  
  
 **Eingabespalte**  
 Dieser Tabelle wird automatisch eine Eingabespalte hinzugefügt, wenn Sie sie unter **Verfügbare Eingabespalten** auswählen. Alternativ können Sie die Eingabespalte direkt in dieser Tabelle auswählen.  
  
 **Ausgabealias**  
 Geben Sie einen anderen Namen an, der für die Ausgabespalte verwendet werden soll.  
  
## Siehe auch  
 [Rohdatendatei-Ziel](../../integration-services/data-flow/raw-file-destination.md)  
  
  