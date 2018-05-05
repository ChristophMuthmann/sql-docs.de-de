---
title: Erstellen eines Linkattributs (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- attributes [Master Data Services], creating link attributes
- creating link attributes [Master Data Services]
ms.assetid: e6658e9c-5b08-4b8d-b556-17ec2dd041d2
caps.latest.revision: 9
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f48a6b30ef8492200eeb233c77ef7143f02039d3
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="create-a-link-attribute-master-data-services"></a>Erstellen eines Linkattributs (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Erstellen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ein Linkattribut, wenn Sie möchten, dass Benutzer einen Link als Attributwert eingeben, z.B. http://www.contoso.com.  
  
> [!NOTE]  
>  Wenn Benutzer einen Wert für ein Linkattribut eingeben, muss die Zeichenfolge mit **http://** beginnen, oder ein Fehler wird angezeigt.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
-   Eine Entität muss vorhanden sein, um das Attribut dafür erstellen zu können. Weitere Informationen finden Sie unter [Erstellen einer Entität &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
## <a name="attribute-information"></a>Attributinformationen  
 Für jedes erstellte Attribut wird dem Raster eine Zeile mit sieben Spalten hinzugefügt. In der folgenden Tabelle werden diese Spalten beschrieben.  
  
|Spalte|Description|  
|------------|-----------------|  
|Status|Der Attributstatus.<br /><br /> Wenn Sie auf „Speichern“ klicken, wird das Bild ![Symbol für den Aktualisierungsstatus](../master-data-services/media/mds-statusicon-updating.png "Icon for updating status") angezeigt, das angibt, dass das Attribut aktualisiert wird.<br /><br /> Wenn beim Erstellen oder Bearbeiten eines Attributs Fehler auftreten, wird das Bild ![Fehlerstatussymbol](../master-data-services/media/mds-statusicon-error.png "Icon for error status") angezeigt.<br /><br /> Andernfalls ist der Status „OK“, und das Bild ![Symbol für den Status OK](../master-data-services/media/mds-statusicon-ok.png "Icon for OK status") wird angezeigt.|  
|Name|Der Attributname.|  
|Anzeigename|Der Anzeigename des Attributs.|  
|Description|Die Attributbeschreibung.|  
|Pixelbreite anzeigen|Die Breite des Attributs.|  
|Typ und Eigenschaften|Die Typ- und Datentypinformationen des Attributs.|  
|Änderungsnachverfolgung aktivieren|Gibt an, ob das Attribut für die Änderungsnachverfolgung aktiviert ist, und zeigt die Gruppennummer in Klammern.|  
  
 Wenn Sie auf ein Attribut klicken, werden die folgenden Informationen angezeigt.  
  
-   **Erstellt von**: Name des Benutzers, der das Attribut erstellt hat.  
  
-   **Am**: Datum und Uhrzeit der Erstellung des Attributs.  
  
-   **Aktualisiert von**: Name des Benutzers, der das Attribut aktualisiert hat.  
  
-   **Am**: Datum und Uhrzeit der letzten Aktualisierung des Attributs.  
  
### <a name="to-create-a-link-attribute"></a>So erstellen Sie ein Linkattribut  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Wählen Sie auf der Seite **Modell verwalten** im Raster ein Modell aus, und klicken Sie dann auf **Entitäten**.  
  
3.  Wählen Sie auf der Seite **Entität verwalten** die Zeile der Entität aus, für die Sie ein Attribut erstellen möchten.  
  
4.  Klicken Sie auf **Attribute**.  
  
5.  Führen Sie auf der Seite **Attribute verwalten** einen der folgenden Schritte aus, und klicken Sie dann auf **Hinzufügen**.  
  
    -   Wenn das Attribut für Blattelemente bestimmt ist, wählen Sie **Blatt** im Listenfeld **Elementtypen** aus.  
  
    -   Wenn das Attribut für konsolidierte Elemente bestimmt ist, wählen Sie **Konsolidiert** im Listenfeld **Elementtypen** aus.  
  
    -   Wenn das Attribut für Sammlungen bestimmt ist, wählen Sie **Sammlung** im Listenfeld **Elementtypen** aus.  
  
6.  Geben Sie im Feld **Name** einen Namen für das Attribut ein. Eine Liste von Wörtern, die nicht als Attributnamen verwendet werden sollten, finden Sie unter [Reservierte Wörter &#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md).  
  
7.  Geben Sie optional einen Anzeigenamen ein und in das Feld **Beschreibung** eine Beschreibung des Attributs ein.  
  
8.  Geben Sie im Feld **Pixelbreite anzeigen** die Breite der Attributspalte ein, die im **Explorerraster** angezeigt werden soll.  
  
9. Wählen Sie in der Liste **Attributtyp** die Option **Freiform**aus.  
  
10. Wählen Sie **Link** in der Liste **Datentyp**aus.  
  
11. Geben Sie im Feld **Länge** die maximal zulässige Anzahl von Zeichen ein.  
  
12. Optional können Sie **Änderungsnachverfolgung aktivieren** auswählen, um Änderungen an Gruppen von Attributen nachzuverfolgen. Weitere Informationen finden Sie unter [Hinzufügen von Attributen zu einer Änderungsnachverfolgungsgruppe &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).  
  
13. Klicken Sie auf **Speichern**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Attribute &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)   
 [Ändern eines Attributnamens und Datentyps &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [Erstellen eines domänenbasierten Attributs &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [Erstellen eines Dateiattributs &#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
