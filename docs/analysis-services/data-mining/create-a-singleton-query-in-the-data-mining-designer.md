---
title: Erstellen eine Singleton-Abfrage im Datamining-Designer | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- singleton queries [Analysis Services]
- Mining Model Prediction [Analysis Services], singleton queries
ms.assetid: 6cdca8a0-cf16-46eb-a652-0bff820625ab
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dfbb55881c274dee8560cbba14319bcc831b38c2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-singleton-query-in-the-data-mining-designer"></a>Erstellen einer SINGLETON-Abfrage im Data Mining-Designer
  Eine SINGLETON-Abfrage ist nützlich, wenn Sie eine Vorhersage für einen einzelnen Fall erstellen möchten. Weitere Informationen zu SINGLETON-Abfragen finden Sie unter [Data Mining-Abfragen](../../analysis-services/data-mining/data-mining-queries.md).  
  
 Auf der Registerkarte **Miningmodellvorhersage** im Data Mining-Designer können Sie zahlreiche unterschiedliche Abfragetypen erstellen. Sie können eine Abfrage mit dem Designer erstellen oder durch das Eingeben von DMX-Anweisungen (Data Mining-Erweiterungen). Sie können auch mit dem Designer beginnen und die auf diese Weise erstellte Abfrage durch Änderung der DMX-Anweisungen oder durch Hinzufügen einer WHERE- oder ORDER BY-Klausel anpassen.  
  
 Um zwischen der Abfragedesignansicht und der Abfragetextansicht zu wechseln, klicken Sie auf die erste Schaltfläche auf der Symbolleiste. Wenn Sie sich in der Abfragetextansicht befinden, können Sie den vom Generator für Vorhersageabfragen erstellten DMX-Code sehen. Sie können auch die Abfrage ausführen und ändern und dann die geänderte Abfrage erneut ausführen. Die geänderte Abfrage wird jedoch nicht persistent gespeichert, wenn Sie zurück zur Entwurfssicht wechseln.  
  
 Im folgenden Code wird ein Beispiel einer SINGLETON-Abfrage für das Targeted Mailing-Modell TM_Decision_Tree veranschaulicht.  
  
```  
SELECT [Bike Buyer], PredictProbability([Bike Buyer]) as ProbableBuyer  
FROM [TM_Decision_Tree]  
NATURAL PREDICTION JOIN  
(SELECT '2' AS [Number Children At Home], '45' as [Age])  
AS [t]  
```  
  
 Die folgenden Schritte erläutern, wie diese Vorhersageabfrage erstellt wird.  
  
### <a name="to-create-a-singleton-query-by-using-the-data-mining-designer"></a>So erstellen Sie eine SINGLETON-Abfrage mithilfe des Data Mining-Designers  
  
1.  Klicken Sie auf die **Miningmodellvorhersage** -Registerkarte im Data Mining-Designer.  
  
2.  Klicken Sie in der **Miningmodell** -Tabelle auf **Modell auswählen** .  
  
     Das Dialogfeld **Miningmodell auswählen** wird geöffnet. Es zeigt alle Miningstrukturen an, die im aktuellen Projekt vorhanden sind.  
  
     Wählen Sie das Modell aus, das Sie zum Erstellen einer Vorhersage verwenden möchten.  
  
     Wählen Sie TM_Decision_Tree aus, und klicken Sie auf **OK**, um beispielsweise den Beispielcode zu Beginn dieses Themas zu erstellen.  
  
3.  Klicken Sie auf der Symbolleiste der Registerkarte **Miningmodellvorhersage** auf **SINGLETON-Abfrage** .  
  
     Die Tabelle **SINGLETON-Abfrageeingabe** wird auf der Registerkarte angezeigt, deren Spalten automatisch den Spalten in der **Miningmodell** -Tabelle zugeordnet sind.  
  
4.  Wählen Sie in der **SINGLETON-Abfrageeingabe** -Tabelle in der **Wert** -Spalte Werte aus, mit denen der Fall beschrieben wird, für den Sie eine Vorhersage erstellen möchten.  
  
     Wählen Sie beispielsweise für **Number Children At Home** den Wert **2**aus, und geben Sie für **Age** den Wert **45**ein.  
  
5.  Ziehen Sie eine vorhersagbare Spalte aus der **Miningmodell** -Tabelle in die **Quelle** -Spalte unten auf der Registerkarte. Optional können Sie einen Alias für die Spalte eingeben.  
  
     Ziehen Sie beispielsweise **Bike Buyer** in die Spalte **Quelle** .  
  
6.  Fügen Sie je nach Bedarf die zusätzlichen Funktionen der Abfrage hinzu, indem Sie **Vorhersagefunktion** oder **Benutzerdefinierter Ausdruck** aus der Dropdownliste in der **Quelle** -Spalte auswählen.  
  
     Klicken Sie beispielsweise auf **Vorhersagefunktion**, und wählen Sie **PredictProbability**aus.  
  
7.  Klicken Sie in der Zeile **PredictProbability** auf **Kriterium/Argument** , und geben Sie den Namen der vorherzusagenden Spalte ein und optional einen bestimmten vorherzusagenden Wert.  
  
     Geben Sie beispielsweise **[Fahrradkäufer], 1**ein.  
  
8.  Klicken Sie in der Zeile **PredictProbability** auf das Feld **Alias** , und geben Sie einen Verweisnamen für die neue Spalte ein.  
  
     Beispiel: **ProbableBuyer**.  
  
9. Klicken Sie auf der Symbolleiste der Registerkarte **Miningmodellvorhersage** auf **Zur Abfragergebnissicht wechseln** .  
  
     Ein neuer Bildschirm wird geöffnet, der das Ergebnis der Abfrage anzeigt. Um die DMX-Anweisung anzuzeigen, die Sie gerade erstellt haben, klicken Sie auf **SQL**.  
  
## <a name="see-also"></a>Siehe auch  
 [Vorhersageabfragen &#40;Data Mining&#41;](../../analysis-services/data-mining/prediction-queries-data-mining.md)  
  
  

