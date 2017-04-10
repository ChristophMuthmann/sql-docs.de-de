---
title: "Lektion 2: Angeben von Verbindungsinformationen (Reporting Services) | Microsoft Docs"
ms.custom: ""
ms.date: "05/23/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
caps.latest.revision: 53
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 51
---
# Lektion 2: Angeben von Verbindungsinformationen (Reporting Services)
Nachdem Sie dem Tutorial-Projekt einen Bericht hinzugefügt haben, müssen Sie eine *Datenquelle* erstellen. Bei dieser handelt es sich um Verbindungsinformationen, mit denen der Bericht auf Daten aus einer relationalen Datenbank, einer mehrdimensionalen Datenbank oder einer sonstigen Ressource zugreift.  
  
In dieser Lektion verwenden Sie die Beispieldatenbank [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] als Datenquelle. In diesem Tutorial wird davon ausgegangen, dass diese Datenbank in der Standardinstanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] auf Ihrem lokalen Computer installiert ist.  
  
### So richten Sie eine Verbindung ein  
  
1.  Klicken Sie im **Berichtsdatenbereich** auf **Neu** und anschließend auf **Datenquelle**.  
Zum Anzeigen des **Berichtsdatenbereichs** klicken Sie im Menü **Ansicht** auf **Berichtsdaten**.  
  
   2.  Geben Sie im Feld **Name** den Namen *Adventureworks2014* ein.  
  
3.  Stellen Sie sicher, dass **Eingebettete Verbindung** aktiviert ist.  
  
4.  Wählen Sie unter **Typ** die Option **Microsoft SQL Server** aus.  
  
5.  Geben Sie für **Verbindungszeichenfolge** Folgendes ein:  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
Bei dieser Verbindungszeichenfolge wird davon ausgegangen, dass [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], der Berichtsserver und die [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)]-Datenbank zusammen auf dem lokalen Computer installiert sind und Sie über die Berechtigung verfügen, sich bei der [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)]-Datenbank anzumelden. Wenn die AdventureWorks2014-Datenbank nicht auf dem lokalen Computer vorhanden ist, ändern Sie die Verbindungszeichenfolge, und Ersetzen Sie *Localhost* mit dem Namen Ihrer Datenbankserverinstanz.
   
  
 > [!NOTE]  
 > Wenn Sie [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services oder eine benannte Instanz verwenden, muss die Verbindungszeichenfolge Instanzinformationen einschließen:  
 >   
 > `Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2014`  
 >   
 > Weitere Informationen zu Verbindungszeichenfolgen finden Sie unter:  
 > *  [Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
    > * [Datenquelleneigenschaften (Dialogfeld), Allgemein](../Topic/Data%20Source%20Properties%20Dialog%20Box,%20General.md)  
        
  
6.  Klicken Sie im linken Bereich auf **Anmeldeinformationen**, und klicken Sie auf **Windows-Authentifizierung verwenden (integrierte Sicherheit)**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)] Die Datenquelle [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] wird dem **Berichtsdatenbereich** hinzugefügt.  
![ssrs_adventureworks_datasource](../reporting-services/media/ssrs-adventureworks-datasource.png)  
## Nächste Aufgabe  
Sie haben erfolgreich eine Verbindung mit der [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)]-Beispieldatenbank definiert. Als Nächstes erstellen Sie den Bericht. Weitere Informationen finden Sie unter [Lektion 3: Definieren eines Datasets für den Tabellenbericht &#40;Reporting Services&#41;](../reporting-services/lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md).  
  
## Siehe auch  
[Datenquelleneigenschaften (Dialogfeld), Allgemein](../Topic/Data%20Source%20Properties%20Dialog%20Box,%20General.md)  
[Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
  
