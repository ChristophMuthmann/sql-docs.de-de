---
title: Erstellen eines Indexes (Master Data Services) | Microsoft-Dokumentation
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
ms.assetid: d694a105-69b1-4ff6-99d3-1f408b916b81
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: ee405ebea31b8ca2a178b2d287a1ba1b8d4e97f8
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="create-an-index-master-data-services"></a>Erstellen eines Indexes (Master Data Services)
  Erstellen Sie einen benutzerdefinierten Index anhand einer Liste von Attributen, die Sie häufig abfragen, und verbessern Sie so die Abfrageleistung.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich "Systemverwaltung" zuzugreifen. Weitere Informationen finden Sie unter [Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
 **So erstellen Sie einen Index**  
  
1.  Klicken Sie im Master Data Manager auf **Systemverwaltung**.  
  
2.  Wählen Sie auf der Seite **Modell verwalten** im Raster ein Modell aus, und klicken Sie anschließend auf **Entitäten**.  
  
3.  Wählen Sie auf der Seite **Entität verwalten** im **Raster** die Zeile der Entität aus, für die Sie einen Index erstellen möchten.  
  
4.  Klicken Sie auf **Indizes**.  
  
5.  Geben Sie im Feld **Name** einen Namen für den Index ein.  
  
6.  Wählen Sie **Ist eindeutig** aus, wenn Sie einen eindeutigen Index erstellen möchten. Weitere Informationen zu Indextypen finden Sie unter [Benutzerdefinierter Index &#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md).  
  
7.  Klicken Sie im Feld **Verfügbare Attribute** auf Attribute, und klicken Sie auf den Pfeil für **Hinzufügen** . Um alle Attribute hinzuzufügen, klicken Sie auf den Pfeil **Alle hinzufügen** .  
  
8.  Klicken Sie auf **Speichern**.  
  
 Für jeden erstellten Index wird dem Raster eine Zeile mit vier Spalten hinzugefügt. In der folgenden Tabelle werden diese Spalten beschrieben.  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|Status|Der Indexstatus.<br /><br /> Wenn Sie auf **Speichern** klicken, wird das ![Symbol für Statusaktualisierung](../master-data-services/media/mds-statusicon-updating.png "Icon for updating status") angezeigt, das angibt, dass der Index aktualisiert wird.<br /><br /> Wenn beim Erstellen oder Bearbeiten eines Indexes Fehler auftreten, wird das Bild ![Symbol für den Fehlerstatus](../master-data-services/media/mds-statusicon-error.png "Icon for error status") angezeigt.<br /><br /> Andernfalls ist der Status „OK“, und das Bild ![Symbol für den Status OK](../master-data-services/media/mds-statusicon-ok.png "Icon for OK status") wird angezeigt.|  
|Name|Der Indexname.|  
|Ist eindeutig|Gibt an, ob der Index eindeutig ist.|  
|On Attributes|Zeigt die Anzeigenamen der Attribute, auf deren Basis der Index definiert ist.|  
  
 Wenn Sie auf einen Index klicken, werden die folgenden Informationen angezeigt.  
  
-   **Erstellt von**: Der Name des Benutzers, der den Index erstellt hat.  
  
-   **Am**: Datum und Uhrzeit, wann der Index erstellt wurde.  
  
-   **Aktualisiert von**: Der Name des Benutzers, der den Index zuletzt aktualisiert hat.  
  
-   **Am**: Datum und Uhrzeit, wann der Index zuletzt aktualisiert wurde.  
  
## <a name="next-steps"></a>Nächste Schritte  
 [Bearbeiten und Löschen eines Indexes &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-index-master-data-services.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Benutzerdefinierter Index &#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md)  
  
  
