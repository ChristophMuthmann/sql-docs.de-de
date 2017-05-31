---
title: Spalteneigenschaften (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.designers.properties.Column.ColumnIdentitySpec
- vdt.designers.properties.Column
- vdt.tablecolumn
- vdt.designers.properties.Column.ColumnComputedColumnSpec
- vdt.designers.properties.Column.ColumnFulltextSpec
ms.assetid: e549a2a8-4154-4ec8-b146-614564169b39
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: dfd26bcff6aa621967ab9295ac65a92718db9f8c
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="column-properties-visual-database-tools"></a>Spalteneigenschaften (Visual Database Tools)
Für Spalten gibt es zwei Sätze von Eigenschaften: einen vollständigen Satz, der im Tabellen-Designer auf der Registerkarte **Spalteneigenschaften** angezeigt wird (nur für [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Datenbanken verfügbar), und eine Teilmenge, die im Server-Explorer im Eigenschaftenfenster angezeigt wird.  
  
> [!NOTE]  
> Die in diesem Thema behandelten Eigenschaften sind nicht alphabetisch, sondern nach Kategorie angeordnet.  
  
> [!NOTE]  
> Die angezeigten Dialogfelder und Menübefehle können von den in der Hilfe beschriebenen abweichen. Dies hängt von Ihren aktiven Einstellungen oder Ihrer Edition ab. Um Ihre Einstellungen zu ändern, wählen Sie **Einstellungen importieren und exportieren** im Menü **Extras** aus.  
  
## <a name="properties-window"></a>Eigenschaftenfenster  
Die folgenden Eigenschaften werden im Eigenschaftenfenster angezeigt, wenn Sie im Server-Explorer eine Spalte auswählen.  
  
> [!NOTE]  
> Wenn Sie mit dem Server-Explorer auf diese Eigenschaften zugreifen, sind diese schreibgeschützt. Um die Spalteneigenschaften für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datenbanken zu bearbeiten, müssen Sie die Spalte im Tabellen-Designer auswählen. Diese Eigenschaften werden später in diesem Thema beschrieben.  
  
**Kategorie Identität**  
Wird erweitert, um die Eigenschaften **Name** und **Datenbank** anzuzeigen.  
  
**Name**  
Zeigt den Namen der Spalte an.  
  
**Datenbank**  
Zeigt den Namen der Datenquelle für die ausgewählte Spalte an. (Gilt nur für OLE DB.)  
  
**Kategorie Verschiedenes**  
Wird erweitert, um die restlichen Eigenschaften anzuzeigen.  
  
**Datentyp**  
Zeigt den Datentyp der ausgewählten Spalte an. Weitere Informationen finden Sie unter [Datentypen (Transact-SQL)](http://msdn.microsoft.com/en-us/a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4).  
  
**ID-Schrittweite**  
Zeigt an, in welchen Schrittweiten der **ID-Startwert** für jede weitere Zeile der Identitätsspalte erhöht wird. (Gilt nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].)  
  
**ID-Startwert**  
Zeigt den der ersten Tabellenzeile der Identitätsspalte zugeordneten Startwert an. (Gilt nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].)  
  
**Ist Identity**  
Zeigt, ob die ausgewählte Spalte die Identity-Spalte der Tabelle ist. (Gilt nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].)  
  
**Länge**  
Zeigt die Anzahl der für zeichenbasierte Datentypen zulässigen Zeichen an.  
  
**NULL zulassen**  
Zeigt an, ob die Spalte NULL-Werte zulässt.  
  
**Genauigkeit**  
Zeigt die maximale Anzahl der für numerische Datentypen zulässigen Stellen. Bei nicht numerischen Datentypen wird diese Eigenschaft mit **0** angegeben.  
  
**Dezimalstellen**  
Zeigt die maximale Anzahl von Stellen an, die bei numerischen Datentypen rechts vom Dezimalkomma erscheinen können. Dieser Wert muss kleiner oder gleich der Genauigkeit sein. Bei nicht numerischen Datentypen wird diese Eigenschaft mit **0** angegeben.  
  
## <a name="column-properties-tab"></a>Registerkarte Spalteneigenschaften  
Um auf diese Eigenschaften zuzugreifen, klicken Sie im Server-Explorer mit der rechten Maustaste auf die Tabelle, in der sich die Spalte befindet, wählen Sie **Tabellendefinition öffnen**aus, und wählen Sie anschließend im Tabellenraster des Tabellen-Designers die Zeile aus.  
  
> [!NOTE]  
> Diese Eigenschaften gelten nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Kategorie Allgemein**  
Wird erweitert, um **Name**, **NULL-Werte zulassen**, **Datentyp**, **Standardwert oder -bindung**, **Länge**, **Genauigkeit**und **Dezimalstellen**anzuzeigen.  
  
**Name**  
Zeigt den Namen der Spalte an. Bearbeiten Sie das Textfeld, um den Namen zu ändern.  
  
> [!CAUTION]  
> Wenn vorhandene Abfragen, Sichten, benutzerdefinierte Funktionen, gespeicherte Prozeduren oder Programme auf die betreffende Spalte verweisen, werden alle diese Objekte ungültig.  
  
**NULL-Werte zulassen**  
Zeigt an, ob der Datentyp der Spalte NULL-Werte zulässt.  
  
**Datentyp**  
Zeigt den Datentyp der ausgewählten Spalte an. Um diese Eigenschaft zu bearbeiten, klicken Sie auf ihren Wert, erweitern Sie die Dropdownliste, und wählen Sie einen anderen Wert aus. Weitere Informationen finden Sie unter [Datentypen (Transact-SQL)](http://msdn.microsoft.com/en-us/a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4).  
  
**Standardwert oder -bindung**  
Zeigt, welcher Standardwert für die Spalte verwendet wird, wenn kein Wert angegeben ist. Die Dropdownliste enthält alle in der Datenquelle definierten globalen Standards. Um die Spalte an einen globalen Standard zu binden, wählen Sie diesen aus der Dropdownliste aus. Sie können den Standardwert aber auch direkt als Text eingeben, um eine Standardeinschränkung für die Spalte zu erstellen.  
  
**Länge**  
Zeigt die Anzahl der für zeichenbasierte Datentypen zulässigen Zeichen an. Diese Eigenschaft ist nur für zeichenbasierte Datentypen verfügbar.  
  
**Genauigkeit**  
Zeigt die maximale Anzahl der für numerische Datentypen zulässigen Stellen. Bei nicht numerischen Datentypen wird diese Eigenschaft mit **0** angegeben. Diese Eigenschaft ist nur für numerische Datentypen verfügbar.  
  
**Dezimalstellen**  
Zeigt die maximale Anzahl von Stellen an, die bei numerischen Datentypen rechts vom Dezimalkomma erscheinen können. Dieser Wert muss kleiner oder gleich der Genauigkeit sein. Bei nicht numerischen Datentypen wird diese Eigenschaft mit **0** angegeben. Diese Eigenschaft ist nur für numerische Datentypen verfügbar.  
  
**Kategorie Tabellen-Designer**  
Wird erweitert, um die restlichen Eigenschaften anzuzeigen.  
  
**Sortierung**  
Zeigt die Sortierungseinstellung der ausgewählten Spalte an. Um diese Einstellung zu ändern, klicken Sie auf **Sortierung** und dann rechts neben dem Wert auf die Schaltfläche mit den drei Punkten **(…)** .  
  
**Spezifikationskategorie der berechneten Spalte**  
Wird erweitert, um die Eigenschaften für **Formel** und für **Ist Persisted**anzuzeigen. Wenn die Spalte berechnet ist, wird außerdem die Formel angezeigt. Um die Formel zu bearbeiten, erweitern Sie diese Kategorie, und bearbeiten Sie sie in der **Formel** -Eigenschaft.  
  
**Formel**  
Zeigt, wenn es sich um eine berechnete Spalte handelt, die von der ausgewählten Spalte verwendete Formel. In diesem Feld können Sie eine Formel angeben oder ändern.  
  
**Ist Persisted**  
Ermöglicht das Speichern der berechneten Spalte mit der Datenquelle. Eine persistente berechnete Spalte kann indiziert werden.  
  
**Datentyp-Kurzform**  
Zeigt die Informationen zum Felddatentyp an, im gleichen Format wie in der SQL-Anweisung CREATE TABLE. Beispiel: Ein Feld, das eine Zeichenfolge variabler Länge mit einer maximalen Länge von 20 Zeichen enthält, würde als "varchar(20)" dargestellt. Um diese Eigenschaft zu ändern, geben Sie den Wert direkt ein.  
  
**Description**  
Zeigt die Beschreibung der Spalte an. Um die vollständige Beschreibung anzuzeigen oder zu bearbeiten, klicken Sie auf Beschreibung und dann rechts neben der Eigenschaft auf die Schaltfläche mit den drei Punkten **(...)** .  
  
**Kategorie Volltextspezifikation**  
Wird erweitert, um die spezifischen Eigenschaften von Volltextspalten anzuzeigen.  
  
**Ist volltextindiziert**  
Gibt an, ob die Spalte volltextindiziert ist. Diese Eigenschaft kann nur dann auf **Ja** festgelegt werden, wenn für den Datentyp der Spalte eine Volltextsuche möglich ist und wenn für die Spalte in der zugehörigen Tabelle ein Volltextindex angegeben ist. Um diesen Wert zu ändern, klicken Sie auf den Wert, erweitern Sie die Dropdownliste, und wählen Sie einen anderen Wert aus.  
  
**Volltexttyp-Spalte**  
Zeigt, welche Spalte verwendet wird, um den Dokumenttyp einer Spalte vom Typ Image zu definieren. Der Datentyp Image kann verwendet werden, um Dokumente zu speichern, die von DOC-Dateien bis zu XML-Dateien reichen.  
  
**Sprache**  
Gibt die für die Indizierung der Spalte verwendete Sprache an.  
  
**Statistische Semantik**  
Wählen Sie aus, ob die statistische semantische Indizierung für die ausgewählte Spalte aktiviert werden soll. Weitere Informationen finden Sie unter [Semantische Suche](http://msdn.microsoft.com/en-us/cd8faa9d-07db-420d-93f4-a2ea7c974b97).  
  
Wenn Sie eine **Sprache** vor der Option **Statistische Semantik**auswählen und die ausgewählte Sprache über kein zugeordnetes semantisches Sprachmodell verfügt, ist die Option **Statistische Semantik** auf **Nein** festgelegt, und sie kann nicht geändert werden. Wenn Sie die Option **Statistische Semantik** auf **Ja** festlegen, bevor Sie eine **Sprache**auswählen, sind in der Spalte **Sprache** nur die Sprachen verfügbar, für die das semantische Sprachmodell unterstützt wird.  
  
**Hat Nicht-SQL Server-Abonnent**  
Zeigt, ob die Spalte einen anderen SQL Server-Abonnenten als Microsoft hat.  
  
**Identitätsspezifikationskategorie**  
Wird erweitert, um die Eigenschaften von **Ist Identity**, **ID-Schrittweite**und **ID-Startwert**anzuzeigen.  
  
**Ist Identity**  
Zeigt, ob die ausgewählte Spalte die Identity-Spalte der Tabelle ist. Um die Eigenschaft zu ändern, öffnen Sie die Tabelle im Tabellen-Designer, und bearbeiten Sie die Eigenschaften im **Eigenschaften** -Fenster. Diese Einstellungen gelten nur für Spalten mit einem zahlenbasierten Datentyp wie *int*.  
  
**ID-Schrittweite**  
Zeigt an, in welchen Schrittweiten der **ID-Startwert** für jede weitere Zeile erhöht wird. Wenn Sie nichts eingeben, wird standardmäßig der Wert 1 zugewiesen. Um diese Eigenschaft zu bearbeiten, geben Sie den Wert direkt ein.  
  
**ID-Startwert**  
Zeigt den der ersten Zeile der Tabelle zugewiesenen Wert an. Wenn Sie nichts eingeben, wird standardmäßig der Wert 1 zugewiesen. Um diese Eigenschaft zu bearbeiten, geben Sie den Wert direkt ein.  
  
**Ist deterministisch**  
Zeigt, ob der Datentyp der ausgewählten Spalte mit Sicherheit bestimmt werden kann.  
  
**Ist DTS-veröffentlicht**  
Zeigt, ob die Spalte DTS-veröffentlicht ist.  
  
**Ist indizierbar**  
Zeigt, ob die ausgewählte Spalte indiziert werden kann. Beispiel: Nichtdeterministische, berechnete Spalten können nicht indiziert werden.  
  
**Ist mit Mergereplikation veröffentlicht**  
Zeigt, ob die Spalte eine Mergeveröffentlichung ist.  
  
**Ist nicht zu replizieren**  
Gibt an, ob die ursprünglichen Identitätswerte bei der Replikation erhalten bleiben. Um diese Eigenschaft zu bearbeiten, klicken Sie auf ihren Wert, erweitern Sie die Dropdownliste, und wählen Sie einen anderen Wert aus.  
  
**Ist repliziert**  
Zeigt, ob diese Spalte an einem anderen Speicherort repliziert wird.  
  
**Ist RowGuid**  
Gibt an, ob [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] die Spalte als ROWGUID verwendet. Diesen Wert können Sie nur für eine Spalte mit dem Datentyp **uniqueidentifier** auf **Ja**festlegen. Um diese Eigenschaft zu bearbeiten, klicken Sie auf ihren Wert, erweitern Sie die Dropdownliste, und wählen Sie einen anderen Wert aus.  
  
**Größe**  
Zeigt die für den Datentyp der Spalte zulässige Größe in Byte an. Beispiel: Ein **nchar** -Datentyp kann eine Länge von 10 haben (die Anzahl von Zeichen), würde aber wegen der Unicode-Zeichensätze aber eine Größe von 20 Byte haben.  
  
> [!NOTE]  
> Die Länge eines **varchar(max)** -Datentyps variiert für jede Zeile. „sp_help“ gibt (-1) als Länge von **varchar(max)** -Spalten zurück. [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] zeigt -1 als Spaltengröße an.  
  

