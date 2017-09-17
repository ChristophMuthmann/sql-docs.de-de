---
title: "Ausführen von Update- und Delete-Anweisungen positioniert | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- ODBC cursor library [ODBC], positioned update or delete
ms.assetid: 1d64f309-2a6e-4ad1-a6b5-e81145549c56
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 78bdb77c8aa4d9351e040b97d9690bb09374856d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="executing-positioned-update-and-delete-statements"></a>Positionierte Update- und Delete-Anweisungen ausführen
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Microsoft empfiehlt die Verwendung der Cursorfunktionalität der Treiber.  
  
 Nachdem eine Anwendung einen Block von Daten mit abgerufen hat **SQLFetchScroll**, können sie aktualisieren oder löschen Sie die Daten im Block. Ausführen von ein positioniertes Update oder Delete, die Anwendung:  
  
1.  Aufrufe **SQLSetPos** , positionieren Sie den Cursor auf die Zeile aktualisiert oder gelöscht werden.  
  
2.  Erstellt eine positionierte Update- oder Delete-Anweisung mit der folgenden Syntax:  
  
     **UPDATE** *Tabellenname*  
  
     **Legen Sie** *Spaltenbezeichner* ** = ** {*Ausdruck* &#124; **NULL**}  
  
     [**,** *Spaltenbezeichner* ** = ** {*Ausdruck* &#124; **NULL**}]  
  
     **WHERE CURRENT OF** *Cursorname*  
  
     **DELETE FROM** *Tabellenname* **WHERE CURRENT OF** *Cursorname*  
  
     Die einfachste Möglichkeit zum Erstellen der **festgelegt** -Klausel in ein positioniertes Update-Anweisung ist die Verwendung von parametermarkierungen für jede Spalte aktualisiert werden, und verwenden **SQLBindParameter** binden diese an die Rowset-Puffer für die die Zeile aktualisiert werden. In diesem Fall wird der C-Datentyp des Parameters der C-Datentyp des Puffers Rowset identisch sein.  
  
3.  Die Rowset-Puffer für die aktuelle Zeile aktualisiert, wenn eine positioniertes Update-Anweisung ausgeführt werden. Nach der erfolgreichen Ausführung eine positioniertes Update-Anweisung, kopiert die Cursorbibliothek die Werte aus jeder Spalte in der aktuellen Zeile aus, in seinem Cache.  
  
    > [!CAUTION]  
    >  Wenn die Anwendung nicht ordnungsgemäß die Puffern Rowset aktualisiert vor der Ausführung einer positioniertes Update-Anweisung, sind die Daten im Cache fehlerhaft, nachdem die Anweisung ausgeführt wird.  
  
4.  Führt die positionierte Update- oder Delete-Anweisung mit einer anderen Anweisung als die Anweisung, die dem Cursor zugeordnet.  
  
    > [!CAUTION]  
    >  Die **, in denen** -Klausel erstellt, indem die Cursorbibliothek zur Identifikation der aktuellen Zeile kann fehlschlagen, um alle Zeilen zu identifizieren, Identifizieren von einer anderen Zeile oder mehr als eine Zeile zu identifizieren. Weitere Informationen finden Sie unter [durchsucht-Anweisungen konstruieren](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Alle positioniert Update und Delete-Anweisungen erfordern kein Cursorname angegeben. Um den Cursornamen angeben, ruft die Anwendung **SQLSetCursorName** , bevor der Cursor geöffnet wird. Ruft eine Anwendung für die Verwendung der Name des Cursors vom Treiber generierten **SQLGetCursorName** nach dem Öffnen des Cursors.  
  
 Nach dem Cursor Library führt ein positioniertes Update oder Delete-Anweisung, die Statusarray Rowset Puffern und Cache, der von der Cursorbibliothek enthalten die Werte, die in der folgenden Tabelle gezeigt.  
  
|-Anweisung verwendet|Wert in zeilenstatusarray|Werte in<br /><br /> Rowset-Puffer|Werte in<br /><br /> Cachepuffer|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|Positioniertes Update|SQL_ROW_UPDATED|Neue Werte [1]|Neue Werte [1]|  
|Positionierte delete|SQL_ROW_DELETED|Alte Werte|Alte Werte|  
  
 [1] die Anwendung muss die Werte in den Puffern Rowset aktualisieren, bevor die positionierte Update-Anweisung ausgeführt; nach dem Ausführen der positionierte Update-Anweisung, kopiert die Cursorbibliothek die Werte in den Puffern Rowset zum Cache.
