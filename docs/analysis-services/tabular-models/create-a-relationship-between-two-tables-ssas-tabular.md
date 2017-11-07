---
title: "Erstellen Sie eine Beziehung zwischen zwei Tabellen (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.createrelatdb.f1
- sql13.asvs.bidtoolset.managereldb.f1
ms.assetid: 052d77b7-7922-408a-a200-786016ee4d15
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9bc0373c1b0e018430106530da93107c600bbdee
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-relationship-between-two-tables-ssas-tabular"></a>Erstellen einer Beziehung zwischen zwei Tabellen (SSAS – tabellarisch)
  Wenn die Tabellen in der Datenquelle nicht über vorhandene Beziehungen verfügen oder wenn Sie neue Tabellen hinzufügen, können Sie zum Erstellen neuer Beziehungen die Tools im Modell-Designer verwenden. Weitere Informationen darüber, wie Beziehungen in tabellarischen Modellen verwendet werden, finden Sie unter [Beziehungen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/relationships-ssas-tabular.md).  
  
## <a name="create-a-relationship-between-two-tables"></a>Erstellen einer Beziehung zwischen zwei Tabellen  
  
#### <a name="to-create-a-relationship-between-two-tables-in-diagram-view-click-and-drag"></a>So erstellen Sie eine Beziehung zwischen zwei Tabellen in der Diagrammsicht (Klicken und Ziehen)  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]auf das Menü **Modell** , auf **Modellansicht**und dann auf **Diagrammsicht**.  
  
2.  Klicken Sie auf eine Spalte innerhalb einer Tabelle, und halten Sie die Maustaste gedrückt. Ziehen Sie dann den Cursor auf eine verknüpfte Suchspalte in einer verknüpften Suchtabelle, und lassen Sie die Maustaste wieder los. Die Beziehung wird automatisch in der richtigen Reihenfolge erstellt.  
  
#### <a name="to-create-a-relationship-between-two-tables-in-diagram-view-right-click"></a>So erstellen Sie eine Beziehung zwischen zwei Tabellen in der Diagrammsicht (durch Rechtsklicken)  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]auf das Menü **Modell** , auf **Modellansicht**und dann auf **Diagrammsicht**.  
  
2.  Klicken Sie mit der rechten Maustaste auf eine Tabellenüberschrift oder eine Spalte, und klicken Sie dann auf **Beziehung erstellen**.  
  
3.  Klicken Sie im Dialogfeld **Beziehung erstellen** auf den Pfeil nach unten für **Tabelle**, und wählen Sie aus der Dropdownliste eine Tabelle aus.  
  
     Diese Tabelle sollte sich auf der n-Seite einer 1:n-Beziehung befinden.  
  
4.  Wählen Sie für **Spalte**die Spalte aus, die die Daten enthält, die sich auf **Verknüpfte Suchspalte**beziehen. Die Spalte wird automatisch ausgewählt, wenn Sie mit der rechten Maustaste auf eine Spalte geklickt haben, um die Beziehung zu erstellen.  
  
5.  Wählen Sie unter **Verknüpfte Suchtabelle**eine Tabelle mit mindestens einer Spalte mit Daten aus, die sich auf die gerade ausgewählte **Tabelle**beziehen.  
  
     Diese Tabelle sollte sich auf der 1-Seite einer 1:n-Beziehung befinden. Dies bedeutet, dass die Werte in der ausgewählten Spalte keine Duplikate enthalten. Wenn Sie versuchen, die Beziehung in der falschen Reihenfolge (1:n statt n:1) zu erstellen, wird ein Symbol neben dem Feld **Verknüpfte Suchspalte** angezeigt. Kehren Sie die Reihenfolge um, um eine gültige Beziehung zu erstellen.  
  
6.  Wählen Sie für **Verknüpfte Suchspalte**eine Spalte mit eindeutigen Werten aus, die den Werten in der für **Spalte**ausgewählten Spalte entsprechen.  
  
7.  Klicken Sie auf **Erstellen**.  
  
#### <a name="to-create-a-relationship-between-two-tables-in-data-view"></a>So erstellen Sie eine Beziehung zwischen Tabellen in der Datenansicht  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]auf das Menü **Tabelle** und dann auf **Beziehungen erstellen**.  
  
2.  Klicken Sie im Dialogfeld **Beziehung erstellen** auf den Pfeil nach unten für **Tabelle**, und wählen Sie aus der Dropdownliste eine Tabelle aus.  
  
     Diese Tabelle sollte sich auf der n-Seite einer 1:n-Beziehung befinden.  
  
3.  Wählen Sie für **Spalte**die Spalte aus, die die Daten enthält, die sich auf **Verknüpfte Suchspalte**beziehen.  
  
4.  Wählen Sie unter **Verknüpfte Suchtabelle**eine Tabelle mit mindestens einer Spalte mit Daten aus, die sich auf die gerade ausgewählte **Tabelle**beziehen.  
  
     Diese Tabelle sollte sich auf der 1-Seite einer 1:n-Beziehung befinden. Dies bedeutet, dass die Werte in der ausgewählten Spalte keine Duplikate enthalten. Wenn Sie versuchen, die Beziehung in der falschen Reihenfolge (1:n statt n:1) zu erstellen, wird ein Symbol neben dem Feld **Verknüpfte Suchspalte** angezeigt. Kehren Sie die Reihenfolge um, um eine gültige Beziehung zu erstellen.  
  
5.  Wählen Sie für **Verknüpfte Suchspalte**eine Spalte mit eindeutigen Werten aus, die den Werten in der für **Spalte**ausgewählten Spalte entsprechen.  
  
6.  Klicken Sie auf **Erstellen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Löschen von Beziehungen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/delete-relationships-ssas-tabular.md)   
 [Beziehungen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/relationships-ssas-tabular.md)  
  
  

