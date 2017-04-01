---
title: "Filter Data before Exporting (MDS Add-in for Excel) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9e30eae0-776b-4a09-aac3-0c0249d92ca5
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 10
---
# Filter Data before Exporting (MDS Add-in for Excel)
  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], Daten zu filtern, wenn Sie die Größe oder den Umfang der Daten, die Sie in Excel exportieren, beschränken möchten.  
  
## Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich **Explorer** verfügen.  
  
### Filtern von Daten vor dem Exportieren  
  
1.  Öffnen Sie Excel, und stellen Sie auf der Registerkarte **Masterdaten** eine Verbindung mit einem MDS-Repository her. Weitere Informationen finden Sie unter [mit einem MDS-Repository & #40; MDS-Add-in für Excel & #41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md).  
  
2.  Wählen Sie im Bereich **Master Data Explorer** ein Modell und eine Version aus. Die Liste der Entitäten wird aufgefüllt.  
  
    -   Wenn der Bereich **Master Data Explorer** nicht sichtbar ist, klicken Sie in der Gruppe **Verbinden und Laden** auf **Explorer anzeigen**.  
  
    -   Wenn die **Master Data Explorer** Bereich ist deaktiviert, da das vorhandene Blatt bereits von MDS verwalteten Daten enthält. Um den Bereich zu aktivieren, öffnen Sie ein neues Arbeitsblatt.  
  
3.  Klicken Sie im Bereich **Master Data Explorer** in der Liste der Entitäten auf die Entität, die Sie filtern möchten.  
  
4.  Klicken Sie im Menüband in der Gruppe **Verbinden und Laden** auf **Filtern**.  
  
5.  Führen Sie die **Filter** Dialogfeld durch Auswählen der Attribute (Spalten) anzeigen, die Reihenfolge der Spalten festlegen und bei Bedarf die Daten filtern, damit weniger Zeilen zurückgegeben werden. Zeigen Sie den Bereich **Zusammenfassung** an, in dem angegeben ist, wie viele Daten zurückgegeben werden. Weitere Informationen finden Sie unter [im Dialogfeld Filter & #40; MDS-Add-in für Excel & #41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md).  
  
6.  Klicken Sie auf **Daten laden**. Das Blatt wird mit von MDS verwalteten Daten aufgefüllt.  
  
    > [!NOTE]  
    >  -   Nur die erste eine Million von Elementen wird in Excel geladen.  
    > -   In Spalten, die beschränkte Listen (domänenbasierte Attribute) sind, werden standardmäßig nur die ersten 25000 Werte geladen.  
  
## Nächste Schritte  
 [Importieren von Daten aus Excel in Master Data Services & #40; MDS-Add-in für Excel & #41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## Siehe auch  
 [Übersicht: Exportieren von Daten in Excel & #40; MDS-Add-in für Excel & #41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [Das Dialogfeld Filter & #40; MDS-Add-in für Excel & #41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)   
 [Anordnen von Spalten & #40; MDS-Add-in für Excel & #41;](../../master-data-services/microsoft-excel-add-in/reorder-columns-mds-add-in-for-excel.md)  
  
  