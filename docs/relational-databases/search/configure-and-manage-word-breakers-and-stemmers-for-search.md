---
title: "Konfigurieren und Verwalten von W&#246;rtertrennungen und Wortstammerkennungen f&#252;r die Suche | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Sprachen [Volltextsuche]"
  - "Volltextsuche [SQL Server], Wortstammerkennung"
  - "Sprachanalyse [Volltextsuche]"
  - "Volltextindizes [SQL Server], linguistische Analyse"
  - "Volltextsuche [SQL Server], Wörtertrennung"
  - "Volltext-Standardsprache (Option)"
  - "Wortstammerkennung [Volltextsuche]"
  - "Konjugieren von Verben [Volltextsuche]"
  - "Wörtertrennungen [Volltextsuche]"
ms.assetid: d4bdd16b-a2db-4101-a946-583d1c674229
caps.latest.revision: 89
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 88
---
# Konfigurieren und Verwalten von W&#246;rtertrennungen und Wortstammerkennungen f&#252;r die Suche
  Wörtertrennung und Wortstammerkennung führen eine linguistische Analyse aller volltextindizierten Daten aus. Zur linguistischen Analyse gehört das Auffinden von Wortgrenzen (Trennfugen) und das Konjugieren von Verben (Wortstammerkennung). Wörtertrennungen und Wortstammerkennungen sind sprachspezifisch, und die Regeln für die linguistische Analyse unterscheiden sich für verschiedene Sprachen. Für eine bestimmte Sprache identifiziert eine *Wörtertrennung* einzelne Wörter, indem die Wortgrenzen basierend auf den lexikalischen Regeln der Sprache ermittelt werden. Jedes Wort (auch bezeichnet als *Token*) wird zur Größenreduzierung in einer komprimierten Darstellung in den Volltextindex eingefügt. Die *Wortstammerkennung* generiert Flexionsformen eines bestimmten Worts basierend auf den jeweiligen Regeln der Sprache. (Zum Beispiel sind „laufend“, „lief“ und „gelaufen“ verschiedene Formen des Worts „laufen“.)  
  
 Wenn Sie sprachspezifische Wörtertrennungen verwenden, können Sie für die jeweilige Sprache genauere Ergebnisbegriffe erzielen. Wenn es eine Wörtertrennung für eine Sprachfamilie gibt, jedoch nicht für die jeweilige Untersprache, wird die Hauptsprache verwendet. Beispielsweise wird Text in kanadischem Französisch mit der Wörtertrennung für Französisch behandelt. Ist für eine Sprache keine Wörtertrennung verfügbar, wird die neutrale Wörtertrennung verwendet. Mit der neutralen Wörtertrennung werden neutrale Zeichen, wie Leerzeichen und Satzzeichen, als Wortgrenzen betrachtet.  
  
##  <a name="register"></a> Registrieren der Wörtertrennungen  
 Die Wörtertrennung muss für eine zu verwendende Sprache jeweils registriert sein. Bei registrierten Wörtertrennungen sind die zugeordneten sprachlichen Ressourcen – Wortstammerkennung, Füllwörter (Stoppwörter) und Thesaurusdateien – für Volltextindizierungs- und Volltextabfragevorgänge verfügbar. Wenn Sie eine Liste der Sprachen anzeigen möchten, deren Wörtertrennungen derzeit in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registriert sind, verwenden Sie die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung:  
  
 SELECT * FROM sys.fulltext_languages  
  
 Wenn Sie eine Wörtertrennung hinzufügen, entfernen oder ändern, müssen Sie die Liste der Microsoft Windows-Gebietsschemabezeichner (LCID) aktualisieren, die bei Volltextindizierung und -abfrage unterstützt werden. Weitere Informationen finden Sie unter [View or Change Registered Filters and Word Breakers](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).  
  
##  <a name="default"></a> Festlegen der Option für die Volltext-Standardsprache  
 Bei einer lokalisierten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird die Option **Volltext-Standardsprache** vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup auf die Sprache des Servers festgelegt, falls eine geeignete Übereinstimmung vorhanden ist. Bei einer nicht lokalisierten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird Englisch für die Option **Volltext-Standardsprache** verwendet.  
  
 Beim Erstellen oder Ändern eines Volltextindex können Sie für jede volltextindizierte Spalte eine andere Sprache angeben. Ist für eine Spalte keine Sprache angegeben, wird standardmäßig der Wert der Konfigurationsoption **Volltext-Standardsprache** verwendet.  
  
> [!NOTE]  
>  Alle Spalten, die in einer einzelnen Klausel für eine Volltextabfragefunktion aufgelistet sind, müssen dieselbe Sprache verwenden, sofern nicht die LANGUAGE-Option in der Abfrage angegeben ist. Die Sprache der volltextindizierten Spalte, auf die sich die Abfrage bezieht, bestimmt die linguistische Analyse, die mit Argumenten der Volltext-Abfrageprädikate ([CONTAINS](../../t-sql/queries/contains-transact-sql.md) und [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)) und -Funktionen ([CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) und [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)) ausgeführt wird.  
  
##  <a name="lang"></a> Auswählen der Sprache für eine indizierte Spalte  
 Beim Erstellen eines Volltextindex wird empfohlen, die Sprache für jede indizierte Spalte anzugeben. Wenn für eine Spalte keine Sprache angegeben ist, wird die Standardsprache des Systems verwendet. Die Sprache einer Spalte bestimmt, welche Wörtertrennung und Wortstammerkennung zum Indizieren dieser Spalte verwendet wird. Außerdem wird die Thesaurusdatei dieser Sprache bei Volltextabfragen der Spalte verwendet.  
  
 Bei der Wahl der Spaltensprache für die Erstellung eines Volltextindex sind mehrere Dinge zu bedenken. Diese beziehen sich darauf, wie der Text vom Volltextmodul in Token zerlegt und anschließend indiziert wird. Weitere Informationen finden Sie unter [Auswählen einer Sprache beim Erstellen eines Volltextindex](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
 **So zeigen Sie die Wörtertrennungssprache einer Spalte an**  
  
-   [Verwalten von Volltextindizes](../Topic/Manage%20Full-Text%20Indexes.md)  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
  
    ```  
    SELECT 'language_id' AS "LCID" FROM sys.fulltext_index_columns;  
    ```  
  
##  <a name="info"></a> Abrufen von Informationen zu Wörtertrennungen  
 **Anzeigen des Tokenisierungsergebnis einer Kombination aus Wörtertrennung, Thesaurus und Stopliste**  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md).  
  
 **So geben Sie Informationen über die registrierten Wörtertrennungen zurück**  
  
-   [sp_help_fulltext_system_components &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
  
##  <a name="tshoot"></a> Behebung von Timeoutfehlern bei der Wörtertrennung  
 Timeoutfehler können bei der Wörtertrennung in verschiedenen Situationen auftreten. Weitere Informationen zu diesen Situationen sowie zur Behandlung dieser Fehler finden Sie unter [MSSQLSERVER_30053](../Topic/MSSQLSERVER_30053.md).  
  
##  <a name="impact"></a> Auswirkungen der neuen Wörtertrennungen  
 Jede Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält in der Regel neue Wörtertrennungen, die über bessere linguistische Regeln als frühere Wörtertrennungen verfügen und außerdem genauer sind. Gegebenenfalls verhalten sich die neuen Wörtertrennungen im Vergleich zu den Wörtertrennungen in importierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Volltextindizes etwas anders. Dies ist wichtig, wenn ein Volltextkatalog importiert wurde, während eine Datenbank auf die neue Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktualisiert wurde. Eine oder mehrere Sprachen, die von den Volltextindizes im Volltextkatalog verwendet werden, sind jetzt ggf. neuen Wörtertrennungen zugeordnet. Weitere Informationen finden Sie unter [Upgrade der Volltextsuche](../../relational-databases/search/upgrade-full-text-search.md).  
  
 Eine vollständige Liste aller Wörtertrennungen finden Sie unter [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
  
## Siehe auch  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)   
 [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [Upgrade der Volltextsuche](../../relational-databases/search/upgrade-full-text-search.md)  
  
  