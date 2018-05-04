---
title: Erstellen eine Singleton-Abfrage im Datamining-Designer | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 56be277d752c3be83f83b7d657a633d80a9688d6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-singleton-query-in-the-data-mining-designer"></a>Erstellen einer SINGLETON-Abfrage im Data Mining-Designer
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
 [Vorhersageabfragen & #40; Datamining & #41;](../../analysis-services/data-mining/prediction-queries-data-mining.md)  
  
  
