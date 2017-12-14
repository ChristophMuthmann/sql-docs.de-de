---
title: Cursors | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: relational-databases-misc
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- results [SQL Server], cursors
- Transact-SQL cursors, about cursors
- cursors [SQL Server]
- data access [SQL Server], cursors
- result sets [SQL Server], cursors
- requesting cursors
- cursors [SQL Server], about cursors
ms.assetid: e668b40c-bd4d-4415-850d-20fc4872ee72
caps.latest.revision: "29"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.openlocfilehash: 4abe8b006f30fd200becd40374df8cd699ffaab0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="cursors"></a>Cursor
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Vorgänge in einer relationalen Datenbank beziehen sich immer auf eine vollständige Gruppe von Zeilen. Beispielsweise besteht der Zeilensatz, der von einer SELECT-Anweisung zurückgegeben wird, aus allen Zeilen, die die Bedingungen der WHERE-Klausel der Anweisung erfüllen. Diese vollständige Gruppe von Zeilen, die von der Anweisung zurückgegeben wird, wird als Resultset bezeichnet. Anwendungen, vor allem interaktive Onlineanwendungen, sind nicht immer effektiv, wenn das gesamte Resultset als eine Einheit bearbeitet wird. Diese Anwendungen benötigen einen Mechanismus, um jeweils eine Zeile oder einen kleinen Zeilenblock zu bearbeiten. Cursor sind eine Erweiterung zu Resultsets und stellen diesen Mechanismus bereit.  
  
 Cursor erweitern die Verarbeitung von Ergebnissen folgendermaßen:  
  
-   Ermöglichen der Positionierung an bestimmten Zeilen des Resultsets.  
  
-   Abrufen einer Zeile oder eines ZeilenBlocks von der aktuellen Position im Resultset.  
  
-   Unterstützen von Datenänderungen in den Zeilen an der aktuellen Position im Resultset.  
  
-   Unterstützen von unterschiedlichen Sichtbarkeitsebenen bei Änderungen, die von anderen Benutzern an den Datenbankdaten, die im Resultset dargestellt werden, ausgeführt wurden.  
  
-   Bereitstellen des Zugriffs auf Daten in einem Resultset für [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen in Skripts, gespeicherte Prozeduren und Trigger.  
  
## <a name="concepts"></a>Konzepte  
 Cursorimplementierungen  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unterstützt drei Cursorimplementierungen.  
  
 Transact-SQL-Cursor  
 Basieren auf der DECLARE CURSOR-Syntax und werden hauptsächlich in [!INCLUDE[tsql](../includes/tsql-md.md)] -Skripts, gespeicherten Prozeduren und Triggern verwendet. [!INCLUDE[tsql](../includes/tsql-md.md)] -Cursor werden auf dem Server implementiert und mithilfe von [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisungen verwaltet, die vom Client an den Server gesendet werden. Sie können auch in Batches, gespeicherten Prozeduren oder Triggern enthalten sein.  
  
 API-Servercursor (Application Programming Interface, Schnittstelle für Anwendungsprogrammierung)  
 Diese unterstützen die API-Cursorfunktionen in OLE DB und ODBC. API-Servercursor werden auf dem Server implementiert. Wenn eine Clientanwendung eine API-Cursorfunktion aufruft, überträgt der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter oder der ODBC-Treiber die Anforderung an den Server, damit Maßnahmen für den API-Servercursor ergriffen werden.  
  
 Clientcursor  
 Sie werden intern vom [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client-ODBC-Treiber und der DLL implementiert, die die ADO-API implementiert. Clientcursor werden durch Zwischenspeichern aller Resultsetzeilen auf dem Client implementiert. Wenn eine Clientanwendung eine API-Cursorfunktion aufruft, führen der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native ODBC-Treiber oder die ADO-DLL die Cursoroperation auf den im Client zwischengespeicherten Resultsetzeilen aus.  
  
 Cursortypen  
 Vorwärtscursor  
 Ein Vorwärtscursor unterstützt keine Bildläufe, sondern ausschließlich das serielle Abrufen von Zeilen vom Anfang bis zum Ende des Cursors. Die Zeilen werden erst dann aus der Datenbank abgerufen, wenn der Abrufvorgang ausgeführt wird. Die Auswirkungen aller INSERT-, UPDATE- und DELETE-Anweisungen, die der aktuelle Benutzer ausführt oder für die von anderen Benutzern ein Commit ausgeführt wurde und die sich auf Zeilen im Resultset auswirken, werden dann sichtbar, wenn die Zeilen aus dem Cursor abgerufen werden.  
  
 Da mit dem Cursor kein Bildlauf rückwärts durchgeführt werden kann, sind die meisten Änderungen, die an Zeilen in der Datenbank vorgenommen wurden, nachdem die jeweilige Zeile abgerufen wurde, über den Cursor nicht sichtbar. In Fällen, in denen ein Wert, der zum Ermitteln der Zeilenposition im Resultset verwendet wird, geändert wird, z. B. durch Aktualisieren einer von einem gruppierten Index abgedeckten Spalte, ist der geänderte Wert über den Cursor sichtbar.  
  
 Obwohl die Datenbank-API-Cursormodelle einen Vorwärtscursor als unterschiedlichen Cursortyp betrachten, gilt dies nicht für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] betrachtet sowohl die Vorwärts- als auch Bildlauffunktion als Optionen, die für statische, keysetgesteuerte und dynamische Cursor übernommen werden können. [!INCLUDE[tsql](../includes/tsql-md.md)] -Cursor unterstützen statische Vorwärtscursor sowie keysetgesteuerte und dynamische Cursor. Die Datenbank-API-Cursormodelle gehen davon aus, dass statische, keysetgesteuerte und dynamische Cursor immer bildlauffähig sind. Wenn das Cursorattribut oder die Cursoreigenschaft einer Datenbank-API auf FORWARD_ONLY festgelegt ist, wird dies von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] als dynamischer Vorwärtscursor implementiert.  
  
 STATIC-Cursor  
 Das vollständige Resultset eines statischen Cursors wird in **tempdb** erstellt, wenn der Cursor geöffnet wird. Ein statischer Cursor zeigt das Resultset immer so an, wie es zur Verfügung stand, als der Cursor geöffnet wurde. Statische Cursor erkennen wenige oder keine Änderungen, beanspruchen beim Durchführen eines Bildlaufs jedoch relativ wenig Ressourcen.  
  
 Der Cursor spiegelt jedoch keinerlei Änderungen wider, die in der Datenbank ausgeführt wurden und die sich entweder auf die Mitgliedschaft des Resultsets oder auf Änderungen an den Werten in den Spalten der Zeilen beziehen, aus denen das Resultset besteht. Ein statischer Cursor zeigt neue Zeilen, die nach dem Öffnen des Cursors in die Datenbank eingefügt wurden, nicht an, selbst wenn sie die Suchbedingungen der SELECT-Anweisung des Cursors erfüllen. Wenn Zeilen, aus denen sich das Resultset zusammensetzt, von anderen Benutzern aktualisiert werden, werden die neuen Datenwerte im statischen Cursor nicht angezeigt. Der statische Cursor zeigt Zeilen an, die nach dem Öffnen des Cursors aus der Datenbank entfernt wurden. Die Operationen UPDATE, INSERT oder DELETE werden in einem statischen Cursor nicht widergespiegelt (es sei denn, der Cursor wird geschlossen und wieder geöffnet). Selbst Änderungen, die mithilfe derselben Verbindung, die den Cursor öffnete, durchgeführt wurden, sind nicht enthalten.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] : Statische Cursor sind immer schreibgeschützt.  
  
 Da das Resultset eines statischen Cursors in einer Arbeitstabelle in **tempdb**gespeichert wird, darf die Größe der Zeilen im Resultset die maximale Zeilengröße einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Tabelle nicht überschreiten.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] werden statische Cursor als Insensitivcursor bezeichnet, also Cursor, bei denen keine Unterscheidung gemacht wird. Von einigen Datenbank-Anwendungsprogrammierschnittstellen (APIs, Application Programming Interfaces) werden sie als Momentaufnahmecursor bezeichnet.  
  
 Keyset  
 Die Mitgliedschaft und Reihenfolge der Zeilen in einem keysetgesteuerten Cursor werden beim Öffnen des Cursors festgelegt. Keysetgesteuerte Cursor werden von einer Reihe von eindeutigen Bezeichnern (Schlüssel) gesteuert, die als das Keyset bezeichnet werden. Die Schlüssel werden anhand einer Reihe von Spalten erstellt, die die Zeilen im Resultset eindeutig identifizieren. Das Keyset ist die Menge der Schlüsselwerte aus allen Zeilen, die zum Zeitpunkt des Öffnens des Cursors die Kriterien der SELECT-Anweisung erfüllten. Das Keyset eines keysetgesteuerten Cursors wird in **tempdb** erstellt, wenn der Cursor geöffnet wird.  
  
 Dynamic  
 Dynamische Cursor sind das Gegenteil von statischen Cursorn. Dynamische Cursor spiegeln alle Änderungen an den Zeilen in den Resultsets beim Durchführen eines Bildlaufs durch den Cursor wider. Die Datenwerte, Reihenfolge und Mitgliedschaft der Zeilen im Resultset können sich bei jedem Abrufvorgang ändern. Jede UPDATE-, INSERT- und DELETE-Anweisung, die von einem Benutzer ausgeführt wurde, ist über den Cursor sichtbar. Updates sind sofort sichtbar, wenn sie über den Cursor mithilfe einer API-Funktion, wie z. B. **SQLSetPos** , oder der WHERE CURRENT OF-Klausel von [!INCLUDE[tsql](../includes/tsql-md.md)] ausgeführt wurden. Updates, die außerhalb des Cursors ausgeführt werden, sind nur dann sichtbar, wenn ein Commit für sie ausgeführt wurde, es sei denn, die Transaktionsisolationsstufe des Cursors wurde so festgelegt, dass ein Commit vor dem Lesevorgang nicht ausgeführt sein muss. Für dynamische Cursorpläne werden nie räumliche Indizes verwendet.  
  
## <a name="requesting-a-cursor"></a>Anfordern eines Cursors  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unterstützt zwei Methoden zum Anfordern eines Cursors:  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)]  
  
     Die [!INCLUDE[tsql](../includes/tsql-md.md)] -Sprache unterstützt eine Syntax für das Verwenden von Cursorn, die sich an der Syntax von ISO-Cursorn orientiert.  
  
-   Cursorfunktionen über Datenbank-APIs (Application Programming Interface, Schnittstelle für Anwendungsprogrammierung)  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unterstützt die Cursorfunktionen der folgenden Datenbank-APIs:  
  
    -   ADO ([!INCLUDE[msCoName](../includes/msconame-md.md)] ActiveX-Datenobjekt)  
  
    -   OLE DB  
  
    -   ODBC (Open Database Connectivity)  
  
 Eine Anwendung sollte niemals diese zwei Methoden für das Anfordern eines Cursors mischen. Eine Anwendung, die die API zum Angeben des Cursorverhaltens verwendet hat, sollte nicht anschließend eine DECLARE CURSOR-Anweisung von [!INCLUDE[tsql](../includes/tsql-md.md)] ausführen, um auch einen [!INCLUDE[tsql](../includes/tsql-md.md)] -Cursor anzufordern. Die Anwendung sollte nur dann DECLARE CURSOR ausführen, wenn alle API-Cursorattribute auf die entsprechenden Standardeinstellungen zurückgesetzt wurden.  
  
 Wenn weder ein [!INCLUDE[tsql](../includes/tsql-md.md)] -Cursor noch ein API-Cursor angefordert wurde, gibt [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] standardmäßig ein vollständiges Resultset, das als Standardresultset bezeichnet wird, an die Anwendung zurück.  
  
## <a name="cursor-process"></a>Cursorprozesse  
 [!INCLUDE[tsql](../includes/tsql-md.md)] -Cursor und API-Cursor verfügen über eine unterschiedliche Syntax. Es wird jedoch der folgende allgemeine Prozess bei allen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Cursorn verwendet:  
  
1.  Verbinden Sie einen Cursor mit dem Resultset einer [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisung, und definieren Sie die Eigenschaften des Cursors (z. B., ob die Zeilen im Cursor aktualisiert werden können).  
  
2.  Führen Sie die [!INCLUDE[tsql](../includes/tsql-md.md)] -Anweisung aus, um den Cursor aufzufüllen.  
  
3.  Rufen Sie die Zeilen in den Cursor ab, die Sie anzeigen möchten. Der Vorgang, durch die eine Zeile oder ein Zeilenblock von einem Cursor abgerufen wird, wird als Abrufvorgang bezeichnet. Wird eine Folge von Abrufvorgängen vorwärts oder rückwärts ausgeführt, wird dies als Durchführen eines Bildlaufs bezeichnet.  
  
4.  Führen Sie optional Änderungsvorgänge (Aktualisieren oder Löschen) in der Zeile an der aktuellen Position im Cursor aus.  
  
5.  Schließen Sie den Cursor.  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Cursorverhalten](../relational-databases/native-client-odbc-cursors/cursor-behaviors.md) [Implementieren von Cursorn](../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
## <a name="see-also"></a>Siehe auch  
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [Cursors &#40;Transact-SQL&#41;](../t-sql/language-elements/cursors-transact-sql.md)   
 [Cursorfunktionen &#40;Transact-SQL&#41;](../t-sql/functions/cursor-functions-transact-sql.md)   
 [Gespeicherte Cursorprozeduren &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/cursor-stored-procedures-transact-sql.md)  
  
  
