---
title: Berichtsteile und Datasets in Berichts-Generator | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/16/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1fe86481-9c41-4535-a4b7-c7c4d780cab6
caps.latest.revision: "9"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8333a60403a32321c8796bb2041d6e95e39160ce
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="report-parts-and-datasets-in-report-builder"></a>Berichtsteile und Datasets in Berichts-Generator
  In Berichts-Generator ist die einfachste Methode, um Daten in einen Bericht einzuschließen, das Hinzufügen von Berichtsteilen aus dem Berichtsteilkatalog. Berichtsteile enthalten die Datasets, von denen sie abhängig sind, so genannte *abhängige Datasets*. Abhängige Datasets basieren auf freigegebenen Datenquellen und können entweder eingebettete Datasets oder freigegebene Datasets sein. Erfahren Sie mehr über [Berichtsteile](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
 Eine weitere einfache Methode zum Einschließen von Daten in einen Bericht ist das Verwenden eines freigegebenen Datasets. Weitere Informationen finden Sie unter [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Adding"></a> Hinzufügen eines Berichtsteils mit abhängigen Datasets zum Bericht  
 Wenn Sie dem Bericht einen Berichtsteil hinzufügen, werden die darin enthaltenen abhängigen Datasets ebenfalls dem Bericht hinzugefügt. Da ein Berichtsteil ein Rechteck mit vielen anderen Berichtselementen umfassen kann, können dem Bericht mehrere abhängige Datasets hinzugefügt werden. Jedes freigegebene Dataset ist ein unabhängiger Verweis. Die freigegebene Datenquelle, von der er abhängt, wird dem Bericht nicht hinzugefügt. Jedes eingebettete Dataset fügt auch die eingebettete oder freigegebene Datenquelle hinzu, von der es abhängt.  
  
 Die Anmeldeinformationen für eine eingebettete Datenquelle werden nicht als Teil des Berichtsteils gespeichert. Wenn dem Bericht eine eingebettete Datenquelle hinzugefügt wird, werden Sie zur Eingabe von Anmeldeinformationen aufgefordert, wenn Sie den Bericht ausführen. Wenn Sie die Nachfrage nach Anmeldeinformationen vermeiden möchten, verwenden Sie lediglich Berichtsteile, die auf freigegebenen Datenquellen mit gespeicherten Anmeldeinformationen basieren.  
  
 Nachdem Sie dem Bericht einen Berichtsteil hinzugefügt haben, unterscheiden sich die hinzugefügten Datasets nicht von anderen eingebetteten oder freigegebenen Datasets, die Sie erstellen. Sie können die zusätzlichen Datasets im Berichtsdatenbereich anzeigen. Eingebettete Datasets werden unter der entsprechenden freigegebenen Datenquelle angezeigt, während freigegebene Datasets im Ordner für freigegebene Datasets aufgeführt werden.  
  
##  <a name="Customizing"></a> Anpassen von abhängigen Datasets  
 Nachdem Sie dem Bericht Berichtsteile hinzugefügt haben, könnten Sie diesen in der Vorschau anzeigen und Änderungen an den Daten vornehmen. Die Art der Änderungen hängt vom Typ der Datasets ab, mit denen Sie arbeiten.  
  
 Um Daten und Datenoptionen für ein eingebettetes Dataset zu ändern, können Sie die Dataseteigenschaften einschließlich der Abfrage so bearbeiten, als ob Sie das Dataset selbst erstellt hätten.  
  
 Bei der Änderung von Daten und Datenoptionen für ein freigegebenes Dataset können Sie die freigegebene Datasetdefinition auf dem Berichtsserver nur ändern, wenn Sie über ausreichende Berechtigungen verfügen. Sie können auch die Instanz des freigegebenen Datasets im Bericht anpassen, indem Sie Filter und berechnete Felder hinzufügen und Datenoptionen wie die Groß- und Kleinschreibung ändern. Weitere Informationen finden Sie unter [Eingebettete und freigegebene Datasets (Berichts-Generator und SSRS)](../../reporting-services/report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md).  
  
 Weitere Informationen zum Ändern der Definition eines freigegebenen Datasets oder zum Anzeigen der letzten Datenänderungen für ein freigegebenes Dataset in Ihrem Bericht finden Sie unter [Erstellen eines freigegebenen Datasets oder eingebetteten Datasets&#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md) und [Hinzufügen, Bearbeiten und Aktualisieren von Feldern im Berichtsdatenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
##  <a name="Publishing"></a> Veröffentlichen von abhängigen Datasets als freigegebene Datasets  
 Wenn Sie ein Berichtselement veröffentlichen, das abhängige Datasets aufweist, können Sie jedes Dataset als freigegebenes Dataset oder als eingebettetes Dataset veröffentlichen, das weiterhin in das Berichtselement eingebettet ist.  
  
 Wenn Sie die Option für das freigegebene Dataset wählen, wird das Dataset auf dem Berichtsserver als freigegebene Datasetdefinition gespeichert. Im Bericht wird jedes Berichtselement, das dieses Dataset verwendet, so aktualisiert, dass es auf das freigegebene Dataset verweist, das sich jetzt auf dem Berichtsserver befindet. Dies hat zwei Ergebnisse zur Folge:  
  
1.  Im Veröffentlichungsdialogfeld wird jedes freigegebene Dataset, das veröffentlicht wurde, aus der Liste der Elemente entfernt, die für die Veröffentlichung verfügbar sind.  
  
2.  Wenn Sie den Berichts-Generator beenden oder einen neuen Bericht starten, werden Sie dazu aufgefordert, den Bericht zu speichern. Wenn Sie den Bericht nicht speichern, kann es sein, dass Sie beim nächsten Öffnen des Berichts und Veröffentlichen von Berichtselementen neue Kopien der gleichen Datasets veröffentlichen. Um das Speichern mehrerer Kopien von freigegebenen Datasets auf dem Berichtsserver verhindern, empfiehlt es sich, den Bericht zu speichern.  
  
> [!IMPORTANT]  
>  Um sicher zu sein, dass Sie und andere Personen weiterhin erfolgreich Daten aus einem freigegebenen Dataset verwenden können, müssen Sie die grundlegenden Prinzipien für das Sichern von Berichtselementen verstehen. Weitere Informationen finden Sie unter [Sichern von freigegebenen Datasetelementen](../../reporting-services/security/secure-shared-dataset-items.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Berichtsentwurfsansicht &#40;Berichts-Generator&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)   
 [Sicherheit (Berichts-Generator)](../../reporting-services/report-builder/security-report-builder.md)   
 [Berichtsteile &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
