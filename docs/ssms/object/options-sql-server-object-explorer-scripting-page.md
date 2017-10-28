---
title: "Optionen (SQL Server-Objekt-Explorer – Seite „Skripterstellung“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.ObjectExplorerScripting
- VS.ToolsOptionsPages.Sql_Server_Object_Explorer.ObjectExplorerScripting
ms.assetid: 6105aec9-1b72-4cb2-bd24-fc35f6d95240
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 3f12671ace99d5fefc199c7b1c2db31e5b3cfade
ms.openlocfilehash: bbe33b53b8dcb416e808f7756fea7da465e61105
ms.contentlocale: de-de
ms.lasthandoff: 08/08/2017

---
# <a name="options-sql-server-object-explorer---scripting-page"></a>Optionen (SQL Server-Objekt-Explorer – Seite „Skripterstellung“)
Auf dieser Seite können Sie Skripterstellungsoptionen festlegen, die auf die folgenden Befehle in Objektkontextmenüs im **Objekt-Explorer**angewendet werden:  
  
-   **Bearbeiten**-Befehle für Benutzertabellen und Sichten.  
  
-   **Skript für <object> erstellen als**-Befehle für vom Benutzer erstellte Objekte.  
  
-   Befehl **Ändern** für vom Benutzer erstellte Objekte.  
  
-   Auf dieser Seite werden zudem die Standardwerte der Skripterstellungsoptionen für den **Assistenten zum Generieren von SQL Server-Skripts**festgelegt.  
  
## <a name="remarks"></a>Hinweise  
Die Befehle **Bearbeiten** und **Ändern** führen möglicherweise zu Ergebnissen, die sich vom Befehl **Skript für <object> erstellen als** für die gleiche Optionseinstellung unterscheiden. Die Befehle **Bearbeiten** und **Ändern** sind für das Ändern von Objekten in der aktuellen Datenbank während einer Abfrage-Editor-Sitzung vorgesehen. Der Befehl **Skript für <object> erstellen als** ist zum Generieren eines Skripts vorgesehen, sodass es später zum Erstellen von Objekten verwendet werden kann.  
  
## <a name="options"></a>enthalten  
Geben Sie Skriptoptionen an, indem Sie eine Auswahl aus den verfügbaren Einstellungen in der Liste rechts neben den einzelnen Optionen treffen.  
  
### <a name="general-scripting-options"></a>Allgemeine Skripterstellungsoptionen  
**Einzelne Anweisungen begrenzen**  
Trennt die einzelnen [!INCLUDE[tsql](../../includes/tsql_md.md)] -Anweisungen mithilfe eines Batchtrennzeichens voneinander ab. Wenn Sie das Standardbatchtrennzeichen für **Abfrage-Editor**ändern möchten, wählen Sie **Extras**/**Optionen**/**Abfrageausführung**/**SQL Server**/**Allgemein**/**Batchtrennzeichen**aus. Der Standardwert lautet False. Weitere Informationen finden Sie unter [GO (Transact-SQL)](https://msdn.microsoft.com/b2ca6791-3a07-4209-ba8e-2248a92dd738).  
  
**Beschreibende Header einschließen**  
Fügt dem Skript beschreibende Kommentare hinzu, indem das Skript in Abschnitte für die einzelnen Objekte aufgeteilt wird. Der Standardwert lautet "True". Weitere Informationen finden Sie unter [/*...*/ (Kommentar) (Transact-SQL)](https://msdn.microsoft.com/4d9ab1b2-4bbb-4c16-beb1-cafc1af7417c).  
  
**Einschließen der Aktivierung von Vardecimal-Komprimierung**  
Schließt die vardecimal-Speicheroptionen ein. Der Standardwert lautet False. Weitere Informationen finden Sie unter [sp_db_vardecimal_storage_format (Transact-SQL)](https://msdn.microsoft.com/9920b2f7-b802-4003-913c-978c17ae4542).  
  
**Skript für Änderungsnachverfolgung erstellen**  
Schließt Nachverfolgungsinformationen für Änderungen im Skript ein.  
  
**Skripterstellung für Volltextkataloge**  
Schließt ein Skript für Volltextkataloge ein. Der Standardwert lautet False. Weitere Informationen finden Sie unter [CREATE FULLTEXT CATALOG (Transact-SQL)](https://msdn.microsoft.com/d7a8bd93-e2d7-4a40-82ef-39069e65523b).  
  
**Skripterstellung für USE <database>**  
Fügt die USE DATABASE-Anweisung dem Skript hinzu, mit dem Datenbankobjekte im Kontext der aktuellen **Objekt-Explorer** -Datenbank erstellt werden. Wenn das Skript für die Verwendung in einer anderen Datenbank vorgesehen ist, wählen Sie False aus, um dies auszulassen. Der Standardwert lautet "True". Weitere Informationen finden Sie unter [USE (Transact-SQL)](https://msdn.microsoft.com/c05acac8-c063-4770-8e36-d7f71d500b10).  
  
### <a name="object-scripting-options"></a>Skripterstellungsoptionen für Objekte  

**Vorhandensein von Objekten überprüfen** Überprüfen Sie vor dem Löschen oder Ändern, ob ein Objekt mit dem angegebenen Namen vorhanden ist, bzw. vor dem Erstellen, ob noch kein Objekt mit dem angegebenen Namen vorhanden ist. Weitere Informationen finden Sie unter [IF... ELSE (Transact-SQL)](https://msdn.microsoft.com/676c881f-dee1-417a-bc51-55da62398e81) und [EXISTS (Transact-SQL)](https://msdn.microsoft.com/b6510a65-ac38-4296-a3d5-640db0c27631).

**Skript für abhängige Objekte generieren**  
Generiert ein Skript für zusätzliche Objekte, die erforderlich sind, wenn das Skript für das ausgewählte Objekt ausgeführt wird. Der Standardwert lautet False.  
  
**Schema für Objektnamen qualifizieren**  
Qualifiziert Objektnamen mit dem Objektschema. Der Standardwert lautet False. Weitere Informationen finden Sie unter [Erstellen eines Datenbankschemas](https://msdn.microsoft.com/ed2a5522-f4d2-4111-95a4-d3e1e5081739).  

**Optionen für die Skriptdatenkomprimierung** Schließt Datenkomprimierungsoptionen in das Skript ein. Der Standardwert lautet False.

**Skripterstellung für erweiterte Eigenschaften**  
Enthält erweiterte Eigenschaften im Skript, wenn das Objekt über erweiterte Eigenschaften verfügt. Der Standardwert lautet False. Weitere Informationen finden Sie unter [sp_addextendedproperty (Transact-SQL)](https://msdn.microsoft.com/565483ea-875b-4133-b327-d0006d2d7b4c).  
  
**Skriptbesitzer**  
Schließt den Besitzer im generierten Skript ein. Der Standardwert lautet False.  
  
**Skripterstellung für Berechtigungen**  
Schließt Berechtigungen für Datenbankobjekte im Skript ein. Der Standardwert lautet "True". Weitere Informationen finden Sie unter [Berechtigungen](https://msdn.microsoft.com/f28e3dea-24e6-4a81-877b-02ec4c7e36b9).  
  
### <a name="tableview-options"></a>Tabellen-/Sichtoptionen  
Die folgenden Optionen gelten nur für Skripts für Tabellen oder Sichten.  
  
**Benutzerdefinierte Datentypen in Basistypen konvertieren**  
Konvertiert benutzerdefinierte Datentypen in die Basistypen, aus denen sie erstellt wurden. Verwenden Sie True, wenn die benutzerdefinierten Datentypen der Quelldatenbank nicht in der Datenbank vorhanden sind, in der das Skript ausgeführt wird. Verwenden Sie False, um die benutzerdefinierten Datentypen beizubehalten. Der Standardwert lautet False. Weitere Informationen finden Sie unter [CREATE TYPE (Transact-SQL)](https://msdn.microsoft.com/2202236b-e09f-40a1-bbc7-b8cff7488905).  
  
**SET ANSI PADDING-Befehle generieren**  
Fügt die SET ANSI_PADDING-Anweisung vor und hinter jeder CREATE TABLE-Anweisung hinzu. Der Standardwert lautet "True". Weitere Informationen finden Sie unter [SET ANSI_PADDING (Transact-SQL)](https://msdn.microsoft.com/92bd29a3-9beb-410e-b7e0-7bc1dc1ae6d0).  
  
**Sortierung einschließen**  
Schließt eine Sortierung in die Spaltendefinition ein. Der Standardwert lautet "True". Weitere Informationen finden Sie unter [Collation and Unicode Support](https://msdn.microsoft.com/92d34f48-fa2b-47c5-89d3-a4c39b0f39eb).  
  
**IDENTITY-Eigenschaft einschließen**  
Schließt Definitionen für den IDENTITY-Ausgangswert und das IDENTITY-Inkrement ein. Der Standardwert lautet "True". Weitere Informationen finden Sie unter [IDENTITY (Eigenschaft) (Transact-SQL)](https://msdn.microsoft.com/8429134f-c821-4033-a07c-f782a48d501c).  
  
**Schema für Fremdschlüsselverweise qualifizieren**  
Fügt Tabellenverweisen für FOREIGN KEY-Einschränkungen den Schemanamen hinzu. Der Standardwert lautet "True".  
  
**Skripterstellung für gebundene Standardwerte und Regeln**  
Schließt die Aufrufe für die bindenden gespeicherten Prozeduren **sp_bindefault** und **sp_bindrule** ein. Der Standardwert lautet "True". Weitere Informationen finden Sie unter [sp_bindefault (Transact-SQL)](https://msdn.microsoft.com/3da70c10-68d0-4c16-94a5-9e84c4a520f6) und [sp_bindrule (Transact-SQL)](https://msdn.microsoft.com/2606073e-c52f-498d-a923-5026b9d97e67).  
  
**Skripterstellung für CHECK-Einschränkungen**  
Fügt dem Skript [CHECK-Einschränkungen](https://msdn.microsoft.com/637098af-2567-48f8-90f4-b41df059833e) hinzu. Der Standardwert lautet "True".  
  
**Skripterstellung für Standard**  
Schließt Spaltenstandardwerte in das Skript ein. Der Standardwert lautet False. Weitere Informationen finden Sie unter [CREATE DEFAULT (Transact-SQL&amp;)](https://msdn.microsoft.com/08475db4-7d90-486a-814c-01a99d783d41).  
  
**Skripterstellung für Dateigruppen**  
Gibt die Dateigruppe in der ON -Klausel für Tabellendefinitionen an. Der Standardwert lautet False. Weitere Informationen finden Sie unter [CREATE TABLE (Transact-SQL&amp;)](https://msdn.microsoft.com/1e068443-b9ea-486a-804f-ce7b6e048e8b).  
  
**Skripterstellung für Fremdschlüssel**  
Schließt [FOREIGN KEY-Einschränkungen](https://msdn.microsoft.com/31fbcc9f-2dc5-4bf9-aa50-ed70ec7b5bcd) in das Skript ein. Der Standardwert lautet False.  
  
**Skripterstellung für Volltextindizes**  
Schließt Volltextindizes in das Skript ein. Der Standardwert lautet False. Weitere Informationen finden Sie unter [CREATE FULLTEXT INDEX (Transact-SQL)](https://msdn.microsoft.com/8b80390f-5f8b-4e66-9bcc-cabd653c19fd).  
  
**Skripterstellung für Indizes**  
Schließt gruppierte Indizes, nicht gruppierte Indizes und XML-Indizes in das Skript ein. Der Standardwert lautet "True". Weitere Informationen finden Sie unter [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/d2297805-412b-47b5-aeeb-53388349a5b9).  
  
**Skripterstellung für Partitionsschemas**  
Schließt Tabellenpartitionierungsschemas in das Skript ein. Der Standardwert lautet False. Weitere Informationen finden Sie unter [CREATE PARTITION SCHEME (Transact-SQL)](https://msdn.microsoft.com/5b21c53a-b4f4-4988-89a2-801f512126e4).  
  
**Skripterstellung für Primärschlüssel**  
Schließt [PRIMARY KEY- und FOREIGN KEY-Einschränkungen](https://msdn.microsoft.com/31fbcc9f-2dc5-4bf9-aa50-ed70ec7b5bcd) in das Skript ein. Der Standardwert lautet "True".  
  
**Skripterstellung für Statistiken**  
Schließt benutzerdefinierte Statistiken in das Skript ein. Der Standardwert lautet False. Weitere Informationen finden Sie unter [CREATE STATISTICS (Transact-SQL)](https://msdn.microsoft.com/b23e2f6b-076c-4e6d-9281-764bdb616ad2).  
  
**Skripterstellung für Trigger**  
Schließt Trigger in das Skript ein. Der Standardwert lautet False. Weitere Informationen finden Sie unter [CREATE TRIGGER (Transact-SQL)](https://msdn.microsoft.com/edeced03-decd-44c3-8c74-2c02f801d3e7).  
  
**Skripterstellung für eindeutige Schlüssel**  
Schließt [UNIQUE-Einschränkungen und CHECK-Einschränkungen](https://msdn.microsoft.com/637098af-2567-48f8-90f4-b41df059833e) in das Skript ein. Der Standardwert lautet False.  
  
**Skripterstellung für Sichtspalten**  
Deklariert Sichtspalten in Sichtheadern. Der Standardwert lautet False. Weitere Informationen finden Sie unter [CREATE VIEW (Transact-SQL)](https://msdn.microsoft.com/aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9).  
  
**Include dri system names (Einschließen von DRI-Systemnamen)**  
Schließt vom System generierte Einschränkungsnamen ein, damit die deklarative referenzielle Integrität erzwungen wird. Der Standardwert lautet False. Weitere Informationen finden Sie unter [REFERENTIAL_CONSTRAINTS (Transact-SQL)](https://msdn.microsoft.com/5d358f18-0a85-4b55-af4b-98d5f4cd1020).  
  
### <a name="version-options"></a>Versionsoptionen

**Skripteinstellungen mit Quelle abgleichen** Falls aktiviert, werden die generierte Zielversion, Modul-Edition und der generierte Modultyp des Skripts auf die Werte des Servers festgelegt, auf dem das Skript für das Objekt erstellt wird. Dadurch werden die anderen Versionsoptionen deaktiviert (und ignoriert). 

**Skript für das Datenbankmodul** Generierte Skripts werden auf die angegebene [Engine Edition (Modul-Edition)](https://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.edition.aspx) ausgerichtet.

**Skript für den Datenbankmodultyp** Generierte Skripts werden auf den angegebenen [Database Engine Type (Datenbankmodultyp)](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.databaseenginetype.aspx) ausgerichtet.

**Skripterstellung für Serverversion**  
Generierte Skripts werden auf die angegebene Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ausgerichtet. Funktionen, die in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] neu sind, können für eine Skripterstellung für frühere Versionen nicht verwendet werden. Einige für [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] erstellte Skripts können weder auf Servern, auf denen eine frühere Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ausgeführt wird, noch in einer Datenbank mit einer früheren [Einstellung des Datenbankkompatibilitätsgrades](https://msdn.microsoft.com/ca5fd220-d5ea-4182-8950-55d4101a86f6)ausgeführt werden.  

## <a name="see-also"></a>Siehe auch  
[Erstellen von Skripts (SQL Server Management Studio)](https://msdn.microsoft.com/9711c617-3c68-4e5a-aea3-befc64d51524)  
  

