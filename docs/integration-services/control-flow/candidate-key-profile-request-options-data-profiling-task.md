---
title: "Optionen f&#252;r die Anforderung f&#252;r Kandidatenschl&#252;sselprofil (Datenprofilerstellungs-Task) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Editor für den Datenprofilerstellungs-Task"
ms.assetid: 8632dbc4-4394-4dc7-b19c-f9adeb21ba52
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Optionen f&#252;r die Anforderung f&#252;r Kandidatenschl&#252;sselprofil (Datenprofilerstellungs-Task)
  Verwenden Sie den Bereich **Anforderungseigenschaften** im Fenster **Profilanforderungen** , um die Optionen für die im Anforderungsbereich ausgewählte **Anforderung für Kandidatenschlüsselprofil** festzulegen. Ein Kandidatenschlüsselprofil meldet, ob eine Spalte oder eine Gruppe von Spalten ein Schlüssel oder ein ungefährer Schlüssel für die ausgewählte Tabelle ist. Dieses Profil hilft Ihnen auch, Probleme bei den Daten zu identifizieren, z. B. doppelte Werte in einer potenziellen Schlüsselspalte.  
  
> [!NOTE]  
>  Die in diesem Thema beschriebenen Optionen werden auf der Seite **Profilanforderungen** im **Editor für den Datenprofilerstellungs-Task**angezeigt. Weitere Informationen zu dieser Seite des Editors finden Sie unter [Editor für den Datenprofilerstellungs-Task &#40;Seite „Profilanforderungen“&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Weitere Informationen zum Verwenden des Datenprofilerstellungs-Tasks finden Sie unter [Einrichten von Datenprofilerstellungs-Tasks](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Weitere Informationen zum Verwenden des Datenprofil-Viewers zum Analysieren der Ausgabe des Datenprofilerstellungs-Tasks finden Sie unter [Datenprofil-Viewer](../../integration-services/control-flow/data-profile-viewer.md).  
  
## Grundlegendes zur Auswahl von Spalten für die KeyColumns-Eigenschaft  
 Jede **Anforderung für Kandidatenschlüsselprofil** berechnet die Schlüsselstärke eines einzelnen Schlüsselkandidaten, der aus einer oder mehreren Spalten besteht:  
  
-   Wenn Sie in **KeyColumns**nur eine Spalte auswählen, berechnet der Task die Schlüsselstärke dieser Spalte.  
  
-   Wenn Sie in **KeyColumns**mehrere Spalten auswählen, berechnet der Task die Schlüsselstärke des zusammengesetzten Schlüssels, der aus allen ausgewählten Spalten besteht.  
  
-   Wenn Sie das Platzhalterzeichen **(\*)** in **KeyColumns** auswählen, berechnet der Task die Schlüsselstärke jeder Spalte in der Tabelle oder Sicht.  
  
 Beispiel: Eine Beispieltabelle enthält die Spalten A, B und C. Sie nehmen die folgende Auswahl für die **KeyColumns**vor:  
  
-   Sie wählen (\*) und Spalte C in **KeyColumns** aus. Der Task berechnet die Schlüsselstärke von Spalte C und anschließend diejenige der zusammengesetzten Schlüsselkandidaten (A, C) und (B, C).  
  
-   Sie wählen (\*) und (\*) in **KeyColumns** aus. Der Task berechnet die Schlüsselstärke der einzelnen Spalten A, B und C und anschließend diejenige der zusammengesetzten Schlüsselkandidaten (A, B), (A, C) und (B, C).  
  
> [!NOTE]  
>  Wenn Sie (*) auswählen, kann diese Option zu zahlreichen Berechnungen führen und die Leistung des Tasks beeinträchtigen. Wenn der Task jedoch eine Teilmenge findet, die den Schwellenwert für einen Schlüssel erfüllt, analysiert der Task keine weiteren Kombinationen. Wenn der Task beispielsweise in der oben beschriebenen Beispieltabelle ermittelt, dass Spalte C ein Schlüssel ist, führt er keine Analyse der zusammengesetzten Schlüsselkandidaten aus.  
  
## Optionen für Anforderungseigenschaften  
 Für eine **Anforderung für Kandidatenschlüsselprofil**zeigt der Bereich **Anforderungseigenschaften** die folgenden Gruppen von Optionen an:  
  
-   **Daten**, die die **TableOrView** -Option und die **KeyColumns** -Option enthalten  
  
-   **Allgemein**  
  
-   **enthalten**  
  
### Datenoptionen  
 **ConnectionManager**  
 Wählen Sie den vorhandenen [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Manager aus, der den .NET-Datenanbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) verwendet, um eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank herzustellen, die die Tabelle oder Sicht enthält, für die ein Profil erstellt werden soll.  
  
 **TableOrView**  
 Wählen Sie die vorhandene Tabelle oder Sicht aus, für die ein Profil erstellt werden soll.  
  
 Weitere Informationen finden Sie im Abschnitt "TableorView-Optionen" in diesem Thema.  
  
 **KeyColumns**  
 Wählen Sie die vorhandene Spalte oder Spalten aus, für die ein Profil erstellt werden soll. Wählen Sie **(\*)** aus, um ein Profil für alle Spalten zu erstellen.  
  
 Weitere Informationen finden Sie unter "Grundlegendes zur Auswahl von Spalten für die KeyColumns-Eigenschaft" und unter "KeyColumns-Optionen" in diesem Thema.  
  
#### TableOrView-Optionen  
 **Schema**  
 Gibt das Schema an, zu dem die ausgewählte Tabelle gehört. Diese Option ist schreibgeschützt.  
  
 **Tabelle**  
 Zeigt den Namen der ausgewählten Tabelle an. Diese Option ist schreibgeschützt.  
  
#### KeyColumns-Optionen  
 Die folgenden Optionen sind für jede Spalte verfügbar, die für die Profilerstellung in **KeyColumns** ausgewählt wird, oder für die Option **(\*)**.  
  
 Weitere Informationen finden Sie im Abschnitt "Grundlegendes zur Auswahl von Spalten für die KeyColumns-Eigenschaft" in diesem Thema.  
  
 **IsWildCard**  
 Gibt an, ob der Platzhalter **(\*)** ausgewählt wurde. Diese Option wird auf **TRUE** festgelegt, wenn Sie **(\*)** ausgewählt haben, um ein Profil für alle Spalten zu erstellen. Die Option wird auf **False** festgelegt, wenn Sie eine einzelne Spalte ausgewählt haben, für die ein Profil erstellt werden soll. Diese Option ist schreibgeschützt.  
  
 **ColumnName**  
 Zeigt den Namen der ausgewählten Spalte an. Diese Option ist leer, wenn Sie **(\*)** ausgewählt haben, um ein Profil für alle Spalten zu erstellen. Diese Option ist schreibgeschützt.  
  
 **StringCompareOptions**  
 Wählen Sie Optionen zum Vergleichen von Zeichenfolgenwerten aus. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen. Der Standardwert für diese Option ist **Default**.  
  
> [!NOTE]  
>  Wenn Sie **(\*)** als Platzhalter für **ColumnName** verwenden, ist **CompareOptions** schreibgeschützt und auf die **Default**-Einstellung festgelegt.  
  
|value|Description|  
|-----------|-----------------|  
|**Default**|Sortiert und vergleicht Daten anhand der Sortierung der Spalte in der Quelltabelle.|  
|**BinarySort**|Sortiert und vergleicht Daten anhand der für jedes Zeichen definierten Bitmuster. Die binäre Sortierreihenfolge unterscheidet nach Groß- und Kleinschreibung und nach Akzent. Die Option Binär ist zudem die schnellste Sortierreihenfolge.|  
|**DictionarySort**|Sortiert und vergleicht Daten anhand der Sortier- und Vergleichsregeln, die in Wörterbüchern für die zugeordnete Sprache definiert sind, oder nach dem jeweiligen Alphabet.|  
  
 Wenn Sie **DictionarySort**auswählen, können Sie auch jede Kombination der in der folgenden Tabelle aufgelisteten Optionen auswählen. Standardmäßig ist keine dieser zusätzlichen Optionen ausgewählt.  
  
|value|Description|  
|-----------|-----------------|  
|**IgnoreCase**|Gibt an, ob beim Vergleichen zwischen Groß- und Kleinbuchstaben unterschieden wird. Falls diese Option festgelegt ist, ignoriert der Zeichenfolgenvergleich die Groß-/Kleinschreibung. Beispielsweise ist dann "ABC" mit "abc" identisch.|  
|**IgnoreNonSpace**|Gibt an, ob beim Vergleichen zwischen Zeichen mit Zwischenraum und diakritischen Zeichen unterschieden wird. Falls diese Option festgelegt ist, ignoriert der Zeichenfolgenvergleich diakritische Zeichen. Beispielsweise ist dann "å" mit "a" identisch.|  
|**IgnoreKanaType**|Gibt an, ob beim Vergleichen zwischen den beiden Typen japanischer Kanazeichen unterschieden wird: Hiragana und Katakana. Falls diese Option festgelegt ist, ignoriert der Zeichenfolgenvergleich den Kanatyp.|  
|**IgnoreWidth**|Gibt an, ob beim Vergleichen zwischen einem Single-Byte-Zeichen und demselben Zeichen als Double-Byte-Zeichen unterschieden wird. Wenn diese Option festgelegt ist, werden die Single-Byte- und die Double-Byte-Darstellung desselben Zeichens als identisch behandelt.|  
  
### Allgemeine Optionen  
 **RequestID**  
 Geben Sie einen beschreibenden Namen ein, um diese Profilanforderung zu kennzeichnen. In der Regel müssen Sie den automatisch generierten Wert nicht ändern.  
  
### enthalten  
 **ThresholdSetting**  
 Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen. Der Standardwert dieser Eigenschaft ist **Specified**.  
  
|value|Description|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|Es ist kein Schwellenwert angegeben. Die Schlüsselstärke wird unabhängig vom Wert gemeldet.|  
|**Specified**|Ein Schwellenwert wird in **KeyStrengthThreshold**angegeben. Die Schlüsselstärke wird nur gemeldet, wenn sie größer als der Schwellenwert ist.|  
|**Exact**|Es ist kein Schwellenwert angegeben. Die Schlüsselstärke wird nur gemeldet, wenn die ausgewählten Spalten ein genauer Schlüssel sind.|  
  
 **KeyStrengthThreshold**  
 Geben Sie (mit einem Wert zwischen 0 und 1) den Schwellenwert an, bei dessen Überschreiten die Schlüsselstärke gemeldet werden sollte. Der Standardwert dieser Eigenschaft ist 0,95. Diese Option ist nur aktiviert, wenn **Specified** als **KeyStrengthThresholdSetting**ausgewählt wird.  
  
 **MaxNumberOfViolations**  
 Geben Sie die maximale Anzahl von Kandidatenschlüsselverstößen an, die in der Ausgabe dokumentiert werden sollen. Der Standardwert dieser Eigenschaft ist 100. Diese Option ist deaktiviert, wenn **Exact** als **KeyStrengthThresholdSetting**ausgewählt wird.  
  
## Siehe auch  
 [Editor für den Datenprofilerstellungs-Task &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Schnellprofilformular für eine einzelne Tabelle &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  