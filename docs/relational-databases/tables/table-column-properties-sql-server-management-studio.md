---
title: Tabellenspalteneigenschaften (SQL Server Management Studio) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:65558
- vdtsql.chm:69657
- vdt.ppg.columns
ms.assetid: 09830897-cc10-46b8-95f5-e0e9681b668c
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: eaf12a0ac440affa5fe6009431d7c90ce7f47c53
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="table-column-properties-sql-server-management-studio"></a>Tabellenspalteneigenschaften (SQL Server Management Studio)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Diese Eigenschaften werden im unteren Bereich des Tabellen-Designers angezeigt. Wenn nicht anders beschrieben, können Sie diese Eigenschaften im Eigenschaftenfenster bearbeiten, wenn die Spalte markiert ist. Die **Spalteneigenschaften** können nach Kategorie oder alphabetisch angezeigt werden. Viele Eigenschaften werden nur für bestimmte Datentypen angezeigt oder können nur für bestimmte Datentypen geändert werden.  
  
> [!NOTE]  
>  Wenn die Tabelle für die Replikation veröffentlicht wird, müssen Sie mithilfe der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) oder mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO) Schemaänderungen vornehmen. Wenn die Schemaänderungen mit dem Tabellen-Designer oder dem Datenbankdiagramm-Designer ausgeführt werden, wird versucht, die Tabelle zu entfernen und erneut zu erstellen. Da veröffentlichte Objekte nicht gelöscht werden können, schlägt die Schemaänderung fehl.  
  
 **Allgemein**  
 Wird erweitert, um **Name**, **NULL-Werte zulassen**, **Datentyp**, **Standardwert oder -bindung**, **Länge**, **Genauigkeit**und **Dezimalstellen**anzuzeigen.  
  
 **Name**  
 Zeigt den Namen der ausgewählten Spalte an.  
  
 **NULL-Werte zulassen**  
 Zeigt an, ob in dieser Spalte NULL-Werte zulässig sind. Klicken Sie zum Bearbeiten dieser Eigenschaft auf das Kontrollkästchen NULL-Werte zulassen, das der Spalte im oberen Bereich des Tabellen-Designers entspricht.  
  
 **Datentyp**  
 Zeigt den Datentyp für die ausgewählte Spalte an. Um diese Eigenschaft zu bearbeiten, klicken Sie auf ihren Wert, erweitern Sie die Dropdownliste, und wählen Sie einen anderen Wert aus.  
  
 **Standardwert oder -bindung**  
 Zeigt den Standardwert für diese Spalte an, wenn kein Wert für die Spalte angegeben ist. Der Wert dieses Felds kann entweder der Wert einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Standardeinschränkung sein oder der Name einer globalen Einschränkung, an die die Spalte gebunden ist. Die Dropdownliste enthält alle in der Datenbank definierten globalen Standardwerte. Um die Spalte an einen globalen Standard zu binden, wählen Sie diesen aus der Dropdownliste aus. Sie können den Standardwert aber auch direkt als Text eingeben, um eine Standardeinschränkung für die Spalte zu erstellen.  
  
 **Länge**  
 Zeigt die Anzahl der für zeichenbasierte Datentypen zulässigen Zeichen an. Diese Eigenschaft ist nur für zeichenbasierte Datentypen verfügbar.  
  
 **Dezimalstellen**  
 Zeigt die Höchstzahl von Ziffern an, die rechts neben dem Komma für Werte in dieser Spalte angezeigt werden können. Bei nicht numerischen Datentypen wird diese Eigenschaft mit **0** angegeben.  
  
 **Genauigkeit**  
 Zeigt die Höchstzahl von Ziffern für Werte in dieser Spalte an. Bei nicht numerischen Datentypen wird diese Eigenschaft mit **0** angegeben.  
  
 **Tabellen-Designer**  
 Erweitert den Abschnitt **Tabellen-Designer** .  
  
 **Sortierung**  
 Zeigt die Sortierreihenfolge an, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] standardmäßig auf die Spalte anwendet wird, wenn die Spaltenwerte zum Sortieren von Zeilen eines Abfrageergebnisses verwendet werden. Wählen Sie zum Bearbeiten der Sortierung die Eigenschaft aus, und klicken Sie auf die Auslassungspunkte (...) rechts neben dem Eigenschaftswert, um das Dialogfeld **Sortierung** anzuzeigen.  
  
 **BerechneteSpalteSpezifikation**  
 Zeigt Informationen über eine berechnete Spalte an. Der für die Eigenschaft angezeigte Wert ist derselbe, wie der Wert der untergeordneten Eigenschaft **Formel** , und zeigt die Formel für die berechnete Spalte an.  
  
> [!NOTE]  
>  Erweitern Sie zum Ändern des für die **ComputedColumnSpecification** -Eigenschaft angezeigten Werts die Eigenschaft, und bearbeiten Sie die untergeordnete Eigenschaft **Formel** .  
  
-   **Formel** Zeigt die Formel für die berechnete Spalte an. Sie können diese Eigenschaft bearbeiten, indem Sie direkt eine neue Formel eingeben.  
  
-   **Ist beständig** Gibt an, ob die Ergebnisse der Formel gespeichert werden. Wenn die Eigenschaft auf **No** festgelegt ist, wird nur die Formel gespeichert, und die Werte werden bei jedem Bezug auf die Spalte berechnet. Um diese Eigenschaft zu bearbeiten, klicken Sie auf ihren Wert, erweitern Sie die Dropdownliste, und wählen Sie einen anderen Wert aus.  
  
 Weitere Informationen finden Sie unter [Specify Computed Columns in a Table](../../relational-databases/tables/specify-computed-columns-in-a-table.md).  
  
 **Datentyp-Kurzform**  
 Zeigt die Informationen zum Felddatentyp an, im gleichen Format wie in der SQL-Anweisung CREATE TABLE. Ein Feld, das eine Zeichenfolge variabler Länge mit höchstens 20 Zeichen enthält, wird beispielsweise als "varchar(20)" dargestellt. Um diese Eigenschaft zu ändern, geben Sie den Wert direkt ein.  
  
 **Beschreibung**  
 Zeigt Text an, durch den die Spalte beschrieben wird. Wählen Sie zum Bearbeiten der Beschreibung die Eigenschaft aus, klicken Sie auf die Auslassungspunkte (   ), die rechts neben dem Eigenschaftswert angezeigt werden, und bearbeiten Sie die Beschreibung im Dialogfeld **Description-Eigenschaft** .  
  
 **Deterministisch**  
 Zeigt, ob der Datentyp der ausgewählten Spalte mit Sicherheit bestimmt werden kann.  
  
 **DTS-veröffentlicht**  
 Zeigt, ob die Spalte DTS-veröffentlicht ist. ([Data Transformation Services (DTS) ist veraltet](https://msdn.microsoft.com/library/cc707786(v=sql.130).aspx#Anchor_0)). 
  
 **Volltextspezifikation**  
 Zeigt Informationen zum Volltextindex an. Der Wert dieser Eigenschaft ist der Wert der untergeordneten Eigenschaft **(Ist volltextindiziert)** und zeigt an, ob diese Spalte volltextindiziert ist.  
  
> [!NOTE]  
>  Erweitern Sie zum Ändern des für die **Volltextspezifikation** -Eigenschaft angezeigten Werts die Eigenschaft, und bearbeiten Sie die untergeordnete Eigenschaft **Ist volltextindiziert** .  
  
-   **Ist volltextindiziert** Gibt an, ob diese Spalte volltextindiziert ist. Diese Eigenschaft kann nur dann auf **Ja** festgelegt werden, wenn für den Datentyp der Spalte eine Volltextsuche möglich ist und wenn für die Spalte in der zugehörigen Tabelle ein Volltextindex angegeben ist. Klicken Sie zum Bearbeiten diese Eigenschaft auf den Wert, erweitern Sie die Dropdownliste, und wählen Sie einen Wert aus.  
  
-   **Volltexttypspalte** zeigt den Namen der Spalte an, für den diese Spalte volltextindiziert ist. Diese Eigenschaft muss festgelegt sein, wenn die **Datentyp** -Eigenschaft für diese Spalte entweder **image** oder **varbinary**ist. Die in dieser Eigenschaft benannte Spalte muss vom Typ **[n]char, [n]varchar,** oder **xml**sein, und die Dropdownliste für diese Eigenschaft enthält nur Spalten, die von einem dieser drei Datentypen sind. Zeilen in den Spalten, die durch diese Eigenschaft benannt werden, zeigen den Dokumenttyp der entsprechenden Zeilen in Spalten an, die mit Volltextsuche durchsucht werden können. Um diese Eigenschaft zu bearbeiten, klicken Sie auf ihren Wert, erweitern Sie die Dropdownliste, und wählen Sie einen anderen Wert aus.  
  
-   **Sprache** Gibt die Sprache für die Wörtertrennung an, die zum Indizieren der Spalte verwendet wird. Der in der Eigenschaft gespeicherte Wert ist der Gebietsschemabezeichner für die Wörtertrennung. Weitere Informationen zur Wörtertrennung und zu LCIDs, finden Sie unter Wörtertrennung und Wortstammerkennungen. Um diese Eigenschaft zu bearbeiten, klicken Sie auf ihren Wert, erweitern Sie die Dropdownliste, und wählen Sie einen anderen Wert aus.  
  
 **Statistische Semantik**  
 Wählen Sie aus, ob die statistische semantische Indizierung für die ausgewählte Spalte aktiviert werden soll. Weitere Informationen finden Sie unter [Semantische Suche &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
 Wenn Sie eine **Sprache** vor der Option **Statistische Semantik**auswählen und die ausgewählte Sprache über kein zugeordnetes semantisches Sprachmodell verfügt, ist die Option **Statistische Semantik** auf **Nein** festgelegt, und sie kann nicht geändert werden. Wenn Sie die Option **Statistische Semantik** auf **Ja** festlegen, bevor Sie eine **Sprache**auswählen, sind in der Spalte **Sprache** nur die Sprachen verfügbar, für die das semantische Sprachmodell unterstützt wird.  
  
 **Hat Nicht-SQL Server-Abonnent**  
 Gibt an, ob die Spalte auf einen Abonnenten repliziert wird, der kein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ist.  
  
 **Identitätsspezifikation**  
 Zeigt Informationen darüber an, ob und wie diese Spalte die Eindeutigkeit der Werte erzwingt. Der Wert dieser Eigenschaft zeigt an, ob diese Spalte eine Identitätsspalte ist, und gleicht dem Wert der untergeordneten Eigenschaft **Ist Identity**.  
  
> [!NOTE]  
>  Zum Ändern des Werts für die **Identitätsspezifikation** -Eigenschaft erweitern Sie die untergeordnete Eigenschaft **Ist Identität** .  
  
-   **Ist Identity** Zeigt an, ob diese Spalte eine Identitätsspalte ist. Um diese Eigenschaft zu bearbeiten, klicken Sie auf ihren Wert, erweitern Sie die Dropdownliste, und wählen Sie einen anderen Wert aus.  
  
-   **ID-Startwert** Zeigt den Ausgangswert an, der während des Erstellens dieser Identitätsspalte angegeben wurde. Dieser Wert wird der ersten Tabellenzeile zugewiesen. Wenn Sie nichts eingeben, wird standardmäßig der Wert 1 zugewiesen. Um diese Eigenschaft zu bearbeiten, geben Sie den Wert direkt ein.  
  
-   **ID-Schrittweite** Zeigt den inkrementellen Wert an, der während des Erstellens dieser Identitätsspalte angegeben wurde. Bei diesem Wert handelt es sich um das Inkrement, der dem **ID-Startwert** für jede weitere Zeile hinzugefügt wird. Wenn Sie nichts eingeben, wird standardmäßig der Wert 1 zugewiesen. Um diese Eigenschaft zu bearbeiten, geben Sie den Wert direkt ein.  
  
 **Indizierbar**  
 Zeigt, ob die ausgewählte Spalte indiziert werden kann. Beispiel: Nichtdeterministische, berechnete Spalten können nicht indiziert werden.  
  
 **Merge-veröffentlicht**  
 Zeigt, ob die Spalte eine Mergeveröffentlichung ist.  
  
 **Not For Replication**  
 Gibt an, ob die ursprünglichen Identitätswerte bei der Replikation erhalten bleiben. Weitere Informationen zur Replikation finden Sie unter CREATE TABLE. Um diese Eigenschaft zu bearbeiten, klicken Sie auf ihren Wert, erweitern Sie die Dropdownliste, und wählen Sie einen anderen Wert aus.  
  
 **Repliziert**  
 Zeigt, ob diese Spalte an einem anderen Speicherort repliziert wird.  
  
 **RowGuid**  
 Gibt an, ob von SQL Server die Spalte als ROWGUID verwendet wird. Sie können diesen Wert nur für eine eindeutige Identitätsspalte auf **Yes** festlegen. Um diese Eigenschaft zu bearbeiten, klicken Sie auf ihren Wert, erweitern Sie die Dropdownliste, und wählen Sie einen anderen Wert aus.  
  
 **Größe**  
 Zeigt die für den Datentyp der Spalte zulässige Größe in Byte an. Beispiel: Ein nchar-Datentyp kann eine Länge von 10 besitzen (die Anzahl der Zeichen), wegen der Unicode-Zeichensätze aber eine Größe von 20 Byte besitzen.  
  
> [!NOTE]  
>  Die Länge für **(max)** -Datentypen ist für jede Zeile unterschiedlich. **sp_help** gibt (-1) als Länge von **(max)** -Spalten zurück. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zeigt -1 als Spaltengröße an.  
  
  
