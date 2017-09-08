---
title: Windows-Sortierungsname (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Windows collations [SQL Server]
- names [SQL Server], collations
- collations [SQL Server], Windows collations
- Collation Designator
ms.assetid: acceef84-2c68-46e2-a021-be019b7ab14e
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7898592af503300cb1bea261d8809a81fa568155
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="windows-collation-name-transact-sql"></a>Name der Windows-Sortierung (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt den Namen der Windows-Sortierung in der COLLATE-Klausel in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an. Der Name der Windows-Sortierung besteht aus dem Sortierungskennzeichner und den Vergleichsarten.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<Windows_collation_name> :: =   
CollationDesignator_<ComparisonStyle>  
  
<ComparisonStyle> :: =   
{ CaseSensitivity_AccentSensitivity  [ _KanatypeSensitive ] [ _WidthSensitive ]    
}  
| { _BIN | _BIN2 }  
```  
  
## <a name="arguments"></a>Argumente  
 *CollationDesignator*  
 Gibt die grundlegenden in der Windows-Sortierung verwendeten Sortierungsregeln an. Zu den grundlegenden Sortierungsregeln zählen:  
  
-   Die Sortierregeln, die angewendet werden, wenn Wörterbuchsortierung angegeben wird. Sortierregeln basieren auf Alphabet oder Sprache.  
  
-   Die Codepage, die zum Speichern von Nichtunicode-Zeichendaten verwendet wird.  
  
 Beispiele hierfür sind:  
  
-   Latin1_General oder French: Beide verwenden Codepage 1252.  
  
-   Turkish: verwendet die Codepage 1254.  
  
 *CaseSensitivity*  
 **CI** gibt Groß-/Kleinschreibung, **CS** gibt Groß-/Kleinschreibung beachtet.  
  
 *AccentSensitivity*  
 **AI** gibt Unterscheidung nach Akzent **AS** gibt an, nach Akzent unterschieden wird.  
  
 *KanatypeSensitive*  
 **Weggelassen** gibt an, Unterscheidung nach Kanatyp **KS** gibt an, nach Kanatyp unterschieden.  
  
 *WidthSensitivity*  
 **Weggelassen** gibt an, Unterscheidung nach Breite **WS** Unterscheidung.  
  
 **"BIN"**  
 Gibt die zu verwendende abwärtskompatible binäre Sortierreihenfolge an.  
  
 **BIN2**  
 Gibt die binäre Sortierreihenfolge an, die die Semantik für den Codepunktvergleich verwendet.  
  
## <a name="remarks"></a>Hinweise  
 Je nach Version der Sortierungen sind einige Codepunkte möglicherweise nicht definiert. Vergleichen Sie beispielsweise:  
  
```  
SELECT LOWER(nchar(504) COLLATE Latin1_General_CI_AS);   
SELECT LOWER (nchar(504) COLLATE Latin1_General_100_CI_AS);  
GO  
```  
  
 Die erste Zeile gibt einen Großbuchstaben zurück, wenn die Sortierung Latin1_General_CI_AS lautet, da dieser Codepunkt in dieser Sortierung nicht definiert ist.  
  
 Bei der Arbeit mit bestimmten Sprachen kann es entscheidend sein, die älteren Sortierungen zu vermeiden. Das gilt beispielsweise für Telegu.  
  
 In einigen Fällen können Windows-Sortierungen und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortierungen unterschiedliche Abfragepläne für dieselbe Abfrage generieren.  
  
## <a name="examples"></a>Beispiele  
 Im Folgenden finden Sie einige Beispiele für Namen der Windows-Sortierung:  
  
-   **Latin1_General_100_**  
  
 Die Sortierung verwendet die Latin1 General-Wörterbuch-Sortierungsregeln, Codepage 1252. Es erfolgt keine Unterscheidung nach Groß-/Kleinschreibung, aber eine Unterscheidung nach Akzenten. Die Sortierung verwendet die Latin1 General-Wörterbuch-Sortierungsregeln und ist der Codepage 1252 zugeordnet. Zeigt die Versionsnummer der Sortierung an, falls es sich um eine Windows-Sortierung handelt: _90 oder _100. Ist Groß-/Kleinschreibung (CI) und Unterscheidung nach Akzent (AS).  
  
-   **Estonian_CS_AS**  
  
     Sortierung verwendet die estnischen Wörterbuchsortierregeln, Codepage 1257. Es erfolgt eine Unterscheidung nach Groß-/Kleinschreibung und nach Akzenten.  
  
-   **Latin1_General_BIN**  
  
     Die Sortierung verwendet Codepage 1252 und binäre Sortierungsregeln. Die Latin1 General-Wörterbuch-Sortierungsregeln werden ignoriert.  
  
## <a name="windows-collations"></a>Windows-Sortierreihenfolgen  
 Führen Sie die folgende Abfrage aus, um die von Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz unterstützten Windows-Sortierungen aufzulisten.  
  
```  
SELECT * FROM sys.fn_helpcollations() WHERE name NOT LIKE 'SQL%';  
```  
  
 In der folgenden Tabelle werden alle Windows-Sortierungen aufgelistet, die in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] unterstützt werden.  
  
|Windows-Gebietsschema|Sortierungsversion 100|Sortierungsversion 90|  
|--------------------|---------------------------|--------------------------|  
|Elsässisch (Frankreich)|Latin1_General_100_|Nicht verfügbar|  
|Amharisch (Äthiopien)|Latin1_General_100_|Nicht verfügbar|  
|Armenisch (Armenien)|Cyrillic_General_100_|Nicht verfügbar|  
|Assamisch (Indien)|Assamese_100_ <sup>1</sup>|Nicht verfügbar|  
|Baschkirisch (Russische Föderation)|Bashkir_100_|Nicht verfügbar|  
|Baskisch (Baskisch)|Latin1_General_100_|Nicht verfügbar|  
|Bangla (Bangladesch)|Bengali_100_<sup>1</sup>|Nicht verfügbar|  
|Bangla (Indien)|Bengali_100_<sup>1</sup>|Nicht verfügbar|  
|Bosnisch (Bosnien und Herzegowina, kyrillisch)|Bosnian_Cyrillic_100_|Nicht verfügbar|  
|Bosnisch (Bosnien und Herzegowina, lateinisch)|Bosnian_Latin_100_|Nicht verfügbar|  
|Bretonisch (Frankreich)|Breton_100_|Nicht verfügbar|  
|Chinesisch (Macao SAR)|Chinese_Traditional_Pinyin_100_|Nicht verfügbar|  
|Chinesisch (Macao SAR)|Chinese_Traditional_Stroke_Order_100_|Nicht verfügbar|  
|Chinesisch (Singapur)|Chinese_Simplified_Stroke_Order_100_|Nicht verfügbar|  
|Korsisch (Frankreich)|Corsican_100_|Nicht verfügbar|  
|Kroatisch (Bosnien und Herzegowina, lateinisch)|Croatian_100_|Nicht verfügbar|  
|Dari (Afghanistan)|Dari_100_|Nicht verfügbar|  
|Englisch (Indien)|Latin1_General_100_|Nicht verfügbar|  
|Englisch (Malaysia)|Latin1_General_100_|Nicht verfügbar|  
|Englisch (Singapur)|Latin1_General_100_|Nicht verfügbar|  
|Philippinisch (Philippinen)|Latin1_General_100_|Nicht verfügbar|  
|Friesisch (Niederlande)|Frisian_100_|Nicht verfügbar|  
|Georgisch (Georgien)|Cyrillic_General_100_|Nicht verfügbar|  
|Grönländisch (Grönland)|Danish_Greenlandic_100_|Nicht verfügbar|  
|Gujarati (Indien)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Hausa (Nigeria, lateinisch)|Latin1_General_100_|Nicht verfügbar|  
|Hindi (Indien)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Igbo (Nigeria)|Latin1_General_100_|Nicht verfügbar|  
|Inuktitut (Kanada, lateinisch)|Latin1_General_100_|Nicht verfügbar|  
|Inuktitut (Syllabics) Kanada|Latin1_General_100_|Nicht verfügbar|  
|Irisch (Irland)|Latin1_General_100_|Nicht verfügbar|  
|Japanisch (Japan XJIS)|Japanese_XJIS_100_|Japanese_90_, Japanese_|  
|Japanisch (Japan)|Japanese_Bushu_Kakusu_100_|Nicht verfügbar|  
|Kannada (Indien)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Khmer (Kambodscha)|Khmer_100_<sup>1</sup>|Nicht verfügbar|  
|K'iche (Guatemala)|Modern_Spanish_100_|Nicht verfügbar|  
|Kinyarwanda (Ruanda)|Latin1_General_100_|Nicht verfügbar|  
|Konkani (Indien)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Lao (Volksrepublik Laos)|Lao_100_<sup>1</sup>|Nicht verfügbar|  
|Niedersorbisch (Deutschland)|Latin1_General_100_|Nicht verfügbar|  
|Luxemburgisch (Luxemburg)|Latin1_General_100_|Nicht verfügbar|  
|Malayalam (Indien)|Indic_General_100_<sup>1</sup>|Nicht verfügbar|  
|Maltesisch (Malta)|Maltese_100_|Nicht verfügbar|  
|Maori (Neuseeland)|Maori_100_|Nicht verfügbar|  
|Mapudungun (Chile)|Mapudungan_100_|Nicht verfügbar|  
|Marathi (Indien)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Mohawk (Kanada)|Mohawk_100_|Nicht verfügbar|  
|Mongolisch (VRC)|Cyrillic_General_100_|Nicht verfügbar|  
|Nepali (Nepal)|Nepali_100_<sup>1</sup>|Nicht verfügbar|  
|Norwegisch (Bokmål, Norwegen)|Norwegian_100_|Nicht verfügbar|  
|Norwegisch (Nynorsk, Norwegen)|Norwegian_100_|Nicht verfügbar|  
|Okzitanisch (Frankreich)|French_100_|Nicht verfügbar|  
|Oriya (Indien)|Indic_General_100_<sup>1</sup>|Nicht verfügbar|  
|Paschtu (Afghanistan)|Pashto_100_<sup>1</sup>|Nicht verfügbar|  
|Persisch (Iran)|Persian_100_|Nicht verfügbar|  
|Punjabi (Indien)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Quechua (Bolivien)|Latin1_General_100_|Nicht verfügbar|  
|Quechua (Ecuador)|Latin1_General_100_|Nicht verfügbar|  
|Quechua (Peru)|Latin1_General_100_|Nicht verfügbar|  
|Rätoromanisch (Schweiz)|Romansh_100_|Nicht verfügbar|  
|Inari-Sami (Finnland)|Sami_Sweden_Finland_100_|Nicht verfügbar|  
|Lule-Sami (Norwegen)|Sami_Norway_100_|Nicht verfügbar|  
|Lule-Sami (Schweden)|Sami_Sweden_Finland_100_|Nicht verfügbar|  
|Nord-Sami (Finnland)|Sami_Sweden_Finland_100_|Nicht verfügbar|  
|Nord-Sami (Nord, Norwegen)|Sami_Norway_100_|Nicht verfügbar|  
|Nord-Sami (Schweden)|Sami_Sweden_Finland_100_|Nicht verfügbar|  
|Skolt-Sami (Finnland)|Sami_Sweden_Finland_100_|Nicht verfügbar|  
|Süd-Sami (Norwegen)|Sami_Norway_100_|Nicht verfügbar|  
|Süd-Sami (Schweden)|Sami_Sweden_Finland_100_|Nicht verfügbar|  
|Sanskrit (Indien)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Serbisch (Bosnien und Herzegowina, kyrillisch)|Serbian_Cyrillic_100_|Nicht verfügbar|  
|Serbisch (Bosnien und Herzegowina, lateinisch)|Serbian_Latin_100_|Nicht verfügbar|  
|Serbisch (Serbien, kyrillisch)|Serbian_Cyrillic_100_|Nicht verfügbar|  
|Serbisch (Serbien, lateinisch)|Serbian_Latin_100_|Nicht verfügbar|  
|Sesotho sa Leboa/Nord-Sotho (Südafrika)|Latin1_General_100_|Nicht verfügbar|  
|Setswana/Tswana (Südafrika)|Latin1_General_100_|Nicht verfügbar|  
|Sinhala (Sri Lanka)|Indic_General_100_<sup>1</sup>|Nicht verfügbar|  
|Suaheli (Kenia)|Latin1_General_100_|Nicht verfügbar|  
|Syrisch (Syrien)|Syriac_100_<sup>1</sup>|Syriac_90_|  
|Tadschikisch (Tadschikistan)|Cyrillic_General_100_|Nicht verfügbar|  
|Tamazight (Algerien, lateinisch)|Tamazight_100_|Nicht verfügbar|  
|Tamil (Indien)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Telugu (Indien)|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|Tibetisch (VRC)|Tibetan_100_<sup>1</sup>|Nicht verfügbar|  
|Turkmenisch (Turkmenistan)|Turkmen_100_|Nicht verfügbar|  
|Uighurisch (VRC)|Uighur_100_|Nicht verfügbar|  
|Obersorbisch (Deutschland)|Upper_Sorbian_100_|Nicht verfügbar|  
|Urdu (Pakistan)|Urdu_100_|Nicht verfügbar|  
|Walisisch (Großbritannien)|Welsh_100_|Nicht verfügbar|  
|Wolof (Senegal)|French_100_|Nicht verfügbar|  
|Xhosa/isiXhosa (Südafrika)|Latin1_General_100_|Nicht verfügbar|  
|Jakutisch (Russische Föderation)|Yakut_100_|Nicht verfügbar|  
|Yi (VRC)|Latin1_General_100_|Nicht verfügbar|  
|Yoruba (Nigeria)|Latin1_General_100_|Nicht verfügbar|  
|Zulu/isiZulu (Südafrika)|Latin1_General_100_|Nicht verfügbar|  
|Veraltet, nicht verfügbar auf Serverebene in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] oder höher|Hindi|Hindi|  
|Veraltet, nicht verfügbar auf Serverebene in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] oder höher|Korean_Wansung_Unicode|Korean_Wansung_Unicode|  
|Veraltet, nicht verfügbar auf Serverebene in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] oder höher|Lithuanian_Classic|Lithuanian_Classic|  
|Veraltet, nicht verfügbar auf Serverebene in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] oder höher|Macedonian|Macedonian|  
  
 <sup>1</sup>nur-Unicode-Windows-Sortierungen können nur auf Spaltenebene und Ausdrucksebene Daten angewendet werden. Sie können nicht für Sortierungen auf Server- oder Datenbankebene verwendet werden.  
  
 <sup>2</sup>wie die Sortierung für Chinesisch (Taiwan), Chinesisch (Macao) die Regeln für Chinesisch (vereinfacht) verwendet; im Unterschied zu Chinesisch (Taiwan), die Codepage 950 verwendet.  
  
## <a name="see-also"></a>Siehe auch  
 [Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [Konstanten &#40; Transact-SQL &#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [Table &#40; Transact-SQL &#41;](../../t-sql/data-types/table-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)  
  
  
