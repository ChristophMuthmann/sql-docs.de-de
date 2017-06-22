---
title: "Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- languages [full-text search]
- full-text search [SQL Server], stemmers
- linguistic analysis [full-text search]
- full-text indexes [SQL Server], linguistic analysis
- full-text search [SQL Server], word breakers
- default full-text language option
- stemmers [full-text search]
- conjugating verbs [full-text search]
- word breakers [full-text search]
ms.assetid: d4bdd16b-a2db-4101-a946-583d1c674229
caps.latest.revision: 89
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5023aeceed2edd6170b58500edafb7342c21ba28
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="configure-and-manage-word-breakers-and-stemmers-for-search"></a>Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche

Wörtertrennung und Wortstammerkennung führen eine linguistische Analyse aller volltextindizierten Daten aus. Die linguistische Analyse führt die folgenden beiden Schritte aus:

-   **Suchen von Wortgrenzen (Wörtertrennung)**. Die *Wörtertrennung* identifiziert einzelne Wörter, indem die Wortgrenzen basierend auf den lexikalischen Regeln der Sprache ermittelt werden. Jedes Wort (auch bezeichnet als *Token*) wird zur Größenreduzierung in einer komprimierten Darstellung in den Volltextindex eingefügt.

-   **Konjugieren von Verben (Wortstammerkennung)**. Die *Wortstammerkennung* generiert Flexionsformen eines bestimmten Worts basierend auf den jeweiligen Regeln der Sprache. (Zum Beispiel sind „laufend“, „lief“ und „gelaufen“ verschiedene Formen des Worts „laufen“.)

## <a name="word-breakers-and-stemmers-are-language-specific"></a>Wörtertrennungen und Wortstammerkennungen sind sprachspezifisch.

Wörtertrennungen und Wortstammerkennungen sind sprachspezifisch, und die Regeln für die linguistische Analyse unterscheiden sich für verschiedene Sprachen. Mit sprachspezifischen Wörtertrennungen erzielen Sie für die jeweilige Sprache genauere Ergebnisbegriffe.

Um Wörtertrennungen und Wortstammerkennungen für alle von SQL Server unterstützten Sprachen zu verwenden, müssen Sie in der Regel keine Maßnahmen ergreifen.

-   Wenn es eine Wörtertrennung für eine Sprachfamilie gibt, jedoch nicht für die jeweilige Untersprache, wird die Hauptsprache verwendet. Beispielsweise wird Text in kanadischem Französisch mit der Wörtertrennung für Französisch behandelt.
-   Ist für eine Sprache keine Wörtertrennung verfügbar, wird die neutrale Wörtertrennung verwendet. Mit der neutralen Wörtertrennung werden neutrale Zeichen, wie Leerzeichen und Satzzeichen, als Wortgrenzen betrachtet.

## <a name="get-the-list-of-supported-languages"></a>Anzeigen der vollständigen Liste der unterstützten Sprachen

Verwenden Sie die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung, um die Liste der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Volltextsuche unterstützten Sprachen anzuzeigen. Das Vorhandensein einer Sprache in der Liste gibt an, dass Wörtertrennungen für diese Sprache registriert sind. 
  
```tsql
SELECT * FROM sys.fulltext_languages
```

##  <a name="register"></a> Anzeigen der Liste der registrierten Wörtertrennungen

Zur Verwendung der Wörtertrennungen für eine Sprache durch die Volltextsuche müssen diese registriert werden. Bei registrierten Wörtertrennungen sind die zugeordneten sprachlichen Ressourcen – Wortstammerkennung, Füllwörter (Stoppwörter) und Thesaurusdateien – für Volltextindizierungs- und Volltextabfragevorgänge verfügbar.

Verwenden Sie die folgende Anweisung, um die Liste der registrierten Wörtertrennungskomponenten anzuzeigen.

```tsql
EXEC sp_help_fulltext_system_components 'wordbreaker';  
GO  
```

Zusätzliche Optionen und weitere Informationen finden Sie unter [sp_help_fulltext_system_components &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md).
 
## <a name="if-you-add-or-remove-a-word-breaker"></a>Hinzufügen oder Entfernen einer Wörtertrennung  
Wenn Sie eine Wörtertrennung hinzufügen, entfernen oder ändern, müssen Sie die Liste der Microsoft Windows-Gebietsschemabezeichner (LCID) aktualisieren, die bei Volltextindizierung und -abfrage unterstützt werden. Weitere Informationen finden Sie unter [View or Change Registered Filters and Word Breakers](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).  
  
##  <a name="default"></a> Festlegen der Option für die Volltext-Standardsprache  
 Bei einer lokalisierten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wird die Option [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Volltext-Standardsprache **vom** -Setup auf die Sprache des Servers festgelegt, falls eine geeignete Übereinstimmung vorhanden ist. Bei einer nicht lokalisierten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wird Englisch für die Option **Volltext-Standardsprache** verwendet.  
  
 Beim Erstellen oder Ändern eines Volltextindexes können Sie für jede volltextindizierte Spalte eine andere Sprache angeben. Ist für eine Spalte keine Sprache angegeben, wird standardmäßig der Wert der Konfigurationsoption **Volltext-Standardsprache**verwendet.  
  
> [!NOTE]  
>  Alle Spalten, die in einer einzelnen Klausel für eine Volltextabfragefunktion aufgelistet sind, müssen dieselbe Sprache verwenden, sofern nicht die LANGUAGE-Option in der Abfrage angegeben ist. Die Sprache der volltextindizierten Spalte, auf die sich die Abfrage bezieht, bestimmt die linguistische Analyse, die mit Argumenten der Volltext-Abfrageprädikate ([CONTAINS](../../t-sql/queries/contains-transact-sql.md) und [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)) und -Funktionen ([CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) und [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)) ausgeführt wird.  
  
##  <a name="lang"></a> Auswählen der Sprache für eine indizierte Spalte  
 Beim Erstellen eines Volltextindex wird empfohlen, die Sprache für jede indizierte Spalte anzugeben. Wenn für eine Spalte keine Sprache angegeben ist, wird die Standardsprache des Systems verwendet. Die Sprache einer Spalte bestimmt, welche Wörtertrennung und Wortstammerkennung zum Indizieren dieser Spalte verwendet wird. Außerdem wird die Thesaurusdatei dieser Sprache bei Volltextabfragen der Spalte verwendet.  
  
 Bei der Wahl der Spaltensprache für die Erstellung eines Volltextindex sind mehrere Dinge zu bedenken. Diese beziehen sich darauf, wie der Text vom Volltextmodul in Token zerlegt und anschließend indiziert wird. Weitere Informationen finden Sie unter [Auswählen einer Sprache beim Erstellen eines Volltextindex](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
Führen Sie die folgende Anweisung aus, um die Wörtertrennungssprache bestimmter Spalten anzuzeigen.
   
```tsql 
SELECT 'language_id' AS "LCID" FROM sys.fulltext_index_columns;
```  

Zusätzliche Optionen und weitere Informationen finden Sie unter [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md).

##  <a name="tshoot"></a> Behebung von Timeoutfehlern bei der Wörtertrennung  
 Timeoutfehler können bei der Wörtertrennung in verschiedenen Situationen auftreten. Weitere Informationen zu diesen Situationen sowie zur Behandlung dieser Fehler finden Sie unter [MSSQLSERVER_30053](https://msdn.microsoft.com/en-us/library/cc879279.aspx).

### <a name="info-about-the-mssqlserver30053-error"></a>Informationen zum Fehler MSSQLSERVER_30053
  
|Eigenschaft|Wert|
|-|-|
|Produktname|SQL Server|  
|Ereignis-ID|30053|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|FTXT_QUERY_E_WORDBREAKINGTIMEOUT|  
|Meldungstext|Timeout bei der Wörtertrennung für die Volltextabfragezeichenfolge. Dies kann passieren, wenn die Verarbeitung der Volltextabfragezeichenfolge lange dauert oder eine große Anzahl von Abfragen auf dem Server ausgeführt wird. Führen Sie die Abfrage bei geringerer Auslastung erneut aus.|  
  
#### <a name="explanation"></a>Erklärung  
 In den folgenden Fällen kann es zu Timeoutfehlern bei der Wörtertrennung kommen:  
  
-   Die Wörtertrennung für die Abfragesprache ist falsch konfiguriert; z. B. sind die entsprechenden Registrierungseinstellungen falsch.  
  
-   Die Wörtertrennung schlägt bei einer bestimmten Abfragezeichenfolge fehl.  
  
-   Die Wörtertrennung gibt bei einer bestimmten Abfragezeichenfolge zu viele Daten zurück. Diese Daten werden als möglicher Angriff in Form eines Pufferüberlaufs interpretiert, was dafür sorgt, dass der für die Ausführung der Wörtertrennungsdienste verantwortliche Filterdaemonprozess (fdhost.exe) beendet wird.  
  
-   Der Filterdaemonprozess wurde falsch konfiguriert.  
  
     Zu den häufigsten Konfigurationsproblemen gehören abgelaufene Kennwörter oder Domänenrichtlinien, die eine Anmeldung am Filterdaemonkonto verhindern.  
  
-   Auf der Serverinstanz wird eine sehr große Abfragelast ausgeführt, z. B. dauert die Verarbeitung der Volltextabfragezeichenfolge sehr lange, oder es wird eine große Anzahl von Abfragen auf dem Server ausgeführt. Dies ist die wahrscheinliche Ursache.  
  
#### <a name="user-action"></a>Benutzeraktion  
 Wählen Sie wie folgt die Benutzeraktion aus, die der wahrscheinlichen Ursache des Timeouts entspricht:  
  
|Wahrscheinliche Ursache|Benutzeraktion|  
|--------------------|-----------------|  
|Die Wörtertrennung ist für die Abfragesprache nicht richtig konfiguriert.|Wenn Sie die Wörtertrennung eines Drittanbieters verwenden, ist sie möglicherweise auf dem Betriebssystem falsch registriert. Registrieren Sie die Wörtertrennung in diesem Fall erneut. Weitere Informationen finden Sie unter [Wiederherstellen der von der Suche verwendeten Wörtertrennungen auf die vorherige Version](revert-the-word-breakers-used-by-search-to-the-previous-version.md).|  
|Die Wörtertrennung schlägt bei einer bestimmten Abfragezeichenfolge fehl.|Wenn die Wörtertrennung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt wird, wenden Sie sich an den Microsoft-Kundenservice und -support.|  
|Die Wörtertrennung gibt bei einer bestimmten Abfragezeichenfolge zu viele Daten zurück.|Wenn die Wörtertrennung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt wird, wenden Sie sich an den Microsoft-Kundenservice und -support.|  
|Der Filterdaemonprozess wurde falsch konfiguriert.|Stellen Sie sicher, dass Sie das aktuelle Kennwort verwenden und dass die Anmeldung unter dem Filterdaemonkonto nicht von einer Domänenrichtlinie verhindert wird.|  
|Auf der Serverinstanz wird eine große Abfragelast ausgeführt.|Führen Sie die Abfrage bei geringerer Auslastung erneut aus.|  

##  <a name="impact"></a> Auswirkungen der aktualisierten Wörtertrennungen  
 Jede Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält in der Regel neue Wörtertrennungen, die über bessere linguistische Regeln als frühere Wörtertrennungen verfügen und außerdem genauer sind. Gegebenenfalls verhalten sich die neuen Wörtertrennungen im Vergleich zu den Wörtertrennungen in importierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Volltextindizes etwas anders.
 
Dies ist wichtig, wenn ein Volltextkatalog importiert wurde, während eine Datenbank auf die neue Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]aktualisiert wurde. Eine oder mehrere Sprachen, die von den Volltextindizes im Volltextkatalog verwendet werden, sind jetzt ggf. neuen Wörtertrennungen zugeordnet. Weitere Informationen finden Sie unter [Upgrade der Volltextsuche](../../relational-databases/search/upgrade-full-text-search.md).  
  

## <a name="see-also"></a>Siehe auch  
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)    
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 
  

