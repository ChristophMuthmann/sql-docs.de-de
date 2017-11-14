---
title: Grundlegendes zu Cursortypen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4f4d3db7-4f76-450d-ab63-141237a4f034
caps.latest.revision: 51
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a65c11a0f6c623162049661a11cbc392a3d8b178
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-cursor-types"></a>Grundlegendes zu Cursortypen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Vorgänge in einer relationalen Datenbank beziehen sich immer auf eine vollständige Gruppe von Zeilen. Die von einer SELECT-Anweisung zurückgegebene Gruppe von Zeilen besteht aus allen Zeilen, die die Bedingungen der WHERE-Klausel der Anweisung erfüllen. Diese vollständige Gruppe von Zeilen, die von der Anweisung zurückgegeben wird, wird als Resultset bezeichnet. Anwendungen sind nicht immer effektiv, wenn das gesamte Resultset als eine Einheit bearbeitet wird. Diese Anwendungen benötigen einen Mechanismus, um jeweils eine Zeile oder einen kleinen Zeilenblock zu bearbeiten. Cursor sind eine Erweiterung zu Resultsets und stellen diesen Mechanismus bereit.  
  
 Cursor erweitern die Verarbeitung von Resultsets durch folgende Aktionen:  
  
-   Ermöglichen der Positionierung an bestimmten Zeilen des Resultsets.  
  
-   Abrufen einer Zeile oder eines ZeilenBlocks von der aktuellen Position im Resultset.  
  
-   Unterstützen von Datenänderungen in der Zeile an der aktuellen Position im Resultset.  
  
-   Unterstützen von unterschiedlichen Sichtbarkeitsebenen bei Änderungen, die von anderen Benutzern an den Datenbankdaten, die im Resultset dargestellt werden, ausgeführt wurden.  
  
> [!NOTE]  
>  Eine vollständige Beschreibung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Cursortypen finden Sie im Thema "Cursortypen (Datenbankmodul)" in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
 Die JDBC-Spezifikation stellt Unterstützung für Vorwärtscursor und scrollfähige Cursor bereit, die Änderungen durch andere Aufträge berücksichtigen oder nicht berücksichtigen können und schreibgeschützt oder aktualisierbar sein können. Diese Funktionalität wird bereitgestellt, indem Sie die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Klasse.  
  
## <a name="remarks"></a>Hinweise  
 Der JDBC-Treiber unterstützt die folgenden Cursortypen:  
  
|Resultset<br /><br /> (Cursor) Typ|SQL Server-Cursortyp|Merkmale|select<br /><br /> Methode|Antwort<br /><br /> Pufferung|Description|  
|------------------------------------|----------------------------|---------------------|-----------------------|----------------------------|-----------------|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|–|Vorwärtscursor, schreibgeschützt|Direkte|Volle|Die Anwendung muss ein Pass-Through (vorwärts) für das Resultset ausführen. Dies ist das Standardverhalten und entspricht einem TYPE_SS_DIRECT_FORWARD_ONLY-Cursor. Der Treiber liest das gesamte Resultset während der Ausführung der Anweisung aus dem Server in einen Speicher.|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|–|Vorwärtscursor, schreibgeschützt|Direkte|adaptive|Die Anwendung muss ein Pass-Through (vorwärts) für das Resultset ausführen. Das Verhalten entspricht dem Verhalten eines TYPE_SS_DIRECT_FORWARD_ONLY-Cursors. Der Treiber liest Zeilen vom Server, wenn die Anwendung sie anfordert, und minimiert so die Speicherauslastung auf Clientseite.|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|Schneller Vorwärtscursor|Vorwärtscursor, schreibgeschützt|cursor|–|Die Anwendung muss mithilfe eines Servercursors ein Pass-Through (vorwärts) für das Resultset ausführen. Das Verhalten entspricht dem Verhalten eines TYPE_SS_SERVER_CURSOR_FORWARD_ONLY-Cursors.<br /><br /> Zeilen werden in durch die Abrufgröße angegebene Blöcke vom Server abgerufen.|  
|TYPE_FORWARD_ONLY (CONCUR_UPDATABLE)|Dynamisch (Vorwärtscursor)|Vorwärtscursor, aktualisierbar|–|–|Die Anwendung muss ein Pass-Through (vorwärts) für das Resultset ausführen, um eine oder mehrere Zeilen zu aktualisieren.<br /><br /> Zeilen werden in durch die Abrufgröße angegebene Blöcke vom Server abgerufen.<br /><br /> Standardmäßig ist die Abrufgröße festgelegt, wenn die Anwendung aufruft, die [SetFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) Methode der [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.<br /><br /> **Hinweis:** der JDBC-Treiber bietet eine Funktion für adaptive Pufferung, die Sie zum Abrufen der Ergebnisse von ermöglicht die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ab, wenn die Anwendung benötigt, anstatt alle auf einmal abzurufen. Wenn die Anwendung beispielsweise eine große Datenmenge abrufen muss, für die der Anwendungsspeicher nicht ausreicht, kann die Clientanwendung den Wert mithilfe der adaptiven Pufferung als Datenstrom abrufen. Das Standardverhalten des Treibers ist "**adaptive**". Um die adaptive Pufferung für das nur vorwärts aktualisierbare Resultset mit Vorwärtscursor, die Anwendung muss jedoch explizit aufrufen, die [SetResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) Methode der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt durch die Bereitstellung einer **Zeichenfolge** Wert "**adaptive"**. Beispielcode finden Sie unter [große Datenbeispiel aktualisieren](../../connect/jdbc/updating-large-data-sample.md).|  
|TYPE_SCROLL_INSENSITIVE|STATIC-Cursor|Scrollfähig, nicht aktualisierbar<br /><br /> Externe Zeilenupdates, -einfügungen und -löschvorgänge sind nicht sichtbar.|N/V|–|Die Anwendung erfordert eine Datenbankmomentaufnahme. Das Resultset kann nicht aktualisiert werden. Nur CONCUR_READ_ONLY wird unterstützt.  Alle anderen Parallelitätstypen führen bei Verwendung mit diesem Cursortyp zu einer Ausnahme.<br /><br /> Zeilen werden in durch die Abrufgröße angegebene Blöcke vom Server abgerufen.|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_READ_ONLY)|Keyset|Scrollfähig, schreibgeschützt. Externe Zeilenupdates sind sichtbar, und Löschvorgänge werden als fehlende Daten angezeigt.<br /><br /> Externe Zeileneinfügungen sind nicht sichtbar.|–|–|Die Anwendung muss geänderte Daten nur für vorhandene Zeilen anzeigen.<br /><br /> Zeilen werden in durch die Abrufgröße angegebene Blöcke vom Server abgerufen.|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Keyset|Scrollfähig, aktualisierbar<br /><br /> Externe und interne Zeilenupdates sind sichtbar, Löschvorgänge werden als fehlende Daten angezeigt, und Einfügungen sind nicht sichtbar.|–|–|Die Anwendung kann Daten in den vorhandenen Zeilen ändern, mithilfe der ResultSet-Objekt. Die Anwendung muss auch die Änderungen an Zeilen, die von anderen außerhalb der ResultSet-Objekt zu sehen sein.<br /><br /> Zeilen werden in durch die Abrufgröße angegebene Blöcke vom Server abgerufen.|  
|TYPE_SS_DIRECT_FORWARD_ONLY|–|Vorwärtscursor, schreibgeschützt|–|"full" oder "adaptive"|Ganzzahliger Wert = 2003. Stellt einen schreibgeschützten clientseitigen Cursor bereit, der vollständig gepuffert wird. Es wird kein Servercursor erstellt.<br /><br /> Nur der Parallelitätstyp CONCUR_READ_ONLY wird unterstützt. Alle anderen parallelitätstypen dazu führen, dass eine Ausnahme bei Verwendung mit diesem Cursortyp.|  
|TYPE_SS_SERVER_CURSOR_FORWARD_ONLY|Schneller Vorwärtscursor|Vorwärtscursor|–|–|Ganzzahliger Wert = 2004. Schnell, greift über einen Servercursor auf alle Daten zu. Bei Verwendung mit dem Parallelitätstyp CONCUR_UPDATABLE aktualisierbar.<br /><br /> Zeilen werden in durch die Abrufgröße angegebene Blöcke vom Server abgerufen.<br /><br /> Zum Abrufen der adaptiven Pufferung in diesem Fall, muss die Anwendung explizit aufrufen der [SetResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) Methode der [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt durch Bereitstellen einer **Zeichenfolge**  Wert "**adaptive"**. Beispielcode finden Sie unter [große Datenbeispiel aktualisieren](../../connect/jdbc/updating-large-data-sample.md).|  
|TYPE_SS_SCROLL_STATIC|STATIC-Cursor|Die Updates von anderen Benutzern werden nicht reflektiert.|–|–|Ganzzahliger Wert = 1004. Die Anwendung erfordert einen Datenbanksnapshot. Dies ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]--spezifische Synonym für den JDBC TYPE_SCROLL_INSENSITIVE und weist das gleiche Verhalten der Parallelität festlegen.<br /><br /> Zeilen werden in durch die Abrufgröße angegebene Blöcke vom Server abgerufen.|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_READ_ONLY)|Keyset|Scrollfähig, schreibgeschützt Externe Zeilenupdates sind sichtbar, und Löschvorgänge werden als fehlende Daten angezeigt.<br /><br /> Externe Zeileneinfügungen sind nicht sichtbar.|–|–|Ganzzahliger Wert = 1005. Die Anwendung muss geänderte Daten nur für vorhandene Zeilen anzeigen. Dies ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]--spezifische Synonym für den JDBC TYPE_SCROLL_SENSITIVE und weist das gleiche Verhalten der Parallelität festlegen.<br /><br /> Zeilen werden in durch die Abrufgröße angegebene Blöcke vom Server abgerufen.|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Keyset|Scrollfähig, aktualisierbar<br /><br /> Externe und interne Zeilenupdates sind sichtbar, Löschvorgänge werden als fehlende Daten angezeigt, und Einfügungen sind nicht sichtbar.|–|–|Ganzzahliger Wert = 1005. Die Anwendung muss Daten ändern oder geänderte Daten für vorhandene Zeilen anzeigen. Dies ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]--spezifische Synonym für den JDBC TYPE_SCROLL_SENSITIVE und weist das gleiche Verhalten der Parallelität festlegen.<br /><br /> Zeilen werden in durch die Abrufgröße angegebene Blöcke vom Server abgerufen.|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_READ_ONLY)|Dynamic|Scrollfähig, schreibgeschützt.<br /><br /> Externe Zeilenupdates und -einfügungen werden angezeigt. Löschvorgänge werden als temporäre fehlende Daten im aktuellen Fetchpuffer angezeigt.|–|–|Ganzzahliger Wert = 1006. Die Anwendung muss geänderte Daten für vorhandene Zeilen anzeigen und eingefügte und gelöschte Zeilen während der Lebensdauer des Cursors anzeigen.<br /><br /> Zeilen werden in durch die Abrufgröße angegebene Blöcke vom Server abgerufen.|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Dynamic|Scrollfähig, aktualisierbar<br /><br /> Externe und interne Zeilenupdates und -einfügungen werden angezeigt. Löschvorgänge werden als temporäre fehlende Daten im aktuellen Fetchpuffer angezeigt.|–|–|Ganzzahliger Wert = 1006. Die Anwendung kann Daten für vorhandene Zeilen ändern oder einfügen oder Löschen von Zeilen mithilfe der ResultSet-Objekt. Die Anwendung muss auch Änderungen, einfügungen und Löschvorgänge von anderen außerhalb der ResultSet-Objekt zu sehen sein.<br /><br /> Zeilen werden in durch die Abrufgröße angegebene Blöcke vom Server abgerufen.|  
  
## <a name="cursor-positioning"></a>Cursorpositionierung  
 Die Cursor TYPE_FORWARD_ONLY, TYPE_SS_DIRECT_FORWARD_ONLY und TYPE_SS_SERVER_CURSOR_FORWARD_ONLY unterstützen nur die [Weiter](../../connect/jdbc/reference/next-method-sqlserverresultset.md) positionierungsmethode.  
  
 Der TYPE_SS_SCROLL_DYNAMIC-Cursor unterstützt nicht die [absolute](../../connect/jdbc/reference/absolute-method-sqlserverresultset.md) und [GetRow](../../connect/jdbc/reference/getrow-method-sqlserverresultset.md) Methoden. Der absolute-Methode kann durch eine Kombination von Aufrufen näherungsweise der [erste](../../connect/jdbc/reference/first-method-sqlserverresultset.md) und [relative](../../connect/jdbc/reference/relative-method-sqlserverresultset.md) Methoden für dynamic-Cursor.  
  
 Die GetRow-Methode wird von nur auf die Cursor TYPE_FORWARD_ONLY, TYPE_SS_DIRECT_FORWARD_ONLY, TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, TYPE_SS_SCROLL_KEYSET und TYPE_SS_SCROLL_STATIC unterstützt. Die GetRow-Methode mit allen Arten von Vorwärtscursor gibt die Anzahl der bisher über den Cursor gelesenen Zeilen zurück.  
  
> [!NOTE]  
>  Wenn eine Anwendung einen nicht unterstützten cursorpositionierungsaufruf oder einen nicht unterstützten Aufruf an die GetRow-Methode ausführt, eine Ausnahme mit der folgenden Meldung ausgelöst wird, "der angeforderte Vorgang wird mit diesen Cursortyp nicht unterstützt."  
  
 Nur der TYPE_SS_SCROLL_KEYSET-Cursor und der entsprechende TYPE_SCROLL_SENSITIVE-Cursor machen gelöschte Zeilen verfügbar. Wenn der Cursor in einer gelöschten Zeile positioniert ist, sind Spaltenwerte nicht verfügbar, und die [RowDeleted](../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) Methode gibt "true" zurück. Aufrufe zum Abrufen\<Typ > Methoden lösen eine Ausnahme mit der folgenden Meldung: "Kann nicht abgerufen Wert aus gelöschter Zeile". Gelöschte Zeilen können nicht aktualisiert werden. Wenn Sie versuchen, ein Update Aufrufen\<Typ > Methode für eine gelöschte Zeile eine Ausnahme mit der folgenden Meldung ausgelöst wird, "eine gelöschte Zeile kann nicht aktualisiert werden". Der TYPE_SS_SCROLL_DYNAMIC-Cursor weist dasselbe Verhalten auf, bis der Cursor aus dem aktuellen Fetchpuffer verschoben wird.  
  
 Vorwärtscursor und dynamische Cursor machen gelöschte Zeilen auf ähnliche Weise verfügbar, jedoch nur, wenn auf die Cursor weiterhin im Fetchpuffer zugegriffen werden kann. Für Vorwärtscursor ist dies relativ einfach. Bei dynamischen Cursorn ist dies komplexer, wenn die Fetchgröße größer als 1 ist. Eine Anwendung kann den Cursor in dem vom Fetchpuffer definierten Fenster vorwärts und rückwärts verschieben, die gelöschte Zeile wird jedoch nicht mehr angezeigt, wenn der ursprüngliche Fetchpuffer, in dem sie aktualisiert wurde, verlassen wird. Wenn eine Anwendung keine temporären gelöschten Zeilen mithilfe von dynamischen Cursorn anzeigen soll, sollte eine Fetchrelative (0) verwendet werden.  
  
 Wenn die Schlüsselwerte einer TYPE_SS_SCROLL_KEYSET-Cursorzeile oder einer TYPE_SCROLL_SENSITIVE-Cursorzeile mit dem Cursor aktualisiert werden, behält die Zeile die ursprüngliche Position im Resultset bei, unabhängig davon, ob die aktualisierte Zeile die Auswahlkriterien des Cursors erfüllt. Wenn die Zeile außerhalb des Cursors aktualisiert wurde, wird eine gelöschte Zeile an der ursprünglichen Position der Zeile angezeigt, die Zeile wird jedoch nur im Cursor angezeigt, wenn eine andere Zeile mit den neuen Schlüsselwerten im Cursor vorhanden war, aber anschließend gelöscht wurde.  
  
 Bei dynamischen Cursorn behalten aktualisierte Zeilen ihre Position im Fetchpuffer bei, bis das vom Fetchpuffer definierte Fenster verlassen wird. Aktualisierte Zeilen werden möglicherweise anschließend an anderen Positionen im Resultset erneut angezeigt oder überhaupt nicht mehr angezeigt. In Anwendungen, in denen temporäre Inkonsistenzen im Resultset vermieden werden sollen, sollte eine Fetchgröße von 1 verwendet werden. (Der Standardwert beträgt 8 Zeilen bei CONCUR_SS_SCROLL_LOCKS-Parallelität und 128 Zeilen bei anderen Parallelitäten.)  
  
## <a name="cursor-conversion"></a>Cursorkonvertierung  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]kann in einigen Fällen einen Cursortyp als der angeforderte implementiert, dies wird als implizite cursorkonvertierung (oder cursordegradierung) bezeichnet. Weitere Informationen zur impliziten cursorkonvertierung finden Sie unter dem Thema "Verwenden impliziter Cursorkonvertierungen" in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
 Mit [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], bei der Aktualisierung der Daten über das Ergebnis ResultSet.TYPE_SCROLL_SENSITIVE und ResultSet.CONCUR_UPDATABLE festgelegt, wird eine Ausnahme mit einer Meldung "der Cursor ist schreibgeschützt," ausgelöst. Diese Ausnahme tritt auf, weil die [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)] verfügt über eine implizite cursorkonvertierung für das Resultset ausgeführt und den aktualisierbaren Cursor, der angefordert wurde, hat nicht zurückgegeben.  
  
 Um dieses Problem zu umgehen, können Sie eine der folgenden Lösungen auswählen:  
  
-   Stellen Sie sicher, dass die zugrunde liegende Tabelle einen Primärschlüssel aufweist.  
  
-   Verwendung [Type_ss_scroll_dynamic](../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md) statt ResultSet.TYPE_SCROLL_SENSITIVE beim Erstellen einer Anweisung.  
  
## <a name="cursor-updating"></a>Cursoraktualisierung  
 Ersetzungsupdates werden bei Cursorn unterstützt, bei denen Cursortyp und Parallelität Updates unterstützen. Wenn der Cursor nicht in einer aktualisierbaren Zeile im Resultset positioniert ist (keine Get\<Typ >-Methodenaufruf erfolgreich), einen Aufruf von einem Update\<Typ > Methode löst eine Ausnahme mit der Meldung, "das Resultset verfügt über keine aktuelle Zeile." Die JDBC-Spezifikation gibt an, dass eine Ausnahme ausgelöst wird, wenn eine Updatemethode für eine Spalte eines CONCUR_READ_ONLY-Cursors aufgerufen wird. In Situationen, in denen die Zeile kann nicht aktualisiert werden, z. B. aufgrund eines Konflikts der vollständigen Parallelität z. B. einen konkurrierenden Aktualisierungs- oder Löschvorgang, der die Ausnahme nicht bis zum auftreten kann [InsertRow](../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md), [UpdateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md), oder [DeleteRow](../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md) aufgerufen wird.  
  
 Nach einem Aufruf von update\<Typ >, die betreffende Spalte kann nicht zugegriffen werden, indem Sie Get\<Typ > bis UpdateRow oder [CancelRowUpdates](../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md) aufgerufen wurde. So werden Probleme vermieden, wenn eine Spalte durch einen anderen Typ als den vom Server zurückgegebenen Typ aktualisiert wird und folgende Abrufaufrufe clientseitige Typkonvertierungen aufrufen könnten, die ungenaue Ergebnisse liefern. Aufrufe zum Abrufen\<Typ > löst eine Ausnahme mit der Meldung "aktualisierte Spalten können nicht zugegriffen werden, bis updateRow() oder cancelRowUpdates() aufgerufen wurde."  
  
> [!NOTE]  
>  Wenn die UpdateRow-Methode aufgerufen wird, wenn keine Spalten aktualisiert wurden, löst der JDBC-Treiber eine Ausnahme mit der Meldung, "updateRow() aufgerufen, wenn keine Spalten aktualisiert wurden."  
  
 Nach dem [MoveToInsertRow](../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) wurde aufgerufen, eine Ausnahme wird ausgelöst, wenn andere Methode als abrufen\<Typ >, aktualisieren\<Typ >, InsertRow, und cursorpositionierungsmethoden (einschließlich [ MoveToCurrentRow](../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md)) für das Resultset aufgerufen werden. Die MoveToInsertRow-Methode effektiv versetzt das Resultset, die in den Einfügemodus, und cursorpositionierungsmethoden beenden den Einfügemodus. Relative cursorpositionierungsaufrufe verschieben den Cursor relativ zur Position, der er zu war, bevor MoveToInsertRow aufgerufen wurde. Nach Cursorpositionierungsaufrufen wird die Zielcursorposition die neue Cursorposition.  
  
 Wenn der cursorpositionierungsaufruf Aufruf erfolgt im Einfügemodus nicht erfolgreich ist, die Cursorposition nach Abschluss der fehlgeschlagene Aufrufe der ursprüngliche Cursorposition vor dem MoveToInsetRow aufgerufen wurde. Wenn InsertRow ein Fehler auftritt, der Cursor in der Einfügezeile bleibt, und der Cursor im bleibt Einfügemodus.  
  
 Spalten in der Einfügezeile befinden sich anfänglich in einem nicht initialisierten Status. Aufrufe an das Update\<Typ >-Methode Festlegen der Spaltenstatus auf initialisiert. Ein Aufruf von Get\<Typ > Methode für eine nicht initialisierte Spalte löst eine Ausnahme aus. Ein Aufruf an die InsertRow-Methode gibt alle Spalten in der Einfügezeile in einem nicht initialisierten Status zurück.  
  
 Wenn alle Spalten nicht initialisiert werden, wenn InsertRow-Methode aufgerufen wird, wird der Standardwert für die Spalte eingefügt. Wenn kein Standardwert vorhanden ist, die Spalte jedoch auf NULL festgelegt werden kann, wird NULL eingefügt. Wenn kein Standardwert vorhanden ist und die Spalte nicht auf NULL festgelegt werden kann, gibt der Server einen Fehler zurück, und es wird eine Ausnahme ausgelöst.  
  
> [!NOTE]  
>  Aufrufe der GetRow-Methode im Einfügemodus 0 zurück.  
>   
>  Der JDBC-Treiber unterstützt keine positionierten Updates oder Löschvorgänge. Gemäß der JDBC-Spezifikation die [SetCursorName](../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md) Methode hat keine Auswirkungen und die [GetCursorName](../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md) Methode löst eine Ausnahme aus, wenn Sie aufgerufen wird.  
>   
>  Schreibgeschützte und statische Cursor können nie aktualisiert werden.  
>   
>  SQL Server schränkt Servercursor auf ein einziges Resultset ein. Wenn ein Batch oder eine gespeicherte Prozedur mehrere Anweisungen enthält, muss ein schreibgeschützter Vorwärtsclientcursor verwendet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Resultsets mit dem JDBC-Treiber legt diese fest](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  

