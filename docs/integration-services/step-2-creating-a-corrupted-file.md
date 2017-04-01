---
title: "Schritt&#160;2: Erstellen einer besch&#228;digten Datei | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: cd0b18dc-66c3-4d88-86ef-8e40cb660fae
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Schritt&#160;2: Erstellen einer besch&#228;digten Datei
Um die Konfiguration und die Behandlung von Transformationsfehlern zu demonstrieren, müssen Sie eine Beispielflatfile erstellen, die beim Verarbeiten für eine Komponente einen Fehler erzeugt.  
  
In dieser Aufgabe erstellen Sie eine Kopie einer vorhandenen Beispielflatfile. Anschließend öffnen Sie die Datei im Editor und bearbeiten die **CurrencyID**-Spalte, um sicherzustellen, dass von ihr keine Übereinstimmung während der Transformationssuche produziert wird. Wenn die neue Datei verarbeitet wird, erzeugt der Suchfehler einen Fehler der Currency Key Lookup-Transformation, sodass auch der Rest des Pakets fehlschlägt. Nach dem Erstellen der beschädigten Beispieldatei führen Sie das Paket aus, um den vom Paket verursachten Fehler anzuzeigen.  
  
### So erstellen Sie eine beschädigte Beispielflatfile  
  
1.  Öffnen Sie in Editor oder einem anderen Texteditor die Datei Currency_VEB.txt.  
  
    Die Beispieldaten sind in den SSIS-Lektionspaketen enthalten. Um die Beispieldaten und die Lektionspakete herunterzuladen, gehen Sie wie folgt vor.  
  
    1.  Navigieren Sie zu [Integration Services Product Samples](http://go.microsoft.com/fwlink/?LinkID=267527).  
  
    2.  Klicken Sie auf die Registerkarte **DOWNLOADS**.  
  
    3.  Klicken Sie auf die Datei SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
2.  Suchen Sie mithilfe der Funktion des Texteditors zum Suchen und Ersetzen alle Instanzen von **VEB** und ersetzen Sie sie durch **BAD**.  
  
3.  Speichern Sie im gleichen Ordner wie die anderen Beispieldatendateien die geänderte Datei als **Currency_BAD.txt**.  
  
    > [!IMPORTANT]  
    > Speichern Sie **Currency_BAD.txt** im selben Ordner wie die anderen Beispieldatendateien.  
  
4.  Schließen Sie den Texteditor.  
  
### So überprüfen Sie das Auftreten eines Fehlers während der Laufzeit  
  
1.  Klicken Sie im Menü **Debuggen** auf **Debuggen starten**.  
  
    In der dritten Iteration des Datenflusses wird von der Lookup Currency Key-Transformation versucht, die Datei Currency_BAD.txt zu verarbeiten, und die Transformation erzeugt einen Fehler. Der Fehler der Transformation erzeugt einen Fehler des gesamten Pakets.  
  
2.  Klicken Sie im Menü **Debuggen** auf **Debuggen beenden**.  
  
3.  Klicken Sie auf der Entwurfsoberfläche auf die Registerkarte **Ausführungsergebnisse**.  
  
4.  Durchsuchen Sie das Protokoll und überprüfen Sie, ob der folgende nicht behandelte Fehler aufgetreten ist:  
  
    `[Lookup Currency Key[27]] Error: Row yielded no match during lookup.`  
  
    > [!NOTE]  
    > Die Zahl 27 ist die ID der Komponente. Dieser Wert wird zugewiesen, wenn Sie den Datenfluss erstellen. Der Wert in Ihrem Paket kann sich von diesem Wert unterscheiden.  
  
## Nächste Schritte  
[Schritt 3: Hinzufügen von Fehlerflussumleitungen](../integration-services/step-3-adding-error-flow-redirection.md)  
  
  
  
