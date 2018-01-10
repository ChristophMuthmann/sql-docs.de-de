---
title: Erstellen einer rekursiven Hierarchiegruppe (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b830ba5-4d64-4348-a2b1-76b9338a1462
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 55996678941459c5f6797e02bfc30d82331a718f
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="create-a-recursive-hierarchy-group-report-builder-and-ssrs"></a>Erstellen einer rekursiven Hierarchiegruppe (Berichts-Generator und SSRS)
In paginierten [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichten organisiert eine rekursive Hierarchiegruppe Daten aus einem einzelnen Berichtsdataset, das mehrere hierarchische Ebenen aufweist, z.B. eine Berichtsstruktur für die Beziehung zwischen Managern und Mitarbeitern in der Hierarchie einer Organisation.  
  
 Bevor Sie Daten in einer Tabelle als rekursive Hierarchiegruppe organisieren können, müssen Sie ein Dataset erstellen, das alle hierarchischen Daten enthält. Sie benötigen separate Felder für das zu gruppierende Element und das Element, nach dem gruppiert wird. Ein Dataset, in dem Sie Mitarbeiter rekursiv unter dem Manager gruppieren möchten, kann z. B. einen Namen, einen Mitarbeiternamen, eine Mitarbeiter-ID und eine Manager-ID enthalten.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-create-a-recursive-hierarchy-group"></a>So erstellen Sie eine rekursive Hierarchiegruppe  
  
1.  Fügen Sie in der Entwurfsansicht eine Tabelle hinzu, und ziehen Sie die anzuzeigenden Datasetfelder in die Tabelle. Normalerweise ist das Feld, das Sie als Hierarchie anzeigen möchten, in der ersten Spalte angeordnet.  
  
2.  Klicken Sie mit der rechten Maustaste in der Tabelle an einer beliebigen Stelle, um sie auszuwählen. Im Bereich Gruppierung wird die Detailgruppe für die gewählte Tabelle angezeigt. Klicken Sie im Bereich „Zeilengruppen“ mit der rechten Maustaste auf **Details**, und klicken Sie anschließend auf **Gruppe bearbeiten**. Das Dialogfeld **Gruppeneigenschaften** wird angezeigt.  
  
3.  Klicken Sie unter **Gruppierungsausdrücke**auf **Hinzufügen**. Im Raster wird eine neue Zeile angezeigt.  
  
4.  Wählen Sie in der Liste **Gruppieren nach** das zu gruppierende Feld aus, oder geben Sie es ein.  
  
5.  Klicken Sie auf **Erweitert**.  
  
6.  Wählen Sie in der Liste **Rekursives übergeordnetes Element** das Feld aus, nach dem gruppiert werden soll, oder geben Sie es ein.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Führen Sie den Bericht aus. Im Bericht wird die rekursive Hierarchiegruppe angezeigt. Die Anzeige erfolgt jedoch ohne einen Einzug, der die Hierarchie verdeutlichen würde.  
  
## <a name="to-format-a-recursive-hierarchy-group-with-indent-levels"></a>So formatieren Sie eine rekursive Hierarchiegruppe mit Einzugsebenen  
  
1.  Klicken Sie auf das Textfeld mit dem Feld, dem Sie Einzugsebenen hinzufügen möchten, um ein Hierarchieformat anzuzeigen. Die Eigenschaften für das Textfeld werden im Bereich Eigenschaften angezeigt.  
  
    > [!NOTE]  
    >  Wenn der Bereich Eigenschaften geschlossen ist, klicken Sie auf der Registerkarte **Ansicht** auf **Eigenschaften** .  
  
2.  Erweitern Sie im Bereich „Eigenschaften“ den Knoten **Auffüllung**, klicken Sie auf **Links**, und wählen Sie in der Dropdownliste den Eintrag **\<Ausdruck…>**.  
  
3.  Geben Sie im Ausdruckfenster den folgenden Ausdruck ein:  
  
     `=CStr(2 + (Level()*10)) + "pt"`  
  
     Die Auffüllung-Eigenschaften erfordern alle eine Zeichenfolge im Format *nnyy*. Dabei steht *nn* für eine Zahl und *yy* für die Maßeinheit. Im obigen Beispielausdruck wird eine Zeichenfolge generiert, bei der die Auffüllung mithilfe der **Level** -Funktion basierend auf der Rekursionsebene vergrößert wird. Eine Zeile mit der Ebene 1 hätte z.B. die Auffüllung (2 + (1\*10))=12pt, und eine Zeile mit der Ebene 3 hätte die Auffüllung (2 + (3\*10))=32pt. Informationen zur **Level** -Funktion finden Sie unter [Ebene](../../reporting-services/report-design/report-builder-functions-level-function.md).  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Führen Sie den Bericht aus. Der Bericht zeigt eine hierarchische Ansicht der gruppierten Daten an.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen von rekursiven Hierarchiegruppen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)   
 [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Aggregatfunktionsreferenz &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)   
 [Tabellen (Berichts-Generator und SSRS)](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrizen (Berichts-Generator und SSRS)](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Listen (Berichts-Generator und SSRS)](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabellen, Matrizen und Listen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
