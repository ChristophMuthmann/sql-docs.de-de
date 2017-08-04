---
title: Erstellen einer Abonnementsicht zum Exportieren von Daten (Master Data Services) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscription views [Master Data Services], creating
- creating subscription views [Master Data Services]
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4934e49ef7b8e4f6b56439dd3b414fc93d5af832
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-subscription-view-to-export-data-master-data-services"></a>Erstellen einer Abonnementsicht zum Exportieren von Daten (Master Data Services)
  Erstellen Sie eine Abonnementsicht, um Master Data Services-Daten in Abonnementsysteme zu exportieren. Erstellen Sie eine Sicht Ihrer Daten in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die entsprechende Berechtigung für den Zugriff auf den Funktionsbereich **Integrationsmanagement** verfügen. Weitere Informationen finden Sie unter [Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-create-and-edit-a-subscription-view"></a>So erstellen und bearbeiten Sie eine Abonnementsicht  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Integrationsmanagement**.  
  
2.  Klicken Sie auf der Menüleiste auf **Sichten erstellen**.  
  
3.  Klicken Sie auf der Seite **Abonnementsichten** auf **Hinzufügen** , um eine Sicht zu erstellen, oder klicken Sie auf **Bearbeiten** , um eine Sicht zu bearbeiten. Auf der rechten Seite wird ein Panel angezeigt.  
  
4.  Geben Sie im Bereich **Abonnementsicht erstellen** im Feld **Name** einen Namen für die Sicht ein.  
  
     Geben Sie im Bereich **Abonnementsicht bearbeiten** im Feld **Name** den aktualisierten Namen für die Sicht ein.  
  
5.  Wählen Sie aus der Liste **Modell** ein Modell aus.  
  
6.  Wählen Sie **Include soft-deleted members**(vorläufig gelöschte Elemente miteinbeziehen) aus, um vorläufig gelöschte Elemente in die Sicht miteinzubeziehen.  
  
7.  Wählen Sie unter **Versionsoptionen** entweder die Option **Version** oder die Option **Versionsflag**aus, und wählen Sie dann aus der entsprechenden Liste aus.  
  
    > [!TIP]  
    >  Erstellen Sie auf Grundlage eines Versionsflags eine Abonnementsicht. Wenn Sie eine Version sperren, können Sie das Flag einer geöffneten Version erneut zuweisen, ohne die Abonnementsicht zu aktualisieren.  
  
8.  Wählen Sie für die Option **Datenquellen** entweder **Entität** oder **Abgeleitete Hierarchie** aus, und wählen Sie dann aus der entsprechenden Liste aus.  
  
9. Wählen Sie aus der Liste **Format** ein Format für die Abonnementsicht aus.  
  
10. Wenn Sie **Explizite Ebenen** oder **Abgeleitete Ebenen** aus der Liste **Format** ausgewählt haben, geben Sie die Anzahl der in die Sicht aufzunehmenden Hierarchieebenen ein.  
  
11. Klicken Sie auf **Speichern**.  
  
## <a name="view-information"></a>Sichtinformationen  
 Für jede erstellte Sicht wird dem Raster eine Zeile mit sieben Spalten hinzugefügt. In der folgenden Tabelle werden diese Spalten beschrieben.  
  
|Column|Description|  
|------------|-----------------|  
|Status|Der Status der Sicht.<br /><br /> Beim Klicken auf **speichern**, ![Symbol für Status aktualisieren](../master-data-services/media/mds-statusicon-updating.png "Symbol für Status aktualisieren") angezeigt, das angibt, dass die Ansicht aktualisiert wird.<br /><br /> Treten Fehler beim Erstellen oder Bearbeiten einer Ansicht der ![Symbol nach dem Fehlerstatus](../master-data-services/media/mds-statusicon-error.png "Symbol nach dem Fehlerstatus") Bild angezeigt.<br /><br /> Andernfalls ist der Status OK und die ![Symbol für Status OK](../master-data-services/media/mds-statusicon-ok.png "Symbol für Status OK") Bild angezeigt.|  
|Name|Der Name der Abonnementsicht.|  
|Modell|Der Name des Modells.|  
|Versionsoptionen|Der Name der Version.|  
|Version|Der Name des Versionsflags.|  
|Entität|Der Name der abgeleiteten Hierarchie.|  
|Datenquellen|Der Name der Entität.|  
|Format|Gibt den Typ der Daten in der Sicht an.|  
|Ebene|Gibt die Anzahl von Ebenen in der Sicht an, die nur für Sichtformate mit expliziten oder abgeleiteten Ebenen verwendet werden|  
|Miteinbeziehen von gelöschten Elementen|Gibt an, ob vorläufig gelöschte Elemente in die Sicht miteinbezogen werden.|  
  
 Wenn Sie auf eine Sicht klicken, werden die folgenden Informationen angezeigt.  
  
-   **Erstellt von**: Der Name des Benutzers, der die Sicht erstellt hat.  
  
-   **Am**: Das Datum und die Uhrzeit der Erstellung der Sicht.  
  
-   **Aktualisiert von**: Der Name des Benutzers, der die Sicht zuletzt aktualisiert hat.  
  
-   **Am**: Das Datum und die Uhrzeit der letzten Aktualisierung der Sicht.  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht: Exportieren von Daten &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)   
 [Löschen einer Abonnementsicht &#40; Master Data Services &#41;](../master-data-services/delete-a-subscription-view-master-data-services.md)   
 [Erstellen eines Versionsflags &#40; Master Data Services &#41;](../master-data-services/create-a-version-flag-master-data-services.md)  
  
  
