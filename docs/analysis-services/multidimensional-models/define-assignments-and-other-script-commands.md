---
title: Definieren von Zuweisungen und anderen Skriptbefehlen | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 024a70622607b3c40af491320085199c921f23fe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="define-assignments-and-other-script-commands"></a>Definieren von Zuweisungen und anderen Skriptbefehlen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Klicken Sie im Cube-Designer auf der Registerkarte **Berechnungen** auf der Symbolleiste auf das Symbol **Neuer Skriptbefehl** , um ein leeres Skript zu erstellen. Wenn Sie ein neues Skript erstellen, wird es zunächst mit einem leeren Titel im Bereich **Skriptplaner** auf der Registerkarte Berechnungen angezeigt. Die von Ihnen im Bereich für Berechnungsausdrücke eingegebenen Zeichen werden als Name des Elements in **Skriptplaner**angezeigt. Daher können Sie einen kommentierten Namen in die erste Zeile eingeben, damit Sie das Skript im Bereich **Skriptplaner** leichter identifizieren können. Weitere Informationen finden Sie unter [Introduction to MDX Scripting in Microsoft SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81892)(in Englisch). Weitere Informationen zu Leistungsproblemen im Zusammenhang mit MDX-Abfragen und -Berechnungen finden Sie im Abschnitt "Writing Efficient MDX" unter [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621)(in Englisch).  
  
> [!IMPORTANT]  
>  Wenn Sie zum ersten Mal zur Registerkarte **Berechnungen** im Cube-Designer wechseln, enthält der Bereich **Skriptplaner** ein einzelnes Skript mit einem CALCULATE-Befehl. Mit dem CALCULATE-Befehl wird die Aggregation der Zellen im Cube gesteuert. Er sollte nur bearbeitet werden, wenn Sie die Aggregation des Cubes manuell angeben möchten.  
  
 Verwenden Sie den Bereich für Berechnungsausdrücke, um einen Ausdruck in MDX-Syntax (Multidimensional Expressions) zu erstellen. Während Sie den Ausdruck erstellen, können Sie die Cubekomponenten, Funktionen und Vorlagen aus dem Bereich **Berechnungstools** in den Bereich für Berechnungsausdrücke ziehen oder kopieren. Dadurch wird das Skript für das Element dem Bereich für Berechnungsausdrücke an der Position hinzugefügt, an der Sie es ablegen oder einfügen. Ersetzen Sie die Argumente und ihre Trennzeichen (« und ») durch den entsprechenden Wert.  
  
> [!IMPORTANT]  
>  Wenn Sie einen Ausdruck mit mehreren Anweisungen schreiben, indem Sie den Bereich für Berechnungsausdrücke verwenden, müssen Sie sicherstellen, dass alle Zeilen außer der letzten Zeile des MDX-Skripts mit einem Semikolon (;) enden. Berechnungen werden in einem einzelnen MDX-Skript verkettet, und an jedes Skript wird ein Semikolon angefügt, um sicherzustellen, dass das MDX-Skript ordnungsgemäß kompiliert wird. Falls Sie der letzten Skriptzeile im Bereich für Berechnungsausdrücke ein Semikolon hinzufügen, wird der Cube erstellt und ordnungsgemäß bereitgestellt. Es können jedoch keine Abfragen für ihn ausgeführt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Berechnungen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
