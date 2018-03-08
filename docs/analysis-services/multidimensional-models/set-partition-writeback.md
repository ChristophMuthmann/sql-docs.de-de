---
title: "Festlegen des Rückschreibens von Partitionen | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- write-enabled partitions [Analysis Services]
- partitions [Analysis Services], writeback
- partitions [Analysis Services], write-enabled
- writeback [Analysis Services], partitions
ms.assetid: 38bb09cc-2652-4971-8373-0cf468cdc7a6
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c1e6971bd8c1bc228386ad5b39a498f0e0ed5d42
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="set-partition-writeback"></a>Einrichten des Rückschreibens von Partitionen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Wenn Sie den Schreibzugriff für eine Measuregruppe aktivieren, können Endbenutzer Cubedaten während des Durchsuchens ändern. Die Änderungen werden dabei in einer getrennten Tabelle, der Rückschreibetabelle, gespeichert und nicht in den Cubedaten oder Quelldaten. Endbenutzer, die eine Partition mit aktiviertem Schreibzugriff durchsuchen, können die Auswirkungen der Änderungen in der Rückschreibetabelle für die Partition anzeigen.  
  
 Sie können Rückschreibedaten anzeigen oder löschen. Rückschreibedaten können außerdem zu einer Partition konvertiert werden. Bei einer Partition mit aktiviertem Schreibzugriff können Sie Cuberollen verwenden, um Benutzern und Gruppen von Benutzern Lese-/Schreibzugriff zu gewähren und den Zugriff auf bestimmte Zellen oder Gruppen von Zellen in der Partition zu beschränken.  
  
 Ein kurzes Einführungsvideo zur Rückschreibefunktion finden Sie unter [Rückschreiben von Daten in Analysis Services mit Excel 2010](http://go.microsoft.com/fwlink/p/?LinkId=394951). Ausführlichere Informationen zu dieser Funktion finden Sie in der Blogreihe [Building a Writeback Application with Analysis Services (blog)](http://go.microsoft.com/fwlink/?LinkId=394977)(Erstellen einer Rückschreibeanwendung mit Analysis Services (Blog)).  
  
> [!NOTE]  
>  Das Rückschreiben wird ausschließlich bei relationalen SQL Server-Datenbanken und Data Marts und nur in Verbindung mit mehrdimensionalen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Modellen unterstützt.  
  
## <a name="how-to-write-enable-a-partition"></a>Aktivieren des Schreibzugriffs auf eine Partition  
 Sie können den Schreibzugriff auf Measuregruppen einer Partition aktivieren, indem Sie im Cube-Designer in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]den Schreibzugriff für die Partition selbst aktivieren.  
  
-   Klicken Sie im Cube-Designer auf der Registerkarte „Partitionen“ mit der rechten Maustaste auf eine Partition, und wählen Sie **Rückschreibeeinstellungen**aus.  
  
-   Erweitern Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]die Optionen „Datenbank“ &gt; „Cube“ &gt; „Measuregruppe“, klicken Sie anschließend mit der rechten Maustaste auf **Rückschreiben** , und wählen Sie **Rückschreiben aktivieren**aus.  
  
 Das Rückschreiben wird nur bei Measures unterstützt, die die SUM-Aggregation verwenden. Sie können das Rückschreibeverhalten mithilfe der Sales Targets-Measuregruppe in der AdventureWorks-Beispieldatenbank testen.  
  
 Wenn Sie den Schreibzugriff für eine Partition aktivieren, geben Sie einen Tabellennamen und eine Datenquelle an, in der die Rückschreibetabelle gespeichert werden soll. Alle folgenden Änderungen an der Measuregruppe werden in dieser Tabelle aufgezeichnet.  
  
## <a name="browse-writeback-data-in-a-partition"></a>Durchsuchen von Rückschreibedaten in einer Partition  
 Mithilfe des Dialogfelds **Daten durchsuchen** können Sie den Inhalt der Rückschreibetabelle eines Cubes durchsuchen. Sie können auf dieses Dialogfeld zugreifen, indem Sie auf der Registerkarte **Partitionen** im Cube-Designer mit der rechten Maustaste auf eine Partition klicken, für die der Schreibzugriff aktiviert ist.  
  
## <a name="delete-writeback-data-or-disable-writeback"></a>Löschen von Rückschreibedaten oder Deaktivieren des Rückschreibens  
 Beim Löschen der Rückschreibedaten wird der Rückschreibcache gelöscht. Sobald diese Daten gelöscht sind, werden weitere Rückschreibaktionen auf einer bereinigten Liste ausgeführt. Wenn Sie Rückschreiben für eine Cubepartition deaktivieren, wird Rückschreiben für diese Partition abgeschaltet.  
  
## <a name="convert-writeback-data-to-a-partition"></a>Konvertieren von Rückschreibedaten zu einer Partition  
 Sie können die Daten in der Rückschreibetabelle einer Partition zu einer Partition konvertieren. Durch dieses Verfahren wird die Rückschreibetabelle zur Faktentabelle der neuen Partition.  
  
> [!CAUTION]  
>  Die falsche Verwendung von Partitionen kann zu ungenauen Cubedaten führen. Weitere Informationen finden Sie unter [Erstellen und Verwalten einer lokalen Partition &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md).  
  
 Beim Konvertieren der Rückschreibetabelle zu einer Partition wird auch der Schreibzugriff für die Partition deaktiviert. Alle Richtlinien für unbeschränkte Lese-/Schreiboperationen und alle Lese-/Schreibberechtigungen für die Zellen der Partition sind deaktiviert, und Endbenutzer können keine Änderungen an den angezeigten Cubedaten durchführen. (Endbenutzer mit deaktivierten Richtlinien für unbeschränkte Lese-/Schreiboperationen oder deaktivierten Lese-/Schreibberechtigungen können den Cube jedoch weiterhin durchsuchen.) Leseberechtigungen und Berechtigungen, die durch die Option Lesen (abhängig) erteilt werden, sind nicht betroffen.  
  
 Verwenden Sie zum Konvertieren von Rückschreibedaten in eine Partition das Dialogfeld **In Partition konvertieren**. Öffnen Sie dieses Dialogfeld, indem Sie mit der rechten Maustaste auf die Rückschreibetabelle einer Partition mit aktiviertem Schreibzugriff in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] klicken. Geben Sie einen Namen für die Partition an, und geben Sie an, ob die Aggregation für die Partition später oder beim Erstellen der Partition entworfen werden soll. Um die Aggregation zu demselben Zeitpunkt zu erstellen, zu dem die Partition von Ihnen ausgewählt wird, müssen Sie die Option zum Kopieren des Aggregationsentwurfs aus einer vorhandenen Partition auswählen. Dies ist normalerweise, aber nicht notwendigerweise, die aktuelle Rückschreibepartition. Sie haben auch die Möglichkeit, die Partition gleichzeitig zu verarbeiten und zu erstellen.  
  
## <a name="see-also"></a>Siehe auch  
 [Partitionen mit aktiviertem Schreibzugriff](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [Aktivieren des Rückschreibens in einen OLAP-Cube auf Zellebene in Excel 2010](http://go.microsoft.com/fwlink/p/?LinkId=394952)   
 [Aktivieren und Sichern der Dateneingabe mit Analysis Services-Rückschreiben](http://go.microsoft.com/fwlink/p/?LinkId=394953)  
  
  
