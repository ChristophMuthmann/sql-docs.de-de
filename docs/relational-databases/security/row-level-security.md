---
title: Sicherheit auf Zeilenebene | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 03/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- access control predicates
- row level security
- security [SQL Server], predicate based access control
- row level security described
- predicate based security
ms.assetid: 7221fa4e-ca4a-4d5c-9f93-1b8a4af7b9e8
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: d9a995f7d29fe91e14affa9266a9bce73acc9010
ms.openlocfilehash: 8a5a44c3da9c34cf3bc64b632ce8cb8f86ff53e9
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="row-level-security"></a>Sicherheit auf Zeilenebene
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  ![Grafik zur Sicherheit auf Zeilenebene](../../relational-databases/security/media/row-level-security-graphic.png "Row level security graphic")  
  
 Mithilfe der Sicherheit auf Zeilenbene können Kunden den Zugriff auf die Zeilen in einer Datenbanktabelle auf Grundlage der Merkmale des Benutzers steuern, der eine Abfrage ausführt (z. B. Gruppenmitgliedschaft oder Ausführungskontext).  
  
 Eine zeilenbasierte Sicherheit vereinfacht den Entwurf und die Sicherheitscodierung in Ihrer Anwendung. Mit RLS können Sie Einschränkungen in den Datenzeilenzugriff implementieren. Dazu können Sie beispielsweise sicherstellen, dass Mitarbeiter nur auf die Datenzeilen zugreifen können, die für ihre Abteilung relevant sind oder Sie können den Datenzugriff eines Kunden auf die Daten beschränken, die nur für sein Unternehmen relevant sind.  
  
 Die Datenbeschränkungszugriffslogik befindet sich auf der Datenbankebene, statt fern der Daten auf einer anderen Anwendungsebene. Das Datenbanksystem wendet die Zugriffsbeschränkungen bei jedem Zugriffsversuch auf Daten aus einer beliebigen Ebene an. Dadurch wird Ihr Sicherheitssystem zuverlässiger und robuster, indem die Oberfläche Ihres Sicherheitssystems verringert wird.  
  
 Implementieren Sie RLS, indem Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung [CREATE SECURITY POLICY](../../t-sql/statements/create-security-policy-transact-sql.md) und Prädikate verwenden, die als [Inline-Tabellenwertfunktionen](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md) erstellt werden.  
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] , ([hier beziehen](http://azure.micosoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).  
  

##  <a name="Description"></a> Beschreibung  
 RLS unterstützt zwei Arten von Sicherheitsprädikaten.  
  
-   FILTER-Prädikate filtern automatisch die Zeilen, die für Lesevorgänge (SELECT, UPDATE und DELETE) zur Verfügung stehen.  
  
-   BLOCK-Prädikate blockieren explizit Schreibvorgänge (AFTER INSERT, AFTER UPDATE, BEFORE UPDATE, BEFORE DELETE), die gegen das Prädikat verstoßen.  
  
 Der Zugriff auf Daten auf Zeilenebene in einer Tabelle wird durch ein Sicherheitsprädikat beschränkt, das als Inline-Tabellenwertfunktion definiert ist. Die Funktion wird dann aufgerufen und durch eine Sicherheitsrichtlinie erzwungen. Für FILTER-Prädikate gilt: Es gibt keinen Hinweis für die Anwendung, dass Zeilen aus dem Resultset gefiltert wurden. Wenn alle Zeilen gefiltert werden, wird ein Nullsatz zurückgegeben. Für BLOCK-Prädikate gilt: Alle Vorgänge, die gegen das Prädikat verstoßen, misslingen mit einem Fehler.  
  
 Filterprädikate werden beim Lesen von Daten aus der Basistabelle angewendet. Dies betrifft alle GET-Vorgänge: **AUSWÄHLEN** **LÖSCHEN** (d.h., der Benutzer kann keine Zeilen löschen, die gefiltert werden), und **UPDATE** (d.h., der Benutzer kann keine Zeilen aktualisieren, die gefiltert werden, obwohl es möglich ist, Zeilen so zu aktualisieren, dass sie anschließend gefiltert werden). BLOCK-Prädikate betreffen alle Schreibvorgänge.  
  
-   Die Prädikate AFTER INSERT und AFTER UPDATE können Benutzer am Ändern von Zeilen in Werte hindern, die gegen das Prädikat verstoßen.  
  
-   Prädikate des Typs BEFORE UPDATE können Benutzer am Ändern von Zeilen in Werte hindern, die derzeit gegen das Prädikat verstoßen.  
  
-   Prädikate des Typs BEFORE DELETE können Löschvorgänge blockieren.  
  
 FILTER- und BLOCK-Prädikate und Sicherheitsrichtlinien weisen folgendes Verhalten auf:  
  
-   Sie können eine Prädikatfunktion definieren, die mit einer anderen Tabelle verknüpft wird und/oder eine Funktion aufruft. Wenn die Sicherheitsrichtlinie mit `SCHEMABINDING = ON`erstellt wird, ist die Verknüpfung oder Funktion über die Abfrage zugänglich und funktioniert wie erwartet, ohne zusätzliche Berechtigungsüberprüfungen durchführen zu müssen. Wenn die Sicherheitsrichtlinie mit `SCHEMABINDING = OFF`erstellt wird, benötigen die Benutzer zum Abfragen der Zieltabelle **SELECT** - oder **EXECUTE** -Berechtigungen für diese zusätzlichen Tabellen und Funktionen.
  
-   Sie können eine Abfrage auf eine Tabelle anwenden, für die ein Sicherheitsprädikat zwar definiert, jedoch deaktiviert ist. Alle Zeilen, die gefiltert oder blockiert worden wären, sind nicht betroffen.  
  
-   Wenn der Benutzer „dbo“, ein Mitglied der **db_owner** -Rolle oder der Tabellenbesitzer eine Tabelle abfragt, für die eine Sicherheitsrichtlinie definiert und aktiviert ist, werden die Zeilen gemäß Definition durch die Sicherheitsrichtlinie gefiltert oder blockiert.  
  
-   Versuche, das Schema einer Tabelle zu ändern, die durch eine Sicherheitsrichtlinie an ein Schema gebunden ist, führen zu einem Fehler. Allerdings können vom Prädikat nicht referenzierte Spalten geändert werden.  
  
-   Versuche, einer Tabelle ein Prädikat hinzuzufügen, für die bereits eines für den angegebenen Vorgang definiert ist (unabhängig davon, ob aktiviert oder deaktiviert), führen zu einem Fehler.  
  
-   Für an ein Schema gebundene Sicherheitsrichtlinien gilt, dass Versuche, eine als Prädikat für eine Tabelle verwendete Funktion innerhalb einer Sicherheitsrichtlinie zu ändern, zu einem Fehler führen.  
  
-   Das Definieren mehrerer aktiver Sicherheitsrichtlinien, die nicht überlappende Prädikate enthalten, kann erfolgreich ausgeführt werden.  
  
 FILTER-Prädikate weisen folgendes Verhalten auf:  
  
-   Definieren Sie eine Sicherheitsrichtlinie, die die Zeilen einer Tabelle filtert. Der Anwendung ist nicht bekannt, dass Zeilen nach **SELECT**-, **UPDATE**- und **DELETE** -Vorgängen gefiltert wurden, einschließlich Situationen, in denen alle Zeilen gefiltert wurden. Die Anwendung kann eine beliebige Anzahl von Zeilen mit **INSERT** einfügen, unabhängig davon, ob sie bei einem anderen Vorgang gefiltert werden.  
  
 BLOCK-Prädikate weisen folgendes Verhalten auf:  
  
-   BLOCK-Prädikate für UPDATE werden in getrennte Vorgänge für BEFORE und AFTER unterteilt. Deshalb ist es beispielsweise nicht möglich zu blockieren, dass Benutzer eine Zeile in einen Wert ändern, der höher als der aktuelle ist. Wenn diese Art von Logik erforderlich ist, müssen Sie Trigger mit den Zwischentabellen des Typs DELETED und INSERTED verwenden, um gemeinsam auf die alten und neuen Werte zu verweisen.  
  
-   Der Optimierer überprüft kein BLOCK-Prädikat des Typs AFTER UPDATE, wenn keine der von der Prädikatfunktion verwendeten Spalten geändert wurde. Beispiel: Alice soll nicht in der Lage sein, ein Gehalt in einen Wert größer als 100.000 zu ändern. Sie soll aber die Adresse eines Mitarbeiters ändern können, dessen Gehalt bereits größer als 100.000 ist (und deshalb bereits gegen das Prädikat verstößt).  
  
-   An den APIs für Massenvorgänge, einschließlich BULK INSERT, sind keine Änderungen erfolgt. Dies bedeutet, dass BLOCK-Prädikate des Typs AFTER INSERT für Masseneinfügevorgänge genauso wie für herkömmliche Einfügevorgänge gelten.  
  
  
##  <a name="UseCases"></a> Einsatzgebiete  
 Hier sind Entwurfsbeispiele dazu, wie RLS verwendet werden kann:  
  
-   Ein Krankenhaus kann eine Sicherheitsrichtlinie erstellen, mit dem Krankenschwestern nur Datenzeilen für ihre eigenen Patienten anzeigen können.  
  
-   Eine Bank kann eine Richtlinie erstellen, um den Zugriff auf die Zeilen von Finanzdaten anhand der Geschäftsabteilung des Mitarbeiters oder anhand des Mitarbeiter-Rolle innerhalb des Unternehmens zu beschränken.  
  
-   Eine Anwendung mit mehreren Mandanten kann eine Richtlinie zum Erzwingen einer logischen Trennung der einzelnen Datenzeilen der Mandanten aus jeder anderen Mandanten-Zeile erstellen. Effizienzen werden durch den Datenspeicher für viele Mandanten in einer einzelnen Tabelle erreicht. Natürlich kann jeder Mandant nur die eigenen Datenzeilen anzeigen.  
  
 RLS-Filterprädikate sind funktional äquivalent zum Anhängen einer **WHERE** -Klausel. Bei dem Prädikat kann es sich um komplexe Geschäftsabläufe handeln oder die Klausel kann so einfach sein wie das `WHERE TenantId = 42`.  
  
 Formaler ausgedrückt führt RLS eine prädikatbasierte Zugriffssteuerung ein. Es bietet eine flexible, zentrale und prädikatbasierte Bewertung, die Metadaten oder andere Kriterien berücksichtigt, die der Administrator nach Bedarf bestimmt. Das Prädikat wird als Kriterium verwendet, um zu bestimmen, ob der Benutzer den entsprechenden Zugriff auf die Daten anhand von Benutzerattributen verfügt. Die bezeichnungsbasierte Zugriffssteuerung kann mithilfe der prädikatbasierten Zugriffssteuerung implementiert werden.  
  
  
##  <a name="Permissions"></a> Berechtigungen  
 Für das Erstellen, Ändern oder Löschen von Sicherheitsrichtlinien ist die **ALTER ANY SECURITY POLICY** -Berechtigung erforderlich. Für das Erstellen oder Löschen einer Sicherheitsrichtlinie ist bei dem Schema die **ALTER** -Berechtigung erforderlich.  
  
 Darüber hinaus sind die folgenden Berechtigungen für jedes hinzugefügte Prädikat erforderlich:  
  
-   **SELECT** - und **REFERENCES** -Berechtigungen für die Funktion, die als Prädikat verwendet wird.  
  
-   **REFERENCES** -Berechtigung für die Zieltabelle, die an die Richtlinie gebunden wird.  
  
-   **REFERENCES** -Berechtigung für jede Spalte in der Zieltabelle, die als Argument verwendet wird.  
  
 Sicherheitsrichtlinien gelten für alle Benutzer, einschließlich der Dbo-Benutzer in der Datenbank. Dbo-Benutzer können Sicherheitsrichtlinien ändern oder löschen, ihre Änderungen an Sicherheitsrichtlinien können jedoch überwacht werden. Wenn Benutzer mit hohen Berechtigungen (z. B. sysadmin oder db_owner) alle Zeilen sehen müssen, um Probleme mit Daten zu beheben oder Daten zu überprüfen, muss die Sicherheitsrichtlinie entsprechend geschrieben werden.  
  
 Wenn eine Sicherheitsrichtlinie mit `SCHEMABINDING = OFF`erstellt wird, benötigen die Benutzer zum Abfragen der Zieltabelle die  **SELECT** - oder **EXECUTE** -Berechtigung für die Prädikatfunktion und alle weiteren Tabellen, Sichten oder Funktionen, die innerhalb der Prädikatfunktion verwendet werden. Wenn eine Sicherheitsrichtlinie mit `SCHEMABINDING = ON` erstellt wird (Standard), werden diese Berechtigungsprüfungen umgangen, wenn Benutzer die Zieltabelle abfragen.  
  
  
##  <a name="Best"></a> Bewährte Methoden  
  
-   Es wird dringend empfohlen, ein separates Schema für die RLS-Objekte zu erstellen (Prädikatfunktion und Sicherheitsrichtlinie).  
  
-   Die **ALTER ANY SECURITY POLICY** -Berechtigung richtet sich an hoch privilegierte Benutzer (z. B. ein Sicherheitsrichtlinienmanager). Die Sicherheitsrichtlinienmanager erfordert keine **SELECT** -Berechtigung für die Tabellen, die sie schützen.  
  
-   Vermeiden Sie Konvertierungen in Prädikatfunktionen, um potenzielle Laufzeitfehler zu vermeiden.  
  
-   Vermeiden Sie nach Möglichkeit Rekursionen in Prädikatfunktionen, um Leistungseinbußen zu vermeiden. Der Abfrageoptimierer versucht die direkten Rekursionen zu erkennen, gewährleistet jedoch nicht, indirekte Rekursionen zu finden (d. h. wenn eine zweite Funktion die Prädikatfunktion aufruft).  
  
-   Vermeiden Sie übermäßige Tabellenverknüpfungen Prädikatfunktionen, um die Leistung zu maximieren.  
  
 Vermeiden Sie Prädikatlogik, die von sitzungsspezifischen [SET](../../t-sql/statements/set-statements-transact-sql.md)-Optionen abhängt: Wenngleich ihre Verwendung in der Praxis eher unwahrscheinlich ist, können Prädikatfunktionen, deren Logik von bestimmten sitzungsspezifischen **SET** -Optionen abhängt, Informationen preisgeben, wenn Benutzer in der Lage sind, beliebige Abfragen auszuführen. Beispiel: Eine Prädikatfunktion, die eine Zeichenfolge implizit in **datetime** konvertiert, kann unterschiedliche Zeilen basierend auf der Option **SET DATEFORMAT** für die aktuelle Sitzung filtern. Im Allgemeinen sollten Prädikatfunktionen die folgenden Regeln einhalten:  
  
-   Prädikatfunktionen dürfen Zeichenfolgen nicht implizit in **date**, **smalldatetime**, **datetime**, **datetime2** oder **datetimeoffset** bzw. umgekehrt konvertieren, da diese Konvertierungen von den Optionen [SET DATEFORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md) und [SET LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md) beeinflusst werden. Verwenden Sie stattdessen die **CONVERT**-Funktion, und geben Sie den „style“-Parameter explizit an.  
  
-   Prädikatfunktionen dürfen nicht vom Wert des ersten Tages der Woche abhängig sein, da dieser Wert von der Option [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md) beeinflusst wird.  
  
-   Prädikatfunktionen dürfen nicht von arithmetischen oder Aggregationsausdrücken abhängig sein, die bei einem Fehler (wie z. B. Überlauf oder Division durch null) **NULL** zurückgeben, da dieses Verhalten von den Optionen [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md), [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md) und [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md) beeinflusst wird.  
  
-   Prädikatfunktionen dürfen verkettete Zeichenfolgen nicht mit **NULL** vergleichen, da dieses Verhalten von der Option [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md) beeinflusst wird.  
   
  
##  <a name="SecNote"></a> Sicherheitshinweis: Seitenkanalangriffe  
 **Schädlicher Manager für Sicherheitsrichtlinien:** Es ist wichtig zu beachten, dass ein schädlicher Manager für Sicherheitsrichtlinien mit ausreichenden Berechtigungen zum Erstellen einer Sicherheitsrichtlinie für eine vertrauliche Spalte und der Berechtigung zum Erstellen oder Ändern von Inline-Tabellenwertfunktionen mit einem anderen Benutzer zusammenwirken kann, der SELECT-Berechtigungen für eine Tabelle hat. Es kann dann eine Datenexfiltration erfolgen, indem schädliche Inline-Tabellenwertfunktionen mit dem Zweck erstellt werden, Seitenkanalangriffe zum Ableiten von Daten zu verwenden. Solche Angriffe bedürfen der Absprache (oder übermäßig erteilte Berechtigungen bei einem schädlichen Benutzer), und sie erfordern wahrscheinlich mehrere Iterationen zum Ändern der Richtlinie (erfordert die Berechtigung zum Entfernen des Prädikats, um die Schemabindung aufzuheben), zum Ändern der Inline-Tabellenwertfunktionen und zum wiederholen Ausführen ausgewählter Anweisungen für die Zieltabelle. Es wird dringend empfohlen, Berechtigungen nach Bedarf zu beschränken, und sie nach verdächtigen Aktivitäten wie dem konstanten Ändern von Richtlinien und Inline-Tabellenwertfunktionen im Zusammenhang mit der zeilenbasierter Sicherheit zu überwachen.  
  
 **Sorgfältig erstellte Abfragen:** Es ist möglich, die Offenlegung von Informationen durch die Verwendung sorgfältig erstellter Abfragen zu verursachen. Beispiel: `SELECT 1/(SALARY-100000) FROM PAYROLL WHERE NAME='John Doe'` würde einen schädlichen Benutzer wissen lassen, dass das Gehalt von John Doe 100.000 USD beträgt. Auch wenn ein Sicherheitsprädikat eingerichtet ist, um zu verhindern, dass ein schädlicher Benutzer die Gehälter anderer Personen direkt abfragen kann, kann der Benutzer bestimmen, wann die Abfrage eine Division-durch-Null-Ausnahme zurückgibt.  
   
  
##  <a name="Limitations"></a> Featureübergreifende Kompatibilität  
 Im Allgemeinen funktioniert Sicherheit auf Zeilenebene featureübergreifend wie erwartet. Es gibt jedoch einige Ausnahmen. In diesem Abschnitt finden Sie verschiedene Hinweise und Vorsichtsmaßnahmen bei Verwenden von Sicherheit auf Zeilenebene mit bestimmten anderen Features von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **DBCC SHOW_STATISTICS** meldet eine Statistik zu ungefilterten Daten und kann somit zur Offenlegung von Informationen führen, die ansonsten durch eine Sicherheitsrichtlinie geschützt sind. Aus diesem Grund muss der Benutzer zum Anzeigen des Statistikobjekts für eine Tabelle mit geltender Richtlinie zur Sicherheit auf Zeilenebene der Besitzer der Tabelle oder Mitglied der festen Serverrolle „sysadmin“, der festen Datenbankrolle „db_owner“ oder der festen Datenbankrolle „db_ddladmin“ sein.  
  
-   **Filestream** RLS ist nicht kompatibel mit Filestream.  
  
-   **Polybase** RLS ist nicht kompatibel mit Polybase.  
  
-   **Speicheroptimierte Tabellen**Die Inline-Tabellenwertfunktion, die für ein Sicherheitsprädikat für eine speicheroptimierte Tabelle verwendet wird, muss mit der Option `WITH NATIVE_COMPILATION` definiert werden. Bei dieser Option werden von speicheroptimierten Tabellen nicht unterstützte Sprachfeatures gesperrt, und zur Erstellungszeit wird der entsprechende Fehler ausgelöst. Weitere Informationen finden Sie im Abschnitt **Sicherheit auf Zeilenebene** in [Einführung in speicheroptimierte Tabellen](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md).  
  
-   **Indizierte Sichten** Im allgemeinen können Sicherheitsrichtlinien basierend auf Sichten erstellt werden. Sichten können basierend auf Tabellen erstellt werden, die durch Sicherheitsrichtlinien gebunden sind. Allerdings können indizierte Sichten nicht basierend auf Tabellen erstellt werden, für die eine Sicherheitsrichtlinie gilt, da die Richtlinie bei Zeilensuchvorgängen über den Index umgangen würde.  
  
-   **Change Data Capture** Change Data Capture kann ganze Zeilen preisgeben, die für Mitglieder von **db_owner** oder Benutzer gefiltert werden sollen, die Mitglieder der „Gating-Rolle“ sind, die angegeben wird, wenn CDC für eine Tabelle aktiviert ist (Hinweis: Sie können diese Einstellung explizit auf **NULL** festlegen, damit alle Benutzer auf die Änderungsdaten zugreifen können). Im Endeffekt können **db_owner** und Mitglieder dieser Gating-Rolle alle Datenänderungen für eine Tabelle anzeigen, auch wenn für die Tabelle eine Sicherheitsrichtlinie gilt.  
  
-   **Änderungsnachverfolgung** Eine Änderungsnachverfolgung kann zum Preisgeben des Primärschlüssels von Zeilen führen, die für Benutzer mit den Berechtigungen **SELECT** und **VIEW CHANGE TRACKING** gefiltert werden sollen. Tatsächliche Datenwerte werden nicht preisgegeben, sondern nur dass Spalte A für die Spalte mit dem Primärschlüssel B aktualisiert/eingefügt/gelöscht wurde. Dies ist problematisch, wenn der primäre Schlüssel ein vertrauliches Element enthält, z. B. eine US-Sozialversicherungsnummer. In der Praxis ist **CHANGETABLE** jedoch fast immer mit der ursprünglichen Tabelle verknüpft, um die neuesten Daten abzurufen.  
  
-   **Volltextsuche** Eine Leistungsverschlechterung wird für Abfragen erwartet, die die folgenden Volltextsuch- und semantischen Suchfunktionen verwenden. Der Grund ist ein zusätzlicher Joinvorgang, der für das Aktivieren der Sicherheit auf Zeilenebene und Vermeiden der Preisgabe der Primärschlüssel von Zeilen erfolgt, die gefiltert werden sollen: **CONTAINSTABLE**, **FREETEXTTABLE**, semantickeyphrasetable, semanticsimilaritydetailstable, semanticsimilaritytable.  
  
-   **Columnstore-Indizes** RLS ist kompatibel mit sowohl gruppierten als auch nicht gruppierten Columnstore-Indizes. Da für die Sicherheit auf Zeilenebene jedoch eine Funktion angewendet wird, ist es möglich, dass der Optimierer den Abfrageplan so ändert, dass nicht der Batchmodus verwendet wird.  
  
-   **Partitionierte Sichten** BLOCK-Prädikate können nicht für partitionierte Sichten definiert werden, und partitionierte Sichten können nicht basierend auf Tabellen erstellt werden, die BLOCK-Prädikate verwenden. FILTER-Prädikate sind kompatibel mit partitionierten Sichten.  
  
-   **Temporale Tabellen** sind mit RLS kompatibel. Sicherheitsprädikate für die aktuelle Tabelle werden jedoch nicht automatisch in die Verlaufstabelle repliziert. Um eine Sicherheitsrichtlinie auf die aktuellen und Verlaufstabellen anzuwenden, müssen Sie für jede Tabelle ein Sicherheitsprädikat einzeln hinzufügen.  
  
  
##  <a name="CodeExamples"></a> Beispiele  
  
###  <a name="Typical"></a> A. Szenario für Benutzer, die sich bei der Datenbank authentifizieren  
 In diesem kurzen Beispiel werden drei Benutzer erstellt, es wird eine Tabelle mit 6 Zeilen erstellt, und eine Inline-Tabellenwertfunktion sowie eine Sicherheitsrichtlinie für die Tabelle wird erstellt. Im Beispiel wird gezeigt, wie ausgewählte Anweisungen für verschiedene Benutzer gefiltert werden.  
  
 Erstellen Sie drei Benutzerkonten, anhand derer unterschiedliche Zugriffsmöglichkeiten vorgeführt werden.  
  
```sql  
CREATE USER Manager WITHOUT LOGIN;  
CREATE USER Sales1 WITHOUT LOGIN;  
CREATE USER Sales2 WITHOUT LOGIN;  
```  
  
 Erstellen Sie eine einfache Tabelle zum Speichern von Daten.  
  
```  
CREATE TABLE Sales  
    (  
    OrderID int,  
    SalesRep sysname,  
    Product varchar(10),  
    Qty int  
    );  
```  
  
 Füllen Sie die Tabelle mit 6 Datenzeilen, die drei Bestellungen für jeden Vertriebsmitarbeiter enthalten.  
  
```  
INSERT Sales VALUES   
(1, 'Sales1', 'Valve', 5),   
(2, 'Sales1', 'Wheel', 2),   
(3, 'Sales1', 'Valve', 4),  
(4, 'Sales2', 'Bracket', 2),   
(5, 'Sales2', 'Wheel', 5),   
(6, 'Sales2', 'Seat', 5);  
-- View the 6 rows in the table  
SELECT * FROM Sales;  
```  
  
 Gewähren Sie den Benutzern Lesezugriff auf die Tabelle.  
  
```  
GRANT SELECT ON Sales TO Manager;  
GRANT SELECT ON Sales TO Sales1;  
GRANT SELECT ON Sales TO Sales2;  
```  
  
 Erstellen ein neues Schema, und eine Inline-Tabellenwertfunktion. Die Funktion gibt 1 zurück, wenn eine Zeile in der Spalte SalesRep dem Benutzer entspricht, der die Abfrage ausführt (`@SalesRep = USER_NAME()`) oder wenn der Benutzer, der die Abfrage ausführt, der Manager-Benutzer ist (`USER_NAME() = 'Manager'`).  
  
```  
CREATE SCHEMA Security;  
GO  
  
CREATE FUNCTION Security.fn_securitypredicate(@SalesRep AS sysname)  
    RETURNS TABLE  
WITH SCHEMABINDING  
AS  
    RETURN SELECT 1 AS fn_securitypredicate_result   
WHERE @SalesRep = USER_NAME() OR USER_NAME() = 'Manager';  
```  
  
 Erstellen Sie eine Sicherheitsrichtlinie, die die Funktion als Filterprädikat hinzufügt. Der Status muss auf ON festgelegt werden, um die Richtlinie zu aktivieren.  
  
```  
CREATE SECURITY POLICY SalesFilter  
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesRep)   
ON dbo.Sales  
WITH (STATE = ON);  
```  
  
 Testen Sie jetzt das Filterungsprädikat, indem Sie sie als jeweiliger Benutzer aus der Sales-Tabelle auswählen.  
  
```  
EXECUTE AS USER = 'Sales1';  
SELECT * FROM Sales;   
REVERT;  
  
EXECUTE AS USER = 'Sales2';  
SELECT * FROM Sales;   
REVERT;  
  
EXECUTE AS USER = 'Manager';  
SELECT * FROM Sales;   
REVERT;  
```  
  
 Dem Manager sollten alle 6 Zeilen angezeigt werden. Den Benutzern Sales1 und Sales2 sollten nur ihre eigenen Verkäufe angezeigt werden.  
  
 Ändern Sie die Sicherheitsrichtlinie, um die Richtlinie zu deaktivieren.  
  
```  
ALTER SECURITY POLICY SalesFilter  
WITH (STATE = OFF);  
```  
  
 Jetzt werden den Benutzern Sales1 und Sales2 alle 6 Zeilen angezeigt.  
  
  
###  <a name="MidTier"></a> B. Szenario für Benutzer, die sich über eine Middle-Tier Application mit der Datenbank verbinden  
 Dieses Beispiel zeigt, wie eine Anwendung der mittleren Schicht eine Verbindungsfilterung implementieren kann, bei der Anwendungsbenutzer (oder Mandanten) den gleichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benutzer (die Anwendung) gemeinsam verwenden. Die Anwendung legt nach dem Verbinden mit der Datenbank die aktuelle Anwendungsbenutzer-ID in [SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md) fest. Dann sorgen Sicherheitsrichtlinien dafür, dass Zeilen transparent herausgefiltert werden, die für diese ID nicht sichtbar sein sollen. Außerdem wird der Benutzer am Einfügen von Zeilen für die falsche Benutzer-ID gehindert. Es sind keine weiteren App-Änderungen erforderlich.  
  
 Erstellen Sie eine einfache Tabelle zum Speichern von Daten.  
  
```  
CREATE TABLE Sales (  
    OrderId int,  
    AppUserId int,  
    Product varchar(10),  
    Qty int  
);  
```  
  
 Füllen Sie die Tabelle mit 6 Datenzeilen, die drei Bestellungen für jeden Vertriebsmitarbeiter enthalten.  
  
```  
INSERT Sales VALUES   
    (1, 1, 'Valve', 5),   
    (2, 1, 'Wheel', 2),   
    (3, 1, 'Valve', 4),  
    (4, 2, 'Bracket', 2),   
    (5, 2, 'Wheel', 5),   
    (6, 2, 'Seat', 5);  
```  
  
 Erstellen Sie ein Benutzerkonto mit geringen Berechtigungen, das die Anwendung zum Herstellen der Verbindung verwendet.  
  
```  
-- Without login only for demo  
CREATE USER AppUser WITHOUT LOGIN;   
GRANT SELECT, INSERT, UPDATE, DELETE ON Sales TO AppUser;  
  
-- Never allow updates on this column  
DENY UPDATE ON Sales(AppUserId) TO AppUser;  
```  
  
 Erstellen Sie ein neues Schema und eine Prädikatfunktion, die die Anwendungsbenutzer-ID verwendet, die in **SESSION_CONTEXT** zum Filtern von Zeilen gespeichert ist.  
  
```  
CREATE SCHEMA Security;  
GO  
  
CREATE FUNCTION Security.fn_securitypredicate(@AppUserId int)  
    RETURNS TABLE  
    WITH SCHEMABINDING  
AS  
    RETURN SELECT 1 AS fn_securitypredicate_result  
    WHERE  
        DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('AppUser')    
        AND CAST(SESSION_CONTEXT(N'UserId') AS int) = @AppUserId;   
GO  
```  
  
 Erstellen Sie eine Sicherheitsrichtlinie, die diese Funktion als FILTER-Prädikat und BLOCK-Prädikat für `Sales`hinzufügt. Das BLOCK-Prädikat benötigt nur **AFTER INSERT**, da **BEFORE UPDATE** und **BEFORE DELETE** bereits gefiltert sind und **AFTER UPDATE** unnötig ist, da die Spalte `AppUserId` aufgrund von zuvor festgelegten Spaltenberechtigungen nicht in andere Werte geändert werden kann.  
  
```  
CREATE SECURITY POLICY Security.SalesFilter  
    ADD FILTER PREDICATE Security.fn_securitypredicate(AppUserId)   
        ON dbo.Sales,  
    ADD BLOCK PREDICATE Security.fn_securitypredicate(AppUserId)   
        ON dbo.Sales AFTER INSERT   
    WITH (STATE = ON);  
```  
  
 Nun können wir die Verbindungsfilterung durch Auswahl der Tabelle `Sales` simulieren, nachdem in **SESSION_CONTEXT**andere Benutzer-IDs festgelegt wurden. In der Praxis ist die Anwendung nach Öffnen einer Verbindung zuständig für das Festlegen der aktuellen Benutzer-ID in **SESSION_CONTEXT** .  
  
```  
EXECUTE AS USER = 'AppUser';  
EXEC sp_set_session_context @key=N'UserId', @value=1;  
SELECT * FROM Sales;  
GO  
  
--  Note: @read_only prevents the value from changing again   
--  until the connection is closed (returned to the connection pool)  
EXEC sp_set_session_context @key=N'UserId', @value=2, @read_only=1;   
  
SELECT * FROM Sales;  
GO  
  
INSERT INTO Sales VALUES (7, 1, 'Seat', 12); -- error: blocked from inserting row for the wrong user ID  
GO  
  
REVERT;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [ALTER SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-security-policy-transact-sql.md)   
 [DROP SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)   
 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [sys.security_predicates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)   
 [Erstellen benutzerdefinierter Funktionen &#40;Datenbankmodul&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)  
  
  

