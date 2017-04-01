---
title: "Erfordern von Attributwerten (Master Data Services) | Microsoft Docs"
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
  - "Geschäftsregeln [Master Data Services], Erfordern von Attributwerten"
  - "Attribute [Master Data Services], Erfordern von Werten"
ms.assetid: a360ef13-0c34-43b8-a87e-2f5d8732d30e
caps.latest.revision: 9
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# Erfordern von Attributwerten (Master Data Services)
  Erfordern Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Attributwerte, wenn Sie sicherstellen möchten, dass die Masterdaten vollständig sind.  
  
> [!NOTE]  
>  Elemente, denen domänenbasierte Attributwerte fehlen, werden nicht in abgeleiteten Hierarchien angezeigt, die auf diesen Beziehungen basieren.  
  
## Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren & #40; Master Data Services & #41;](../master-data-services/administrators-master-data-services.md).  
  
### So erfordern Sie Attributwerte  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Geschäftsregeln**.  
  
3.  Auf der **Geschäftsregeln** Seite aus der **Modell** Dropdown-Liste, ein Modell auswählen.  
  
4.  Aus der **Entität** Dropdown-Liste, wählen Sie eine Entität.  
  
5.  Aus der **Membertypen** Dropdown-Liste, wählen Sie einen Typ des Elements für die Geschäftsregel angewendet.  
  
6.  Klicken Sie auf **Hinzufügen**.  
  
7.  In den **Namen** Geben Sie einen Namen für die Geschäftsregel.  
  
8.  Optional können Sie in der **Beschreibung** Geben die Beschreibung der Business-Regel.  
  
9. Unter den **dann** blockieren, klicken Sie auf **Hinzufügen**. Ein Bereich wird angezeigt.  
  
10. Aus der **Operator** Dropdown-Liste **erforderliche Aktion**.  
  
11. Aus der **Attribut** Dropdown-Liste, wählen Sie ein Attribut.  
  
12. Klicken Sie auf **Speichern**. Wird eine neue Zeile hinzugefügt werden, um die **dann** Raster.  
  
13. Klicken Sie auf **Speichern**.  
  
14. Klicken Sie auf **Alle veröffentlichen**.  
  
15. Klicken Sie im Bestätigungsdialogfeld auf **OK**. Der Wert in der **Business Regelstatus** Spalte **Active**.  
  
## Nächste Schritte  
  
-   Führen Sie zum Anwenden von Geschäftsregeln auf Daten eine der folgenden Prozeduren aus:  
  
    -   [Überprüfen von bestimmten Elementen auf Geschäftsregeln & #40; Master Data Services & #41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [Überprüfen einer Version anhand von Geschäftsregeln & #40; Master Data Services & #41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## Siehe auch  
 [Geschäftsregeln & #40; Master Data Services & #41;](../master-data-services/business-rules-master-data-services.md)   
 [Abgeleitete Hierarchien & #40; Master Data Services & #41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  