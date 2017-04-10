---
title: "Erstellen und Ver&#246;ffentlichen einer Gesch&#228;ftsregel (Master Data Services) | Microsoft Docs"
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
  - "Geschäftsregeln [Master Data Services], erstellen"
  - "Erstellen von Geschäftsregeln [Master Data Services]"
ms.assetid: 6961d636-4d69-468e-81f7-8d0be6a4a039
caps.latest.revision: 14
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 14
---
# Erstellen und Ver&#246;ffentlichen einer Gesch&#228;ftsregel (Master Data Services)
  Erstellen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] eine Geschäftsregel, um die Genauigkeit der Masterdaten sicherzustellen. Nachdem Sie eine Regel erstellt haben, müssen Sie diese veröffentlichen, damit Sie sie auf Daten anwenden können.  
  
## Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### So erstellen und veröffentlichen Sie eine Geschäftsregel  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Geschäftsregeln**.  
  
3.  Wählen Sie auf der Seite **Geschäftsregeln** aus der Dropdownliste **Modell** ein Modell aus.  
  
4.  Wählen Sie in der Dropdownliste **Entität** eine Entität aus.  
  
5.  Wählen Sie in der Dropdownliste **Member Types** (Elementtypen) einen Typ des Elements aus, auf das die Geschäftsregel angewendet werden soll.  
  
6.  Klicken Sie auf **Hinzufügen**.  
  
7.  Geben Sie in das Feld **Name** einen Namen für die neue Geschäftsregel ein.  
  
8.  Optional können Sie im Feld **Beschreibung** die Beschreibung der Geschäftsregel eingeben.  
  
9. Aktivieren Sie optional die Option **Benachrichtigungen senden**, und wählen Sie aus der Dropdownliste einen Benutzer oder eine Gruppe aus, an den bzw. die die E-Mail-Benachrichtigung gesendet wird.  
  
    > [!NOTE]  
    >  Benachrichtigungen werden nur für Regeln gesendet, die eine Überprüfungsaktion einschließen.  
  
10. Klicken Sie im **IF**-Abschnitt auf **Hinzufügen**. Ein Panel wird angezeigt.  
  
11. Wählen Sie ein Attribut aus der Dropdownliste **Attribut** aus.  
  
12. Wählen Sie eine Bedingung aus der Dropdownliste **Operator** aus.  
  
13. Füllen Sie alle Pflichtfelder aus.  
  
14. Klicken Sie auf die Schaltfläche **Speichern**. Eine neue Zeile wird dem **IF**-Raster hinzugefügt.  
  
    > [!TIP]  
    >  Sie können Elemente aus Ihrer Geschäftsregel löschen, indem Sie mit der rechten Maustaste auf jedes Element klicken und **Löschen** auswählen.  
  
15. Fügen Sie der Regel option mehrere Bedingungen hinzu. Weitere Informationen finden Sie unter [Hinzufügen mehrerer Bedingungen zu einer Geschäftsregel &#40;Master Data Services&#41;](../master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md).  
  
16. Klicken Sie im **THEN**-Abschnitt auf **Hinzufügen**. Ein Panel wird angezeigt.  
  
17. Wählen Sie ein Attribut aus der Dropdownliste **Attribut** aus.  
  
18. Wählen Sie eine Aktion aus der Dropdownliste **Operator** aus.  
  
19. Füllen Sie alle Pflichtfelder aus.  
  
20. Klicken Sie auf **Speichern**. Eine neue Zeile wird dem **Then**-Raster hinzugefügt.  
  
21. Optional können Sie eine **ELSE**-Aktion hinzufügen, indem Sie folgende Schritte ausführen.  
  
    1.  Klicken Sie unter dem **ELSE**-Abschnitt auf **Hinzufügen**. Ein Panel wird angezeigt.  
  
    2.  Wählen Sie ein Attribut aus der Dropdownliste **Attribut** aus.  
  
    3.  Wählen Sie eine Aktion aus der Dropdownliste **Operator** aus.  
  
    4.  Füllen Sie alle Pflichtfelder aus.  
  
    5.  Klicken Sie auf **Speichern**. Eine neue Zeile wird dem **ELSE**-Raster hinzugefügt.  
  
22. Klicken Sie auf **Speichern**. Eine neue Zeile wird dem Geschäftsregelraster hinzugefügt.  
  
23. Klicken Sie auf **Alle veröffentlichen**.  
  
24. Klicken Sie im Bestätigungsdialogfeld auf **OK**. Der Wert in der Spalte **Geschäftsregelstatus** lautet **Aktiv**.  
  
## Rasterspalten  
 Für jede erstelle Geschäftsregel wird dem Raster eine Zeile mit sechs Spalten hinzugefügt. Das sind die Spalten.  
  
|Name|Description|  
|----------|-----------------|  
|Status|Wenn Sie auf **Speichern** klicken, wird das folgende Bild angezeigt, das angibt, dass die Geschäftsregel aktualisiert wird.<br /><br /> ![mds_BR_refresh](../master-data-services/media/mds-br-refresh.png "mds_BR_refresh")<br /><br /> Falls beim Erstellen oder Bearbeiten einer Geschäftsregel Fehler auftreten, wird das folgende Bild angezeigt.<br /><br /> ![mds_br_error](../master-data-services/media/mds-br-error.png "mds_br_error")<br /><br /> Falls der Status „OK“ lautet, wird das folgende Bild angezeigt.<br /><br /> ![mds_BR_success](../master-data-services/media/mds-br-success.png "mds_BR_success")|  
|Name|Der Geschäftsregelname|  
|Description|Die Beschreibung der Geschäftsregel.|  
|Geschäftsregelstatus|Einer der folgenden Geschäftsregelstatus: : „Keine Regel definiert“, „Aktiv“, „Ausgeschlossen“, „ausstehende Änderungen“, „ausstehender Ausschluss“ und „ausstehende Löschung“.|  
|Ausgeschlossen|Gibt an, ob die Geschäftsregel ausgeschlossen ist.|  
|Benachrichtigung|Gibt den Benutzer oder eine Gruppe an, an den bzw. die die E-Mail-Benachrichtigung gesendet werden soll.|  
  
## Nächste Schritte  
  
-   Führen Sie zum Anwenden von Geschäftsregeln auf Daten eine der folgenden Prozeduren aus:  
  
    -   [Überprüfen von bestimmten Elementen auf Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Überprüfen einer Version anhand von Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## Siehe auch  
 [Konfigurieren von Geschäftsregeln für das Senden von Benachrichtigungen &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)   
 [Ändern des Namens einer Geschäftsregel &#40;Master Data Services&#41;](../master-data-services/change-a-business-rule-name-master-data-services.md)   
 [Hinzufügen mehrerer Bedingungen zu einer Geschäftsregel &#40;Master Data Services&#41;](../master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)  
  
  