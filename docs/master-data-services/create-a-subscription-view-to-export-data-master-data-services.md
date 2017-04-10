---
title: "Erstellen einer Abonnementsicht zum Exportieren von Daten (Master Data Services) | Microsoft Docs"
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
helpviewer_keywords: 
  - "Abonnementsichten [Master Data Services], Erstellen"
  - "Erstellen von Abonnementsichten [Master Data Services]"
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 10
---
# Erstellen einer Abonnementsicht zum Exportieren von Daten (Master Data Services)
  Erstellen Sie eine Abonnementsicht, um Master Data Services-Daten in Abonnementsysteme zu exportieren. Erstellen Sie eine Ansicht der Daten in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Datenbank.  
  
## Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die entsprechende Berechtigung für den Zugriff auf den Funktionsbereich **Integrationsmanagement** verfügen. Weitere Informationen finden Sie unter [funktionale Bereichsberechtigungen & #40; Master Data Services & #41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren & #40; Master Data Services & #41;](../master-data-services/administrators-master-data-services.md).  
  
### So erstellen und bearbeiten Sie eine Abonnementsicht  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Integrationsmanagement**.  
  
2.  Klicken Sie auf der Menüleiste auf **Sichten erstellen**.  
  
3.  Auf der **Abonnementsichten** auf **Hinzufügen** eine Ansicht erstellen, oder klicken Sie auf **Bearbeiten** um eine Ansicht zu bearbeiten. Auf der rechten Seite wird ein Panel angezeigt.  
  
4.  In der **Abonnementsicht erstellen** Bereich, in den **Namen** Geben Sie einen Namen für die Ansicht.  
  
     In der **Abonnementsicht bearbeiten** Bereich, in den **Namen** Geben Sie den neuen Namen für die Ansicht.  
  
5.  Wählen Sie aus der Liste **Modell** ein Modell aus.  
  
6.  Wählen Sie **vorläufig gelöscht Mitglieder einschließen**, vorläufig gelöscht Mitglieder in der Ansicht einbezogen werden sollen.  
  
7.  Wählen Sie entweder **Version** oder **Version-Flag** in **Version Optionen**, und wählen Sie dann in der entsprechenden Liste aus.  
  
    > [!TIP]  
    >  Erstellen Sie auf Grundlage eines Versionsflags eine Abonnementsicht. Wenn Sie eine Version sperren, können Sie das Flag einer geöffneten Version erneut zuweisen, ohne die Abonnementsicht zu aktualisieren.  
  
8.  Wählen Sie entweder **Entität** oder **abgeleitete Hierarchie** in die **Datenquellen** aus, und wählen Sie dann in der entsprechenden Liste aus.  
  
9. Aus der **Format** wählen Sie ein Format für die Abonnementsicht.  
  
10. Wenn Sie ausgewählt haben **explizite Ebenen** oder **abgeleitete Ebenen** aus der **Format** Geben die Anzahl der Ebenen in der Hierarchie in der Ansicht enthalten.  
  
11. Klicken Sie auf **Speichern**.  
  
## Sichtinformationen  
 Für jede erstellte Sicht wird dem Raster eine Zeile mit sieben Spalten hinzugefügt. In der folgenden Tabelle werden diese Spalten beschrieben.  
  
|Spalte|Beschreibung|  
|------------|-----------------|  
|Status|Der Status der Sicht.<br /><br /> Beim Klicken auf **Speichern**,  ![Icon for updating status](../master-data-services/media/mds-statusicon-updating.png "Icon for updating status") Bild angezeigt wird, gibt an, dass die Ansicht aktualisiert wird.<br /><br /> Treten Fehler beim Erstellen oder Bearbeiten einer Ansicht der ![Icon for error status](../master-data-services/media/mds-statusicon-error.png "Icon for error status") Bild angezeigt.<br /><br /> Andernfalls wird der Status OK und ![Icon for OK status](../master-data-services/media/mds-statusicon-ok.png "Icon for OK status") Bild angezeigt.|  
|Name|Der Name der Abonnementsicht.|  
|Modell|Der Name des Modells.|  
|Version|Der Name der Version.|  
|Versionsflag|Der Name des Versionsflags.|  
|Abgeleitete Hierarchie|Der Name der abgeleiteten Hierarchie.|  
|Entität|Der Name der Entität.|  
|Format|Gibt den Typ der Daten in der Sicht an.|  
|Ebene|Gibt die Anzahl von Ebenen in der Sicht an, die nur für Sichtformate mit expliziten oder abgeleiteten Ebenen verwendet werden|  
|Miteinbeziehen von gelöschten Elementen|Gibt an, ob vorläufig gelöschte Elemente in die Sicht miteinbezogen werden.|  
  
 Wenn Sie auf eine Sicht klicken, werden die folgenden Informationen angezeigt.  
  
-   **Erstellt von**: der Name des Benutzers, der die Sicht erstellt.  
  
-   **Auf**: das Datum und die Uhrzeit der Erstellung die Ansicht.  
  
-   **Aktualisiert von**: der Name des Benutzers, der zuletzt aktualisiert die Ansicht.  
  
-   **Auf**: Datum und Uhrzeit, wann die Ansicht zuletzt aktualisiert wurde.  
  
## Siehe auch  
 [Übersicht: Exportieren von Daten & #40; Master Data Services & #41;](../master-data-services/overview-exporting-data-master-data-services.md)   
 [Löschen Sie eine Abonnementsicht & #40. Master Data Services & #41;](../master-data-services/delete-a-subscription-view-master-data-services.md)   
 [Erstellen Sie ein Versionsflag & #40. Master Data Services & #41;](../master-data-services/create-a-version-flag-master-data-services.md)  
  
  