---
title: Transact-SQL-Syntaxkonventionen (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7c4eb67190b5123296fbcffb3fac3f09e9ec2000
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="transact-sql-syntax-conventions-transact-sql"></a>Transact-SQL-Syntaxkonventionen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  In der folgenden Tabelle werden die Konventionen aufgeführt und beschrieben, die in den Syntaxdiagrammen in der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Referenz verwendet werden.  
  
|Konvention|Syntaxelemente|  
|----------------|--------------|  
|GROSSBUCHSTABEN|[!INCLUDE[tsql](../../includes/tsql-md.md)]-Schlüsselwörter.|  
|*Kursiv*|Vom Benutzer anzugebende Parameter der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Syntax.|  
|**Fett**|Datenbanknamen, Tabellennamen, Spaltennamen, Indexnamen, gespeicherte Prozeduren, Hilfsprogramme, Datentypnamen und Text, der wie aufgeführt eingegeben werden muss.|  
|**underline**|Gibt den Standardwert an, der verwendet wird, wenn die Klausel mit dem unterstrichenen Wert in der Anweisung ausgelassen wird.|  
|&#124; (Senkrechter Strich)|Trennt in eckigen oder geschweiften Klammern eingeschlossene Syntaxelemente. Sie können nur eines der Elemente verwenden.|  
|`[ ]` (eckige Klammern)|Optionale Syntaxelemente. Geben Sie die eckigen Klammern nicht ein.|  
|{ } (geschweifte Klammern)|Erforderliche Syntaxelemente. Geben Sie die geschweiften Klammern nicht ein.|  
|[**,**...*n*]|Zeigt an, dass das vorherige Element *n* -mal wiederholt werden kann. Die einzelnen Vorkommen werden durch Kommas voneinander getrennt.|  
|[...*n*]|Zeigt an, dass das vorherige Element *n* -mal wiederholt werden kann. Die einzelnen Vorkommen werden durch Leerzeichen voneinander getrennt.|  
|;|[!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungsabschlusszeichen.Dieses Abschlusszeichen ist für die meisten Anweisungen in dieser Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht zwingend erforderlich, in zukünftigen Versionen kann sich dies jedoch ändern.|  
|\<label> ::=|Der Name eines Syntaxblockes. Diese Konvention dient zur Gruppierung und Bezeichnung von Abschnitten einer langen Syntax oder einer Syntaxeinheit, die an mehreren Stellen innerhalb einer Anweisung verwendet werden kann. Jede Stelle, an der der Syntaxblock verwendet werden kann, wird durch die in spitze Klammern eingeschlossene Bezeichnung angezeigt: \<label>.<br /><br /> Ein Set ist eine Collection von Ausdrücken, z.B. \<Gruppierungssatz>. Eine Liste ist eine Collection von Sets, z.B. \<Liste zusammengesetzter Elemente>.|  
  
## <a name="multipart-names"></a>Mehrteilige Namen  
 Wenn keine anderen Angaben vorliegen, können alle [!INCLUDE[tsql](../../includes/tsql-md.md)]-Referenzen auf den Namen eines Datenbankobjekts aus vier Teilen bestehende Namen im folgenden Format sein:  
  
 *server_name* **.**[*database_name*]**.**[*schema_name*]**.***object_name*  
  
 | *database_name***.**[*schema_name*]**.***object_name*  
  
 | *schema_name***.***object_name*  
  
 *| object_name*  
  
 *server_name*  
 Gibt den Namen eines Verbindungs- oder Remoteservers an.  
  
 *database_name*  
 Gibt den Namen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank an, wenn sich das Objekt in einer lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] befindet. Wenn sich das Objekt auf einem verknüpften Server befindet, wird mit *database_name* ein OLE DB-Katalog angegeben.  
  
 *schema_name*  
 Gibt den Namen des Schemas an, das das Objekt enthält, wenn sich das Objekt in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank befindet. Wenn sich das Objekt auf einem Verbindungsserver befindet, wird mit *schema_name* ein OLE DB-Schemaname angegeben.  
  
 *object_name*  
 Gibt den Namen des Objekts an.  
  
 Wenn Sie auf ein bestimmtes Objekt verweisen, müssen Sie nicht immer den Server, die Datenbank und das Schema angeben, damit das Objekt vom [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] identifiziert werden kann. Wenn das Objekt jedoch nicht gefunden werden kann, wird ein Fehler zurückgegeben.  
  
> [!NOTE]  
>  Um Fehler bei der Namensauflösung zu vermeiden, wird empfohlen, den Schemanamen bei jeder Angabe eines Objekts anzugeben, das Schemas als Bereiche besitzt.  
  
 Um Zwischenknoten wegzulassen, verwenden Sie Punkte, um diese Positionen anzuzeigen. In der folgenden Tabelle sind die gültigen Formate für Objektnamen aufgeführt.  
  
|Objektverweisformat|Description|  
|-----------------------------|-----------------|  
|*server* **.** *database* **.** *schema* **.** *object*|Vierteiliger Name.|  
|*server* **.** *database* **..** *object*|Der Schemaname wird weggelassen.|  
|*server* **..** *schema* **.** *object*|Der Datenbankname wird weggelassen.|  
|*server* **...** *object*|Der Datenbank- und der Schemaname werden weggelassen.|  
|*database* **.** *schema* **.** *object*|Der Servername wird weggelassen.|  
|*database* **..** *object*|Der Server- und der Schemaname werden weggelassen.|  
|*schema* **.** *object*|Der Server- und der Datenbankname werden weggelassen.|  
|*object*|Der Server-, der Datenbank- und der Schemaname werden weggelassen.|  
  
## <a name="code-example-conventions"></a>Konventionen für Codebeispiele  
 Wenn nicht anders angegeben, wurden die Beispiele in der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Referenz anhand von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und den Standardeinstellungen für die folgenden Optionen getestet:  
  
-   ANSI_NULLS  
  
-   ANSI_NULL_DFLT_ON  
  
-   ANSI_PADDING  
  
-   ANSI_WARNINGS  
  
-   CONCAT_NULL_YIELDS_NULL  
  
-   QUOTED_IDENTIFIER  
  
 Die meisten Codebeispiele in der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Referenz wurden auf Servern getestet, auf denen eine Sortierreihenfolge gilt, bei der die Groß-/Kleinschreibung beachtet wird. Auf den Testservern wurde in der Regel die ANSI/ISO-Codepage 1252 verwendet.  
  
 Vielen Codebeispielen gehen Unicode-Zeichenfolgenkonstanten mit dem Buchstaben **N** voran. Ohne das **N**-Präfix wird die Zeichenfolge in die Standardcodepage der Datenbank konvertiert. Diese Standardcodepage erkennt möglicherweise bestimmte Zeichen nicht.  
  
## <a name="applies-to-references"></a>„Applies to“-Verweise  
 Der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Verweis enthält Artikel im Zusammenhang mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] und [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]. Am oberen Rand jedes Artikels befindet sich ein Abschnitt, der angibt, welche Produkte den Betreff des Artikels unterstützen. Wenn ein Produkt fehlt, ist das im Artikel beschriebene Feature in diesem Produkt nicht verfügbar. Beispielsweise wurden Verfügbarkeitsgruppen in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] eingeführt. Im Artikel **CREATE AVAILABILITY GROUP** wird darauf hingewiesen, dass er sich auf **SQL Server (SQL Server 2012 bis zur aktuellen Version)** bezieht, da er sich nicht auf [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] oder [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] bezieht.  
  
 In einigen Fällen kann der allgemeine Gegenstand eines Artikels in einem Produkt verwendet werden, aber es werden nicht alle Argumente unterstützt. Beispielsweise wurden Benutzer für eigenständige Datenbank in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] eingeführt. Die Anweisung **CREATE USER** kann in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Produkt verwendet werden, die Syntax **WITH PASSWORD** kann jedoch nicht mit älteren Versionen verwendet werden. In diesem Fall werden zusätzliche **Applies to**-Abschnitte in den Beschreibungen der entsprechenden Arguments in den Text des Artikels eingefügt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Transact-SQL-Referenz &#40;Datenbankmodul&#41;](../../t-sql/transact-sql-reference-database-engine.md)  
  
  


