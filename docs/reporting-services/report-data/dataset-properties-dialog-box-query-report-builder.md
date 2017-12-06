---
title: Dataseteigenschaften (Dialogfeld), Abfrage (Berichts-Generator) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- "10024"
- sql13.rtp.rptdesigner.datasetproperties.query.f1
- "10160"
ms.assetid: 75432318-0b00-4797-917c-0a2e74f9d951
caps.latest.revision: "12"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 03a8561e921834373686c6582f6630c8047417b4
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="dataset-properties-dialog-box-query-report-builder"></a>Dataseteigenschaften (Dialogfeld), Abfrage (Berichts-Generator)
  Wählen Sie im Dialogfeld **Dataseteigenschaften** die Option **Abfrage** aus, um ein freigegebenes Dataset von einem Berichtsserver auszuwählen oder ein eingebettetes Dataset zu erstellen. Für ein eingebettetes Dataset müssen Sie eine Datenquelle auswählen und eine Abfrage erstellen.  
  
 Im Dialogfeld **Dataseteigenschaften** ist Folgendes enthalten:  
  
-   [Dataseteigenschaften (Dialogfeld), Parameter &#40;Berichts-Generator&#41;](http://msdn.microsoft.com/library/3a0672ad-c969-455b-b952-585164ce1dda)  
  
-   [Dataseteigenschaften (Dialogfeld), Felder &#40;Berichts-Generator&#41;](http://msdn.microsoft.com/library/75c7e54a-3d20-4c9a-88da-ab36dce2ce42)  
  
-   [Dataseteigenschaften (Dialogfeld), Optionen &#40;Berichts-Generator&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-options-report-builder.md)  
  
-   [Dataseteigenschaften (Dialogfeld), Filter &#40;Berichts-Generator&#41;](http://msdn.microsoft.com/library/933a6f44-4eb7-4e73-9c40-ac0fd17b23d3)  
  
 Weitere Informationen finden Sie unter [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="options"></a>enthalten  
 **Name**  
 Geben Sie einen Namen für das Dataset ein. Der Name darf nicht mit dem Namen eines Datenbereichs oder einer Gruppe im Bericht identisch sein.  
  
 **Verwenden Sie ein freigegebenes Dataset.**  
 Wählen Sie diese Option, um ein vordefiniertes Dataset vom Berichtsserver zu verwenden.  
  
 **Durchsuchen**  
 Wechseln zu einem Ordner auf einen Berichtsserver oder einer SharePoint-Site und Auswählen eines freigegebenen Datasets (.rsd).  
  
 **Verwenden Sie ein in den eigenen Bericht eingebettetes Dataset.**  
 Wählen Sie diese Option, um ein Dataset ausschließlich zur Verwendung in diesem Bericht zu erstellen.  
  
 **Datenquelle**  
 Wählen Sie eine Datenquelle als Basis für das Dataset aus. Klicken Sie auf **Neu**, um eine neue Datenquelle zu erstellen.  
  
 **Abfragetyp**  
 Wählen Sie den Typ von Befehl oder Abfrage aus, der für das Dataset verwendet werden soll. Wählen Sie **Text** aus, um eine Abfrage auszuführen und Daten von der Datenbank abzurufen. Wählen Sie **Tabelle** aus, um mit der **TableDirect** -Funktion von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle Felder innerhalb einer Tabelle auszuwählen. Wählen Sie **Gespeicherte Prozedur** aus, um eine gespeicherte Prozedur nach Namen auszuführen. Standardmäßig ist**Text** ausgewählt. Diese Einstellung wird für einen Großteil der Abfragen verwendet. Um die ausgewählte Datenquellenabfrage zu bearbeiten, klicken Sie auf **Abfrage-Designer**.  
  
> [!NOTE]  
>  Nicht alle Abfragetypen werden von allen Datenquellen unterstützt. Zum Beispiel wird **Tabelle** nur von den Datenquellentypen **OLE DB** und **ODBC**unterstützt.  
  
 **Dataseteigenschaften**  
 Diese Option wird angezeigt, wenn Sie die Befehlstypoption **Text** auswählen. Geben Sie eine Abfrage ein, oder importieren Sie eine bereits vorhandene Abfrage, indem Sie auf **Importieren**klicken. Klicken Sie auf die Schaltfläche **Ausdruck** (*fx*), um den Ausdruck zu bearbeiten.  
  
> [!NOTE]  
>  Wenn Sie die Abfrage mit einem Abfrage-Designer erstellt haben, wird der Text der Abfrage in diesem Feld angezeigt.  
  
 **Tabellenname**  
 Geben Sie den Namen der Tabelle ein, die Sie als Dataset verwenden möchten. Diese Option wird angezeigt, wenn Sie **Tabelle**auswählen.  
  
 **Auswählen oder Eingeben des Namens einer gespeicherten Prozedur**  
 Geben Sie den Namen der zu verwendenden gespeicherten Prozedur ein, oder wählen Sie ihn aus. Klicken Sie auf die Schaltfläche **Ausdruck** (*fx*), um den Ausdruck zu bearbeiten. Diese Option wird angezeigt, wenn Sie die Befehlstypoption Gespeicherte Prozedur auswählen.  
  
 **Timeout (in Sekunden)**  
 Geben Sie die Anzahl an Sekunden als Timeoutwert für die Abfrage ein. Der Standardwert ist 30 Sekunden. Der angegebene Wert für **Timeout** muss leer oder größer als null sein. Wird das Feld leer gelassen, gibt es für die Abfrage kein Timeout.  
  
 **Felder aktualisieren**  
 Führen Sie diesen Abfragebefehl aus, um die Liste der Felder auf der Seite [Dataseteigenschaften (Dialogfeld), Felder](http://msdn.microsoft.com/library/75c7e54a-3d20-4c9a-88da-ab36dce2ce42) zu aktualisieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Berichtsdatasets &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Hilfe zu Dialogfeldern, Bereichen und Assistenten in Berichts-Generator](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [Abfrage-Designer &#40;Berichts-Generator&#41;](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9)  
  
  
