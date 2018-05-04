---
title: Befehl "INDEX" | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- index command [ODBC]
ms.assetid: 694e8cf5-2f69-4001-9c1e-b735a4da3aff
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5d5be9318a701b23dc0f6ceb67b9056c2455c7d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="index-command"></a>Befehl "INDEX"
Erstellt eine Indexdatei zum Anzeigen und Zugreifen auf Tabellendatensätze in einer logischen Reihenfolge.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
INDEX ON eExpression TO IDXFileName | TAG TagName [OF CDXFileName]  
   [FOR lExpression]  
   [COMPACT]  
   [ASCENDING | DESCENDING]  
   [UNIQUE | CANDIDATE]  
   [ADDITIVE]  
```  
  
## <a name="arguments"></a>Argumente  
 *eExpression*  
 Gibt einen Indexausdruck, der den Namen des Felds oder der Felder aus der aktuellen Tabelle enthalten kann. Ein Indexschlüssel basierend auf den Indexausdruck wird in die Indexdatei für jeden Datensatz in der Tabelle erstellt. Visual FoxPro verwendet diesen Schlüssel zum Anzeigen und Zugreifen auf Datensätze in der Tabelle.  
  
> [!NOTE]  
>  Obwohl nicht zu empfehlen, *eExpression* kann auch eine Arbeitsspeicher-Variable, ein Arrayelement oder ein Feld oder den Feldausdruck aus einer Tabelle in einem anderen Arbeitsbereich. Memo-Felder können nicht allein in Indexausdrücke-Datei verwendet werden. Sie müssen mit anderen Zeichenausdrücke kombiniert werden. Wenn Sie einen Index, der enthält eine Variable oder ein Feld, das nicht mehr vorhanden oder kann nicht gefunden werden zugreifen, generiert Visual FoxPro eine Fehlermeldung an.  
  
 Wenn Sie versuchen, einen Index mit einem Schlüssel zu erstellen, die Länge variiert, wird der Schlüssel mit Leerzeichen aufgefüllt. Indexschlüssel mit variabler Länge werden nicht in der Visual FoxPro unterstützt.  
  
 Es ist möglich, einen Indexschlüssel zu erstellen, mit der Länge 0. Beispielsweise wird ein 0 (null) Länge Indexschlüssel erstellt, wenn die Indexausdruck eine Teilzeichenfolge des Memofelds leere ist. 0 (null) Länge Schlüssel eines Indexes wird eine Fehlermeldung generiert. Wenn Visual FoxPro ein Index erstellt wird, wertet ihn Felder im ersten Datensatz in der Tabelle. Wenn ein Feld leer ist, kann es einige temporäre Daten in das Feld in den ersten Datensatz, um zu verhindern, dass der Schlüssel eines Indexes mit der Länge 0 eingeben erforderlich sein.  
  
 UM *IDXFileName*  
 Erstellt eine IDX-Indexdatei an. Die Indexdatei ist der standardmäßige Erweiterung IDX angegeben.  
  
 TAG *TagName*[OF *CDXFileName*]  
 Erstellt eine zusammengesetzten Indexdatei. Eine zusammengesetzte Indexdatei ist ein einzelner Index-Datei, aus die eine beliebige Anzahl von separaten Tags (Indexeinträge) besteht. Jeden Tag wird durch seinen Namen eindeutiges Tag identifiziert. Tag-Namen müssen mit einem Buchstaben oder Unterstrich beginnen und können eine beliebige Kombination von bis zu 10 Buchstaben, Ziffern oder Unterstrichen bestehen. Die Anzahl der Transponder in einer Indexdatei zusammengesetzten wird nur durch den verfügbaren Arbeitsspeicher und Speicherplatz beschränkt.  
  
 Zusammengesetzte unterschiedlichem-Indexdateien sind immer compact. Es ist nicht erforderlich, COMPACT enthalten, beim Erstellen einer Indexdatei zusammengesetzten. Namen von zusammengesetzten Indexdateien Erweiterung CDX erhalten.  
  
 Zwei Arten von zusammengesetzten Indexdateien erstellt werden können: strukturellen und nonstructural.  
  
 **Strukturelle zusammengesetzten Indexdateien** können, erstellen Sie eine strukturelle zusammengesetzten Indexdatei mit TAG *TagName* durch Ausschließen der optionalen OF *CDXFileName* Klausel. Eine zusammengesetzte Indexdatei immer hat den gleichen Basisnamen wie die Tabelle und wird automatisch geöffnet, wenn die Tabelle geöffnet wird.  
  
 **Nonstructural zusammengesetzten Indexdateien** Sie können eine Indexdatei nonstructural zusammengesetzten erstellen, indem Sie einschließlich der *CDXFileName* nach TAG *TagName*. Im Gegensatz zu einer Indexdatei strukturellen zusammengesetzten muss eine Indexdatei nonstructural zusammengesetzten explizit mit der INDEX-Klausel verwendet geöffnet werden.  
  
 Wenn eine Indexdatei zusammengesetzten bereits erstellt und geöffnet wurde, ausstellen INDEX mit TAG *TagName* zusammengesetzten Index-Datei ein-Tag hinzugefügt.  
  
 FÜR *lExpression*  
 Gibt eine Bedingung, bei dem nur die Datensätze, die dem Filterausdruck genügen *lExpression* stehen für die Anzeige und Zugriff; Indexschlüssel werden erstellt, in der Indexdatei nur die Datensätze mit dem Filterausdruck übereinstimmen.  
  
 Visual FoxPro-Rushmore Technologie optimiert einen INDEX... FÜR *lExpression* -Befehl, falls *lExpression* ist ein optimierbarer Ausdruck. Verwenden Sie für optimale Leistung einen optimierbaren Ausdruck in der FOR-Klausel ein.  
  
 KOMPRIMIEREN  
 Erstellt eine compact IDX-Datei.  
  
 AUFSTEIGEND  
 Gibt eine aufsteigende Reihenfolge CDX-Datei an. Standardmäßig werden CDX Tags in aufsteigender Reihenfolge erstellt. (Sie können als Erinnerung an die Indexdatei Reihenfolge AUFSTEIGEND einschließen.) Eine Tabelle kann in umgekehrter Reihenfolge dazu ABSTEIGEND indiziert werden.  
  
 ABSTEIGEND  
 Gibt eine absteigende Sortierreihenfolge für die CDX-Datei an. Wenn IDX Indexdateien erstellen, können Sie keine ABSTEIGEND einschließen.  
  
 UNIQUE  
 Gibt an, dass nur der erste Datensatz gefunden, die mit einem bestimmten Index-Schlüsselwert in einer IDX-Datei oder ein Tag CDX enthalten ist. UNIQUE kann verwendet werden, um die Anzeige von oder Zugriff auf doppelte Datensätze zu verhindern. Alle Datensätze mit Doppelte Indexschlüssel hinzugefügt werden die Indexdatei ausgeschlossen. Mit der EINDEUTIGEN INDEX-Option entspricht dem Ausführen von SET UNIQUE ON vor dem Ausstellen von Index- oder REINDEX.  
  
 Wenn ein EINDEUTIGER Index oder der Indexname aktiv ist, und ein doppelter Datensatz in einer Weise, die die Indexschlüssel ändert geändert wird, wird der Index oder Indexname aktualisiert. Allerdings kann nicht der nächste doppelten Datensatz mit dem ursprünglichen Indexschlüssel zugegriffen oder angezeigt, bis Sie die Datei mit REINDEX Neuindizieren.  
  
 KANDIDAT  
 Erstellt eine strukturelle Indexname geeignet. Das Schlüsselwort CANDIDATE kann eingeschlossen werden nur beim Erstellen einer strukturellen Indexname; andernfalls generiert der Visual FoxPro eine Fehlermeldung angezeigt.  
  
 Ein Kandidat Indexname wird verhindert, dass doppelte Werte in das Feld oder eine Kombination von Feldern, die in den Indexausdruck angegebenen *eExpression*. Der Begriff *Candidate* bezieht sich auf den Typ des Indexes; da kandidatenindizes doppelte Werte verhindert wird, sie infrage kommt als "Kandidat" einen primären Index.  
  
 Visual FoxPro generiert einen Fehler, wenn Sie erstellen ein Kandidat Index Tag für ein Feld oder eine Kombination von Feldern, die bereits doppelte Werte enthält.  
  
 ADDITIVE  
 Behält alle zuvor geöffneten Indexdateien zu öffnen. Wenn Sie die ADDITIVE-Klausel weglassen, wenn Sie eine Indexdatei oder Dateien für eine Tabelle mit dem INDEX erstellen, werden alle zuvor geöffneten Indexdateien (mit Ausnahme der strukturellen zusammengesetzter Index) geschlossen.  
  
## <a name="remarks"></a>Hinweise  
 Datensätze in eine Tabelle mit einer Indexdatei werden angezeigt und in der Reihenfolge gemäß den Indexausdruck zugegriffen wird. Die physische Reihenfolge der Datensätze in der Tabelle wird nicht durch eine Indexdatei geändert.  
  
## <a name="index-types"></a>Indextypen  
 Visual FoxPro können Sie zwei Arten von Indexdateien erstellen:  
  
-   Zusammengesetzte CDX Indexdateien, enthält mehrere Indexeinträge genannter tags  
  
-   IDX-Indexdateien, enthält einen Indexeintrag  
  
 Sie können auch eine Indexdatei strukturellen zusammengesetzten erstellen, die mit der Tabelle automatisch geöffnet wird.  
  
> [!NOTE]  
>  Da die strukturellen zusammengesetzten Indexdateien automatisch geöffnet werden, wenn die Tabelle geöffnet wird, sind sie der bevorzugte Indextyp an.  
  
 Schließen Sie COMPACT compact IDX Indexdateien erstellen. Zusammengesetzte Indexdateien sind immer compact.  
  
## <a name="index-order-and-updating"></a>Indexreihenfolge und aktualisieren  
 Nur eine (die Indexdatei Masterindex) oder Tag (Tag master) steuert die Reihenfolge, in der die Tabelle oder zugegriffen wird. Bestimmte Befehle (z. B. SEEK) mithilfe der Masterindex-Datei oder der Tag um nach Datensätzen zu suchen. Allerdings alle geöffneten IDX und CDX Indexdateien werden aktualisiert, wenn Änderungen an der Tabelle vorgenommen werden.  
  
## <a name="user-defined-functions"></a>Benutzerdefinierte Funktionen  
 Obwohl ein Indexausdruck eine benutzerdefinierte Funktion enthalten kann, sollten Sie nicht von benutzerdefinierten Funktionen in einem Indexausdruck verwenden. Benutzerdefinierte Funktionen in einem Indexausdruck Erhöhen der Zeitaufwand zum Erstellen oder aktualisieren den Index. Darüber hinaus auftreten indexupdates nicht, wenn eine benutzerdefinierte Funktion für einen Indexausdruck verwendet wird.  
  
 Wenn Sie eine benutzerdefinierte Funktion in einem Indexausdruck verwenden, muss Visual FoxPro der User-defined Function, suchen können. Wenn Visual FoxPro einen Index erstellt, der Indexausdruck wird in die Indexdatei gespeichert, sondern lediglich ein Verweis auf die benutzerdefinierte Funktion im Indexausdruck enthalten.  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE - SQL-Befehl](../../odbc/microsoft/alter-table-sql-command.md)   
 [Löschen Sie die TAG-Befehl](../../odbc/microsoft/delete-tag-command.md)   
 [SET COLLATE-Befehl](../../odbc/microsoft/set-collate-command.md)   
 [Befehl SET UNIQUE](../../odbc/microsoft/set-unique-command.md)
