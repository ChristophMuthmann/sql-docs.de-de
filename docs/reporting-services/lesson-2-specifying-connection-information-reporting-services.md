---
title: 'Lektion 2: Angeben von Verbindungsinformationen (Reporting Services) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 05/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
caps.latest.revision: "53"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Active
ms.openlocfilehash: 344cc77269e09ab61806f2093220f834b72329b3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>Lektion 2: Angeben von Verbindungsinformationen (Reporting Services)
Nachdem Sie Ihrem Tutorial-Projekt in Lektion 1 einen paginierten Bericht von [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] hinzugefügt haben, müssen Sie eine *Datenquelle* erstellen. Bei dieser handelt es sich um Verbindungsinformationen, mit denen der Bericht auf Daten aus einer relationalen Datenbank, einer mehrdimensionalen Datenbank oder einer sonstigen Ressource zugreift.  
  
In dieser Lektion verwenden Sie die Beispieldatenbank [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] als Datenquelle. In diesem Tutorial wird davon ausgegangen, dass diese Datenbank in einer Standardinstanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] auf Ihrem lokalen Computer installiert ist.  
  
### <a name="to-set-up-a-connection"></a>So richten Sie eine Verbindung ein  
  
1.  Klicken Sie im **Berichtsdatenbereich** auf **Neu** und anschließend auf **Data Source**.  
Zum Anzeigen des **Berichtsdatenbereichs** klicken Sie im Menü **Ansicht** auf **Berichtsdaten**.  

    ![ssrs-table-tutorial-2-new-data-source](../reporting-services/media/ssrs-table-tutorial-2-new-data-source.png)
  
   2.  Geben Sie im Feld **Name**den Namen *AdventureWorks2014*ein.  
  
3.  Stellen Sie sicher, dass **Eingebettete Verbindung** aktiviert ist.  
  
4.  Wählen Sie unter **Typ**die Option **Microsoft SQL Server**aus.  
  
5.  Geben Sie für **Verbindungszeichenfolge**Folgendes ein:  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
     Bei dieser Verbindungszeichenfolge wird davon ausgegangen, dass [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], der Berichtsserver und die [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] -Datenbank zusammen auf dem lokalen Computer installiert sind und Sie über die Berechtigung verfügen, sich bei der [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] -Datenbank anzumelden. Wenn die AdventureWorks2014-Datenbank nicht auf dem lokalen Computer vorhanden ist, ändern Sie die Verbindungszeichenfolge, und ersetzen Sie *localhost* durch den Namen Ihrer Datenbankserverinstanz.
  
     >[!NOTE]  
    >Wenn Sie [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services oder eine benannte Instanz verwenden, muss die Verbindungszeichenfolge Instanzinformationen einschließen:  
    >  
    >`Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2014`  
    >  
    >Weitere Informationen zu Verbindungszeichenfolgen finden Sie unter: [Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
     
  
6.  Klicken Sie im linken Bereich auf **Anmeldeinformationen** , und klicken Sie auf **Windows-Authentifizierung verwenden (integrierte Sicherheit)**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)] Die Datenquelle **AdventureWorks2014** wird dem **Berichtsdatenbereich** hinzugefügt.  
![ssrs_adventureworks_datasource](../reporting-services/media/ssrs-adventureworks-datasource.png)  
## <a name="next-task"></a>Nächste Aufgabe  
Sie haben erfolgreich eine Verbindung mit der [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] -Beispieldatenbank definiert. Als Nächstes erstellen Sie den Bericht. Weitere Informationen finden Sie unter [Lektion 3: Definieren eines Datasets für den Tabellenbericht (Reporting Services)](../reporting-services/lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md).  
  
## <a name="see-also"></a>Siehe auch  
[Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
  

