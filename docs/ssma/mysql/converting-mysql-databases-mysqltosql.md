---
title: Konvertieren von MySQL-Datenbanken (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ac21850b-fb32-4704-9985-5759b7c688c7
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2f5784f994169d8a43752b7e935cc06ae4aaacea
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="converting-mysql-databases-mysqltosql"></a>Konvertieren von MySQL-Datenbanken (MySQLToSQL)
Nachdem Sie eine Verbindung mit MySQL hergestellt haben, verbunden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, und Festlegen von Projekt- und Datenoptionen für die Zuordnung, können Sie MySQL-Datenbankobjekte konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbankobjekte.  
  
## <a name="the-conversion-process"></a>Konvertierungsprozess  
Konvertieren von Datenbankobjekten nimmt die Objektdefinitionen aus MySQL, konvertiert diese in ähnlichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objekte und lädt dann diese Informationen in die SSMA-Metadaten. Es lädt nicht die Informationen in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Sie können dann die Objekte und deren Eigenschaften anzeigen, mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer.  
  
Bei der Konvertierung druckt SSMA Ausgabenachrichten in den Ausgabebereich und Fehlermeldungen in den Bereich Fehlerliste. Verwenden Sie die Ausgabe und Fehler Informationen, um festzustellen, ob Sie so ändern Sie Ihre MySQL-Datenbanken oder die Konvertierung in die gewünschte Konvertierungsergebnisse zu erhalten haben.  
  
## <a name="setting-conversion-options"></a>Festlegen von Optionen  
Lesen Sie vor dem Konvertieren von Objekten, das Projekt Konvertierungsoptionen in der **Projekteinstellungen** (Dialogfeld). Mithilfe dieses Dialogfelds können Sie festlegen, wie SSMA Tabellen und Indizes konvertiert. Weitere Informationen finden Sie unter [Projekteinstellungen &#40;Konvertierung&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
## <a name="conversion-results"></a>Konvertierungsergebnisse  
Die folgende Tabelle zeigt, welche MySQL Objekte konvertiert werden, und die resultierende [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Objekte:  
  
|||  
|-|-|  
|**MySQL-Objekte**|**Resultierende SQL Server-Objekte**|  
|Tabellen mit abhängigen Objekte wie Indizes|SSMA erstellt Tabellen mit abhängigen Objekten. Tabelle mit allen Indizes und Einschränkungen konvertiert. Indizes werden in separaten konvertiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Objekte.<br /><br />**Räumliche datentypzuordnung** können nur auf Tabellenebene-Knoten ausgeführt werden.<br /><br />Weitere Informationen zu den Einstellungen für die Konvertierung der Tabelle finden Sie unter [Konvertierungseinstellungen](http://msdn.microsoft.com/en-us/f551cf6e-1575-4206-9cca-975b5b43a6b8)|  
|Funktionen|Wenn die Funktion direkt in Transact-SQL konvertiert werden kann, wird eine Funktion von SSMA erstellt. In einigen Fällen muss die Funktion in einer gespeicherten Prozedur konvertiert werden. Dies kann geschehen, indem Sie mithilfe von **Funktion Konvertierung** in den Projekteinstellungen. In diesem Fall erstellt SSMA einer gespeicherten Prozedur und eine Funktion, die gespeicherte Prozedur aufruft.<br /><br />**Optionen, die angegeben werden:**<br /><br />Konvertieren Sie gemäß den Einstellungen für Projektdateien<br /><br />Konvertieren von-Funktion<br /><br />Konvertieren Sie in der gespeicherten Prozedur<br /><br />Weitere Informationen zu Konvertierungseinstellungen-Funktion, finden Sie unter [Konvertierungseinstellungen](http://msdn.microsoft.com/en-us/f551cf6e-1575-4206-9cca-975b5b43a6b8)|  
|Vorgehensweisen|Wenn die Prozedur direkt in Transact-SQL konvertiert werden kann, erstellt der SSMA eine gespeicherte Prozedur. In einigen Fällen muss eine gespeicherte Prozedur in einer autonomen Transaktion aufgerufen werden. In diesem Fall SSMA erstellt zwei Prozeduren: eine, die implementiert werden, die Prozedur, und ein anderes, das zum Aufrufen der Implementierung verwendet wird, gespeicherte Prozedur.|  
|Datenbankkonvertierung|Datenbanken als MySQL-Objekte werden nicht direkt von SSMA für MySQL konvertiert. MySQL-Datenbanken mehr wie einen Schemanamen behandelt, und die physische Parameter werden während der Konvertierung verloren gehen. SSMA für die MySQL verwendet [MySQL-Datenbanken in SQL Server-Schemas zuordnen &#40;MySQLToSQL&#41; ](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md) Objekte von MySQL-Datenbank auf der entsprechenden SQL Server-Datenbank-Schema-Paar zugeordnet.|  
|Trigger-Konvertierung|**SSMA erstellt Trigger, die anhand der folgenden Regeln:**<br /><br />Bevor Trigger in INSTEAD OF T-SQL-Trigger konvertiert werden<br /><br />AFTER-Trigger werden in nach dem T-SQL-Trigger mit oder ohne Iterationen pro Zeilen konvertiert.|  
|View-Konvertierung|SSMA erstellt Ansichten mit abhängigen Objekten|  
|-Anweisungskonvertierung|– Jeder SQL Statement-Objekt kann eine einzelne MySQL-Anweisung (z. B. DDL, DML und andere Typen von Anweisungen) enthalten oder zu beginnen... END-Block.<br />-   **Mit mehreren Anweisungen Konvertierung: BEGIN... END-Block Konvertierung**SQL-Anweisung enthalten auch eine BEGIN... END-Block, wie in der Prozedur, Funktion oder Trigger-Definition. Die Blöcke, die sollen die gleiche Weise konvertiert werden, die sie für die einzelnen Objekte der MySQL-Anweisung konvertiert werden.|  
  
## <a name="converting-mysql-database-objects"></a>Konvertieren von Objekten der MySQL-Datenbank  
Für das Konvertieren von MySQL-Datenbankobjekte, stellen Sie zunächst wählen Sie die Objekte, die Sie konvertieren möchten, und lassen dann SSMA die Konvertierung auszuführen. Anzeige von Ausgabenachrichten bei der Konvertierung auf der **Ansicht** klicken Sie im Menü **Ausgabe**.  
  
**Konvertieren von MySQL-Objekte in SQL Server- bzw. SQL Azure-syntax**  
  
1.  In MySQL-Metadaten-Explorer, erweitern Sie den MySQL-Server, und erweitern Sie dann **Datenbanken**.  
  
2.  Wählen Sie Objekte zu konvertieren:  
  
    -   Um alle Schemas konvertieren möchten, aktivieren Sie das Kontrollkästchen neben **Datenbanken**.  
  
    -   Zum konvertieren, oder lassen Sie eine Datenbank, wählen Sie das Kontrollkästchen neben dem Datenbanknamen.  
  
    -   Zum konvertieren, oder lassen Sie eine Kategorie von Objekten, erweitern Sie ein Schema wählen Sie aus, oder deaktivieren Sie das Kontrollkästchen neben der Kategorie.  
  
    -   Zum konvertieren, oder lassen Sie einzelne Objekte, erweitern Sie den Kategorieordner wählen Sie aus, oder deaktivieren Sie das Kontrollkästchen neben dem Objekt.  
  
3.  Um alle ausgewählten Objekte zu konvertieren, Maustaste **Datenbanken** , und wählen Sie **Schema konvertieren**.  
  
    Sie können auch einzelne Objekte oder Kategorien von Objekten durch das Objekt oder der übergeordnete Ordner mit der rechten Maustaste, und wählen Sie dann konvertieren **Schema konvertieren**.  
  
## <a name="viewing-conversion-problems"></a>Probleme bei der Konvertierung anzeigen  
Einige MySQL-Objekte können nicht konvertiert werden. Sie können die Erfolgsquoten Konvertierung durch Anzeigen der Zusammenfassung Konvertierungsbericht bestimmen.  
  
**So zeigen Sie einen Zusammenfassungsbericht an**  
  
1.  Wählen Sie im MySQL-Metadaten-Explorer **Datenbanken**.  
  
2.  Wählen Sie im rechten Bereich die **Bericht** Registerkarte.  
  
    Dieser Bericht zeigt die Zusammenfassung Bewertungsbericht für alle Datenbankobjekte, die bewertet oder konvertiert wurden. Sie können auch einen Zusammenfassungsbericht für einzelne Objekte anzeigen:  
  
    -   Um den Bericht für ein einzelnes Schema anzuzeigen, wählen Sie die Datenbank in MySQL-Metadaten-Explorer aus.  
  
    -   Um den Bericht für ein einzelnes Objekt anzuzeigen, wählen Sie das Objekt in MySQL-Metadaten-Explorer aus. Objekte sind, die haben Probleme bei der Konvertierung, ein rotes Fehlersymbol.  
  
Für Objekte, die Fehler bei der Konvertierung, können Sie die Syntax anzeigen, die in der Konvertierungsfehler bewirkt, dass geführt haben.  
  
**Einzelne Konvertierungsprobleme anzeigen**  
  
1.  Erweitern Sie im MySQL-Metadaten-Explorer **Datenbanken**.  
  
2.  Erweitern Sie die Datenbank, in der ein rotes Fehlersymbol angezeigt.  
  
3.  Erweitern Sie einen Ordner mit einem roten Fehlersymbol, unter der Datenbank.  
  
4.  Wählen Sie das Objekt, das ein rotes Fehlersymbol verfügt.  
  
5.  Klicken Sie im rechten Bereich auf die **Bericht** Registerkarte.  
  
6.  Am oberen Rand der **Bericht** Registerkarte ist eine Dropdown-Liste. Wenn die Liste zeigt **Statistiken**, ändern Sie die Auswahl auf **Quelle**.  
  
    SSMA wird der Quellcode und mehrere Schaltflächen direkt über dem Code angezeigt.  
  
7.  Klicken Sie auf die **weiter Problem** Schaltfläche. Dies ist ein rotes Fehlersymbol mit einem Pfeil nach rechts.  
  
    SSMA wird die erste problematisch Quellcode zu markieren, die in das aktuelle Objekt gefunden.  
  
Für jedes Element, das nicht konvertiert werden konnte, müssen Sie ermitteln, was Sie mit diesem Objekt ausführen möchten:  
  
-   Sie können das Objekt in der MySQL-Datenbank zu entfernen oder zu überarbeiten problematischen Code ändern. Um den aktualisierten Code in SSMA zu laden, müssen Sie die Metadaten zu aktualisieren. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   Sie können das Objekt von der Migration ausschließen. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer und MySQL-Metadaten-Explorer, deaktivieren Sie das Kontrollkästchen neben dem Element vor dem Laden der Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure und Migrieren von Daten aus MySQL.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht [konvertiert Datenbankobjekte in SQL Server laden &#40;MySQLToSQL&#41;](../../ssma/mysql/loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von MySQL-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
