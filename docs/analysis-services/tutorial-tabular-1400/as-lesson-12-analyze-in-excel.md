---
title: 'Analysis Services Tutorial Lektion 12: in Excel analysieren | Microsoft Docs'
description: Beschreibt, wie in Excel analysieren in Analysis Services Tutorial-Projekt zu verwenden.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: dda8a42cd5e82c60f98de8ab351274f3c1e93820
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="analyze-in-excel"></a>In Excel analysieren

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In dieser Lektion verwenden Sie Funktion in Excel analysieren zu Microsoft Excel öffnen, automatisch eine Verbindung mit den Modellarbeitsbereich zu erstellen und dem Arbeitsblatt automatisch eine PivotTable hinzuzufügen. Die Funktion In Excel analysieren stellt eine schnelle und einfache Methode dar, um die Wirksamkeit Ihres Modellentwurfs vor der Modellbereitstellung zu testen. Sie führen in dieser Lektion keine Datenanalyse durch. Der Zweck dieser Lektion ist es, Sie, den Modellautor, mit den Tools vertraut zu machen, die Sie zum Testen des Modellentwurfs verwenden können.   
  
Um diese Lektion abzuschließen, muss Excel auf demselben Computer wie Visual Studio installiert sein.
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **5 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  

Dieser Artikel ist Teil eines Lernprogramms zur tabellenmodellierung, das in Reihenfolge absolviert werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 11: Erstellen von Rollen](../tutorial-tabular-1400/as-lesson-11-create-roles.md).  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>Durchsuchen mit der Standardperspektive und der Internet Sales-Perspektive  

In diesen ersten Aufgaben durchsuchen Sie das Modell mit der Standardperspektive, die alle Modellobjekte einschließt, sowie mit der Internet Sales-Perspektive Sie weiter oben. Die Internet Sales-Perspektive enthält nicht das Customer-Tabellenobjekt.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>So durchsuchen Sie das Modell mit der Standardperspektive  
  
1.  Klicken Sie auf die **Modell** Menü > **in Excel analysieren**.  
  
2.  Klicken Sie im Dialogfeld **In Excel analysieren** auf **OK**.  
  
    Excel wird mit einer neuen Arbeitsmappe geöffnet. Es wird eine Datenquellenverbindung mit dem aktuellen Benutzerkonto erstellt, und zum Definieren von Anzeigefeldern wird die Standardperspektive verwendet. Das Arbeitsblatt wird automatisch eine PivotTable hinzugefügt.  
  
3.  In Excel in der **Feldliste "PivotTable"**, beachten Sie die **DimDate** und **FactInternetSales** Measuregruppen angezeigt. Die **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, und **FactInternetSales** auch Tabellen mit den entsprechenden Spalten angezeigt werden.  
  
4.  Schließen Sie Excel, ohne die Arbeitsmappe zu speichern.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>So durchsuchen Sie das Modell mit der Internet Sales-Perspektive  
  
1.  Klicken Sie auf die **Modell** Menü, und klicken Sie dann auf **in Excel analysieren**.  
  
2.  Lassen Sie im Dialogfeld **In Excel analysieren** die Option **Aktueller Windows-Benutzer** aktiviert, wählen Sie im Dropdownlistenfeld **Perspektive** den Eintrag **Internet Sales**aus, und klicken Sie anschließend auf **OK**. 
    
    ![Perspektive als Lektion 12](../tutorial-tabular-1400/media/as-lesson12-perspective.png)
    
3.  In Excel in **PivotTable Fields**, beachten Sie die DimCustomer-Tabelle aus der Feldliste ausgeschlossen ist.  
    
    ![as-lesson12-fields](../tutorial-tabular-1400/media/as-lesson12-fields.png)
    
4.  Schließen Sie Excel, ohne die Arbeitsmappe zu speichern.  
  
## <a name="browse-by-using-roles"></a>Durchsuchen Sie mithilfe von Rollen  

Rollen sind ein wichtiger Bestandteil der tabellarische Modelle. Ohne mindestens eine Rolle, die Benutzer als Mitglieder hinzugefügt werden, können nicht der Benutzer Zugriff auf und Analysieren von Daten mithilfe des Modells. Die Funktion In Excel analysieren bietet eine Möglichkeit zum Testen der Rollen, die Sie definiert haben.  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>Mit der Benutzerrolle Sales Manager durchsuchen  
  
1.  Klicken Sie in SSDT, auf die **Modell** Menü, und klicken Sie dann auf **in Excel analysieren**.  
  
2.  In **Geben Sie den Benutzernamen oder die Rolle für die Verbindung mit dem Modell mit**Option **Rolle**, und wählen Sie dann im Dropdown-Listenfeld **Sales Manager**, und klicken Sie dann auf **OK**.  
  
    Excel wird mit einer neuen Arbeitsmappe geöffnet. Automatisch wird eine PivotTable erstellt. Die PivotTable-Feldliste enthält alle Datenfelder im neuen Modell verfügbar sind.  
      
3.  Schließen Sie Excel, ohne die Arbeitsmappe zu speichern.  
  
## <a name="whats-next"></a>Wie geht es weiter?

Wechseln Sie zur nächsten Lektion: [Lektion 13: Bereitstellen von](../tutorial-tabular-1400/as-lesson-13-deploy.md).

  
  
  
