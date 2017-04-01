---
title: "Lernprogramm: Verwenden der OData-Quelle | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2c64cf8b-5edb-48df-8ffe-697096258f71
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Lernprogramm: Verwenden der OData-Quelle
  Dieses Lernprogramm führt Sie schrittweise durch den Prozess, bei dem die Sammlung **Employees** aus dem OData-Beispieldienst **Northwind** (http://services.odata.org/V3/Northwind/Northwind.svc/) extrahiert und anschließend in eine Flatfile geladen wird.  
  
## 1. Erstellen eines Integration Services-Projekts  
  
1.  Starten Sie **SQL Server Data Tools** oder [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
2.  Klicken Sie auf **Datei**, zeigen Sie auf **Neu**, und klicken Sie auf **Projekt**.  
  
3.  Erweitern Sie im Dialogfeld **Neues Projekt** die Knoten **Installiert**, **Vorlagen**und **Business Intelligence**, und klicken Sie auf **Integration Services**.  
  
4.  Wählen Sie als Projekttyp **Integration Services-Projekt** aus.  
  
5.  Geben Sie einen **Namen** ein, und wählen Sie einen **Speicherort** für das Projekt aus. Klicken Sie anschließend auf **OK**.  
  
## 2. Hinzufügen und Konfigurieren einer OData-Quelle für das SSIS-Paket  
  
1.  Ziehen Sie einen **Datenflusstask** aus der **SSIS-Toolbox** auf die Entwurfsoberfläche der Ablaufsteuerung des SSIS-Pakets.  
  
2.  Klicken Sie auf die Registerkarte **Datenfluss** , oder doppelklicken Sie auf den neu hinzugefügten **Datenflusstask** , um die **Datenfluss-Entwurfsoberfläche**zu starten.  
  
3.  Ziehen Sie die **OData-Quelle** aus der Gruppe **Allgemein** in die **SSIS-Toolbox**. Beim erstmaligen Installieren der **OData-Quelle** wird sie unter der Gruppe **Allgemein** in der **SSIS-Toolbox**angezeigt.  
  
4.  Doppelklicken Sie auf die Komponente **OData-Quelle** , um das Dialogfeld **Quellen-Editor für OData** zu öffnen.  
  
5.  Klicken Sie auf **Neu…** , um einen neuen OData-Verbindungs-Manager hinzuzufügen.  
  
6.  Geben Sie die OData-Dienst-URL als **Speicherort des Dienstdokuments**ein. Hierbei kann es sich um die URL zum Dienstdokument oder zu einem bestimmten Feed oder einer bestimmten Entität handeln. Geben Sie für die Zwecke dieses Lernprogramms [http://services.odata.org/V3/Northwind/Northwind.svc/](http://services.odata.org/V3/Northwind/Northwind.svc/) ein.  
  
7.  Vergewissern Sie sich, dass als **Authentifizierung** der Typ **Windows-Authentifizierung** für den Zugriff auf den OData-Dienst ausgewählt ist. **Windows-Authentifizierung** ist standardmäßig ausgewählt. Wenn Sie die Standardauthentifizierung verwenden möchten, wählen Sie **Diesen Benutzernamen und dieses Kennwort verwenden**aus.  
  
8.  Klicken Sie für die Verbindung auf **Verbindung testen** , und klicken Sie auf **OK** , um eine Instanz des OData-Verbindungs-Managers zu erstellen.  
  
9. Vergewissern Sie sich im Dialogfeld **Quellen-Editor für OData** , dass **Auflistung** für die Option **Auflistung für Ressourcenpfad verwenden** ausgewählt ist.  
  
10. Wählen Sie in der Dropdownliste **Auflistung** den Eintrag **Employees**aus.  
  
11. Geben Sie zusätzliche OData-Abfrageoptionen oder Filter für **Abfrageoptionen**ein. Ex. $orderby=CompanyName&$top=100. Geben Sie für die Zwecke dieses Lernprogramms **$top=5** ein.  
  
12. Klicken Sie auf **Vorschau** , um eine Vorschau der Daten aufzurufen.  
  
13. Klicken Sie im linken Navigationsbereich auf **Spalten** , um zur Seite **Spalten** zu wechseln.  
  
14. Wählen Sie in **Verfügbare externe Spalten**die Spalten **EmployeeID**, **FirstName** und **LastName** aus, indem Sie die Kontrollkästchen aktivieren.  
  
15. Klicken Sie auf **OK** , um das Dialogfeld **Quellen-Editor für OData** zu schließen.  
  
## 3. Hinzufügen eines Flatfileziels und Testen der Projektmappe  
  
1.  Ziehen Sie nun ein **Flatfileziel** aus der **SSIS-Toolbox** auf die Entwurfsoberfläche Datenfluss unter die Komponente **OData-Quelle**.  
  
2.  Verbindung Sie über einen blauen Pfeil die Komponente **OData-Quelle** mit der Komponente **Flatfileziel** .  
  
3.  Doppelklicken Sie auf **Flatfileziel**. Das Dialogfeld **Ziel-Editor für Flatfiles** wird geöffnet.  
  
4.  Klicken Sie im Dialogfeld **Ziel-Editor für Flatfiles** auf **Neu** , um einen neuen Verbindungs-Manager für Flatfiles zu erstellen.  
  
5.  Wählen Sie im Dialogfeld **Flatfileformat** die Option **Mit Trennzeichen**aus. Das Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** wird geöffnet.  
  
6.  Geben Sie im Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** für **Dateiname** den Namen **c:\Employees.txt** ein.  
  
7.  Klicken Sie im linken Navigationsbereich auf **Spalten**. Auf dieser Seite können Sie die Daten in der Vorschau anzeigen.  
  
8.  Klicken Sie auf OK, um das Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** zu schließen.  
  
9. Klicken Sie im Dialogfeld **Ziel-Editor für Flatfiles** im linken Navigationsbereich auf **Zuordnungen** . Überprüfen Sie die Zuordnungen.  
  
10. Klicken Sie auf OK, um das Dialogfeld **Ziel-Editor für Flatfiles** zu schließen.  
  
11. Kompilieren Sie das SSIS-Paket, und führen Sie es aus. Überprüfen Sie, ob die Ausgabedatei mit ID, Vorname und Nachname für fünf Mitarbeiter aus dem OData-Feed erstellt wird.  
  
  