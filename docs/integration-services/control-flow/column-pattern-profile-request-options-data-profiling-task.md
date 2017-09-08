---
title: Muster Profil Anforderung Spaltenoptionen (Datenprofilerstellungs-Task) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 9ccb8fc5-f65e-41a2-9511-7fa55586eb8b
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 05976158e43d7dfafaf02289462d1537f5beeb36
ms.openlocfilehash: e718e67c8756d691338a614c775c2ff71df4b06c
ms.contentlocale: de-de
ms.lasthandoff: 09/08/2017

---
# <a name="column-pattern-profile-request-options-data-profiling-task"></a>Optionen für die Anforderung für Spaltenmusterprofil (Datenprofilerstellungs-Task)
  Verwenden Sie den Bereich **Anforderungseigenschaften** der Seite **Profilanforderungen** , um die Optionen für die im Anforderungsbereich ausgewählte **Anforderung für Spaltenmusterprofil** festzulegen. Ein Spaltenmusterprofil meldet einen Satz von regulären Ausdrücken, die den angegebenen Prozentsatz der Werte in einer Zeichenfolgenspalte abdecken. Mit diesem Profil können Sie Probleme in Ihren Daten, wie z. B. ungültige Zeichenfolgen, ermitteln und reguläre Ausdrücke vorschlagen, die in Zukunft zum Überprüfen neuer Werte verwendet werden können. Beispiel: Ein Musterprofil einer Spalte mit US-Postleitzahlen kann die regulären Ausdrücke \d{5}-\d{4}, \d{5}, und \d{9}.erstellen. Wenn Sie andere reguläre Ausdrücke erhalten, enthalten Ihre Daten wahrscheinlich ungültige oder falsch formatierte Werte.  
  
> [!NOTE]  
>  Die in diesem Thema beschriebenen Optionen werden auf der Seite **Profilanforderungen** im **Editor für den Datenprofilerstellungs-Task**angezeigt. Weitere Informationen zu dieser Seite des Editors finden Sie unter [Editor für den Datenprofilerstellungs-Task &#40;Seite „Profilanforderungen“&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Weitere Informationen zum Verwenden des Datenprofilerstellungs-Tasks finden Sie unter [Einrichten von Datenprofilerstellungs-Tasks](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Weitere Informationen zum Verwenden des Datenprofil-Viewers zum Analysieren der Ausgabe des Datenprofilerstellungs-Tasks finden Sie unter [Datenprofil-Viewer](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="understanding-the-use-of-delimiters-and-symbols"></a>Grundlegendes zur Verwendung von Trennzeichen und Symbolen  
 Vor dem Berechnen der Muster für eine **Anforderung für Spaltenmusterprofil**versieht der Datenprofilerstellungs-Task die Daten mit einem Token. Das heißt, der Task unterteilt die Zeichenfolgenwerte in kleinere Einheiten, die als Token bezeichnet werden. Der Task unterteilt Zeichenfolgen anhand der Trennzeichen und Symbole, die Sie für die **Delimiters** -Eigenschaft und die **Symbols** -Eigenschaft angeben, in Token:  
  
-   **Trennzeichen** Standardmäßig enthält die Liste der Trennzeichen die folgenden Zeichen: Leerzeichen, horizontaler Tabstopp (\t), Neue-Zeile-Zeichen (\n) und Wagenrücklauf (\r). Sie können zusätzliche Trennzeichen angeben, Sie können die Standardtrennzeichen jedoch nicht entfernen.  
  
-   **Symbole** wird standardmäßig die Liste der **Symbole** enthält die folgenden Zeichen: `,.;:-"'~=&/@!?()<>[]{}|#*^%`. Sind die Symbole beispielsweise "`()-`", wird der Wert "(425) 123-4567" mit dem Token ["(", "425", ")", "123", "-", "4567", ")"] versehen.  
  
 Ein Zeichen kann nicht zugleich ein Trennzeichen und ein Symbol sein.  
  
 Alle Trennzeichen werden im Rahmen des Prozesses zur Tokenerstellung in ein Leerzeichen normalisiert, während Symbole beibehalten werden.  
  
## <a name="understanding-the-use-of-the-tag-table"></a>Grundlegendes zur Verwendung der Tagtabelle  
 Sie können zusammengehörige Token optional mit einem Tag gruppieren. Dazu speichern Sie Tags und die zugehörigen Ausdrücke in einer speziellen Tabelle, die Sie in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank erstellen. Die Tagtabelle muss zwei Zeichenfolgenspalten aufweisen, eine mit der Bezeichnung "Tag" und eine weitere mit der Bezeichnung "Begriff". Diese Spalten können vom Typ **char**, **nchar**, **varchar**oder **nvarchar**sein, jedoch nicht **text** oder **ntext**. Sie können mehrere Tags und die entsprechenden Ausdrücke in einer einzelnen Tabelle kombinieren. Eine Anforderung für Spaltenmusterprofil kann nur eine Tagtabelle verwenden. Sie können einen separaten [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager verwenden, um eine Verbindung zur Tagtabelle herzustellen. Daher kann sich die Tagtabelle in einer anderen Datenbank oder auf einem anderen Server befinden als die Quelldaten.  
  
 Sie können z. B. die Werte "Ost", "West", "Nord" und "Süd", die in Straßennamen angezeigt werden können, mit dem Tag "Richtung" gruppieren. Die folgende Tabelle ist ein Beispiel für eine Tagtabelle.  
  
|Tag|Begriff|  
|---------|----------|  
|Richtung|Ost|  
|Richtung|West|  
|Richtung|Nord|  
|Richtung|Süd|  
  
 Sie können ein andere Tag verwenden, um die verschiedenen Wörter zu gruppieren, die die Bezeichnung einer "Straße" in Straßennamen ausdrücken.  
  
|Tag|Begriff|  
|---------|----------|  
|Straße|Straße|  
|Straße|Allee|  
|Straße|Platz|  
|Straße|Weg|  
  
 Anhand dieser Kombination aus Tags könnte das resultierende Muster für eine Straßenbezeichnung dem folgenden Muster ähneln:  
  
 `\d+\ LookupTag=Direction \d+\p{L}+\ LookupTag=Street`  
  
> [!NOTE]  
>  Die Verwendung einer Tagtabelle beeinträchtigt die Leistung des Datenprofilerstellungs-Tasks. Verwenden Sie nicht mehr als 10 Tags oder mehr als 100 Begriffe pro Tag.  
  
 Derselbe Begriff kann zu mehreren Tags gehören.  
  
## <a name="request-properties-options"></a>Optionen für Anforderungseigenschaften  
 Für eine **Anforderung für Spaltenmusterprofil**zeigt der Bereich **Anforderungseigenschaften** die folgenden Gruppen von Optionen an:  
  
-   **Daten**, die die Optionen **TableOrView** und **Spalte** enthalten  
  
-   **Allgemein**  
  
-   **Options**  
  
### <a name="data-options"></a>Datenoptionen  
 **ConnectionManager**  
 Wählen Sie den vorhandenen [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager aus, der den .NET-Datenanbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) verwendet, um eine Verbindung zur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank herzustellen, die die Tabelle oder Sicht enthält, für die ein Profil erstellt werden soll.  
  
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
 Diese Option gilt nicht für das Spaltenmusterprofil.  
  
### <a name="general-options"></a>Allgemeine Optionen  
 **RequestID**  
 Geben Sie einen beschreibenden Namen ein, um diese Profilanforderung zu kennzeichnen. In der Regel müssen Sie den automatisch generierten Wert nicht ändern.  
  
### <a name="options"></a>enthalten  
 **MaxNumberOfPatterns**  
 Geben Sie die maximale Anzahl von Mustern an, die das Profil berechnen soll. Der Standardwert dieser Option ist 10. Der Maximalwert ist 100.  
  
 **PercentageDataCoverageDesired**  
 Geben Sie den Prozentwert der Daten an, die die berechneten Muster abdecken sollen. Der Standardwert dieser Option ist 95 (Prozent).  
  
 **CaseSensitive**  
 Geben Sie an, ob bei den Mustern die Groß-/Kleinschreibung beachtet werden soll. Der Standardwert für diese Option ist **False**.  
  
 **Delimiters**  
 Führen Sie die Zeichen auf, die als Entsprechung der Leerzeichen zwischen Wörtern behandelt werden sollen, wenn Text mit Token versehen wird. Standardmäßig enthält die Liste der **Trennzeichen** die folgenden Zeichen: Leerzeichen, horizontaler Tabstopp (\t), Neue-Zeile-Zeichen (\n) und Wagenrücklauf (\r). Sie können zusätzliche Trennzeichen angeben, Sie können die Standardtrennzeichen jedoch nicht entfernen.  
  
 Weitere Informationen finden Sie unter "Grundlegendes zur Verwendung von Trennzeichen und Symbolen" in diesem Thema.  
  
 **Symbols**  
 Führen Sie die Symbole auf, die als Teil von Mustern beibehalten werden sollen. Beispiele könnten "/" für Datumsangaben, ":" für Uhrzeiten und "@" für E-Mail-Adressen enthalten. Standardmäßig enthält die Liste der **Symbole** die folgenden Zeichen: `,.;:-"'`~=&/@!?()<>[]{}|#*^%`.  
  
 Weitere Informationen finden Sie unter "Grundlegendes zur Verwendung von Trennzeichen und Symbolen" in diesem Thema.  
  
 **TagTableConnectionManager**  
 Wählen Sie den vorhandenen [!INCLUDE[vstecado](../../includes/vstecado-md.md)] -Verbindungs-Manager aus, der den .NET-Datenanbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) verwendet, um eine Verbindung zur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank herzustellen, die die Tagtabelle enthält.  
  
 Weitere Informationen finden Sie unter "Grundlegendes zur Verwendung der Tagtabelle" in diesem Thema.  
  
 **TagTableName**  
 Wählen Sie die vorhandene Tagtabelle aus, die zwei Zeichenfolgenspalten mit der Bezeichnung "Tag" und "Begriff" aufweisen muss.  
  
 Weitere Informationen finden Sie unter "Grundlegendes zur Verwendung der Tagtabelle" in diesem Thema.  
  
## <a name="see-also"></a>Siehe auch  
 [Editor für den Datenprofilerstellungs-Task &#40;Seite "Allgemein"&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Schnellprofilformular für einzelne Tabelle &#40; Datenprofilerstellungs-Task &#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  

