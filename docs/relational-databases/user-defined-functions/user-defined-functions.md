---
title: Benutzerdefinierte Funktionen | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user-defined functions [SQL Server], components
- user-defined functions [SQL Server], about user-defined functions
ms.assetid: d7ddafab-f5a6-44b0-81d5-ba96425aada4
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 43841807dce9cb747c2c5b182174f83f0540b030
ms.openlocfilehash: 12297570eae81459949b6c910fba26525e27d9ed
ms.contentlocale: de-de
ms.lasthandoff: 05/05/2017

---
# <a name="user-defined-functions"></a>Benutzerdefinierte Funktionen
  Ebenso wie Funktionen in Programmiersprachen sind auch benutzerdefinierte Funktionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Routinen, die Parameter annehmen, eine Aktion ausführen (z. B. eine komplexe Berechnung) und das Ergebnis dieser Aktion als Wert zurückgeben können. Der Rückgabewert kann ein einzelner Skalarwert oder ein Resultset sein.  
   
##  <a name="Benefits"></a> Benutzerdefinierte Funktionen  
Warum diese verwenden? 
  
-   Modulare Programmierung.  
  
     Sie können die Funktion einmal erstellen, sie dann in der Datenbank speichern und beliebig oft in einem Programm aufrufen. Benutzerdefinierte Funktionen können unabhängig vom Programmquellcode geändert werden.  
  
-   Schnellere Ausführung.  
  
     Ähnlich wie gespeicherte Prozeduren verringern auch benutzerdefinierte Funktionen von [!INCLUDE[tsql](../../includes/tsql-md.md)] die Kompilierungskosten von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code, da die Pläne zwischengespeichert und für wiederholte Ausführungen erneut verwendet werden. Dies bedeutet, dass die benutzerdefinierte Funktion nicht für jede Verwendung neu analysiert und optimiert werden muss; aus diesem Umstand ergeben sich wesentlich schnellere Ausführungszeiten.  
  
     CLR-Funktionen bieten gegenüber [!INCLUDE[tsql](../../includes/tsql-md.md)] -Funktionen für Berechnungsaufgaben, Zeichenfolgebearbeitung und Geschäftslogik erhebliche Leistungsvorteile. [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen sind besser für datenzugriffsintensive Programmlogik geeignet.  
  
-   Reduzierung der Netzwerkverkehrs.  
  
     Eine Operation, die Daten basierend auf einer komplexen Einschränkung filtert, die nicht als einzelner Skalarausdruck ausgedrückt werden kann, kann als Funktion definiert werden. Diese Funktion kann anschließend in der WHERE-Klausel aufgerufen werden, um die Anzahl der Zeilen zu verringern, die an den Client gesendet werden.  
  
> [!NOTE]
> Benutzerdefinierte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen in Abfragen können nur auf einem einzelnen Thread (serieller Ausführungsplan) ausgeführt werden.  
  
##  <a name="FunctionTypes"></a> Funktionstypen  
**Skalarfunktion**  
 Benutzerdefinierte Skalarfunktionen geben einen einzelnen Datenwert des definierten Datentyps in einer RETURNS-Klausel zurück. Bei einer Inlineskalarfunktion gibt es keinen Funktionshauptteil; der Skalarwert ist das Ergebnis einer einzelnen SELECT-Anweisung. Bei einer aus mehreren Anweisungen bestehenden Skalarfunktion enthält der in einem BEGIN…END-Block definierte Hauptteil der Funktion eine Reihe von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen, die den einzelnen Wert zurückgeben. Der Rückgabetyp kann ein beliebiger Datentypen mit Ausnahme von **text**, **ntext**, **image**, **cursor**und **timestamp**sein. 
 **[Beispiele.](https://msdn.microsoft.com/library/bb386973(v=vs.110).aspx)**
  
**Tabellenwertfunktionen**  
 Benutzerdefinierte Tabellenwertfunktionen geben einen **table** -Datentyp zurück. Bei einer Inlinefunktion mit Tabellenrückgabe gibt es keinen Funktionshauptteil; die Tabelle ist das Resultset einer einzelnen SELECT-Anweisung. **[Beispiele.](https://msdn.microsoft.com/library/bb386954(v=vs.110).aspx)**
  
**Systemfunktionen**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt viele Systemfunktionen bereit, mit denen Sie eine Vielzahl von Vorgängen ausführen können. Sie können nicht geändert werden. Weitere Informationen finden Sie unter [Integrierte Funktionen &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md), [Systemgespeicherte Funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-functions/system-functions-for-transact-sql.md) und [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
##  <a name="Guidelines"></a> Richtlinien  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]-Fehler, die dazu führen, dass eine Anweisung abgebrochen und mit der nächsten Anweisung fortgefahren wird (z.B. Trigger oder gespeicherte Prozeduren), werden innerhalb einer Funktion anders behandelt. In Funktionen bewirken solche Fehler, dass die Ausführung der Funktion beendet wird. Dies hat wiederum zur Folge, dass die Anweisung abgebrochen wird, die die Funktion aufgerufen hat.  
  
 Die Anweisungen in einem BEGIN…END-Block dürfen keine Nebeneffekte haben. Nebeneffekte von Funktionen sind dauerhafte Änderungen am Status einer Ressource, deren Gültigkeitsbereich außerhalb der Funktion liegt, wie z. B. Änderungen an einer Datenbanktabelle. Die einzigen Änderungen, die von den Anweisungen in der Funktion vorgenommen werden dürfen, sind Änderungen an lokalen Objekten der Funktion, wie z. B. lokale Cursor oder Variablen. Änderungen an Datenbanktabellen, Cursorvorgänge außerhalb der Funktion, das Senden von E-Mails, das Ausführen einer Katalogänderung und das Generieren eines Resultsets, das an den Benutzer zurückgegeben wird, sind Beispiele für Aktionen, die in einer Funktion nicht ausgeführt werden können.  
  
> [!NOTE]
> Wenn eine CREATE FUNCTION-Anweisung zu Nebeneffekten bei Ressourcen führt, die beim Ausgeben der CREATE FUNCTION-Anweisung nicht vorhanden sind, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Anweisung aus. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] führt die Funktion jedoch beim Aufrufen nicht aus.  
  
 Wie oft eine in einer Abfrage angegebene Funktion tatsächlich ausgeführt wird, kann bei den vom Abfrageoptimierer erstellten Ausführungsplänen variieren. Ein Beispiel hierfür ist eine Funktion, die von einer Unterabfrage in einer WHERE-Klausel aufgerufen wird. Wie oft die Unterabfrage und deren Funktion ausgeführt wird, kann bei den verschiedenen Zugriffsmethoden variieren, die der Abfrageoptimierer auswählt.  
  
##  <a name="ValidStatements"></a> Gültige Anweisungen in einer Funktion  
Die folgenden Anweisungstypen sind in einer Funktion zulässig:  
  
-   DECLARE-Anweisungen zum Definieren von lokalen Datenvariablen und lokalen Cursorn für die Funktion.  
  
-   Zuweisungen von Werten zu lokalen Objekten für die Funktion, wie z. B. das Zuweisen von Werten zu lokalen Skalar- und Tabellenwerten mithilfe von SET.  
  
-   Cursorvorgänge, die auf lokale Cursor verweisen, die in der Funktion deklariert, geöffnet, geschlossen und deren Zuordnungen aufgehoben werden. FETCH-Anweisungen, die Daten an den Client zurückgeben, sind nicht zulässig. Nur FETCH-Anweisungen, die lokalen Variablen Werte mithilfe der INTO-Klausel zuweisen, sind zulässig.  
  
-   Anweisungen zur Ablaufsteuerung mit Ausnahme von TRY...CATCH-Anweisungen.  
  
-   SELECT-Anweisungen, die Auswahllisten mit Ausdrücken enthalten, in denen Werte Variablen zugewiesen werden, die in der Funktion lokal gelten.  
  
-   UPDATE-, INSERT- und DELETE-Anweisungen, die lokale Tabellenvariablen der Funktion ändern.  
  
-   EXECUTE-Anweisungen, die eine erweiterte gespeicherte Prozedur aufrufen.  
  
### <a name="built-in-system-functions"></a>Integrierte Systemfunktionen  
 Die folgenden nicht deterministischen integrierten Funktionen können in benutzerdefinierten Transact-SQL-Funktionen verwendet werden.  
  
|||  
|-|-|  
|CURRENT_TIMESTAMP|@@MAX_CONNECTIONS|  
|GET_TRANSMISSION_STATUS|@@PACK_RECEIVED|  
|GETDATE|@@PACK_SENT|  
|GETUTCDATE|@@PACKET_ERRORS|  
|@@CONNECTIONS|@@TIMETICKS|  
|@@CPU_BUSY|@@TOTAL_ERRORS|  
|@@DBTS|@@TOTAL_READ|  
|@@IDLE|@@TOTAL_WRITE|  
|@@IO_BUSY||  
  
 Die folgenden nicht deterministischen integrierten Funktionen können in benutzerdefinierten Transact-SQL-Funktionen **nicht** verwendet werden.  
  
|||  
|-|-|  
|NEWID|RAND|  
|NEWSEQUENTIALID|TEXTPTR|  
  
 Eine Liste der deterministischen und nicht deterministischen integrierten Systemfunktionen finden Sie unter [Deterministische und nicht deterministische Funktionen](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
##  <a name="SchemaBound"></a> Schemagebundene Funktionen  
 CREATE FUNCTION unterstützt eine SCHEMABINDING-Klausel, die die Funktion an das Schema von Objekten bindet, auf die verwiesen wird, wie z. B. Tabellen, Sichten und andere benutzerdefinierte Funktionen. Der Versuch, ein Objekt zu ändern oder zu löschen, auf das von einer schemagebundenen Funktion verwiesen wird, erzeugt einen Fehler.  
  
 Die folgenden Bedingungen müssen erfüllt sein, um SCHEMABINDING in [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) angeben zu können:  
  
-   Alle Sichten und benutzerdefinierten Funktionen, auf die die Funktion verweist, müssen schemagebunden sein.  
  
-   Alle Objekte, auf die die Funktion verweist, müssen sich in derselben Datenbank wie die Funktion befinden. Auf die Objekte muss mit ein- oder zweiteiligen Namen verwiesen werden.  
  
-   Sie benötigen die REFERENCES-Berechtigung für alle Objekte (Tabellen, Sichten und benutzerdefinierte Funktion), auf die in der Funktion verwiesen wird.  
  
 Mit ALTER FUNCTION können Sie die Schemabindung entfernen. Die ALTER FUNCTION-Anweisung sollte die Funktion neu definieren, ohne WITH SCHEMABINDING anzugeben.  
  
##  <a name="Parameters"></a> Angeben von Parametern  
 Eine benutzerdefinierte Funktion verwendet null oder mehr Eingabeparameter und gibt einen Skalarwert oder eine Tabelle zurück. Eine Funktion kann maximal 1024 Eingabeparameter haben. Wenn ein Parameter der Funktion über einen Standardwert verfügt, muss beim Aufrufen der Funktion das DEFAULT-Schlüsselwort angegeben werden, um den Standardwert zu erhalten. In diesem Punkt gibt es einen Unterschied zu den Parametern einer benutzerdefinierten gespeicherten Prozedur. Fehlt im Aufruf einer benutzerdefinierten gespeicherten Prozedur ein Parameter, der einen Standardwert hat, wird automatisch dieser Standardwert verwendet. Benutzerdefinierte Funktionen unterstützen keine Ausgabeparameter.  
  
##  <a name="Tasks"></a> Weitere Beispiele!  
  
|||  
|-|-|  
|**Taskbeschreibung**|**Thema**|  
|Beschreibt, wie eine benutzerdefinierte Transact-SQL-Funktion erstellt wird.|[Erstellen benutzerdefinierter Funktionen &#40;Datenbankmodul&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)|  
|Beschreibt, wie eine CLR-Funktion erstellt wird.|[Erstellen von CLR-Funktionen](../../relational-databases/user-defined-functions/create-clr-functions.md)|  
|Beschreibt, wie eine benutzerdefinierte Aggregatfunktion erstellt wird.|[Erstellen benutzerdefinierter Aggregate](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)|  
|Beschreibt, wie eine benutzerdefinierte Transact-SQL-Funktion geändert wird.|[Ändern benutzerdefinierter Funktionen](../../relational-databases/user-defined-functions/modify-user-defined-functions.md)|  
|Beschreibt, wie eine benutzerdefinierte Funktion gelöscht wird.|[Löschen von benutzerdefinierten Funktionen](../../relational-databases/user-defined-functions/delete-user-defined-functions.md)|  
|Beschreibt, wie eine benutzerdefinierte Funktion ausgeführt wird.|[Ausführen von benutzerdefinierten Funktionen](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)|  
|Beschreibt, wie eine benutzerdefinierte Funktion umbenannt wird.|[Umbenennen von benutzerdefinierten Funktionen](../../relational-databases/user-defined-functions/rename-user-defined-functions.md)|  
|Beschreibt, wie die Definition einer benutzerdefinierten Funktion angezeigt wird.|[Anzeigen benutzerdefinierter Funktionen](../../relational-databases/user-defined-functions/view-user-defined-functions.md)|  
  
  

