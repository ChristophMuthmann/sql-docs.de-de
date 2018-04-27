---
title: Aggregieren von Werten in einem Dataset mithilfe der Transformation für das Aggregieren | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- aggregate values [Integration Services]
- datasets [Integration Services], aggregate values
ms.assetid: 01b81c0f-d5e0-483b-81b2-73800a6945ac
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b1aa6a99fd0e3109e244cdaeb9988ba75793d005
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="aggregate-values-in-a-dataset-by-using-the-aggregate-transformation"></a>Aggregieren von Werten in einem Dataset mithilfe der Transformation für das Aggregieren
  Um eine Transformation für das Aggregieren hinzuzufügen und zu konfigurieren, muss das Paket bereits mindestens einen Datenflusstask und eine Quelle enthalten.  
  
### <a name="to-aggregate-values-in-a-dataset"></a>So aggregieren Sie Werte in einem Dataset  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Datenfluss** , und ziehen Sie dann aus dem Bereich **Toolbox**die Transformation für das Aggregieren auf die Entwurfsoberfläche.  
  
4.  Verbinden Sie die Transformation für das Aggregieren mit dem Datenfluss, indem Sie einen Konnektor von der Quelle oder der vorherigen Transformation auf die Transformation für das Aggregieren ziehen.  
  
5.  Doppelklicken Sie auf die Transformation.  
  
6.  Klicken Sie im Dialogfeld **Transformations-Editor für Aggregieren** auf die Registerkarte **Aggregationen** .  
  
7.  Aktivieren Sie in der Liste **Verfügbare Eingabespalten** das Kontrollkästchen neben den Spalten, für die Sie Werte aggregieren wollen. Die ausgewählten Spalten werden in der Tabelle angezeigt.  
  
    > [!NOTE]  
    >  Sie können eine Spalte mehrmals auswählen und mehrere Transformationen auf die Spalte anwenden. Um Aggregationen eindeutig zu identifizieren, wird an den Standardnamen des Ausgabealias der Spalte eine Zahl angefügt.  
  
8.  Optional können Sie den Wert in den **Ausgabealias** -Spalten ändern.  
  
9. Um den Standardaggregationsvorgang, **GROUP BY**, zu ändern, wählen Sie in der Liste **Vorgang** einen anderen Vorgang aus.  
  
10. Wählen Sie zum Ändern des Standardvergleichs die jeweiligen in der **Vergleichsflags** -Spalte aufgelisteten Vergleichsflags aus. Beim Vergleichen werden standardmäßig die Groß-/Kleinschreibung, der Kanatyp, Zeichen ohne Zwischenraum und die Zeichenbreite ignoriert.  
  
11. Geben Sie optional für die **COUNT DISTINCT** -Aggregation die genaue Anzahl von unterschiedlichen Werten in der **COUNT DISTINCT-Schlüssel** -Spalte an, oder wählen Sie die geschätzte Anzahl in der **COUNT DISTINCT-Skala** -Spalte aus.  
  
    > [!NOTE]  
    >  Durch Bereitstellen der genauen oder geschätzten Anzahl von unterschiedlichen Werten wird die Leistung optimiert, da die Transformation die hierfür erforderliche Arbeitsspeichermenge zuordnen kann.  
  
12. Klicken Sie optional auf **Erweitert** , und aktualisieren Sie den Namen der Ausgabe für die Transformation für das Aggregieren. Wenn die Aggregationen einen **Group By** -Vorgang einschließen, können Sie die geschätzte Anzahl von Gruppierungsschlüsselwerten in der **Schlüsselskala** -Spalte auswählen oder die genaue Anzahl von Gruppierungsschlüsselwerten in der **Schlüssel** -Spalte angeben.  
  
    > [!NOTE]  
    >  Durch Bereitstellen der genauen oder geschätzten Anzahl von unterschiedlichen Werten wird die Leistung optimiert, da die Transformation die hierfür erforderliche Arbeitsspeichermenge zuordnen kann.  
  
    > [!NOTE]  
    >  Die Optionen **Schlüsselskala** und **Schlüssel** schließen sich gegenseitig aus. Wenn Sie in beide Spalten Werte eingeben, wird der jeweils größere Wert der **Schlüsselskala** -Spalte bzw. der **Schlüssel** -Spalte verwendet.  
  
13. Klicken Sie optional auf die Registerkarte **Erweitert** , und legen Sie die Attribute fest, die zum Optimieren aller Vorgänge gelten, die die Transformation für das Aggregieren ausführt.  
  
14. Klicken Sie auf **OK**.  
  
15. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Transformation für das Aggregieren](../../../integration-services/data-flow/transformations/aggregate-transformation.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [SQL Server Integration Services-Pfade](../../../integration-services/data-flow/integration-services-paths.md)   
 [Datenflusstask](../../../integration-services/control-flow/data-flow-task.md)  
  
  
