---
title: "Löschen einer Spalte | Microsoft Docs"
ms.custom: 
ms.date: 02/22/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 703db83b-e554-450e-813e-23ad08c1cdad
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c18504b3e6430807f124938b60d7f022a8050379
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="delete-a-column"></a>Löschen einer Spalte 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
In diesem Artikel wird beschrieben, wie eine Spalte aus einer Tabelle eines tabellarische Modells gelöscht wird.  
  
## <a name="delete-a-model-table-column"></a>Löschen von Modelltabellenspalten  
  
> [!NOTE]  
>  Wenn Sie eine Spalte aus einer Modelltabelle löschen, wird die Spalte nicht aus einer Partitionsabfragedefinition gelöscht. Falls die Spalte, die Sie löschen, Teil einer Partition ist, müssen Sie die Spalte manuell aus der Partitionsabfragedefinition löschen. Wenn Sie die Spalte nicht aus der Partitionsabfragedefinition löschen, wird die Spalte bei Verarbeitungsvorgängen abgefragt und Daten zurückgegeben, aber nicht in der Modelltabelle ausgefüllt. Weitere Informationen finden Sie unter [Partitionen](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
#### <a name="to-delete-a-model-table-column"></a>So löschen Sie eine Modelltabellenspalte  
  
-   Klicken Sie im Modell-Designer in der Tabelle, die die Spalte enthält, mit der rechten Maustaste auf die Spalte und anschließend auf **Löschen**.  
  
#### <a name="to-delete-a-model-table-column-by-using-the-table-properties-dialog-box"></a>So löschen Sie mithilfe des Dialogfelds 'Tabelleneigenschaften' eine Modelltabellenspalte  
  
1.  Klicken Sie im Modell-Designer auf die Tabelle, die die zu löschende Spalte enthält, klicken Sie auf das Menü **Tabelle** und dann auf  **Tabelleneigenschaften**.  
  
2.  Wählen Sie unter **Spaltennamen aus**die Option **Modell** aus,*um Modelltabellen-Spaltennamen zu verwenden, falls diese von der Quelle abweichen*.  
  
3.  Deaktivieren Sie im Dialogfeld **Tabelleneigenschaften bearbeiten** im Tabellenvorschaufenster die Spalte, die Sie löschen möchten, und klicken Sie dann auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
 [Hinzufügen von Spalten zu einer Tabelle](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)   
 [Partitionen](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  
