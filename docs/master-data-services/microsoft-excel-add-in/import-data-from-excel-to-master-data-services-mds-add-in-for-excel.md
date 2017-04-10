---
title: "Importieren von Daten aus Excel in Master Data Services (MDS-Add-In f&#252;r Excel) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 89fce454-a816-4b33-a26a-d1b9741d269b
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 10
---
# Importieren von Daten aus Excel in Master Data Services (MDS-Add-In f&#252;r Excel)
  Veröffentlichen Sie in [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]Daten an das MDS-Repository, wenn Sie mit der Arbeit in Excel fertig sind und die Änderungen speichern möchten, damit andere Benutzer Zugriff auf sie haben.  
  
> [!NOTE]  
>  -   Wenn Sie Änderungen veröffentlichen, werden die Kommentare zu von MDS verwalteten Zellen gelöscht.  
> -   Eine Formel wird in einer von MDS verwalteten Zelle nicht unterstützt. Eine Formel in einer von MDS verwalteten Zelle wird als Textwert behandelt.  
  
## Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich **Explorer** verfügen.  
  
-   Das aktive Arbeitsblatt muss von MDS verwaltete Daten enthalten, und Sie müssen Änderungen oder Hinzufügungen zu den von MDS verwalteten Daten vorgenommen haben.  
  
-   Wenn Sie Elemente hinzufügen, müssen Sie keinen **Code** -Wert angeben, wenn Codes für die Entität automatisch generiert werden. Weitere Informationen finden Sie unter [Automatische Codeerstellung &#40;Master Data Services&#41;](../../master-data-services/automatic-code-creation-master-data-services.md).  
  
### So veröffentlichen Sie Daten im MDS-Repository  
  
1.  Klicken Sie in der Gruppe **Veröffentlichen und Validieren** auf **Veröffentlichen**.  
  
2.  Optional. Wenn das Dialogfeld **Veröffentlichen und mit Anmerkung versehen** angezeigt wird, wählen Sie die Freigabe der gleichen Anmerkung (Kommentar) für alle Updates oder die Kommentierung jeder Änderung einzeln.  
  
3.  Optional. Aktivieren Sie das Kontrollkästchen **Dieses Dialogfeld nicht mehr anzeigen** . Sie können das Dialogfeld zukünftig immer anzeigen, indem Sie **Einstellungen** auswählen und das Kontrollkästchen **Dialogfeld 'Veröffentlichen und mit Anmerkung versehen' beim Veröffentlichen anzeigen** aktivieren.  
  
4.  Klicken Sie auf **Veröffentlichen**.  
  
> [!NOTE]  
>  Wenn Sie dem Arbeitsblatt neue Elemente (Zeilen) hinzufügen, sie aber nicht erfolgreich im MDS-Repository veröffentlichen können, verfügen Sie möglicherweise nicht für alle Attribute im Arbeitsblatt über die Berechtigung **Aktualisieren**. Klicken Sie auf der Registerkarte **Überprüfen** in der Gruppe **Änderungen** auf **Blattschutz aufheben** , und versuchen Sie, erneut zu veröffentlichen.  
  
## Nächste Schritte  
 [Anwenden von Geschäftsregeln &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/apply-business-rules-mds-add-in-for-excel.md)  
  
## Siehe auch  
 [Übersicht: Importieren von Daten aus Excel &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)   
 [Überprüfen von Daten &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md)  
  
  