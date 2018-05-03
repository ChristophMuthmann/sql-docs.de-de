---
title: 'Lektion 13: In Excel analysieren | Microsoft Docs'
ms.custom: ''
ms.date: 03/27/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: ce717071-193b-4c99-9654-c7a613e16327
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 55e49df3d7e9702ce216952664b0110cd169c3c9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-12-analyze-in-excel"></a>Lektion 12: In Excel analysieren
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In dieser Lektion verwenden Sie die analysieren in Excel-Funktion in SSDT öffnen Sie Microsoft Excel, erstellen Sie automatisch eine datenquellenverbindung mit der Arbeitsbereich "Modell" und dem Arbeitsblatt automatisch eine PivotTable hinzuzufügen. Die Funktion In Excel analysieren stellt eine schnelle und einfache Methode dar, um die Wirksamkeit Ihres Modellentwurfs vor der Modellbereitstellung zu testen. Sie führen in dieser Lektion keine Datenanalyse aus. Der Zweck dieser Lektion ist es, Sie, den Modellautor, mit den Tools vertraut zu machen, die Sie zum Testen des Modellentwurfs verwenden können. Im Gegensatz zur Verwendung von analysieren in Excel-Funktion, die für Modellentwickler vorgesehen ist, verwendet die Endbenutzer Clientanwendungen zur berichterstellung wie Excel oder Power BI eine Verbindung herstellen, und navigieren Sie Modelldaten bereitgestellt.  
  
Um diese Lektion abzuschließen, muss Excel auf dem gleichen Computer wie SSDT installiert sein. Weitere Informationen finden Sie unter [In Excel analysieren](../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)installiert sein.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **20 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 11: Erstellen von Rollen](../analysis-services/lesson-11-create-roles.md).  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>Durchsuchen mit der Standardperspektive und der Internet Sales-Perspektive  
In diesen ersten Aufgaben durchsuchen Sie das Modell mit der Standardperspektive, die alle Modellobjekte einschließt, sowie mit der Internet Sales-Perspektive Sie weiter oben. Die Internet Sales-Perspektive enthält nicht das Customer-Tabellenobjekt.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>So durchsuchen Sie das Modell mit der Standardperspektive  
  
1.  Klicken Sie auf die **Modell** Menü > **in Excel analysieren**.  
  
2.  Klicken Sie im Dialogfeld **In Excel analysieren** auf **OK**.  
  
    Excel wird mit einer neuen Arbeitsmappe geöffnet. Es wird eine Datenquellenverbindung mit dem aktuellen Benutzerkonto erstellt, und zum Definieren von Anzeigefeldern wird die Standardperspektive verwendet. Das Arbeitsblatt wird automatisch eine PivotTable hinzugefügt.  
  
3.  In Excel in der **Feldliste "PivotTable"**, beachten Sie die **DimDate** und **FactInternetSales** Measuregruppen angezeigt werden, sowie die **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**,  **DimProductSubcategory**, und **FactInternetSales** Tabellen mit allen entsprechenden Spalten angezeigt werden.  
  
4.  Schließen Sie Excel, ohne die Arbeitsmappe zu speichern.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>So durchsuchen Sie das Modell mit der Internet Sales-Perspektive  
  
1.  Klicken Sie auf die **Modell** Menü, und klicken Sie dann auf **in Excel analysieren**.  
  
2.  Lassen Sie im Dialogfeld **In Excel analysieren** die Option **Aktueller Windows-Benutzer** aktiviert, wählen Sie im Dropdownlistenfeld **Perspektive** den Eintrag **Internet Sales**aus, und klicken Sie anschließend auf **OK**. 
    
    ![als-tabellarische-Lektion 12-Perspektive](../analysis-services/media/as-tabular-lesson12-perspective.png)
    
3.  In Excel in **PivotTable Fields**, beachten Sie die DimCustomer-Tabelle aus der Feldliste ausgeschlossen ist.  
    
    ![als tabellarische-Lektion 12-Felder](../analysis-services/media/as-tabular-lesson12-fields.png)
    
4.  Schließen Sie Excel, ohne die Arbeitsmappe zu speichern.  
  
## <a name="browse-by-using-roles"></a>Durchsuchen Sie mithilfe von Rollen  
Rollen sind wesentlicher Bestandteil sämtlicher tabellarischer Modelle. Ohne mindestens eine Rolle, die Benutzer als Mitglieder hinzugefügt werden, werden Benutzer nicht zugreifen und Analysieren von Daten mithilfe des Modells. Die Funktion In Excel analysieren bietet eine Möglichkeit zum Testen der Rollen, die Sie definiert haben.  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>Mit der Benutzerrolle Sales Manager durchsuchen  
  
1.  Klicken Sie in SSDT, auf die **Modell** Menü, und klicken Sie dann auf **in Excel analysieren**.  
  
2.  In der **in Excel analysieren** Dialogfeld **Geben Sie den Benutzernamen oder die Rolle für die Verbindung mit dem Modell mit**Option **Rolle**, und wählen Sie dann im Dropdown-Listenfeld **Sales Manager**, und klicken Sie dann auf **OK**.  
  
    Excel wird mit einer neuen Arbeitsmappe geöffnet. Automatisch wird eine PivotTable erstellt. Die PivotTable-Feldliste enthält alle Datenfelder, die im neuen Modell verfügbar sind.  
      
3.  Schließen Sie Excel, ohne die Arbeitsmappe zu speichern.  
  
## <a name="whats-next"></a>Wie geht es weiter?
Wechseln Sie zur nächsten Lektion: [Lektion 13: Bereitstellen von](../analysis-services/lesson-13-deploy.md).

  
  
  
