---
title: "Umgehung der Zeilenbeschränkung in Excel 2003 | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a4c8700b-bef5-4440-a99c-bba5dcc46bfd
caps.latest.revision: "12"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 764b6da1c5ea43d02d7b5b950aa056434acf1a12
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="work-around-the-excel-2003-row-limitation"></a>Work Around the Excel 2003 Row Limitation
  In diesem Thema wird erläutert, wie Sie beim Exportieren von paginierten Berichten nach Excel die Zeilenbeschränkung von Excel 2003 umgehen. Die Problemumgehung bezieht sich auf einen Bericht, der nur eine Tabelle enthält.  
  
> [!IMPORTANT]  
>  Die [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003-Renderingerweiterung (.xls) ist veraltet. Weitere Informationen finden Sie unter [Als veraltet markierte Funktionen in SQL Server Reporting Services in SQL Server 2016](../../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md).  
  
 Excel 2003 unterstützt maximal 65.536 Zeilen pro Arbeitsblatt. Sie können diese Einschränkung umgehen, indem Sie nach einer bestimmten Anzahl von Zeilen einen expliziten Seitenumbruch erzwingen. Der Excel-Renderer erstellt bei jedem expliziten Seitenumbruch ein neues Arbeitsblatt.  
  
### <a name="to-create-an-explicit-page-break"></a>So erstellen Sie einen expliziten Seitenumbruch  
  
1.  Öffnen Sie den Bericht in [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] oder im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Webportal.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Datenzeile in der Tabelle, und klicken Sie anschließend auf **Gruppe hinzufügen** > **Übergeordnete Gruppe** , um eine äußere Tabellengruppe hinzuzufügen.  
  
     ![Wählen Sie die übergeordnete Gruppe](../../reporting-services/report-builder/media/datarow-selectparentgroup.png "Select the Parent Group")  
  
3.  Geben Sie die folgende Formel im Ausdrucksfeld **Gruppieren nach** ein, und klicken Sie dann auf **OK** , um die übergeordnete Gruppe hinzuzufügen.  
  
     =Int((RowNumber(Nothing)-1)/65000)  
  
     Durch die Formel wird jedem im Dataset enthaltenen Satz von 65.000 Zeilen eine Zahl zugewiesen. Wenn ein Seitenumbruch für die Gruppe definiert ist, führt dieser Ausdruck alle 65.000 Zeilen zu einem Seitenumbruch.  
  
     Durch das Hinzufügen der äußeren Tabellengruppe wird dem Bericht eine Gruppenspalte hinzugefügt.  
  
4.  Löschen Sie die Gruppenspalte, indem Sie mit der rechten Maustaste auf die Spaltenüberschrift klicken, auf **Spalten löschen**klicken, **Nur Spalten löschen**auswählen und anschließend auf **OK**klicken.  
  
     ![Löschen einer Gruppenspalte](../../reporting-services/report-builder/media/groupcolumn-delete-updated.png "Delete a group column")  
  
5.  Klicken Sie mit der rechten Maustaste im Bereich **Zeilengruppen** auf **Gruppe 1** , und klicken Sie dann auf **Gruppeneigenschaften**.  
  
     ![Anzeigen von Gruppeneigenschaften](../../reporting-services/report-builder/media/groupproperties-updated.png "View group properties")  
  
6.  Wählen Sie im Dialogfeld **Gruppeneigenschaften** auf der Seite **Sortierung** die Standardsortierungsoption aus, und klicken Sie auf **Löschen**.  
  
     ![Löschen der Standardsortierung](../../reporting-services/report-builder/media/groupproperties-sorting-updated.png "Delete default sorting")  
  
7.  Klicken Sie auf der Seite **Seitenumbrüche** auf **Zwischen den einzelnen Instanzen einer Gruppe** , und klicken Sie auf **OK**.  
  
     ![Festlegen von Seitenumbrüchen](../../reporting-services/report-builder/media/groupproperties-pagebreaks-updated.png "Set page breaks")  
  
8.  Speichern Sie den Bericht. Beim Exportieren des Berichts nach Excel wird dieser in mehrere Arbeitsblätter exportiert. Jedes Arbeitsblatt enthält maximal 65.000 Zeilen.  
  
  
