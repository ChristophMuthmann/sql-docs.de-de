---
title: "Hinzufügen von Kontointelligenz zu einer Dimension | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], Business Intelligence enhancements
- Business Intelligence enhancements [Analysis Services], account intelligence
- account intelligence [Analysis Services]
ms.assetid: 36f454ae-a9f2-4a59-b19d-40310af9f901
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 970daabf89244a93719e273b4bff7f322cb23fe6
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="bi-wizard---add-account-intelligence-to-a-dimension"></a>BI-Assistent – Hinzufügen von Kontointelligenz zu einer Dimension
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Die Kontointelligenzerweiterung kann einem Cube oder eine Dimension hinzugefügt werden, um Elementen eines Kontoattributs Standardkontoklassifikationen wie Einnahmen und Ausgaben zuzuweisen. Diese Erweiterung identifiziert auch Kontotypen (wie Asset und Liability) und weist jedem Kontotyp die entsprechende Aggregation zu. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] kann die Klassifikationen zum Aggregieren von Konten über die Zeit verwenden.  
  
> [!NOTE]  
>  Kontointelligenz ist nur für Dimensionen verfügbar, die auf vorhandenen Datenquellen basieren. Für Dimensionen, die ohne Datenquelle erstellt wurden, müssen Sie den Schemagenerierungs-Assistenten ausführen, um vor dem Hinzufügen von Kontointelligenz eine Datenquellensicht zu erstellen.  
  
 Sie wenden Kontointelligenz auf eine Dimension an, die Kontoinformationen festlegt (z. B. Kontonamen, Kontonummer und Kontotyp). Verwenden Sie zum Hinzufügen von Intelligenz den Business Intelligence-Assistenten, und wählen Sie die Option **Kontointelligenz definieren** auf der Seite **Erweiterung auswählen** aus. Der Assistent leitet Sie dann durch die Schritte zum Auswählen einer Dimension, der Sie Kontointelligenz zuweisen wollen, zum Identifizieren von Kontoattributen in der ausgewählten Kontodimension und dem anschließenden Zuordnen von Kontotypen in der Dimensionstabelle zu Kontotypen, die von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erkannt werden.  
  
## <a name="selecting-a-dimension"></a>Auswählen einer Dimension  
 Auf der ersten Seite **Kontointelligenz definieren** des Assistenten geben Sie die Dimension an, der Sie Kontointelligenz hinzufügen möchten. Die der ausgewählten Dimension hinzugefügte Kontointelligenzerweiterung führt zu Änderungen an der Dimension. Diese Änderungen werden an alle Cubes vererbt, die die ausgewählte Dimension enthalten.  
  
## <a name="specifying-account-attributes"></a>Festlegen von Kontoattributen  
 Auf der Seite **Dimensionsattribute konfigurieren** des Assistenten legen Sie die Kontoattribute in der ausgewählten Kontodimension fest. Aktivieren Sie dazu zunächst in der Spalte **Einschließen** das Kontrollkästchen neben den jeweiligen Kontoattributtypen, die Sie einem Dimensionsattribut in der Dimension zuordnen wollen. Erweitern Sie anschließend in der Spalte **Dimensionsattribut** die Dropdownliste, und wählen Sie das Attribut in der Dimension aus, das dem ausgewählten Attributtyp entspricht. Durch das Auswählen des Attributs aus der Liste wird die **Type** -Attributeigenschaft für die Kontoattribute festgelegt.  
  
## <a name="mapping-account-types"></a>Zuordnen von Kontotypen  
 Auf der zweiten Seite **Kontointelligenz definieren** werden die Kontotypwerte aus der Dimensionstabelle Kontotypen zugeordnet, die von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erkannt werden. Diese Seite wird nur angezeigt, wenn Sie das **Account Type** -Dimensionsattribut in die Dimension aufgenommen haben. Um die **Account Type** -Dimension aufzunehmen, aktivieren Sie auf der Seite **Kontointelligenzeinstellungen definieren** des Assistenten das Kontrollkästchen neben **Kontotyp**, und wählen Sie dann das entsprechende Attribut aus.  
  
 Auf der zweiten Seite **Kontointelligenz definieren** gibt es zwei Spalten:  
  
-   In der Spalte **Kontotypen der Quelltabelle** sind alle Kontotypen aufgelistet, die der Assistent aus der Dimensionstabelle erhält.  
  
-   Die Spalte **Serverkontotypen** identifiziert den entsprechenden Kontotyp, der von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erkannt wird. In der folgenden Tabelle sind die Kontotypen aufgelistet, die von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erkannt werden, sowie die Standardaggregation für die einzelnen Typen. Die Auswahl erfolgt automatisch, wenn die Dimensionstabelle dieselben Kontotypnamen verwendet wie [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
    |Serverkontotyp|Aggregation|Description|  
    |-------------------------|-----------------|-----------------|  
    |**Statistisch**|**InclusionThresholdSetting**|Ein berechnetes Verhältnis von etwas oder eine Anzahl von etwas, das nicht im Verlauf der Zeit aggregiert wird. Für diesen Kontotyp wird keine Konvertierung von Währungsdaten mit Konvertierungsregeln ausgeführt.|  
    |**Liability**|**LastNonEmpty**|Das Geld oder der Wert von Dingen, das bzw. der zu einem bestimmten Zeitpunkt geschuldet wird. Für diesen Kontotyp werden im Verlauf der Zeit keine Akkumulierungen und daher auch keine natürlichen Aggregationen ausgeführt. So entspricht z. B. die Menge für Year dem Wert des letzten Monats, der Daten enthält. Für diesen Kontotyp können Währungen mit dem zum End of Period-Zeitpunkt gültigen Wechselkurs konvertiert werden.|  
    |**Asset**|**LastNonEmpty**|Das Geld oder der Wert von Dingen, die zu einem bestimmten Zeitpunkt im Besitz sind. Für diesen Kontotyp werden im Verlauf der Zeit Akkumulierungen und somit keine natürlichen Aggregationen ausgeführt. So entspricht z. B. die Menge für Year dem Wert des letzten Monats, der Daten enthält. Für diesen Kontotyp können Währungen mit dem zum End of Period-Zeitpunkt gültigen Wechselkurs konvertiert werden.|  
    |**Balance**|**LastNonEmpty**|Die Anzahl von etwas zu einem bestimmten Zeitpunkt. Für diesen Kontotyp werden im Verlauf der Zeit Akkumulierungen, jedoch keine natürlichen Aggregationen ausgeführt. So entspricht z. B. die Menge für Year dem Wert des letzten Monats, der Daten enthält.|  
    |**Flow**|**Sum**|Eine inkrementelle Anzahl von etwas. Dieser Kontotyp wird im Verlauf der Zeit als **Sum** aggregiert, es werden jedoch keine Konvertierungen mithilfe von Regeln zur Währungskonvertierung ausgeführt.|  
    |**Expense**|**Sum**|Ausgegebenes Geld oder der Wert, der für Dinge ausgegeben wurde. Dieser Kontotyp wird im Verlauf der Zeit als **Sum** aggregiert, und Währungen werden mit einem Durchschnittskurs konvertiert.|  
    |**Income**|**Sum**|Erhaltenes Geld oder der Wert von erhaltenen Dingen. Dieser Kontotyp wird im Verlauf der Zeit als **Sum** aggregiert, und Währungen werden mit einem Durchschnittskurs konvertiert.|  
  
    > [!NOTE]  
    >  Sie können einem bestimmten Serverkontotyp ggf. mehrere Kontotypen in der Dimension zuordnen.  
  
 Mit dem Datenbank-Designer können Sie die Standardaggregationen ändern, die den einzelnen Kontotypen für eine Datenbank zugeordnet sind.  
  
1.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Analysis Services-Projekt, und klicken Sie auf **Datenbank bearbeiten**.  
  
2.  Wählen Sie im Feld **Kontotypzuordnung** im Dropdown-Listenfeld **Name**einen Kontotyp aus.  
  
3.  Geben Sie im Textfeld **Alias** einen Alias für diesen Kontotyp ein.  
  
4.  Ändern Sie im Dropdown-Listenfeld **Aggregationsfunktion** die Standardaggregationsfunktion für diesen Kontotyp.  
  
  
