---
title: "Filtern von Daten vor dem Exportieren (MDS Add-In für Excel) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: microsoft-excel-add-in
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9e30eae0-776b-4a09-aac3-0c0249d92ca5
caps.latest.revision: "10"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dc82f9020cbaf9b2699c5c31e28d7e30e37656e6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="filter-data-before-exporting-mds-add-in-for-excel"></a>Filtern von Daten vor dem Exportieren (MDS Add-In für Excel)
  Filtern Sie in [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] Daten, wenn Sie die Größe oder den Bereich der Daten einschränken möchten, die Sie in Excel exportieren.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung für den Zugriff auf den Funktionsbereich **Explorer** verfügen.  
  
### <a name="to-filter-data-before-exporting"></a>So filtern Sie Daten vor dem Export  
  
1.  Öffnen Sie Excel, und stellen Sie auf der Registerkarte **Masterdaten** eine Verbindung mit einem MDS-Repository her. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einem MDS-Repository &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md).  
  
2.  Wählen Sie im Bereich **Master Data Explorer** ein Modell und eine Version aus. Die Liste der Entitäten wird aufgefüllt.  
  
    -   Wenn der Bereich **Master Data Explorer** nicht sichtbar ist, klicken Sie in der Gruppe **Verbinden und Laden** auf **Explorer anzeigen**.  
  
    -   Wenn der Bereich **Master Data Explorer** deaktiviert ist, liegt dies daran, dass das vorhandene Blatt bereits von MDS verwaltete Daten enthält. Um den Bereich zu aktivieren, öffnen Sie ein neues Arbeitsblatt.  
  
3.  Klicken Sie im Bereich **Master Data Explorer** in der Liste der Entitäten auf die Entität, die Sie filtern möchten.  
  
4.  Klicken Sie im Menüband in der Gruppe **Verbinden und Laden** auf **Filtern**.  
  
5.  Vervollständigen Sie das Dialogfeld **Filtern** , indem Sie die anzuzeigenden Attribute (Spalten) auswählen, die Reihenfolge der Spalten festlegen und nach Bedarf die Daten so filtern, dass wenigere Zeilen zurückgegeben werden. Zeigen Sie den Bereich **Zusammenfassung** an, in dem angegeben ist, wie viele Daten zurückgegeben werden. Weitere Informationen finden Sie unter [Filtern &#40;Dialogfeld, MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md).  
  
6.  Klicken Sie auf **Daten laden**. Das Blatt wird mit von MDS verwalteten Daten aufgefüllt.  
  
    > [!NOTE]  
    >  -   Nur die erste eine Million von Elementen wird in Excel geladen.  
    > -   In Spalten, die beschränkte Listen (domänenbasierte Attribute) sind, werden standardmäßig nur die ersten 25000 Werte geladen.  
  
## <a name="next-steps"></a>Nächste Schritte  
 [Importieren von Daten aus Excel in Master Data Services &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Overview: Exporting Data to Excel &#40;MDS Add-in for Excel&#41; (Übersicht: Exportieren von Daten nach Excel (MDS-Add-in für Excel))](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [Filtern &#40;Dialogfeld, MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)   
 [Neuanordnen von Spalten &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/reorder-columns-mds-add-in-for-excel.md)  
  
  
