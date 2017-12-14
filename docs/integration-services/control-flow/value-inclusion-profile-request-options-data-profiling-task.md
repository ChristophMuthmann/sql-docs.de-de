---
title: "Optionen für Anforderung für Wertinklusionsprofil (Datenprofilerstellungs-Task) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Data Profiling Task Editor
ms.assetid: ca94da82-a4c9-4e87-9cba-c2d85bd31f01
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 65a3a26b41981e6dc4c67219a52b76f822e78610
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="value-inclusion-profile-request-options-data-profiling-task"></a>Optionen für Anforderung für Wertinklusionsprofil (Datenprofilerstellungs-Task)
  Verwenden Sie den Bereich **Anforderungseigenschaften** der Seite **Profilanforderungen** , um die Optionen für die im Anforderungsbereich ausgewählte **Anforderung für Wertinklusionsprofil** festzulegen. Ein Wertinklusionsprofil berechnet die Überschneidung in den Werten zwischen zwei Spalten oder Gruppen von Spalten. Dieses Profil kann auch ermitteln, ob eine Spalte oder eine Gruppe von Spalten geeignet ist, um als Fremdschlüssel zwischen den ausgewählten Tabellen zu fungieren. Dieses Profil hilft Ihnen auch, Probleme mit den Daten zu identifizieren, z. B. ungültige Werte. Zum Beispiel verwenden Sie ein Wertinklusionsprofil, um ein Profil für die Spalte ProductID einer Vertriebstabelle zu erstellen. Das Profil erkennt, dass die Spalte Werte enthält, die nicht in der Spalte ProductID der Products-Tabelle enthalten sind.  
  
> [!NOTE]  
>  Die in diesem Thema beschriebenen Optionen werden auf der Seite **Profilanforderungen** im **Editor für den Datenprofilerstellungs-Task**angezeigt. Weitere Informationen zu dieser Seite des Editors finden Sie unter [Editor für den Datenprofilerstellungs-Task &#40;Seite „Profilanforderungen“&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Weitere Informationen zum Verwenden des Datenprofilerstellungs-Tasks finden Sie unter [Einrichten von Datenprofilerstellungs-Tasks](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Weitere Informationen zum Verwenden des Datenprofil-Viewers zum Analysieren der Ausgabe des Datenprofilerstellungs-Tasks finden Sie unter [Datenprofil-Viewer](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="understanding-the-selection-of-columns-for-the-inclusioncolumns-property"></a>Grundlegendes zur Auswahl von Spalten für die InclusionColumns-Eigenschaft  
 Eine **Anforderung für Wertinklusionsprofil** berechnet, ob alle Werte aus einer Teilmenge in der Obermenge enthalten sind. Die Obermenge ist oft eine Suche oder Verweistabelle. Zum Beispiel ist die Bundesstaatenspalte in einer Tabelle mit Adressen die untergeordnete Tabelle. Jeder aus zwei Zeichen bestehende Bundesstaatencode in dieser Spalte sollte auch in der Tabelle der Bundesstaatencodes des United States Postal Service enthalten sein. Dies ist die übergeordnete Tabelle.  
  
 Wenn Sie den Platzhalter (*) als Wert der untergeordneten oder der übergeordneten Spalte verwenden, vergleicht der Datenprofilerstellungs-Task jede Spalte auf dieser Seite mit der auf der anderen Seite angegebenen Spalte.  
  
> [!NOTE]  
>  Wenn Sie (*) auswählen, kann diese Option zu zahlreichen Berechnungen führen und die Leistung des Tasks beeinträchtigen.  
  
## <a name="understanding-the-threshold-settings"></a>Grundlegendes zu den Schwellenwerteinstellungen  
 Sie können zwei verschiedene Schwellenwerteinstellungen verwenden, um die Ausgabe einer Anforderung für Wertinklusionsprofil zu verfeinern.  
  
 Wenn Sie für **InclusionThresholdSetting** einen anderen Wert als **Keine**angeben, meldet das Profil die Inklusionsstärke der Teilmenge nur unter einer der folgenden Bedingungen in der Obermenge:  
  
-   Wenn die Inklusionsstärke den in **InclusionStrengthThreshold**angegebenen Schwellenwert überschreitet.  
  
-   Wenn die Inklusionsstärke den Wert 1,0 aufweist und **InclusionStrengthThreshold** auf **Exact**festgelegt ist.  
  
 Sie können die Ausgabe weiter verfeinern, indem Sie Kombinationen ausfiltern, bei denen die übergeordnete Spalte aufgrund nicht eindeutiger Werte kein geeigneter Schlüssel für die übergeordnete Tabelle ist. Wenn Sie für **SupersetColumnsKeyThresholdSetting** einen anderen Wert als **Keine**angeben, meldet das Profil die Inklusionsstärke der Teilmenge nur unter einer der folgenden Bedingungen in der Obermenge:  
  
-   Wenn die Eignung der übergeordneten Spalten als Schlüssel in der übergeordneten Tabelle den in **SupersetColumnsKeyThreshold**angegebenen Schwellenwert überschreitet.  
  
-   Wenn die Inklusionsstärke den Wert 1,0 aufweist und **SupersetColumnsKeyThreshold** auf **Exact**festgelegt ist.  
  
## <a name="request-properties-options"></a>Optionen für Anforderungseigenschaften  
 Für eine **Anforderung für Wertinklusionsbereich**zeigt der Bereich **Anforderungseigenschaften** die folgenden Gruppen von Optionen an:  
  
-   **Daten**, die die **SubsetTableOrView**-, **SupersetTableOrView**- und **InclusionColumns** -Option enthalten  
  
-   **Allgemein**  
  
-   **Options**  
  
### <a name="data-options"></a>Datenoptionen  
 **ConnectionManager**  
 Wählen Sie den vorhandenen [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager aus, der den .NET-Datenanbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) verwendet, um eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank herzustellen, die die Tabelle oder Sicht enthält, für die ein Profil erstellt werden soll.  
  
 **SubsetTableOrView**  
 Wählen Sie die vorhandene Tabelle oder Sicht aus, für die ein Profil erstellt werden soll.  
  
 Weitere Informationen finden Sie im Abschnitt "SubsetTableOrView-Option und SupersetTableOrView-Option" in diesem Thema.  
  
 **SupersetTableOrView**  
 Wählen Sie die vorhandene Tabelle oder Sicht aus, für die ein Profil erstellt werden soll.  
  
 Weitere Informationen finden Sie im Abschnitt "SubsetTableOrView-Option und SupersetTableOrView-Option" in diesem Thema.  
  
 **InclusionColumns**  
 Wählen Sie die Spalten oder die Gruppe von Spalten aus der untergeordneten und der übergeordneten Tabelle aus.  
  
 Weitere Informationen finden Sie unter "Grundlegendes zur Auswahl von Spalten für die InclusionColumns-Eigenschaft" und unter "InclusionColumns-Optionen" in diesem Thema.  
  
#### <a name="subsettableorview-and-supersettableorview-options"></a>SubsetTableOrView-Option und SupersetTableOrView-Option  
 **Schema**  
 Gibt das Schema an, zu dem die ausgewählte Tabelle gehört. Diese Option ist schreibgeschützt.  
  
 **TableOrView**  
 Zeigt den Namen der ausgewählten Tabelle an. Diese Option ist schreibgeschützt.  
  
#### <a name="inclusioncolumns-options"></a>InclusionColumns-Optionen  
 Die folgenden Optionen sind für jede Gruppe von Spalten verfügbar, die für die Profilerstellung in **InclusionColumns**ausgewählt wird.  
  
 Weitere Informationen finden Sie im Abschnitt "Grundlegendes zur Auswahl von Spalten für die InclusionColumns-Eigenschaft" in diesem Thema.  
  
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
  
### <a name="options"></a>-Option enthalten  
 **Keine**  
 Wählen Sie die Schwellenwerteinstellung aus, um die Ausgabe des Profils zu verfeinern. Der Standardwert dieser Eigenschaft ist **Specified**. Weitere Informationen finden Sie im Abschnitt "Grundlegendes zu Schwellenwerteinstellungen" in diesem Thema.  
  
|Wert|Description|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|Gibt keinen Schwellenwert an. Die Schlüsselstärke wird unabhängig vom Wert gemeldet.|  
|**Specified**|Verwenden Sie den Schwellenwert, der in **InclusionStrengthThreshold**angegeben ist. Die Inklusionsstärke wird nur gemeldet, wenn sie größer als der Schwellenwert ist.|  
|**Exact**|Gibt keinen Schwellenwert an. Die Inklusionsstärke wird nur gemeldet, wenn die untergeordneten Werte vollständig in den übergeordneten Werten enthalten sind.|  
  
 **InclusionStrengthThreshold**  
 Geben Sie (mit einem Wert zwischen 0 und 1) den Schwellenwert an, bei dessen Überschreiten die Inklusionsstärke gemeldet werden sollte. Der Standardwert dieser Eigenschaft ist 0,95. Diese Option ist nur aktiviert, wenn **Specified** als **InclusionThresholdSetting**ausgewählt wird.  
  
 Weitere Informationen finden Sie im Abschnitt "Grundlegendes zu Schwellenwerteinstellungen" in diesem Thema.  
  
 **Keine**  
 Geben Sie den übergeordneten Schwellenwert an. Der Standardwert dieser Eigenschaft ist **Specified**. Weitere Informationen finden Sie im Abschnitt "Grundlegendes zu Schwellenwerteinstellungen" in diesem Thema.  
  
|Wert|Description|  
|-----------|-----------------|  
|**InclusionThresholdSetting**|Gibt keinen Schwellenwert an. Die Inklusionsstärke wird unabhängig von der Schlüsselstärke der übergeordneten Spalte gemeldet.|  
|**Specified**|Verwenden Sie den Schwellenwert, der in **SupersetColumnsKeyThreshold**angegeben ist. Die Inklusionsstärke wird nur gemeldet, wenn die Schlüsselstärke der übergeordneten Spalte größer als der Schwellenwert ist.|  
|**Exact**|Gibt keinen Schwellenwert an. Die Inklusionsstärke wird nur gemeldet, wenn die übergeordneten Spalten ein genauer Schlüssel in der übergeordneten Tabelle sind.|  
  
 **SupersetColumnsKeyThreshold**  
 Geben Sie (mit einem Wert zwischen 0 und 1) den Schwellenwert an, bei dessen Überschreiten die Inklusionsstärke gemeldet werden sollte. Der Standardwert dieser Eigenschaft ist 0,95. Diese Option ist nur aktiviert, wenn **Specified** als **SupersetColumnsKeyThresholdSetting**ausgewählt wird.  
  
 Weitere Informationen finden Sie im Abschnitt "Grundlegendes zu Schwellenwerteinstellungen" in diesem Thema.  
  
 **MaxNumberOfViolations**  
 Geben Sie die maximale Anzahl von Inklusionsverstößen an, die in der Ausgabe dokumentiert werden sollen. Der Standardwert dieser Eigenschaft ist 100. Diese Option ist deaktiviert, wenn **Exact** als **InclusionThresholdSetting**ausgewählt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Editor für den Datenprofilerstellungs-Task &#40;Seite "Allgemein"&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Schnellprofilformular für eine einzelne Tabelle &#40;Datenprofilerstellungs-Task&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
