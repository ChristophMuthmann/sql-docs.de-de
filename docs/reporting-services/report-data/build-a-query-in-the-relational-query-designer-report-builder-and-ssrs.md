---
title: Erstellen einer Abfrage im relationalen Abfrage-Designer (Berichts-Generator und SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 28b25861-f3b4-4c3e-a9b0-03d6e4cfea26
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8f7c711b3cd56302b05d7dcf4f3045283c376d73
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="build-a-query-in-the-relational-query-designer-report-builder-and-ssrs"></a>Erstellen einer Abfrage im relationalen Abfrage-Designer (Berichts-Generator und SSRS)
  Ein Abfrage-Designer unterstützt Sie beim Festlegen der Daten, die für ein Berichtsdataset aus einer externen Datenquelle abgerufen werden sollen. Sie verwenden einen Abfrage-Designer, wenn Sie in einem Assistenten eine Abfrage oder eine Datasetabfrage erstellen.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Ein Dataset basiert auf einer Datenquelle. Der Typ der Datenquelle und die Erstellungsumgebung bestimmen, welcher Abfrage-Designer geöffnet wird, wenn Sie die Datasetabfrage definieren. Die Funktionen eines Abfrage-Designers variieren abhängig von der zu Grunde liegenden Datenquelle. Weitere Informationen zu Datenschichten finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen in Berichts-Generator](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34) oder [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
 Ein Abfrage-Designer kann für die folgenden Aufgaben verwendet werden:  
  
-   Durchsuchen der Metadaten für mehrere Schemas in der externen Datenquelle  
  
-   Festlegen der für das Dataset abzurufenden Felder  
  
-   Festlegen von Beziehungen zwischen zwei Objekten, z. B. Tabellen  
  
-   Festlegen von Filtern, um die Daten vor dem Abruf als Berichtsdaten einzuschränken  
  
-   Angeben, ob Parameter erstellt werden  
  
-   Angeben von Aggregaten, um Berechnungen für die externe Datenquelle durchzuführen  
  
 Nach dem Öffnen eines Abfrage-Designers unterscheidet sich die Vorgehensweise zum Erstellen einer Abfrage für ein eingebettetes Dataset nicht von der für ein freigegebenes Dataset. In den folgenden Verfahren wird eine Abfrage für ein eingebettetes Dataset verwendet.  
  
 Weitere Informationen finden Sie unter [Benutzeroberfläche des relationalen Abfrage-Designers &#40;Berichts-Generator&#41;](../../reporting-services/report-data/relational-query-designer-user-interface-report-builder.md).  
  
### <a name="to-build-a-query-for-an-embedded-dataset-in-report-design-view"></a>So erstellen Sie in der Berichtsentwurfssicht eine Abfrage für ein eingebettetes Dataset  
  
1.  Öffnen Sie den Abfrage-Designer. Klicken Sie im Berichtsdatenbereich mit der rechten Maustaste auf das Dataset, und klicken Sie anschließend auf **Abfrage**.  
  
     Der mit der Datenquelle verknüpfte Abfrage-Designer wird geöffnet.  
  
2.  Erweitern Sie im Bereich "Datenbanksicht" die Ordner, die eine hierarchische Ansicht von Datenbankschemaobjekten wie Tabellen, Sichten und gespeicherte Prozeduren enthalten. Klicken Sie auf das Auswahlfeld, um alle Felder für ein Objekt auszuwählen, oder erweitern Sie den Knoten, um einzelne Felder auszuwählen.  
  
     Die im Bereich "Datenbanksicht" ausgewählten Felder werden im Bereich **Felder auswählen** angezeigt.  
  
     Wenn Sie Felder aus mehreren verknüpften Datenbanktabellen auswählen, können Sie im Bereich "Beziehungen" die Tabellenbeziehungen anzeigen, die im Datenbankschema erkannt wurden.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Die Liste der Datasetfelder wird im Berichtsdatenbereich angezeigt.  
  
### <a name="to-specify-limits-for-a-query"></a>So geben Sie Grenzen für eine Abfrage an  
  
1.  Vergewissern Sie sich im relationalen Abfrage-Designer, dass Sie Felder ausgewählt haben und die Felder im Bereich **Ausgewählte Felder** angezeigt werden.  
  
2.  Klicken Sie auf der Symbolleiste des Bereichs "Angewendete Filter" auf **Filter hinzufügen**. Es wird ein neuer Zeilenfilter angezeigt.  
  
3.  Klicken Sie in das Feld **Feldname**, um die Dropdownliste der Felder anzuzeigen, und klicken Sie anschließend auf den Namen des Felds, nach dem Sie filtern möchten. Wenn Sie nach der Menge filtern möchten, klicken Sie z. B. auf das Feld, das die Anzahl von Elementen enthält.  
  
4.  Klicken Sie in das Feld **Operator**, um die Dropdownliste der Operatoren anzuzeigen, und wählen Sie anschließend den im Filter zu verwendenden Vergleichsoperator aus.  
  
5.  Geben Sie im Feld **Wert**den Wert ein, nach dem Sie filtern möchten. Wenn Sie z. B. nach Mengen größer 100 filtern möchten, geben Sie 100 ein.  
  
6.  Wählen Sie die Parameteroption in dieser Zeile aus, um einen Datasetparameter zu erstellen. Dadurch können Benutzer einen Filterwert angeben. Es wird automatisch ein Berichtsparameter erstellt, der dem Datasetparameter entspricht.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Die Liste der Datasetfelder wird im Berichtsdatenbereich angezeigt.  
  
### <a name="to-view-a-query-result-set"></a>So zeigen Sie ein Abfrageresultset an  
  
1.  Klicken Sie auf der Symbolleiste des Abfrage-Designers auf **Abfrage ausführen (!)**.  
  
    > [!NOTE]  
    >  Der Abfrage-Designer verwendet Entwurfszeitanmeldeinformationen, um die Abfrage auszuführen und das Resultset abzurufen. Weitere Informationen finden Sie unter [Angeben von Anmeldeinformationen im Berichts-Generator](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
 Die Abfrage wird für die Datenquelle ausgeführt, und die zurückgegebenen Beispieldaten werden im Bereich "Abfrageergebnisse" angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
 [Berichtsdatasets &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Hinzufügen von Daten aus externen Datenquellen &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md)   
 [Abfrage-Designer &#40;Berichts-Generator&#41;](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9)   
 [Erstellen eines freigegebenen Datasets oder eingebetteten Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Berichtsentwurfsansicht &#40;Berichts-Generator&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)   
 [Freigegebene Datasetentwurfsansicht &#40;Report Builder&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
 [Abfrage-Designer in Reporting Services](http://msdn.microsoft.com/library/07efd3f1-804f-45f7-b62a-3e727a3d9835)  
  
  
