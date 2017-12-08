---
title: "Erstellen und Verwalten von Perspektiven (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.bidtoolset.perspectivedb.f1
ms.assetid: 2a411c2b-2820-4086-ad7f-ce6a941fefc7
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 37228aace939d68a3e97e9b818a8cffe62b7632a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-and-manage-perspectives-ssas-tabular"></a>Erstellen und Verwalten von Perspektiven (SSAS – tabellarisch)
  Eine Perspektive definiert sichtbare Teilmengen eines Modells, die fokussierte, unternehmensspezifische oder anwendungsspezifische Blickpunkte des Modells bereitstellen. In den Tasks in diesem Thema wird beschrieben, wie Perspektiven mithilfe des Dialogfelds **Perspektiven** im Modell-Designer erstellt und verwaltet werden.  
  
 Dieses Thema umfasst folgende Aufgaben:  
  
-   [So fügen Sie eine Perspektive hinzu](#bkmk_add)  
  
-   [So bearbeiten Sie eine Perspektive](#bkmk_edit)  
  
-   [So benennen Sie eine Perspektive um](#bkmk_rename)  
  
-   [So löschen Sie eine Perspektive](#bkmk_delete)  
  
-   [So kopieren Sie eine Perspektive](#bkmk_copy)  
  
## <a name="tasks"></a>Aufgaben  
 Zum Erstellen von Perspektiven verwenden Sie das Dialogfeld **Perspektiven** , in dem Sie Perspektiven hinzufügen, bearbeiten, löschen, kopieren und anzeigen können. Um das Dialogfeld **Perspektiven** anzuzeigen, klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf das Menü **Modell** und dann auf **Perspektiven**.  
  
###  <a name="bkmk_add"></a> So fügen Sie eine Perspektive hinzu  
  
-   Zum Hinzufügen einer neuen Perspektive klicken Sie auf **Neue Perspektive**. Anschließend können Sie die einzufügenden Feldobjekte aktivieren und deaktivieren und einen Namen für die neue Perspektive angeben.  
  
     Wenn Sie eine leere Perspektive erstellen, die alle Felder mit Feldobjekten enthält, wird dem Benutzer, der diese Perspektive verwendet, eine leere Feldliste angezeigt. Perspektiven sollten mindestens eine Tabelle und eine Spalte enthalten.  
  
###  <a name="bkmk_edit"></a> So bearbeiten Sie eine Perspektive  
  
-   Zum Ändern einer Perspektive aktivieren bzw. deaktivieren Sie Felder in der Perspektivenspalte, wodurch Feldobjekte der Perspektive hinzugefügt bzw. daraus entfernt werden.  
  
###  <a name="bkmk_rename"></a> So benennen Sie eine Perspektive um  
  
-   Wenn Sie auf die Spaltenüberschrift einer Perspektive (Name der Perspektive) zeigen, wird die Schaltfläche **Umbenennen** angezeigt. Klicken Sie auf **Umbenennen**, um die Perspektive umzubenennen. Geben Sie dann einen neuen Namen ein, oder bearbeiten Sie den vorhandenen Namen.  
  
###  <a name="bkmk_delete"></a> So löschen Sie eine Perspektive  
  
-   Wenn Sie auf die Spaltenüberschrift einer Perspektive (Name der Perspektive) zeigen, wird die Schaltfläche **Löschen** angezeigt. Klicken Sie zum Löschen der Perspektive auf die Schaltfläche **Löschen** , und klicken Sie im Bestätigungsfenster auf **Ja** .  
  
###  <a name="bkmk_copy"></a> So kopieren Sie eine Perspektive  
  
-   Wenn Sie auf die Spaltenüberschrift einer Perspektive zeigen, wird die Schaltfläche **Kopieren** angezeigt. Klicken Sie auf die Schaltfläche **Kopieren** , um eine Kopie dieser Perspektive zu erstellen. Rechts neben den vorhandenen Perspektiven wird eine Kopie der ausgewählten Perspektive als neue Perspektive hinzugefügt. Die neue Perspektive erbt den Namen der kopierten Perspektive, und an das Ende des Namens wird die Anmerkung *-Kopieren* angefügt. Wenn beispielsweise eine Kopie der Perspektive *Sales* erstellt wird, erhält die neue Perspektive den Namen *Sales – Kopie*.  
  
## <a name="see-also"></a>Siehe auch  
 [Perspektiven &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Hierarchien &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)  
  
  
