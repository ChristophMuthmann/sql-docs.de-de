---
title: 'Lernprogramm: Verwenden der OData-Quelle | Microsoft Docs'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2c64cf8b-5edb-48df-8ffe-697096258f71
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: cbdc4a2e0719e65e378d232c5abcb5404e8342f1
ms.contentlocale: de-de
ms.lasthandoff: 08/23/2017

---
# <a name="tutorial-using-the-odata-source"></a>Lernprogramm: Verwenden der OData-Quelle
  Dieses Lernprogramm führt Sie schrittweise durch den Prozess, bei dem die Sammlung **Employees** aus dem OData-Beispieldienst **Northwind** (http://services.odata.org/V3/Northwind/Northwind.svc/) extrahiert und anschließend in eine Flatfile geladen wird.  
  
## <a name="1-create-an-integration-services-project"></a>1. Erstellen Sie ein Integration Services-Projekt  
  
1.  Starten Sie **SQL Server Data Tools** oder [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
2.  Klicken Sie auf **Datei**, zeigen Sie auf **Neu**, und klicken Sie auf **Projekt**.  
  
3.  Erweitern Sie im Dialogfeld **Neues Projekt** die Knoten **Installiert**, **Vorlagen**und **Business Intelligence**, und klicken Sie auf **Integration Services**.  
  
4.  Wählen Sie als Projekttyp **Integration Services-Projekt** aus.  
  
5.  Geben Sie einen **Namen** ein, und wählen Sie einen **Speicherort** für das Projekt aus. Klicken Sie anschließend auf **OK**.  
  
## <a name="2-add-and-configure-an-odata-source"></a>2. Hinzufügen und Konfigurieren einer OData-Quelle 
  
1.  Ziehen Sie einen **Datenflusstask** aus der **SSIS-Toolbox** auf die Entwurfsoberfläche der Ablaufsteuerung des SSIS-Pakets.  
  
2.  Klicken Sie auf die **Datenfluss** Registerkarte aus, oder doppelklicken Sie auf die **Data Flow Task** auf die Entwurfsoberfläche Datenfluss zu öffnen.  
  
3.  Ziehen Sie die **OData-Quelle** aus der Gruppe **Allgemein** in die **SSIS-Toolbox**.
  
4.  Doppelklicken Sie auf die **OData-Quelle** Komponente zum Starten der **Quellen-Editor für OData-** (Dialogfeld).  
  
5.  Klicken Sie auf **Neu…** , um einen neuen OData-Verbindungs-Manager hinzuzufügen.  
  
6.  Geben Sie die OData-Dienst-URL als **Speicherort des Dienstdokuments**ein. Diese URL kann es sich um die URL zum dienstdokument oder zu einem bestimmten Feed oder die Entität sein. Im Rahmen dieses Lernprogramms, geben Sie die URL zum dienstdokument: [http://services.odata.org/V3/Northwind/Northwind.svc/](http://services.odata.org/V3/Northwind/Northwind.svc/).  
  
7.  Vergewissern Sie sich, dass als **Authentifizierung** der Typ **Windows-Authentifizierung** für den Zugriff auf den OData-Dienst ausgewählt ist. **Windows-Authentifizierung** ist standardmäßig ausgewählt.  
  
8.  Klicken Sie auf **Verbindung testen** testet die Verbindung, und klicken Sie auf **OK** zum Abschließen der Erstellung einer Instanz des OData-Verbindungs-Managers.  
  
9. Vergewissern Sie sich im Dialogfeld **Quellen-Editor für OData** , dass **Auflistung** für die Option **Auflistung für Ressourcenpfad verwenden** ausgewählt ist.  
  
10. Aus der **Auflistung** Dropdown-Liste **Mitarbeiter**.  
  
11. Geben Sie zusätzliche OData-Abfrageoptionen oder Filter für **Abfrageoptionen**ein. Beispiel: `$orderby=CompanyName&$top=100`. Geben Sie im Rahmen dieses Lernprogramms `$top=5`.  
  
12. Klicken Sie auf **Vorschau** , um eine Vorschau der Daten aufzurufen.  
  
13. Klicken Sie im linken Navigationsbereich auf **Spalten** , um zur Seite **Spalten** zu wechseln.  
  
14. Wählen Sie in **Verfügbare externe Spalten**die Spalten **EmployeeID**, **FirstName** und **LastName** aus, indem Sie die Kontrollkästchen aktivieren.  
  
15. Klicken Sie auf **OK** , um das Dialogfeld **Quellen-Editor für OData** zu schließen.  
  
## <a name="3-add-and-configure-a-flat-file-destination"></a>3. Fügen Sie hinzu und konfigurieren Sie ein Flatfileziel
  
1.  Ziehen Sie nun ein **Flatfileziel** aus der **SSIS-Toolbox** auf die Entwurfsoberfläche Datenfluss unter die Komponente **OData-Quelle**.  
  
2.  Verbindung Sie über einen blauen Pfeil die Komponente **OData-Quelle** mit der Komponente **Flatfileziel** .  
  
3.  Doppelklicken Sie auf **Flatfileziel**. Das Dialogfeld **Ziel-Editor für Flatfiles** wird geöffnet.  
  
4.  Klicken Sie im Dialogfeld **Ziel-Editor für Flatfiles** auf **Neu** , um einen neuen Verbindungs-Manager für Flatfiles zu erstellen.  
  
5.  Wählen Sie im Dialogfeld **Flatfileformat** die Option **Mit Trennzeichen**aus. Sie sehen die **Dateiverbindungs-Manager-Editor für Flatfiles** (Dialogfeld).  
  
6.  In der **Dateiverbindungs-Manager-Editor für Flatfiles** im Dialogfeld für die **Dateiname**, geben Sie `c:\Employees.txt`.  
  
7.  Klicken Sie im linken Navigationsbereich auf **Spalten**. Auf dieser Seite können Sie die Daten in der Vorschau anzeigen.  
  
8.  Klicken Sie auf OK, um das Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** zu schließen.  
  
9. Klicken Sie im Dialogfeld **Ziel-Editor für Flatfiles** im linken Navigationsbereich auf **Zuordnungen** . Überprüfen Sie die Zuordnungen.  
  
10. Klicken Sie auf OK, um das Dialogfeld **Ziel-Editor für Flatfiles** zu schließen.  

## <a name="4-run-the-package"></a>4. Führen Sie das Paket
Führen Sie das SSIS-Paket. Stellen Sie sicher, dass die Ausgabedatei, mit der ID, Vorname erstellt wird und Nachname für fünf Mitarbeiter aus dem OData-feed.
  
  

