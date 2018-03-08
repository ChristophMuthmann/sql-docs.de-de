---
title: "Erstellen und Verwenden einer Beziehung für die Entitätensynchronisierung (Master Data Services) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0ddceab4-d2b3-4bc1-bd9c-6b852200b414
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aaa835322bda0e98ac9059bce4612abed5c59a92
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2018
---
# <a name="create-and-execute-an-entity-sync-relationship-master-data-services"></a>Erstellen und Verwenden einer Beziehung für die Entitätensynchronisierung (Master Data Services)
  Entitäten-Synchronisierung ist eine unidirektionale und wiederholbare Synchronisierung zwischen Entitätsversionen. Sie bietet eine Möglichkeit, Entitätsdaten zwischen verschiedenen Modellen freizugeben.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 Komponenten zum Erstellen einer Entitäten-Synchronisierungspartnerschaft:  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich "Systemverwaltung" zuzugreifen. Weitere Informationen finden Sie unter [Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Sie müssen ein Modelladministrator des Zielmodells sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
-   Sie müssen für die Quellentität und deren Entitätsattribute und -elemente mindestens über Lesezugriff verfügen.  
  
 Komponenten zum Ausführen einer Entitäten-Synchronisierungspartnerschaft:  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich "Systemverwaltung" zuzugreifen. Weitere Informationen finden Sie unter [Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Sie müssen ein Modelladministrator des Zielmodells sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
 Berücksichtigen Sie Folgendes, wenn Sie eine Entitäten-Synchronisierungspartnerschaft erstellen:  
  
-   Die Quell- und Zielentitäten müssen sich in unterschiedlichen Modellen befinden  
  
-   Für einen Versionsstatus der Zielentität muss kein Commit ausgeführt werden.  
  
-   Sobald eine Synchronisierungspartnerschaft eingerichtet wurde, wird das Ziel sofort mit der Quelle synchronisiert.  
  
-   Eine Zielentitätsversion kann keine Quellentitätsversion einer anderen Synchronisierungspartnerschaft sein.  
  
 Berücksichtigen Sie Folgendes, wenn Sie eine Entitäten-Synchronisierungspartnerschaft ausführen:  
  
-   Nur Blattelemente werden kopiert  
  
-   Domänenbasierte Attribute werden nicht kopiert.  
  
-   Vorläufig gelöschte Elemente werden nicht kopiert.  
  
-   Synchronisierung generiert keine Zielentitätstransaktionen/-verläufe.  
  
 **Erstellen einer Entitäten-Synchronisierungspartnerschaft**  
  
1.  Klicken Sie im Master Data Manager auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Seite **Modellansicht** auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Entitätensynchronisierung**.  
  
3.  Klicken Sie auf der Seite **Entitätssynchronisierungsverwaltung** auf **Hinzufügen**. Auf der rechten Seite wird ein Bereich angezeigt.  
  
4.  Wählen Sie aus der Quelle **Modell** ein Modell aus.  
  
5.  Wählen Sie aus der Quelle **Version** eine Version aus.  
  
6.  Wählen Sie aus der Quelle **Entität** eine Entität aus.  
  
7.  Wählen Sie aus dem Ziel **Modell** ein Modell aus.  
  
8.  Wählen Sie aus dem Ziel **Version** eine Version aus.  
  
9. Wählen Sie **vorhandene Entität** , und wählen Sie anschließend eine Entität von der Entitätsliste, falls Sie eine bereits vorhandene Entität synchronisieren möchten. Wählen Sie **Neue Entität** aus, und geben Sie den Namen der Zielentität ein, falls Sie eine neue Entität erstellen möchten  
  
10. Wählen Sie **Synchronisierung bei Bedarf**oder **Automatische Synchronisierung** aus, und legen Sie die Häufigkeit fest.  
  
11. Klicken Sie auf **Speichern**.  
  
 **Wie Sie eine Entitäten-Synchronisierungspartnerschaft ausführen**  
  
1.  Klicken Sie im Master Data Manager auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Seite **Modellansicht** auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Entitätensynchronisierung**.  
  
3.  Wählen Sie auf der Seite **Entity Sync Maintenance** (Entitätssynchronisierungsverwaltung) eine Synchronisierungspartnerschaft im Raster aus.  
  
4.  Klicken Sie auf **Ausführen**.  
  
## <a name="sync-relationship-information"></a>Informationen zur Synchronisierungsbeziehung  
 Für jede erstellte Synchronisierungsbeziehung wird dem Raster eine Zeile mit sieben Spalten hinzugefügt. In der folgenden Tabelle werden diese Spalten beschrieben.  
  
|Spalte|Description|  
|------------|-----------------|  
|Status|Der Status der Synchronisierungsbeziehung.<br /><br /> Wenn Sie auf **Speichern** klicken oder eine Synchronisierungspartnerschaft ausführen, wird das Bild ![Symbol für Statusaktualisierung](../master-data-services/media/mds-statusicon-updating.png "Icon for updating status") angezeigt, und gibt an, dass die Synchronisierungspartnerschaft aktualisiert wird.<br /><br /> Wenn beim Erstellen, Bearbeiten oder Ausführen einer Synchronisierungspartnerschaft Fehler auftreten, wird das Bild ![Symbol für den Fehlerstatus](../master-data-services/media/mds-statusicon-error.png "Icon for error status") angezeigt.<br /><br /> Andernfalls ist der Status „OK“, und das Bild ![Symbol für den Status OK](../master-data-services/media/mds-statusicon-ok.png "Icon for OK status") wird angezeigt.|  
|Quellmodell|Der Name des Quellmodells.|  
|Quellversion|Der Name der Quellversion.|  
|Quellentität|Der Name der Quellentität.|  
|Zielmodell|Der Name des Zielmodells.|  
|Zielversion|Der Name der Zielversion.|  
|Zielentität|Der Name der Zielentität.|  
|Häufigkeit|Gibt die Häufigkeit der Synchronisierungsbeziehung an.|  
|Uhrzeit des letzten Versuchs|Zeigt die Uhrzeit des letzten Synchronisierungsversuchs an.|  
|Uhrzeit des letzten erfolgreichen Versuchs|Zeigt die Uhrzeit des letzten erfolgreichen Synchronisierungsversuchs an.|  
  
 Wenn Sie auf einen Index klicken, werden die folgenden Informationen angezeigt.  
  
-   **Fehler des letzten Versuchs**: Zeigt die Fehlerinformationen zum letzten Synchronisierungsversuch an.  
  
-   **Erstellt von**: Der Name des Benutzers, der die Synchronisierung erstellt hat.  
  
-   **Am**: Datum und Uhrzeit, wann die Synchronisierung erstellt wurde.  
  
-   **Aktualisiert von**: Der Name des Benutzers, der die Synchronisierung zuletzt aktualisiert hat.  
  
-   **Am**: Datum und Uhrzeit, wann die Synchronisierung zuletzt aktualisiert wurde.  
  
## <a name="next-steps"></a>Next Steps  
 [Bearbeiten und Löschen einer Entitäten-Synchronisierungspartnerschaft &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-entity-sync-relationship-master-data-services.md)  
  
  
