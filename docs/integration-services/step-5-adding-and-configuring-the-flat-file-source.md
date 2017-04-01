---
title: "Schritt 5: Hinzuf&#252;gen und Konfigurieren der Flatfilequelle | Microsoft Docs"
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
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
caps.latest.revision: 20
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Schritt 5: Hinzuf&#252;gen und Konfigurieren der Flatfilequelle
In dieser Aufgabe fügen Sie Ihrem Paket eine Flatfilequelle hinzu und konfigurieren sie. Eine Flatfilequelle ist eine Datenflusskomponente, die Metadaten verwendet, die durch einen Flatfile-Verbindungs-Manager definiert werden, um das Format und die Struktur der Daten anzugeben, die aus der Flatfile durch einen Transformationsprozess extrahiert werden. Die Flatfilequelle kann zum Extrahieren von Daten aus einer einzigen Flatfile konfiguriert werden, indem die Dateiformatdefinition verwendet wird, die durch den Flatfile-Verbindungs-Manager zur Verfügung gestellt wird.  
  
Für dieses Lernprogramm konfigurieren Sie die Flatfilequelle zum Verwenden des **Sample Flat File Source Data** -Verbindungs-Managers, den Sie vorher erstellt haben.  
  
### So fügen Sie eine Flatfilequellen-Komponente hinzu  
  
1.  Öffnen Sie den **Datenfluss**-Designer, indem Sie entweder auf den **Extract Sample Currency Data**-Datenflusstask doppelklicken, oder indem Sie auf die Registerkarte **Datenfluss** klicken.  
  
2.  Erweitern Sie in der **SSIS-Toolbox** die Option **Weitere Quellen**, und ziehen Sie anschließend **Flatfilequelle** auf die Entwurfsoberfläche der Registerkarte **Datenfluss**.  
  
3.  Klicken Sie auf der **Datenfluss**-Entwurfsoberfläche mit der rechten Maustaste auf die neu hinzugefügte **Flatfilequelle**, klicken Sie auf **Umbenennen**, und ändern Sie den Namen zu **Extract Sample Currency Data**.  
  
4.  Doppelklicken Sie auf die Flatfilequelle, um das Dialogfeld Quellen-Editor für Flatfiles zu öffnen.  
  
5.  Wählen Sie im Feld **Verbindungs-Manager für Flatfiles** den Eintrag **Sample Flat File Source Data**aus.  
  
6.  Klicken Sie auf **Spalten** , und überprüfen Sie, ob die Namen der Spalten ordnungsgemäß sind.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Klicken Sie mit der rechten Maustaste auf die Flatfilequelle, und klicken Sie auf **Eigenschaften**.  
  
9. Überprüfen Sie im Eigenschaftenfenster, ob die **LocaleID**-Eigenschaft auf **Englisch (USA)** festgelegt ist.  
  
## Nächste Aufgabe in der Lektion  
[Schritt 6: Hinzufügen und Konfigurieren von Suchtransformationen](../integration-services/step-6-adding-and-configuring-the-lookup-transformations.md)  
  
## Siehe auch  
[Flatfilequelle](../integration-services/data-flow/flat-file-source.md)  
[Verbindungs-Manager-Editor für Flatfiles &#40;Seite „Allgemein“&#41;](../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)  
  
  
  
