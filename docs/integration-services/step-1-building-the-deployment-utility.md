---
title: "Schritt 1: Erstellen des Bereitstellungs-Hilfsprogramms | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 1ff4dcff-89b3-4b99-a725-5f7963e98abf
caps.latest.revision: 21
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Schritt 1: Erstellen des Bereitstellungs-Hilfsprogramms
In dieser Aufgabe konfigurieren und erstellen Sie ein Bereitstellungsprogramm für das Deployment Tutorial-Projekt.  
  
Vor dem Erstellen des Bereitstellungshilfsprogramms müssen Sie die Eigenschaften des Deployment Tutorial-Projekts ändern. Sie können diese Eigenschaften im Dialogfeld **Deployment Tutorial-Eigenschaftenseiten** konfigurieren. In diesem Dialogfeld müssen Sie die Fähigkeit aktivieren, Konfigurationen während der Bereitstellung zu aktualisieren, und angeben, dass beim Erstellungsvorgang ein Bereitstellungshilfsprogramm generiert werden soll. Nach dem Festlegen der Eigenschaften erstellen Sie das Projekt.  
  
[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] stellt eine Reihe von Fenstern zum Debuggen von Paketen bereit. Sie können Fehler-, Warn- und Informationsmeldungen anzeigen, den Status von Paketen zur Laufzeit nachverfolgen oder den Fortschritt und die Ergebnisse von Erstellungsvorgängen anzeigen. In dieser Lektion verwenden Sie das Ausgabefenster, um den Fortschritt und die Ergebnisse beim Erstellen des Bereitstellungshilfsprogramms anzuzeigen.  
  
### So legen Sie die Eigenschaften des Bereitstellungshilfsprogramms fest  
  
1.  Wenn [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] noch nicht geöffnet ist, klicken Sie auf **Start**, zeigen Sie auf **Alle Programme**, zeigen Sie auf **Microsoft SQL Server 2005**, und klicken Sie dann auf **Business Intelligence Development Studio**.  
  
2.  Klicken Sie im Menü **Datei** auf **Öffnen** > **Projekt/Projektmappe**. Wählen Sie den Ordner **Deployment Tutorial** aus, klicken Sie auf **Öffnen** und anschließend doppelt auf **Deployment Tutorial.sln**.  
  
3.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf „Deployment Tutorial“ und anschließend auf **Eigenschaften**.  
  
4.  Erweitern Sie im Dialogfeld **Deployment Tutorial-Eigenschaftenseiten** den Knoten Konfigurationseigenschaften, und klicken Sie auf Bereitstellungshilfsprogramm.  
  
5.  Überprüfen Sie im rechten Bereich des Dialogfelds **Deployment Tutorial-Eigenschaftenseiten** , ob **AllowConfigurationChanges** auf **true**festgelegt ist, legen Sie **CreateDeploymentUtility** auf **true**fest, und aktualisieren Sie optional den Standardwert von **DeploymentOutputPath**.  
  
6.  Klicken Sie auf **OK**.  
  
### So erstellen Sie das Bereitstellungshilfsprogramm  
  
1.  Klicken Sie im Projektmappen-Explorer auf **Deployment Tutorial**.  
  
2.  Klicken Sie im Menü **Ansicht** auf **Ausgabe**. Das Ausgabefenster befindet sich standardmäßig in der unteren linken Ecke von [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
3.  Klicken Sie im Menü **Erstellen** auf **Deployment Tutorial erstellen**.  
  
4.  Überprüfen Sie im Ausgabefenster die folgenden Informationen:  
  
    Erstellung gestartet: SQL Integration Services-Projekt: Inkrementell ...  
  
    Bereitstellungshilfsprogramm wird erstellt...  
  
    Das Bereitstellungshilfsprogramm wurde erstellt.  
  
    Erstellung abgeschlossen -- 0 Fehler, 0 Warnungen  
  
    ========== Erstellen: 0 erfolgreich, Fehler bei 0, 1 aktuell, 0 übersprungen ==========  
  
5.  Klicken Sie im Menü **Datei** auf **Beenden**. Wenn Sie zum Speichern der Änderungen an Deployment Tutorial-Elementen aufgefordert werden, klicken Sie auf **Ja**.  
  
## Nächste Aufgabe in der Lektion  
[Schritt 2: Überprüfen des Bereitstellungspakets](../integration-services/step-2-verifying-the-deployment-bundle.md)  
  
## Siehe auch  
[Erstellen eines Bereitstellungs-Hilfsprogramms](../integration-services/packages/create-a-deployment-utility.md)  
  
  
  
