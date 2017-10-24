---
title: Transact-SQL-Syntaxkonventionen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sql13.TSQLExpandPortal.f1
dev_langs:
- TSQL
helpviewer_keywords:
- conventions [SQL Server]
- Applies to section in Transact-SQL topics
- code example conventions [SQL Server]
- objects [SQL Server], names
- code [SQL Server], conventions
- multipart names [SQL Server]
- Transact-SQL syntax conventions
- syntax conventions [SQL Server]
- code [SQL Server]
- Transact-SQL
- naming conventions [SQL Server]
- syntax [SQL Server], Transact-SQL
ms.assetid: 35fbcf7f-8b55-46cd-a957-9b8c7b311241
caps.latest.revision: 55
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a1c60d865d1b18eae1cd89ea226e91e8e7b5b9e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="transact-sql-syntax-conventions-transact-sql"></a>Transact-SQL-Syntax Konventionen-Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  In der folgenden Tabelle werden die Konventionen aufgeführt und beschrieben, die in den Syntaxdiagrammen in der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Referenz verwendet werden.  
  
|Konvention|Syntaxelemente|  
|----------------|--------------|  
|GROSSBUCHSTABEN|[!INCLUDE[tsql](../../includes/tsql-md.md)]-Schlüsselwörter.|  
|*Kursiv*|Vom Benutzer anzugebende Parameter der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Syntax.|  
|**Fett**|Datenbanknamen, Tabellennamen, Spaltennamen, Indexnamen, gespeicherte Prozeduren, Hilfsprogramme, Datentypnamen und Text, der wie aufgeführt eingegeben werden muss.|  
|**"Unterstreichen"**|Gibt den Standardwert an, der verwendet wird, wenn die Klausel mit dem unterstrichenen Wert in der Anweisung ausgelassen wird.|  
|&#124; (Senkrechter Strich)|Trennt in eckigen oder geschweiften Klammern eingeschlossene Syntaxelemente. Sie können nur eines der Elemente verwenden.|  
|`[ ]` (eckige Klammern)|Optionale Syntaxelemente. Geben Sie die eckigen Klammern nicht ein.|  
|{ } (geschweifte Klammern)|Erforderliche Syntaxelemente. Geben Sie die geschweiften Klammern nicht ein.|  
|[**,**...*n*]|Zeigt an, dass das vorherige Element *n* -mal wiederholt werden kann. Die einzelnen Vorkommen werden durch Kommas voneinander getrennt.|  
|[...*n*]|Zeigt an, dass das vorherige Element *n* -mal wiederholt werden kann. Die einzelnen Vorkommen werden durch Leerzeichen voneinander getrennt.|  
|;|[!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungsabschlusszeichen.Dieses Abschlusszeichen ist für die meisten Anweisungen in dieser Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht zwingend erforderlich, in zukünftigen Versionen kann sich dies jedoch ändern.|  
|\<Bezeichnung >:: =|Der Name eines Syntaxblockes. Diese Konvention dient zur Gruppierung und Bezeichnung von Abschnitten einer langen Syntax oder einer Syntaxeinheit, die an mehreren Stellen innerhalb einer Anweisung verwendet werden kann. Jeder Standort in der die Syntax kann verwendet werden, wird angegeben, mit der Bezeichnung in spitzen Klammern eingeschlossen: \<Bezeichnung >.<br /><br /> Eine Gruppe ist eine Auflistung von Ausdrücken, z. B. \<gruppierungssatz >; und eine Liste ist eine Auflistung von Sets, z. B. \<Liste zusammengesetzter Elemente >.|  
  
## <a name="multipart-names"></a>Mehrteilige Namen  
 Wenn keine anderen Angaben vorliegen, können alle [!INCLUDE[tsql](../../includes/tsql-md.md)]-Referenzen auf den Namen eines Datenbankobjekts aus vier Teilen bestehende Namen im folgenden Format sein:  
  
 *Server_name* **.** [*Database_name*]**.** [*Schema_name*]**.** *Object_name*  
  
 | *Database_name***.** [*Schema_name*]**.** *Object_name*  
  
 | *Schema_name***.** *Object_name*  
  
 *| object_name*  
  
 *Servername*  
 Gibt den Namen eines Verbindungs- oder Remoteservers an.  
  
 *database_name*  
 Gibt den Namen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank an, wenn sich das Objekt in einer lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] befindet. Wenn das Objekt in einem verknüpften Server ist *Database_name* gibt einen OLE DB-Katalog.  
  
 *schema_name*  
 Gibt den Namen des Schemas an, das das Objekt enthält, wenn sich das Objekt in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank befindet. Wenn das Objekt in einem verknüpften Server ist *Schema_name* gibt einen OLE DB-Schema an.  
  
 *object_name*  
 Gibt den Namen des Objekts an.  
  
 Wenn Sie auf ein bestimmtes Objekt verweisen, müssen Sie nicht immer den Server, die Datenbank und das Schema angeben, damit das Objekt vom [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] identifiziert werden kann. Wenn das Objekt nicht gefunden wird, wird jedoch ein Fehler zurückgegeben.  
  
> [!NOTE]  
>  Um Fehler bei der Namensauflösung zu vermeiden, wird empfohlen, den Schemanamen bei jeder Angabe eines Objekts anzugeben, das Schemas als Bereiche besitzt.  
  
 Um Zwischenknoten wegzulassen, verwenden Sie Punkte, um diese Positionen anzuzeigen. In der folgenden Tabelle sind die gültigen Formate für Objektnamen aufgeführt.  
  
|Objektverweisformat|Description|  
|-----------------------------|-----------------|  
|*Server* **.** *Datenbank* **.** *Schema* **.** *Objekt*|Vierteiliger Name.|  
|*Server* **.** *Datenbank* **...** *Objekt*|Der Schemaname wird weggelassen.|  
|*Server* **...** *Schema* **.** *Objekt*|Der Datenbankname wird weggelassen.|  
|*Server* **...**  *Objekt*|Der Datenbank- und der Schemaname werden weggelassen.|  
|*Datenbank* **.** *Schema* **.** *Objekt*|Der Servername wird weggelassen.|  
|*Datenbank* **...** *Objekt*|Der Server- und der Schemaname werden weggelassen.|  
|*Schema* **.** *Objekt*|Der Server- und der Datenbankname werden weggelassen.|  
|*Objekt*|Der Server-, der Datenbank- und der Schemaname werden weggelassen.|  
  
## <a name="code-example-conventions"></a>Konventionen für Codebeispiele  
 Wenn nicht anders angegeben, wurden die Beispiele in der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Referenz anhand von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und den Standardeinstellungen für die folgenden Optionen getestet:  
  
-   ANSI_NULLS  
  
-   ANSI_NULL_DFLT_ON  
  
-   ANSI_PADDING  
  
-   ANSI_WARNINGS  
  
-   CONCAT_NULL_YIELDS_NULL  
  
-   QUOTED_IDENTIFIER  
  
 Die meisten Codebeispiele in der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Referenz wurden auf Servern getestet, auf denen eine Sortierreihenfolge gilt, bei der die Groß-/Kleinschreibung beachtet wird. Auf den Testservern wurde in der Regel die ANSI/ISO-Codepage 1252 verwendet.  
  
 Vielen Codebeispielen Präfix Unicode-Zeichenfolgenkonstanten mit dem Buchstaben **N**. Ohne die **N** -Präfix wird die Zeichenfolge wird in die Standardcodepage der Datenbank konvertiert. Diese Standardcodepage erkennt möglicherweise bestimmte Zeichen nicht.  
  
## <a name="applies-to-references"></a>„Applies to“-Verweise  
 Die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Verweis enthält Themen im Zusammenhang mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], und [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]. Am oberen Rand jedes Thema ist ein Abschnitt, der angibt, welche Produkte den Betreff des Themas unterstützen. Wenn ein Produkt fehlt, ist die im Thema beschriebene Funktion nicht in diesem Produkt verfügbar. Beispielsweise wurden Verfügbarkeitsgruppen in eingeführt [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Die **Erstellen einer VERFÜGBARKEITSGRUPPE** Thema wird erörtert, gilt dies für **SQL Server (SQL Server 2012 bis aktuelle Version)** , da es nicht für gilt [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], oder [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 In einigen Fällen kann der allgemeine Gegenstand eines Themas in einem Produkt verwendet werden, aber es werden nicht alle Argumente unterstützt. Beispielsweise wurden Benutzer für eigenständige Datenbank in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] eingeführt. Die **CREATE USER** Anweisung kann verwendet werden, in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Produkt, jedoch die **WITH PASSWORD** Syntax kann nicht mit älteren Versionen verwendet werden. In diesem Fall werden zusätzliche **Applies to** -Abschnitte in den Beschreibungen der entsprechenden Arguments in den Text des Themas eingefügt.  
  
## <a name="see-also"></a>Siehe auch  
 [Transact-SQL-Referenz &#40;Datenbankmodul&#41;](../../t-sql/transact-sql-reference-database-engine.md)  
  
  



