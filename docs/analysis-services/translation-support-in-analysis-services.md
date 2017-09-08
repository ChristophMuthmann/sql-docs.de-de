---
title: "Unterstützung für Übersetzungen in Analysis Services | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Business Intelligence Development Studio, translations [Analysis Services]
- translations [Analysis Services], about translations
- object translations [Analysis Services]
- language identifiers [Analysis Services]
- attribute translations [Analysis Services]
- translations [Analysis Services]
ms.assetid: 018471e0-3c82-49ec-aa16-467fb58a6d5f
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 27715bc2c9333955931a1bc500a8267c0b1aa954
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="translation-support-in-analysis-services"></a>Unterstützung für Übersetzungen in Analysis Services
  In einem [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Datenmodell können Sie mehrere Übersetzungen einer Beschriftung oder Beschreibung einbetten, um kulturspezifische Zeichenfolgen basierend auf der LCID (Sprachcode-ID) bereitzustellen. Bei mehrdimensionalen Modellen können Übersetzungen für den Datenbanknamen, Cubeobjekte und Datenbankdimensionsobjekte hinzugefügt werden. Bei tabellarischen Modellen können Beschriftungen und Beschreibungen der Tabellen und Spalten übersetzt werden.  
  
 Durch Definieren einer Übersetzung werden die Metadaten und die übersetzte Beschriftung innerhalb des Modells erstellt. Um lokalisierte Zeichenfolgen in einer Clientanwendung zu rendern, müssen Sie jedoch entweder die **Language** -Eigenschaft für das Objekt festlegen oder einen **Culture** - oder **Locale Identifier** -Parameter in der Verbindungszeichenfolge übergeben (z.B. durch Festlegen von `LocaleIdentifier=1036` , um französische Zeichenfolgen zurückzugeben).  
  
 Planen Sie die Verwendung von **Locale Identifier** , wenn Sie mehrere gleichzeitige Übersetzungen desselben Objekts in verschiedenen Sprachen unterstützen möchten. Das Festlegen der **Language** -Eigenschaft funktioniert, hat aber Auswirkungen auf Verarbeitung und Abfragen, die möglicherweise unerwartete Ergebnisse liefern. Das Festlegen von **Locale Identifier** ist die bessere Wahl, da es nur verwendet wird, um die übersetzten Zeichenfolgen zurückzugeben.  
  
 Eine Übersetzung besteht aus einem Gebietsschemabezeichner (LCID), einer übersetzten Beschriftung für das Objekt (z. B. Dimensions- oder Attributname) und optional einer Bindung an eine Spalte, die Datenwerte in der Zielsprache enthält. Sie können mehrere Übersetzungen haben, jedoch nur jeweils eine für eine bestimmte Verbindung verwenden. Theoretisch können Sie beliebig viele Übersetzungen im Modell einbetten. Jede Übersetzung erhöht jedoch die Komplexität beim Testen, und alle Übersetzungen müssen dieselbe Sortierung verwenden. Beim Entwerfen Ihrer Lösung sollten Sie diese natürlichen Einschränkungen bedenken.  
  
> [!TIP]  
>  Sie können Clientanwendungen wie Excel, Management Studio und SQL Server Profiler verwenden, um übersetzte Zeichenfolgen zurückzugeben. Weitere Informationen finden Sie unter [Tipps und Best Practices für die Globalisierung &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) .  
  
## <a name="how-to-add-translated-metadata-to-model-in-analysis-services"></a>Hinzufügen von übersetzten Metadaten zum Modell in Analysis Services  
 Schrittweise Anweisungen erhalten Sie über die folgenden Links:  
  
-   [Übersetzungen in Tabellenmodellen &#40;Analysis Services&#41;](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)  
  
-   [Übersetzungen in mehrdimensionalen Modellen &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Globalisierungsszenarien für Analysis Services](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Sprachen und Sortierungen &#40; Analysis Services &#41;](../analysis-services/languages-and-collations-analysis-services.md)   
 [Festlegen oder Ändern der Spaltensortierung](../relational-databases/collations/set-or-change-the-column-collation.md)   
 [Globalisierung Tipps und Best Practices &#40; Analysis Services &#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md)  
  
  
