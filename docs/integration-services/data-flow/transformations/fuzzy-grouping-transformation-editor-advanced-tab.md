---
title: "Für die Fuzzysuche Transformations-Editor (Registerkarte \"Erweitert\") | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.fuzzygroupingtransformation.advanced.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: dd820d75-b8a7-4515-aea4-3553ba5b442e
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2eb40d25a2deef0cb95971bf73bb2af4d44cf3c2
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="fuzzy-grouping-transformation-editor-advanced-tab"></a>Transformations-Editor für Fuzzygruppierung (Registerkarte Erweitert)
  Geben Sie mithilfe der Registerkarte **Erweitert** von **Transformations-Editor für Fuzzygruppierung** die Ein- und Ausgabespalten an, legen Sie Schwellenwerte für die Ähnlichkeit fest, und definieren Sie Begrenzungszeichen.  
  
> [!NOTE]  
>  Die **Exhaustive** - und **MaxMemoryUsage** -Eigenschaften der Transformation für Fuzzgruppierung sind im **Transformations-Editor für Fuzzygruppierung**nicht verfügbar, können jedoch mit dem Dialogfeld **Erweiterter Editor**festgelegt werden. Weitere Informationen zu diesen Eigenschaften finden Sie im Abschnitt Transformation für Fuzzgruppierung von [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Weitere Informationen zur Transformation für Fuzzygruppierung finden Sie unter [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## <a name="options"></a>enthalten  
 **Name der Eingabeschlüsselspalte**  
 Geben Sie den Namen einer Ausgabespalte an, die den eindeutigen Bezeichner für jede Eingabezeile enthält. Die **_key_in** -Spalte enthält einen für jede Zeile eindeutigen Wert.  
  
 **Name der Ausgabeschlüsselspalte**  
 Geben Sie den Namen einer Ausgabespalte an, die den eindeutigen Bezeichner für die kanonische Zeile einer Gruppe doppelter Zeilen enthält. Die **_key_out** -Spalte entspricht dem **_key_in** -Wert der kanonischen Datenzeile.  
  
 **Name der Ähnlichkeitsergebnisspalte**  
 Geben Sie einen Namen für die Spalte an, die das Ähnlichkeitsergebnis enthält. Das Ähnlichkeitsergebnis ist ein Wert zwischen 0 und 1, der die Ähnlichkeit zwischen der Eingabezeile und der kanonischen Zeile anzeigt. Je näher das Ergebnis an 1 liegt, desto genauer stimmt die Zeile mit der kanonischen Zeile überein.  
  
 **Schwellenwert für Ähnlichkeit**  
 Legen Sie den Schwellenwert für die Ähnlichkeit mithilfe des Schiebereglers fest. Je näher der Schwellenwert an 1 kommt, desto mehr müssen die Zeilen einander ähneln, um als Duplikate angesehen zu werden. Durch eine Erhöhung des Schwellenwertes kann die Geschwindigkeit beim Abgleich erhöht werden, weil als Kandidaten dann weniger Datensätze berücksichtigt werden müssen.  
  
 **Tokentrennzeichen**  
 Die Transformation bietet einen Standardsatz von Trennzeichen, um Daten mit Tokens zu versehen. Sie können durch Bearbeiten der Liste aber ggf. Trennzeichen hinzufügen oder entfernen.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Identifizieren Sie ähnlicher Datenzeilen mithilfe der Transformation für Fuzzygruppierung](../../../integration-services/data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
