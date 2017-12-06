---
title: Konvertieren von Oracle-Schemas (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Conversion Results
ms.assetid: e021182d-31da-443d-b110-937f5db27272
caps.latest.revision: "14"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: On Demand
ms.openlocfilehash: 698f85fea4a5a21c2fbd697ec53f90ec7e888ccf
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="converting-oracle-schemas-oracletosql"></a>Konvertieren von Oracle-Schemas (OracleToSQL)
Nachdem Sie mit Oracle verbunden haben, verbunden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], konvertiert und dann Projekt festlegen und Optionen für die Zuordnung von Daten, Sie können Datenbankobjekte, die Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datenbankobjekten.  
  
## <a name="the-conversion-process"></a>Konvertierungsprozess  
Konvertieren von Datenbankobjekten nimmt die Objektdefinitionen von Oracle, konvertiert diese in ähnliche [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Objekte und lädt dann diese Informationen in die SSMA-Metadaten. Es lädt nicht die Informationen in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Sie können dann die Objekte und deren Eigenschaften anzeigen, mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer.  
  
Bei der Konvertierung druckt SSMA Ausgabenachrichten in den Ausgabebereich und Fehlermeldungen in den Bereich Fehlerliste. Verwenden Sie die Ausgabe und Fehler Informationen, um festzustellen, ob Sie so ändern Sie die Oracle-Datenbanken oder die Konvertierung in die gewünschte Konvertierungsergebnisse zu erhalten haben.  
  
## <a name="setting-conversion-options"></a>Festlegen von Optionen  
Lesen Sie vor dem Konvertieren von Objekten, das Projekt Konvertierungsoptionen in der **Projekteinstellungen** (Dialogfeld). Mithilfe dieses Dialogfelds können Sie festlegen, wie SSMA Funktionen und globalen Variablen konvertiert. Weitere Informationen finden Sie unter [Projekteinstellungen &#40; Konvertierung &#41; &#40; OracleToSQL &#41; ](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
## <a name="conversion-results"></a>Konvertierungsergebnisse  
Die folgende Tabelle zeigt, welche Oracle Objekte konvertiert werden, und die resultierende [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Objekte:  
  
|||  
|-|-|  
|Oracle-Objekte|Resultierende SQL Server-Objekte|  
|Funktionen|Wenn die Funktion direkt kann, um konvertiert werden [!INCLUDE[tsql](../../includes/tsql_md.md)], SSMA erstellt eine Funktion.<br /><br />In einigen Fällen muss die Funktion in einer gespeicherten Prozedur konvertiert werden. In diesem Fall erstellt SSMA einer gespeicherten Prozedur und eine Funktion, die gespeicherte Prozedur aufruft.|  
|Vorgehensweisen|Wenn die Prozedur direkt kann, um konvertiert werden [!INCLUDE[tsql](../../includes/tsql_md.md)], SSMA erstellt eine gespeicherte Prozedur.<br /><br />In einigen Fällen muss eine gespeicherte Prozedur in einer autonomen Transaktion aufgerufen werden. In diesem Fall SSMA erstellt zwei Prozeduren: eine, die implementiert werden, die Prozedur, und ein anderes, das zum Aufrufen der Implementierung verwendet wird, gespeicherte Prozedur.|  
|Pakete|SSMA erstellt einen Satz von gespeicherten Prozeduren und Funktionen, die von ähnlichen Objektnamen unified sind.|  
|Sequenzen|SSMA Sequence-Objekte (SQL Server 2012 oder SQL Server 2014) erstellt oder Oracle-Sequenzen emuliert.|  
|Tabellen mit abhängigen Objekte wie Indizes und Trigger|SSMA erstellt Tabellen mit abhängigen Objekten.|  
|Zeigen Sie mit abhängigen Objekte, z. B. Trigger an|SSMA wird mit abhängigen Objekten Ansichten erstellt.|  
|Materialisierte Sichten|**SSMA wird mit einigen Ausnahmen indizierte Sichten in SQLServer erstellt. Konvertierung schlägt fehl, wenn die materialisierte Sicht eine oder mehrere der folgenden Konstrukte enthält:**<br /><br />Benutzerdefinierte Funktion<br /><br />Nicht deterministische Feld / Funktion / Wählen Sie im Ausdruck, in dem oder GROUP BY-Klauseln<br /><br />Verwendung von "float"-Spalte in SELECT *, wobei oder GROUP BY-Klauseln (Sonderfall des vorherigen Problem)<br /><br />Benutzerdefinierter Datentyp (inkl. geschachtelten Tabellen)<br /><br />COUNT (distinct &lt;Feld&gt;)<br /><br />FETCH<br /><br />OUTER-Joins (LEFT, RIGHT oder FULL)<br /><br />Unterabfrage, die andere Ansicht<br /><br />ÜBER, RANK, FÜHREN, MELDEN SIE SICH<br /><br />MIN, MAX<br /><br />INTERSECT-UNION, MINUS,<br /><br />HAVING|  
|Trigger|**SSMA erstellt Trigger, die anhand der folgenden Regeln:**<br /><br />Bevor Trigger in INSTEAD OF-Trigger konvertiert wurden.<br /><br />AFTER-Trigger werden in AFTER-Trigger konvertiert.<br /><br />INSTEAD OF-Trigger werden in INSTEAD OF-Trigger konvertiert. Mehrere für den gleichen Vorgang definierten INSTEAD OF-Trigger werden in einem Trigger kombiniert.<br /><br />Trigger auf Zeilenebene werden emuliert die Verwendung von Cursorn.<br /><br />Kaskadierende Trigger werden in mehrere einzelne Trigger konvertiert.|  
|Synonyme|**Synonyme werden für die folgenden Objekttypen erstellt:**<br /><br />Tabellen und Objekttabellen<br /><br />Ansichten und Objekt<br /><br />Gespeicherte Prozeduren<br /><br />Funktionen<br /><br />**Synonyme für die folgenden Objekte werden gelöst und durch direkte Objektverweise ersetzt:**<br /><br />Sequenzen<br /><br />Pakete<br /><br />Schemaobjekte für Java-Klasse<br /><br />Benutzerdefinierte Objekttypen<br /><br />Synonyme für ein anderes Synonym können nicht migriert werden und werden als Fehler gekennzeichnet werden.<br /><br />Synonyme sind nicht für Materialized Ansichten erstellt.|  
|Benutzerdefinierte Typen|**SSMA bietet keine Unterstützung für die Konvertierung von benutzerdefinierten Typen. Benutzerdefinierte Typen, einschließlich seiner Verwendung in PL/SQL-Programmen sind mit speziellen Konvertierungsfehler durch MDX die folgenden Regeln gekennzeichnet:**<br /><br />Tabellenspalte eines benutzerdefinierten Typs ist in vom Datentyp VARCHAR(8000) konvertiert.<br /><br />Argument vom Benutzer definierten Typ an eine gespeicherte Prozedur oder Funktion ist vom Datentyp VARCHAR(8000) konvertiert.<br /><br />Variablen des benutzerdefinierten Typs in PL/SQL-Block ist in vom Datentyp VARCHAR(8000) konvertiert.<br /><br />Objekttabelle wird in einer Standardtabelle konvertiert.<br /><br />Objektansicht wird in einer Standardsicht konvertiert.|  
  
## <a name="converting-oracle-database-objects"></a>Konvertieren von Oracle-Datenbankobjekten  
Für das Konvertieren von Oracle-Datenbankobjekten, stellen Sie zunächst wählen Sie die Objekte, die Sie konvertieren möchten, und lassen dann SSMA die Konvertierung auszuführen. Anzeige von Ausgabenachrichten bei der Konvertierung auf der **Ansicht** klicken Sie im Menü **Ausgabe**.  
  
**Konvertieren von Oracle-Objekten in SQL Server-syntax**  
  
1.  In Oracle-Metadaten-Explorer, erweitern Sie den Oracle-Server, und erweitern Sie dann **Schemas**.  
  
2.  Wählen Sie Objekte zu konvertieren:  
  
    -   Um alle Schemas konvertieren möchten, aktivieren Sie das Kontrollkästchen neben **Schemas**.  
  
    -   Zum konvertieren, oder lassen Sie eine Datenbank, wählen Sie das Kontrollkästchen neben den Schemanamen an.  
  
    -   Zum konvertieren, oder lassen Sie eine Kategorie von Objekten, erweitern Sie ein Schema wählen Sie aus, oder deaktivieren Sie das Kontrollkästchen neben der Kategorie.  
  
    -   Zum konvertieren, oder lassen Sie einzelne Objekte, erweitern Sie den Kategorieordner wählen Sie aus, oder deaktivieren Sie das Kontrollkästchen neben dem Objekt.  
  
3.  Um alle ausgewählten Objekte zu konvertieren, Maustaste **Schemas** , und wählen Sie **Schema konvertieren**.  
  
    Sie können auch einzelne Objekte oder Kategorien von Objekten durch das Objekt oder der übergeordnete Ordner mit der rechten Maustaste, und wählen Sie dann konvertieren **Schema konvertieren**.  
  
## <a name="viewing-conversion-problems"></a>Probleme bei der Konvertierung anzeigen  
Einige Oracle-Objekte können nicht konvertiert werden. Sie können die Erfolgsquoten Konvertierung durch Anzeigen der Zusammenfassung Konvertierungsbericht bestimmen.  
  
**So zeigen Sie einen Zusammenfassungsbericht an**  
  
1.  Wählen Sie in der Oracle-Metadaten-Explorer **Schemas**.  
  
2.  Wählen Sie im rechten Bereich die **Bericht** Registerkarte.  
  
    Dieser Bericht zeigt die Zusammenfassung Bewertungsbericht für alle Datenbankobjekte, die bewertet oder konvertiert wurden. Sie können auch einen Zusammenfassungsbericht für einzelne Objekte anzeigen:  
  
    -   Um den Bericht für ein einzelnes Schema anzuzeigen, wählen Sie das Schema in Oracle-Metadaten-Explorer aus.  
  
    -   Um den Bericht für ein einzelnes Objekt anzuzeigen, wählen Sie das Objekt in der Oracle-Metadaten-Explorer aus. Objekte sind, die haben Probleme bei der Konvertierung, ein rotes Fehlersymbol.  
  
Für Objekte, die Fehler bei der Konvertierung, können Sie die Syntax anzeigen, die in der Konvertierungsfehler bewirkt, dass geführt haben.  
  
**Einzelne Konvertierungsprobleme anzeigen**  
  
1.  Erweitern Sie in der Oracle-Metadaten-Explorer **Schemas**.  
  
2.  Erweitern Sie das Schema, das ein rotes Fehlersymbol zeigt.  
  
3.  Erweitern Sie einen Ordner mit einem roten Fehlersymbol, unter dem Schema.  
  
4.  Wählen Sie das Objekt, das ein rotes Fehlersymbol verfügt.  
  
5.  Klicken Sie im rechten Bereich auf die **Bericht** Registerkarte.  
  
6.  Am oberen Rand der **Bericht** Registerkarte ist eine Dropdown-Liste. Wenn die Liste zeigt **Statistiken**, ändern Sie die Auswahl auf **Quelle**.  
  
    SSMA wird der Quellcode und mehrere Schaltflächen direkt über dem Code angezeigt.  
  
7.  Klicken Sie auf die **weiter Problem** Schaltfläche. Dies ist ein rotes Fehlersymbol mit einem Pfeil nach rechts.  
  
    SSMA wird die erste problematisch Quellcode zu markieren, die in das aktuelle Objekt gefunden.  
  
Für jedes Element, das nicht konvertiert werden konnte, müssen Sie ermitteln, was Sie mit diesem Objekt ausführen möchten:  
  
-   Sie können den Quellcode für Prozeduren ändern, auf die **SQL** Registerkarte.  
  
-   Sie können das Objekt in der Oracle-Datenbank zu entfernen oder zu überarbeiten problematischen Code ändern. Um den aktualisierten Code in SSMA zu laden, müssen Sie die Metadaten zu aktualisieren. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit Oracle-Datenbank &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   Sie können das Objekt von der Migration ausschließen. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer und Oracle-Metadaten-Explorer, deaktivieren Sie das Kontrollkästchen neben dem Element vor dem Laden der Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und Migrieren von Daten aus Oracle-Datenbanken.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht darin [Laden Sie konvertierte Objekte in SQL Server](http://msdn.microsoft.com/en-us/a8ae33b2-1883-4785-922b-ea0e31c0b37a).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Oracle-Datenbanken zu SQLServer &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
