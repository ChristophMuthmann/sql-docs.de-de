---
title: "Optionen f&#252;r die Anforderung f&#252;r funktionales Abh&#228;ngigkeitsprofil (Datenprofilerstellungs-Task) | Microsoft Docs"
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
ms.assetid: 6eb853aa-8016-490c-be4f-06ab8d7f5021
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# Optionen f&#252;r die Anforderung f&#252;r funktionales Abh&#228;ngigkeitsprofil (Datenprofilerstellungs-Task)
  Verwenden Sie den Bereich **Anforderungseigenschaften** im Fenster **Profilanforderungen** , um die Optionen für die im Anforderungsbereich ausgewählte **Anforderung für funktionales Abhängigkeitsprofil** festzulegen. Ein funktionales Abhängigkeitsprofil dokumentiert das Ausmaß, in dem die Werte in einer Spalte (der abhängigen Spalte) von den Werten in einer anderen Spalte oder einer Gruppe von Spalten (der determinanten Spalte) abhängen. Dieses Profil hilft Ihnen auch, Probleme mit den Daten zu identifizieren, z. B. ungültige Werte. Beispiel: Sie erstellen ein Profil der Abhängigkeit zwischen einer Spalte, die Postleitzahlen enthält, und einer Spalte mit US-amerikanischen Bundesstaaten. In diesem Profil sollte dieselbe Postleitzahl immer denselben Bundesstaat aufweisen, doch das Profil entdeckt Verstöße gegen das Abhängigkeitsverhältnis.  
  
> [!NOTE]  
>  Die in diesem Thema beschriebenen Optionen werden auf der Seite **Profilanforderungen** im **Editor für den Datenprofilerstellungs-Task**angezeigt. Weitere Informationen zu dieser Seite des Editors finden Sie unter [Editor für den Datenprofilerstellungs-Task &#40;Seite „Profilanforderungen“&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Weitere Informationen zum Verwenden des Datenprofilerstellungs-Tasks finden Sie unter [Einrichten von Datenprofilerstellungs-Tasks](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Weitere Informationen zum Verwenden des Datenprofil-Viewers zum Analysieren der Ausgabe des Datenprofilerstellungs-Tasks finden Sie unter [Datenprofil-Viewer](../../integration-services/control-flow/data-profile-viewer.md).  
  
## Grundlegendes zur Auswahl von determinanten und abhängigen Spalten  
 Eine **Anforderung für funktionales Abhängigkeitsprofil** berechnet das Ausmaß, in dem die determinante Spalte oder Gruppe von Spalten (wird in der **DeterminantColumns**-Eigenschaft angegeben) den Wert der abhängigen Spalte (wird in der **DependentColumn**-Eigenschaft angegeben) festlegt. Eine Spalte mit US-Bundesstaaten sollte beispielsweise funktional von einer Spalte mit US-Postleitzahlen abhängen. Das heißt, wenn die Postleitzahl (determinante Spalte) 98052 lautet, sollte der Bundesstaat (abhängige Spalte) immer Washington sein.  
  
 Für die determinante Seite können Sie eine Spalte oder Gruppe von Spalten in der **DeterminantColumns** -Eigenschaft angeben. Beispiel: Eine Beispieltabelle enthält die Spalten A, B und C. Sie nehmen die folgende Auswahl für die **DeterminantColumns** -Eigenschaft vor:  
  
-   Wenn Sie den Platzhalter **(\*)** auswählen, prüft der Datenprofilerstellungs-Task jede Spalte als determinante Seite der Abhängigkeit.  
  
-   Wenn Sie den Platzhalter **(\*)** und eine oder mehrere weitere Spalten auswählen, prüft der Datenprofilerstellungs-Task jede Kombination aus Spalten als determinante Seite der Abhängigkeit. Beispiel: Eine Beispieltabelle enthält die Spalten A, B und C. Wenn Sie **(\*)** und Spalte C als Wert der **DeterminantColumns**-Eigenschaft angeben, prüft der Datenprofilerstellungs-Task die Kombinationen (A, C) und (B, C) als determinante Seite der Abhängigkeit.  
  
 Für die abhängige Seite können Sie eine einzelne Spalte oder den Platzhalter **(\*)** in der **DependentColumn**-Eigenschaft angeben. Wenn Sie **(\*)** auswählen, prüft der Datenprofilerstellungs-Task die determinante Spalte oder Gruppe von Spalten im Hinblick auf jede Spalte.  
  
> [!NOTE]  
>  Wenn Sie **(\*)** auswählen, kann dies zu zahlreichen Berechnungen führen und die Leistung des Tasks beeinträchtigen. Wenn der Task jedoch eine Teilmenge findet, die den Schwellenwert für eine funktionale Abhängigkeit erfüllt, analysiert der Task keine weiteren Kombinationen. Wenn der Task beispielsweise in der oben beschriebenen Beispieltabelle ermittelt, dass Spalte C eine determinante Spalte ist, führt er keine Analyse der zusammengesetzten Kandidaten aus.  
  
## Optionen für Anforderungseigenschaften  
 Für eine **Anforderung für funktionales Abhängigkeitsprofil**zeigt der Bereich **Anforderungseigenschaften** die folgenden Gruppen von Optionen an:  
  
-   **Daten**, die die **DeterminantColumns** -Option und die **DependentColumn** -Option enthalten  
  
-   **Allgemein**  
  
-   **enthalten**  
  
### Datenoptionen  
 **ConnectionManager**  
 Wählen Sie den vorhandenen [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Verbindungs-Manager aus, der den .NET-Datenanbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) verwendet, um eine Verbindung zur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank herzustellen, die die Tabelle oder Sicht enthält, für die ein Profil erstellt werden soll.  
  
 **TableOrView**  
 Wählen Sie die vorhandene Tabelle oder Sicht aus, für die ein Profil erstellt werden soll.  
  
 **DeterminantColumns**  
 Wählen Sie die determinante Spalte oder Gruppe von Spalten aus. Das heißt, wählen Sie die Spalte oder Gruppe von Spalten aus, deren Werte den Wert der abhängigen Spalte festlegen.  
  
 Weitere Informationen finden Sie im Abschnitt "Grundlegendes zur Auswahl von determinanten und abhängigen Spalten" und im Abschnitt "Optionen 'DeterminantColumns' und 'DependentColumn'" in diesem Thema.  
  
 **DependentColumn**  
 Wählen Sie die abhängige Spalte aus. Das heißt, wählen Sie die Spalte aus, deren Wert vom Wert der determinanten Spalte oder Gruppe von Spalten festgelegt wird.  
  
 Weitere Informationen finden Sie im Abschnitt "Grundlegendes zur Auswahl von determinanten und abhängigen Spalten" und im Abschnitt "Optionen 'DeterminantColumns' und 'DependentColumn'" in diesem Thema.  
  
#### Optionen 'DeterminantColumns' und 'DependentColumn'  
 Die folgenden Optionen sind für jede Spalte verfügbar, die für die Profilerstellung in **DeterminantColumns** und **DependentColumn**ausgewählt wird.  
  
 Weitere Informationen finden Sie im Abschnitt "Grundlegendes zur Auswahl von determinanten und abhängigen Spalten" in diesem Thema.  
  
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
  
### Allgemeine Optionen  
 **RequestID**  
 Geben Sie einen beschreibenden Namen ein, um diese Profilanforderung zu kennzeichnen. In der Regel müssen Sie den automatisch generierten Wert nicht ändern.  
  
### enthalten  
 **ThresholdSetting**  
 Geben Sie die Schwellenwerteinstellung an. Der Standardwert dieser Eigenschaft ist **Specified**.  
  
|Wert|Description|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|Gibt keinen Schwellenwert an. Die funktionale Abhängigkeitsstärke wird unabhängig vom Wert gemeldet.|  
|**Specified**|Verwenden Sie den Schwellenwert, der in **FDStrengthThreshold**angegeben ist. Die funktionale Abhängigkeitsstärke wird nur gemeldet, wenn sie größer als der Schwellenwert ist.|  
|**Exact**|Gibt keinen Schwellenwert an. Die funktionale Abhängigkeitsstärke wird nur gemeldet, wenn eine genaue funktionale Abhängigkeit zwischen den ausgewählten Spalten besteht.|  
  
 **FDStrengthThreshold**  
 Geben Sie (mit einem Wert zwischen 0 und 1) den Schwellenwert an, bei dessen Überschreiten die funktionale Abhängigkeitsstärke gemeldet werden sollte. Der Standardwert dieser Eigenschaft ist 0,95. Diese Option ist nur aktiviert, wenn **Specified** als **ThresholdSetting**ausgewählt wird.  
  
 **MaxNumberOfViolations**  
 Geben Sie die maximale Anzahl von funktionale Abhängigkeitsverstößen an, die in der Ausgabe dokumentiert werden sollen. Der Standardwert dieser Eigenschaft ist 100. Diese Option ist deaktiviert, wenn **Exact** als **ThresholdSetting**ausgewählt wird.  
  
## Siehe auch  
 [Editor für den Datenprofilerstellungs-Task &#40;Seite "Allgemein"&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Schnellprofilformular für eine einzelne Tabelle &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  