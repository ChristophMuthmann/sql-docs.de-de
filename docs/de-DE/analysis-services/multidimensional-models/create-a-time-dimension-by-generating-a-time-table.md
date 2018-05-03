---
title: Erstellen eine Zeitdimension durch Generieren einer Zeittabelle | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2c5526075c563bfea107592c6e0d583feff3fde2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-time-dimension-by-generating-a-time-table"></a>Erstellen einer Zeitdimension durch Generieren einer Zeittabelle
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]können Sie mit dem Dimensions-Assistenten von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] eine Zeitdimension erstellen, auch wenn keine Zeittabelle in der Quelldatenbank vorhanden ist. Sie können dies ausführen, indem Sie eine der folgenden Optionen auf der Seite **Erstellungsmethode auswählen** auswählen:  
  
-   **Zeittabelle in der Datenquelle generieren** Wählen Sie diese Option, wenn Sie zum Erstellen von Objekten in der zugrunde liegenden Datenquelle berechtigt sind. Der Assistent generiert dann eine Zeittabelle und speichert diese Tabelle in der Datenquelle. Der Assistent erstellt anschließend die Zeitdimension basierend auf dieser Zeittabelle.  
  
-   **Zeittabelle auf dem Server generieren** Wählen Sie diese Option, wenn Sie nicht zum Erstellen von Objekten in der zugrunde liegenden Datenquelle berechtigt sind. Der Assistent generiert dann eine Zeittabelle und speichert sie auf dem Server anstatt in der Datenquelle. (Eine auf dem Server aus einer Zeittabelle erstellte Dimension wird als *Serverzeitdimension* bezeichnet.) Der Assistent erstellt anschließend die Serverzeitdimension basierend auf dieser Tabelle.  
  
 Wenn Sie eine Zeitdimension erstellen, werden die Zeiträume sowie das Anfangs- und Enddatum der Dimension angegeben. Mithilfe der angegebenen Zeiträume werden im Assistenten die Zeitattribute erstellt. Beim Verarbeiten der Dimension werden in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die zur Unterstützung der angegebenen Datumsangaben und Zeiträume erforderlichen Daten generiert und gespeichert. Der Assistent verwendet die für eine Zeitdimension erstellten Attribute, um Hierarchien für die Dimension zu empfehlen. Die Hierarchien spiegeln die Beziehungen zwischen den verschiedenen Zeiträumen wider und berücksichtigen die unterschiedlichen Kalender. In der Hierarchie eines Standardkalenders wird beispielsweise die Weeks-Ebene unter der Years-Ebene, jedoch nicht unter der Month-Ebene angezeigt, da Wochen gleichmäßig in Jahre, jedoch nicht in Monate unterteilt werden. In der Hierarchie eines Produktions- oder Berichtskalenders hingegen sind die Wochen gleichmäßig in Monate unterteilt, sodass die Weeks-Ebene unter der Month-Ebene angezeigt wird.  
  
## <a name="define-time-periods"></a>Zeiträume definieren  
 Geben Sie den Datumsbereich, der in der Dimension enthalten sein soll, mithilfe der Seite **Zeiträume definieren** des Assistenten an. Beispielsweise wählen Sie einen Bereich aus, der in Ihren Daten am 1. Januar des ersten Jahres beginnt und (zur Unterstützung zukünftiger Transaktionen) ein oder zwei Jahre nach dem aktuellen Jahr endet. Transaktionen außerhalb dieses Bereichs werden entweder nicht angezeigt, oder sie werden als unbekannte Elemente in der Dimension angezeigt, abhängig von der Einstellung der **UnknownMemberVisible** -Eigenschaft für die Dimension. Sie können auch den in Ihren Daten verwendeten Wochenbeginn ändern. (Der Standard ist Sonntag.)  
  
 Wählen Sie für die Erstellung der Hierarchien durch den Assistenten beliebige Zeiträume aus, die Ihren Daten zugeordnet sind, wie z. B. Jahre, Halbjahre, Quartale, Trimester, Monate, zehn Tage, Wochen oder Datumsangaben. Sie müssen für Date immer mindestens den Zeitraum auswählen. Das Date-Attribut ist das Schlüsselattribut für die Dimension. Ohne dieses Attribut ist die Dimension funktionslos.  
  
 Wählen Sie neben **Sprache für die Namen der Zeitelemente**die Sprache aus, die zum Bezeichnen der Dimensionselemente verwendet werden soll.  
  
 Nachdem Sie eine auf einem Datumsbereich basierte Zeitdimension erstellt haben, können Sie mit dem Dimensions-Designer Zeitattribute hinzufügen oder entfernen. Das Date-Attribut kann nicht aus der Dimension entfernt werden, da es das Schlüsselattribut der Dimension darstellt. Sie können die **AttributeHierarchyVisible** -Eigenschaft des Date-Attributs in **False**ändern, um es für Benutzer auszublenden.  
  
## <a name="select-calendars"></a>Kalender auswählen  
 Beim Erstellen einer Zeitdimension wird stets der 12-monatige Standardkalender (gregorianischer Kalender) eingeschlossen, welcher am 1. Januar beginnt und am 31. Dezember endet. Sie können im Assistenten auf der Seite **Kalender auswählen** zusätzliche Kalender angeben, auf denen Sie die Hierarchien der Dimension basieren möchten. Eine Beschreibung der Kalenderarten finden Sie unter [Erstellen einer Datumstypdimension](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md).  
  
 Abhängig davon, welche Zeiträume Sie im Assistenten auf der Seite **Zeiträume definieren** auswählen, werden auf Basis der ausgewählten Kalender die in der Dimension erstellten Attribute bestimmt. Wenn Sie im Assistenten auf der Seite **Zeiträume definieren** beispielsweise die Zeiträume **Jahr** und **Quartal** auswählen, und auf der Seite **Kalender auswählen** die Option **Geschäftskalender** auswählen, werden die FiscalYear-, FiscalQuarter- und FiscalQuarterOfYear-Attribute für den Geschäftskalender erstellt.  
  
 Der Assistent erstellt ebenfalls kalenderspezifische Hierarchien, die sich aus den für den Kalender erstellten Attributen zusammensetzen. In jedem Kalender werden die einzelnen Ebenen der Hierarchien zusammengefasst und ergeben so die jeweils nächst höhere Ebene. Im 12-monatigen Standardkalender wird beispielsweise über den Assistenten eine Hierarchie erstellt, bestehend aus den Jahres- und Wochenebenen bzw. den Jahres- und Monatsebenen. Die Wochen sind allerdings nicht gleichmäßig in Monate eines Standardkalenders unterteilt, sodass keine Hierarchie zwischen den Jahres-, Monats- und Wochenebenen besteht. Die in einem Berichts- oder Produktionskalender enthaltenen Wochen sind hingegen gleichmäßig in Monate unterteilt, sodass sich aus den in diesen Kalendern enthaltenen Wochen Monate ergeben.  
  
## <a name="completing-the-dimension-wizard"></a>Abschließen des Dimensions-Assistenten  
 Prüfen Sie auf der Seite **Assistenten abschließen** die vom Assistenten erstellten Attribute und Hierarchien, und benennen Sie dann die Zeitdimension. Klicken Sie auf **Fertig stellen** , um den Assistenten abzuschließen und die Dimension zu erstellen. Nachdem Sie die Dimension abgeschlossen haben, können Sie sie mithilfe des Dimensions-Designers ändern.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenquellsichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Erstellen einer datumstypdimension](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md)   
 [Eigenschaften von Datenbankdimensionen](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)   
 [Dimensionsbeziehungen](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Erstellen einer Dimension durch Generieren einer Nichtzeittabelle in der Datenquelle](../../analysis-services/multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  
