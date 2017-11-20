---
title: Spalte Wert Profil Anforderung Verteilungsoptionen (Datenprofilerstellungs-Task) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: c1e5f5de-04f5-4d00-a9f0-55817186bdf9
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 79ce587ac6e1f0da8bf0c2ae237b6b9c3ae2623f
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="column-value-distribution-profile-request-options-data-profiling-task"></a>Optionen für Anforderung für Verteilungsprofil für Spaltenwert (Datenprofilerstellungs-Task)
  Verwenden Sie den Bereich **Anforderungseigenschaften** der Seite **Profilanforderungen** , um die Optionen für die im Anforderungsbereich ausgewählte **Anforderung für Verteilungsprofil für Spaltenwert** festzulegen. Ein Verteilungsprofil für Spaltenwert dokumentiert alle eindeutigen Längen von Zeichenfolgenwerten in der ausgewählten Spalte sowie den Prozentsatz der Zeilen in der Tabelle, die jeder Wert darstellt. Das Profil kann auch Werte melden, die mehr als einen angegebenen Prozentwert der Zeilen in der Tabelle darstellen. Dieses Profil hilft Ihnen, Probleme mit den Daten zu identifizieren, z. B. eine falsche Anzahl eindeutiger Werte in einer Spalte. Beispiel: Sie erstellen ein Profil für eine Spalte mit US-Bundesstaaten und ermitteln mehr als 50 unterschiedliche Werte.  
  
> [!NOTE]  
>  Die in diesem Thema beschriebenen Optionen werden auf der Seite **Profilanforderungen** im **Editor für den Datenprofilerstellungs-Task**angezeigt. Weitere Informationen zu dieser Seite des Editors finden Sie unter [Editor für den Datenprofilerstellungs-Task &#40;Seite „Profilanforderungen“&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Weitere Informationen zum Verwenden des Datenprofilerstellungs-Tasks finden Sie unter [Einrichten von Datenprofilerstellungs-Tasks](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Weitere Informationen zum Verwenden des Datenprofil-Viewers zum Analysieren der Ausgabe des Datenprofilerstellungs-Tasks finden Sie unter [Datenprofil-Viewer](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="request-properties-options"></a>Optionen für Anforderungseigenschaften  
 Für eine **Anforderung für Verteilungsprofil für Spaltenwert**zeigt der Bereich **Anforderungseigenschaften** die folgenden Gruppen von Optionen an:  
  
-   **Daten**, die die Optionen **TableOrView** und **Spalte** enthalten  
  
-   **Allgemein**  
  
-   **Options**  
  
### <a name="data-options"></a>Datenoptionen  
 **ConnectionManager**  
 Wählen Sie den vorhandenen [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager aus, der den .NET-Datenanbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) verwendet, um eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank herzustellen, die die Tabelle oder Sicht enthält, für die ein Profil erstellt werden soll.  
  
 **TableOrView**  
 Wählen Sie die vorhandene Tabelle oder die Sicht aus, die die Spalte enthält, für die ein Profil erstellt werden soll.  
  
 Weitere Informationen finden Sie im Abschnitt "TableorView-Optionen" in diesem Thema.  
  
 **Spalte**  
 Wählen Sie die vorhandene Spalte aus, für die ein Profil erstellt werden soll. Wählen Sie **(\*)** aus, um ein Profil für alle Spalten zu erstellen.  
  
 Weitere Informationen finden Sie im Abschnitt "Spaltenoptionen" in diesem Thema.  
  
#### <a name="tableorview-options"></a>TableOrView-Optionen  
 **Schema**  
 Gibt das Schema an, zu dem die ausgewählte Tabelle gehört. Diese Option ist schreibgeschützt.  
  
 **Tabelle**  
 Zeigt den Namen der ausgewählten Tabelle an. Diese Option ist schreibgeschützt.  
  
#### <a name="column-options"></a>Spaltenoptionen  
 **IsWildCard**  
 Gibt an, ob der Platzhalter **(\*)** ausgewählt wurde. Diese Option wird auf **TRUE** festgelegt, wenn Sie **(\*)** ausgewählt haben, um ein Profil für alle Spalten zu erstellen. Die Option wird auf **False** festgelegt, wenn Sie eine einzelne Spalte ausgewählt haben, für die ein Profil erstellt werden soll. Diese Option ist schreibgeschützt.  
  
 **ColumnName**  
 Zeigt den Namen der ausgewählten Spalte an. Diese Option ist leer, wenn Sie **(\*)** ausgewählt haben, um ein Profil für alle Spalten zu erstellen. Diese Option ist schreibgeschützt.  
  
 **StringCompareOptions**  
 Wählen Sie Optionen zum Vergleichen von Zeichenfolgenwerten aus. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen. Der Standardwert für diese Option ist **Default**.  
  
> [!NOTE]  
>  Wenn Sie den Platzhalter **(\*)** für **ColumnName** verwenden, ist **CompareOptions** schreibgeschützt und auf die **Default**-Einstellung festgelegt.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Default**|Sortiert und vergleicht Daten anhand der Sortierung der Spalte in der Quelltabelle.|  
|**BinarySort**|Sortiert und vergleicht Daten anhand der für jedes Zeichen definierten Bitmuster. Die binäre Sortierreihenfolge unterscheidet nach Groß- und Kleinschreibung und nach Akzent. Die Option Binär ist zudem die schnellste Sortierreihenfolge.|  
|**DictionarySort**|Sortiert und vergleicht Daten anhand der Sortier- und Vergleichsregeln, die in Wörterbüchern für die zugeordnete Sprache definiert sind, oder nach dem jeweiligen Alphabet.|  
  
 Wenn Sie **DictionarySort**auswählen, können Sie auch jede Kombination der in der folgenden Tabelle aufgelisteten Optionen auswählen. Standardmäßig ist keine dieser zusätzlichen Optionen ausgewählt.  
  
|Wert|Description|  
|-----------|-----------------|  
|**IgnoreCase**|Gibt an, ob beim Vergleichen zwischen Groß- und Kleinbuchstaben unterschieden wird. Falls diese Option festgelegt ist, ignoriert der Zeichenfolgenvergleich die Groß-/Kleinschreibung. Beispielsweise ist dann "ABC" mit "abc" identisch.|  
|**IgnoreNonSpace**|Gibt an, ob beim Vergleichen zwischen Zeichen mit Zwischenraum und diakritischen Zeichen unterschieden wird. Falls diese Option festgelegt ist, ignoriert der Zeichenfolgenvergleich diakritische Zeichen. Beispielsweise ist dann "å" mit "a" identisch.|  
|**IgnoreKanaType**|Gibt an, ob beim Vergleichen zwischen den beiden Typen japanischer Kanazeichen unterschieden wird: Hiragana und Katakana. Falls diese Option festgelegt ist, ignoriert der Zeichenfolgenvergleich den Kanatyp.|  
|**IgnoreWidth**|Gibt an, ob beim Vergleichen zwischen einem Single-Byte-Zeichen und demselben Zeichen als Double-Byte-Zeichen unterschieden wird. Wenn diese Option festgelegt ist, werden die Single-Byte- und die Double-Byte-Darstellung desselben Zeichens als identisch behandelt.|  
  
### <a name="general-options"></a>Allgemeine Optionen  
 **RequestID**  
 Geben Sie einen beschreibenden Namen ein, um diese Profilanforderung zu kennzeichnen. In der Regel müssen Sie den automatisch generierten Wert nicht ändern.  
  
### <a name="options"></a>enthalten  
 **ValueDistributionOption**  
 Geben Sie an, ob die Verteilung für alle Spaltenwerte berechnet werden soll. Der Standardwert für diese Option ist **FrequentValues**.  
  
|Wert|Description|  
|-----------|-----------------|  
|**AllValues**|Die Verteilung wird für alle Spaltenwerte berechnet.|  
|**FrequentValues**|Die Verteilung wird nur für Werte berechnet, deren Frequenz den in **FrequentValueThreshold**angegebenen minimalen Wert übersteigt. Werte, die nicht dem Wert von **FrequentValueThreshold** entsprechen, werden im Ausgabebericht ausgeschlossen.|  
  
 **FrequentValueThreshold**  
 Geben Sie (mit einem Wert zwischen 0 und 1) den Schwellenwert an, bei dessen Überschreiten der Spaltenwert gemeldet werden sollte. Diese Option wird deaktiviert, wenn Sie **AllValues** als **ValueDistributionOption**auswählen. Der Standardwert dieser Option ist 0,001.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenprofilerstellungs-Task-Editor &#40; Seite "Allgemein" &#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Schnellprofilformular für einzelne Tabelle &#40; Datenprofilerstellungs-Task &#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  

