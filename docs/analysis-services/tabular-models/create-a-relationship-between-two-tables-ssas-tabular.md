---
title: Erstellen einer Beziehung | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: multidimensional-tabular
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.asvs.bidtoolset.createrelatdb.f1
- sql13.asvs.bidtoolset.managereldb.f1
ms.assetid: 052d77b7-7922-408a-a200-786016ee4d15
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 52a5638a6531f79673a5165c32b3a375dbdda42a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-relationship"></a>Erstellen einer Beziehung 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Wenn die Tabellen in der Datenquelle nicht über vorhandene Beziehungen verfügen oder wenn Sie neue Tabellen hinzufügen, können Sie zum Erstellen neuer Beziehungen die Tools im Modell-Designer verwenden. Informationen zur Verwendungsweise von Beziehungen in tabellarischen Modellen finden Sie unter [Beziehungen](../../analysis-services/tabular-models/relationships-ssas-tabular.md).  
  
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
 [Löschen von Beziehungen](../../analysis-services/tabular-models/delete-relationships-ssas-tabular.md)   
 [Beziehungen](../../analysis-services/tabular-models/relationships-ssas-tabular.md)  
  
  
