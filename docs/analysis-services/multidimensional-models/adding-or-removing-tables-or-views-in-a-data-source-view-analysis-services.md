---
title: "Hinzufügen oder Entfernen von Tabellen oder Sichten in einer Datenquellensicht (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.dsvdesigner.tablespane.f1
helpviewer_keywords:
- deleting tables
- tables [Analysis Services]
- removing tables
- adding tables
- data source views [Analysis Services], tables
- tables [Analysis Services], data source views
ms.assetid: 98307d04-6548-4d7d-9244-2371dd165249
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2b2f865766530f174cc3affe410679f1880e9813
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services"></a>Hinzufügen oder Entfernen von Tabellen oder Sichten in einer Datenquellensicht (Analysis Services)
  Nachdem Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]eine Datenquellensicht (Data Source View, DSV) erstellt haben, können Sie sie im Datenquellensicht-Designer ändern, indem Sie Tabellen und Spalten hinzufügen oder entfernen. Dies schließt auch Tabellen und Spalten aus einer anderen Datenquelle ein.  
  
 Um die DSV im Datenquellensicht-Designer zu öffnen, doppelklicken Sie im Projektmappen-Explorer auf die DSV. Sobald die DSV geöffnet ist, können Sie sie mit dem Befehl **Tabellen hinzufügen/entfernen** auf der Schaltflächenleiste oder im Menü ändern oder erweitern. Sie können auch mit den Objekten im Diagramm arbeiten. Sie können z. B. ein Objekt auswählen und es dann mit der ENTF-TASTE auf der Tastatur entfernen.  
  
> [!WARNING]  
>  Gehen Sie beim Entfernen einer Tabelle mit Bedacht vor. Beim Entfernen einer Tabelle werden alle zugeordneten Spalten und Beziehungen aus der DSV gelöscht und alle an die Tabelle gebundenen Objekte ungültig.  
  
## <a name="selecting-tables-or-views-to-add-or-remove"></a>Auswählen von Tabellen oder Sichten für das Hinzufügen oder Entfernen  
 Im Dialogfeld **Tabellen hinzufügen/entfernen** können Sie Tabellen oder Sichten zwischen den Listen **Verfügbare Objekte** und **Eingeschlossene Objekte** verschieben. Die Liste **Verfügbare Objekte** enthält zunächst alle Tabellen oder Sichten der Primärdatenquelle, die nicht bereits in der Datenquellensicht enthalten sind. Falls die primäre Datenquelle die **OPENROWSET** -Funktion unterstützt, können Sie auch Tabellen oder Sichten aus anderen Datenquellen des Projekts oder der Datenbank hinzufügen.  
  
 Wenn in einer DSV eine Tabelle hinzugefügt oder entfernt wird, wird die Tabelle ebenfalls im aktuell ausgewählten Diagramm in der DSV hinzugefügt bzw. entfernt. Weitere Informationen finden Sie unter [Verwenden von Diagrammen im Datenquellensicht-Designer &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md).  
  
 Nach dem Verschieben einer Tabelle in die Liste **Eingeschlossene Objekte** des Dialogfelds **Tabellen hinzufügen/entfernen** können Sie alle verknüpften Tabellen hinzufügen. Durch diesen Vorgang werden der Datenquelle Tabellen nach Maßgabe von Fremdschlüsseleinschränkungen (soweit vorhanden) hinzugefügt. Sind keine Fremdschlüsseleinschränkungen vorhanden, können Sie mithilfe der **NameMatchingCriteria** -Eigenschaft der Datenquellensicht Beziehungen festlegen, indem Sie ein Kriterium für die Zuordnung von Spaltennamen in Tabellen zur Generierung möglicher Beziehungen angeben. Falls die **NameMatchingCriteria**-Eigenschaft für die Datenquellensicht angegeben ist, klicken Sie auf **Verknüpfte Tabellen hinzufügen** , um aus der Datenquelle Tabellen hinzuzufügen, zu denen es übereinstimmende Spaltennamen gibt. Weitere Informationen zum Einstellen der **NameMatchingCriteria** -Eigenschaft finden Sie unter [Datenquellensichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
> [!NOTE]  
>  Das Hinzufügen oder Entfernen von Objekten in einer Datenquellensicht hat keine Auswirkungen auf die zugrunde liegende Datenquelle.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenquellensichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Verwenden von Diagrammen im Datenquellensicht-Designer &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  

