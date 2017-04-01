---
title: "Arbeiten mit &#196;nderungsdaten (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Änderungsdaten [SQL Server]"
  - "Change Data Capture [SQL Server], Szenarien für die Abfragefunktion"
  - "Change Data Capture [SQL Server], LSN-Grenzwerte"
  - "Change Data Capture [SQL Server], Abfragefunktionen"
ms.assetid: 5346b852-1af8-4080-b278-12efb9b735eb
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# Arbeiten mit &#196;nderungsdaten (SQL Server)
  Änderungsdaten werden über Tabellenwertfunktionen (Table Valued Function, TVF) für Change Data Capture-Consumer verfügbar gemacht. Für alle Abfragen dieser Funktionen sind zwei Parameter erforderlich, um den Bereich der Protokollfolgenummern (Log Sequence Number, LSN) zu definieren, die bei der Entwicklung des zurückgegebenen Resultsets ausgewählt werden können. Sowohl der untere als auch der obere LSN-Wert, die das Intervall begrenzen, werden in das Intervall eingeschlossen.  
  
 Zur Unterstützung bei der Ermittlung der geeigneten LSN-Werte für die Abfrage einer TVF stehen mehrere Funktionen zur Verfügung. Die Funktion [sys.fn_cdc_get_min_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md) gibt die kleinste LSN des Gültigkeitsintervalls einer Aufzeichnungsinstanz zurück. Beim Gültigkeitsintervall handelt es sich um das Zeitintervall, in dem Änderungsdaten aktuell für Aufzeichnungsinstanzen verfügbar sind. Die Funktion [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) gibt die größte LSN im Gültigkeitsintervall zurück. Mit den Funktionen [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) und [sys.fn_cdc_map_lsn_to_time](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md) können LSN-Werte auf einer konventionellen Zeitachse dargestellt werden. Da Change Data Capture geschlossene Abfrageintervalle verwendet, ist es in einigen Fällen erforderlich, den nächsten LSN-Wert in einer Folge zu generieren, um sicherzustellen, dass Änderungen in aufeinander folgenden Abfragefenstern nicht doppelt vorkommen. Die Funktionen [sys.fn_cdc_increment_lsn](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md) und [sys.fn_cdc_decrement_lsn](../../relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql.md) sind nützlich, wenn ein LSN-Wert inkrementell angepasst werden soll.  
  
##  <a name="LSN"></a> Überprüfen von LSN-Grenzwerten  
 Es wird empfohlen, die LSN-Grenzwerte zu überprüfen, bevor sie in einer TVF-Abfrage verwendet werden. Bei NULL-Endpunkten oder Endpunkten, die außerhalb des Gültigkeitsintervalls einer Aufzeichnungsinstanz liegen, gibt eine Change Data Capture-TVF einen Fehler zurück.  
  
 Beispielsweise wird der folgende Fehler für alle Änderungen einer Abfrage zurückgegeben, wenn ein das Abfrageintervall definierender Parameter ungültig ist, außerhalb des gültigen Bereichs liegt oder die Zeilenfilteroption ungültig ist.  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_all_changes_ ...`  
  
 Für eine **net changes** -Abfrage wird der folgende entsprechende Fehler zurückgegeben:  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_net_changes_ ...`  
  
> [!NOTE]  
>  Es ist uns bekannt, dass die Meldung 313 irreführend ist und die eigentliche Ursache des Fehlers nicht wiedergibt. Der Grund für diese umständliche Verwendung ist, dass aus einer TVF kein expliziter Fehler ausgelöst werden kann. Es wurde jedoch als sinnvoller erachtet, den Wert einer erkennbaren, wenn auch nicht aussagekräftigen Fehlermeldung zurückzugeben als ein leeres Ergebnis. Ein leeres Resultset wäre von einer gültigen Abfrage nicht unterscheidbar, die keine Änderungen zurückgibt.  
  
 Bei der Abfrage aller Änderungen werden bei Autorisierungsfehlern Fehlermeldungen zurückgegeben, wie z. B. folgende:  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object 'fn_cdc_get_all_changes_...', database 'MyDB', schema 'cdc'.`  
  
 Dasselbe gilt für Abfragen von Nettoänderungen:  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object fn_cdc_get_net_changes_...', database 'MyDB', schema 'cdc'.`  
  
 Die Vorlage "Enumerate Net Changes Using TRY CATCH" zeigt, wie Sie diese bekannten TVF-Fehler abfangen und aussagekräftigere Fehlerinformationen zurückgeben können.  
  
> [!NOTE]  
>  Um Change Data Capture-Vorlagen in SQL Server Management Studio aufzurufen, öffnen Sie das Menü **Ansicht**, klicken Sie auf **Vorlagen-Explorer**, erweitern Sie **SQL Server-Vorlagen**, und erweitern Sie anschließend den Ordner **Change Data Capture**.  
  
##  <a name="Functions"></a> Abfragefunktionen  
 Abhängig von den Eigenschaften der nachverfolgten Quelltabelle und der Konfiguration der Aufzeichnungsinstanz werden entweder eine oder zwei TVFs für die Abfrage von Änderungsdaten generiert.  
  
-   Die Funktion [cdc.fn_cdc_get_all_changes_<capture_instance>](../Topic/cdc.fn_cdc_get_all_changes_%3Ccapture_instance%3E%20%20\(Transact-SQL\).md) gibt alle Änderungen zurück, die für das angegebene Intervall aufgetreten sind. Diese Funktion wird immer generiert. Die zurückgegebenen Einträge werden immer sortiert, zunächst nach der LSN des Transaktionscommits der Änderung und dann nach einem Wert, mit dem innerhalb der Transaktion eine Reihenfolge für die Änderung festgelegt wird. Abhängig von der gewählten Zeilenfilteroption werden bei Updates die Endzeile (Zeilenfilteroption "all") oder der neue und der alte Wert (Zeilenfilteroption "all update old") zurückgegeben.  
  
-   Die Funktion [cdc.fn_cdc_get_net_changes_<capture_instance>](../Topic/cdc.fn_cdc_get_net_changes_%3Ccapture_instance%3E%20\(Transact-SQL\).md) wird generiert, wenn der @supports_net_changes-Parameter bei aktivierter Quelltabelle auf den Wert 1 festgelegt wird.  
  
    > [!NOTE]  
    >  Diese Option wird nur unterstützt, wenn für die Quelltabelle ein Primärschlüssel definiert ist, oder wenn der Parameter @index_name zur Identifizierung eines eindeutigen Indexes verwendet wurde.  
  
     Die **netchanges**-Funktion gibt eine Änderung pro geänderte Quelltabellenzeile zurück. Wenn im angegebenen Intervall mehrere Änderungen für die Zeile aufgezeichnet wurden, geben die Spaltenwerte den endgültigen Inhalt der Zeile wieder. Zur korrekten Ermittlung des Vorgangs, der für das Update der Zielumgebung erforderlich ist, muss die TVF sowohl den Anfangsvorgang als auch den Endvorgang für die Zeile berücksichtigen. Wird die Zeilenfilteroption „all“ angegeben, umfassen die von der **net changes**-Abfrage zurückgegebenen Vorgänge entweder Einfüge-, Lösch- oder Aktualisierungsvorgänge (neue Werte). Diese Option gibt die Updatemaske immer als NULL zurück, da mit der Berechnung einer aggregierten Maske ein gewisser Aufwand verbunden ist. Wenn Sie eine aggregierte Maske benötigen, die alle Änderungen einer Zeile wiedergibt, verwenden Sie die Option 'all with mask'. Wenn für die Downstreamverarbeitung die Unterscheidung zwischen Einfüge- und Updatevorgängen nicht erforderlich ist, verwenden Sie die Option 'all with merge'. In diesem Fall ist der Vorgangswert auf zwei Werte festgelegt: 1 für einen Löschvorgang und 5 für einen Vorgang, der ein Einfüge- oder ein Updatevorgang sein kann. Diese Option vermeidet den zusätzlichen Aufwand, der notwendig ist, um zu ermitteln, ob der abgeleitete Vorgang ein Einfüge- oder ein Updatevorgang sein sollte. Die Leistung der Abfrage kann steigen, wenn diese Unterscheidung nicht notwendig ist.  
  
 Die von einer Abfragefunktion zurückgegebene Updatemaske ist eine kompakte Darstellung aller mit einer Zeile der Änderungsdaten verbundenen Spaltenänderungen. In der Regel werden diese Informationen nur für eine kleine Teilmenge der aufgezeichneten Spalten benötigt. Es stehen Funktionen zur Verfügung, die helfen, Informationen aus der Maske in einer Form zu extrahieren, die direkt von Anwendungen verwendet werden kann. Die Funktion [sys.fn_cdc_get_column_ordinal](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md) gibt die Ordnungsposition einer benannten Spalte für eine gegebene Aufzeichnungsinstanz zurück, während die Funktion [sys.fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md) die Parität des Bits in der angegebenen Maske zurückgibt, basierend auf der Ordnungsposition, die im Funktionsaufruf übergeben wurde. Zusammen ermöglichen diese Funktionen, Informationen effizient aus der Updatemaske zu extrahieren und sie mit der Anforderung von Änderungsdaten zurückzugeben. Die Verwendung dieser Funktionen wird in der Vorlage "Enumerate Net Changes Using All With Mask" veranschaulicht.  
  
##  <a name="Scenarios"></a> Szenarios für Abfragefunktionen  
 In den folgenden Abschnitten werden häufige Szenarios für die Abfrage von Change Data Capture-Daten beschrieben, die die Verwendung der Abfragefunktionen "cdc.fn_cdc_get_all_changes_<capture_instance>" und "cdc.fn_cdc_get_net_changes_<capture_instance>" erläutern.  
  
### Abfragen aller Änderungen im Gültigkeitsintervall der Aufzeichnungsinstanz  
 Das einfachste Anforderungsszenario für Änderungsdaten ist die Rückgabe aller aktuellen Änderungsdaten im Gültigkeitsintervall einer Aufzeichnungsinstanz. Bestimmen Sie für eine solche Anforderung zuerst die unteren und oberen LSN-Grenzwerte des Gültigkeitsintervalls. Verwenden Sie anschließend diese Werte, um die Parameter @from_lsn und @to_lsn zu ermitteln, die an die Abfragefunktion "cdc.fn_cdc_get_all_changes_<capture_instance>" oder "cdc.fn_cdc_get_net_changes_<capture_instance>" übergeben werden. Verwenden Sie die Funktion [sys.fn_cdc_get_min_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md), um die Untergrenze zu erhalten, und [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md), um die Obergrenze zu erhalten. Die Vorlage "Enumerate All Changes for the Valid Range" enthält einen Beispielcode zum Abfragen aller aktuellen, gültigen Änderungen mit der Abfragefunktion "cdc.fn_cdc_get_all_changes_<capture_instance>". Die Vorlage "Enumerate Net Changes for the Valid Range" enthält ein ähnliches Beispiel zur Verwendung der Abfragefunktion "cdc.fn_cdc_get_net_changes_<capture_instance>".  
  
### Abfragen aller neuen Änderungen seit dem letzten Änderungssatz  
 In vielen Anwendungen werden Änderungsdaten regelmäßig oder ständig abgefragt, sodass periodisch alle Änderungen seit der letzten Anforderung abgefragt werden. Für solche Abfragen können Sie die Funktion [sys.fn_cdc_increment_lsn](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md) verwenden, die die untere Grenze der aktuellen Abfrage aus der oberen Grenze der vorhergehenden Abfrage herleitet. Mit dieser Methode wird gewährleistet, dass Zeilen nicht wiederholt werden, da das Abfrageintervall immer als geschlossenes Intervall behandelt wird, bei dem beide Endpunkte in das Intervall eingeschlossen sind. Verwenden Sie anschließend die Funktion [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md), um den oberen Endpunkt für das neue Anforderungsintervall zu erhalten. Die Vorlage "Enumerate All Changes Since Previous Request" beinhaltet einen Beispielcode, mit dem das Abfragefenster systematisch verschoben wird, um alle Änderungen seit der letzten Anforderung abzurufen.  
  
### Abfragen aller neuen Änderungen bis zum jetzigen Zeitpunkt  
 Eine typische Einschränkung beim Zurückgeben von Änderungen mit einer Abfragefunktion ist es, nur die Änderungen einzubeziehen, die zwischen der vorhergehenden Anforderung und der aktuellen Uhrzeit und dem aktuellen Datum aufgetreten sind. Für eine solche Abfrage können Sie die Funktion "sys.fn_cdc_increment_lsn" auf den Wert @from_lsn aus der vorhergehenden Anforderung anwenden, um die untere Grenze zu ermitteln. Da die obere Grenze des Zeitintervalls als spezifischer Zeitpunkt angegeben wird, muss dieser Wert vor der Verwendung in einer Abfragefunktion in einen LSN-Wert umgewandelt werden. Bevor der datetime-Wert in einen entsprechenden LSN-Wert umgewandelt werden kann, müssen Sie sicherstellen, dass der Aufzeichnungsprozess alle Änderungen verarbeitet hat, für die mit der angegebenen oberen Grenze ein Commit ausgeführt wurde. Dies ist erforderlich, um zu gewährleisten, dass alle qualifizierenden Änderungen an die Änderungstabelle weitergegeben wurden. Eine Möglichkeit ist das Erstellen einer Warteschleife, die regelmäßig überprüft, ob der aktuelle maximale Commit-LSN für eine der Datenbankänderungstabellen den gewünschten Endzeitpunkt des Anforderungsintervalls überschreitet.  
  
 Nachdem die Verzögerungsschleife bestätigt hat, dass der Aufzeichnungsprozess alle relevanten Protokolleinträge verarbeitet hat, können Sie die Funktion [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) verwenden, um den LSN-Wert für den neuen oberen Endpunkt zu ermitteln. Um sicherzustellen, dass alle Einträge abgerufen werden, für die in der angegebenen Zeit ein Commit ausgeführt wurde, rufen Sie die Funktion "sys.fn_cdc_map_time_to_lsn" und verwenden hierbei die Option 'largest less than or equal'.  
  
> [!NOTE]  
>  In Zeiten ohne Aktivität wird der Tabelle "cdc.lsn_time_mapping" ein Platzhaltereintrag hinzugefügt, um anzuzeigen, dass der Aufzeichnungsprozess die Änderungen bis zu einem bestimmten Commitzeitpunkt verarbeitet hat. Dies soll verhindern, dass der Eindruck entsteht, der Aufzeichnungsprozess wäre mit der Verarbeitung im Rückstand, wenn aktuell keine Änderungen zu verarbeiten sind.  
  
 Die Vorlage "Enumerate All Changes Up Until Now" veranschaulicht, wie Änderungsdaten gemäß der zuvor beschriebenen Strategie abgefragt werden können.  
  
### Hinzufügen einer Commitzeit zu einem Resultset mit allen Änderungen  
 Die Commitzeit jeder Transaktion, der ein Eintrag in einer Datenbankänderungstabelle zugeordnet ist, kann aus der Tabelle [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) abgerufen werden. Wenn der __$start_lsn-Wert, der bei einer Anforderung aller Änderungen zurückgegeben wird, mit dem start_lsn-Wert eines cdc.lsn_time_mapping-Tabelleneintrags verknüpft wird, können Sie den tran_end_time-Wert zusammen mit den Änderungsdaten zurückgeben, um die Änderung mit der Commitzeit aus der Transaktionsquelle zu kennzeichnen. Die Vorlage "Append Commit Time to All Changes Result Set" zeigt, wie Sie diesen Join ausführen können.  
  
### Verknüpfen von Änderungsdaten mit anderen Daten derselben Transaktion  
 In einigen Fällen ist es von Vorteil, Änderungsdaten mit anderen Informationen zu verknüpfen, die beim Commit in der Quelle über die Transaktion gesammelt wurden. Die tran_begin_lsn-Spalte in der cdc.lsn_time_mapping-Tabelle enthält die für einen solchen Join erforderlichen Informationen. Sobald das Update der Quelle stattfindet, muss der Wert für database_transaction_begin_lsn aus der dynamischen Systemsicht [sys.dm_tran_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md) zusammen mit allen anderen Informationen gespeichert werden, die später mit den Änderungsdaten verknüpft werden sollen. Verwenden Sie die Funktion fn_convertnumericlsntobinary, um den database_transaction_begin_lsn-Wert und den tran_begin_lsn-Wert zu vergleichen. Der Code zum Erstellen dieser Funktion ist in der Vorlage "Create Function fn_convertnumericlsntobinary" enthalten. Die Vorlage "Return All Changes with a Given tran_begin_lsn" veranschaulicht die Durchführung des Joins.  
  
### Abfragen mit Datetime-Wrapperfunktionen  
 Ein typisches Anwendungsszenario für die Abfrage von Änderungsdaten ist das periodische Anfordern von Änderungsdaten in einem gleitenden Fenster, das durch datetime-Werte definiert wird. Für diese Klasse von Consumern stellt Change Data Capture die gespeicherte Prozedur [sys.sp_cdc_generate_wrapper_function](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md) bereit, die Skripts zum Erstellen benutzerdefinierter Wrapperfunktionen für die Abfragefunktionen von Change Data Capture generiert. Mit diesen benutzerdefinierten Wrappern kann das Abfrageintervall als datetime-Paar ausgedrückt werden.  
  
 Die Aufrufoptionen für die gespeicherte Prozedur gestatten es, Wrapper für alle Aufzeichnungsinstanzen, auf die der Aufrufer Zugriff hat, oder nur für eine bestimmte Aufzeichnungsinstanz zu generieren. Mit den unterstützten Optionen kann auch angegeben werden, ob der obere Endpunkt des Aufzeichnungsintervalls offen oder geschlossen sein soll, welche der verfügbaren aufgezeichneten Spalten in das Resultset aufgenommen werden sollen und welchen der enthaltenen Spalten Updateflags zugeordnet werden sollen. Die Prozedur gibt ein Resultset mit zwei Spalten zurück: dem Namen der generierten Funktion, der vom Namen der Aufzeichnungsinstanz abgeleitet werden kann, und der Erstellungsanweisung für die gespeicherte Wrapperprozedur. Die Wrapperfunktion für die Abfrage aller Änderungen wird immer generiert. Wenn der @supports_net_changes-Parameter beim Erstellen der Aufzeichnungsinstanz festgelegt wurde, wird auch die Wrapperfunktion für die Funktion für Nettoänderungen generiert.  
  
 Der Anwendungsentwickler muss sicherstellen, dass die gespeicherte Prozedur für die Skriptgenerierung aufgerufen wird und damit die Erstellungsanweisungen für die gespeicherten Wrapperprozeduren generiert werden. Der Entwickler muss außerdem die generierten Erstellungsskripts ausführen, um die Funktionen zu erstellen. Diese Vorgänge werden beim Erstellen einer Aufzeichnungsinstanz nicht automatisch ausgeführt.  
  
 Datetime-Wrapper befinden sich im Besitz des Benutzers und werden nicht im Standardschema des Aufrufers erstellt. Die generierte Funktion ist ohne Änderungen für die meisten Benutzer geeignet. Dennoch können jederzeit weitere Anpassungen am generierten Skript vorgenommen werden, bevor die Funktion erstellt wird.  
  
 Der Name der Wrapperfunktion für die Abfrage aller Änderungen ist "fn_all_changes_", gefolgt vom Namen der Aufzeichnungsinstanz. Das Präfix, das für die Wrapperfunktion für Nettoänderungen verwendet wird, lautet "fn_net_changes_". Beide Funktionen erwarten wie die zugehörigen Change Data Capture-TVFs drei Argumente. Das Abfrageintervall für die Wrapper wird jedoch durch zwei datetime-Werte anstelle zweier LSN-Werte festgelegt. Der @row_filter_option-Parameter für beide Funktionssätze ist identisch.  
  
 Die generierten Wrapperfunktionen unterstützen die folgende Konvention zum systematischen Durchlaufen der Change Data Capture-Zeitachse: Es wird davon ausgegangen, dass der @end_time-Parameter des vorhergehenden Intervalls als @start_time-Parameter des nachfolgenden Intervalls verwendet wird. Die Wrapperfunktion übernimmt die Zuordnung der datetime-Werte zu den LSN-Werten und stellt sicher, dass keine Daten verloren gehen oder wiederholt werden, sofern diese Konvention eingehalten wird.  
  
 Beim Generieren der Wrapper kann angegeben werden, ob die Wrapper im angegebenen Abfragefenster eine geschlossene oder eine offene obere Grenze unterstützen sollen. Das heißt, der Aufrufer kann festlegen, ob Einträge mit einer Commitzeit in das Intervall aufgenommen werden sollen, die der oberen Grenze des Extrahierungsintervalls entspricht. Standardmäßig wird die Obergrenze aufgenommen.  
  
 Die generierten Abfrage-TVFs geben einen Fehler zurück, wenn ein NULL-Wert im @from_lsn-Wert oder im @to_lsn-Wert übergeben wird. Die datetime-Wrapperfunktionen geben stattdessen NULL zurück, sodass die datetime-Wrapper alle aktuellen Änderungen zurückgeben können. Wenn NULL als unterer Endpunkt des Abfragefensters an den Datetime-Wrapper übergeben wird, wird der untere Endpunkt des Gültigkeitsintervalls der Aufzeichnungsinstanz in der zugrunde liegenden SELECT-Anweisung auf die Abfrage-TVF angewendet. Wenn NULL als oberer Endpunkt des Abfragefensters übergeben wird, wird entsprechend der obere Endpunkt des Gültigkeitsintervalls der Aufzeichnungsinstanz beim Auswählen aus der Abfrage-TVF verwendet.  
  
 Das von einer Wrapperfunktion zurückgegebene Resultset beinhaltet alle angeforderten Spalten, gefolgt von einer Vorgangsspalte mit einem ein oder zwei Zeichen langen Code, der den der Zeile zugeordneten Vorgang identifiziert. Wenn Updateflags angefordert wurden, werden diese als Bitspalten nach dem Vorgangscode in der vom @update_flag_list-Parameter festgelegten Reihenfolge aufgeführt. Informationen zu den Aufrufoptionen für das Anpassen der generierten datetime-Wrapper finden Sie unter [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md).  
  
 Die Vorlage "Instantiate a Wrapper TVF With Update Flag" zeigt, wie Sie eine generierte Wrapperfunktion anpassen können, um bei einer Abfrage der Nettoänderungen dem Resultset ein Updateflag für eine angegebene Spalte hinzuzufügen. Die Vorlage "Instantiate CDC Wrapper TVFs for a Schema" zeigt, wie Sie die Datetime-Wrappers für die Abfrage-TVFs aller Aufzeichnungsinstanzen instanziieren, die für die Quelltabellen in einem bestimmten Datenbankschema erstellt wurden.  
  
 Ein Beispiel, in dem ein datetime-Wrapper zum Abfragen von Änderungsdaten verwendet wird, finden Sie in der Vorlage "Get Net Changes Using Wrapper With Update Flags". Diese Vorlage zeigt, wie Nettoänderungen mit einer Wrapperfunktion abgefragt werden, wenn der Wrapper für die Rückgabe von Aktualisierungsflags konfiguriert wurde. Beachten Sie, dass die Zeilenfilteroption 'all with mask' für die zugrunde liegende Abfragefunktion benötigt wird, um bei einem Update eine Updatemakse zurückzugeben, die nicht NULL ist. NULL-Werte werden sowohl für die untere als auch für die obere datetime-Intervallgrenze übergeben, um anzuzeigen, dass die Funktion bei der zugrunde liegenden LSN-basierten Abfrage den unteren und den oberen Endpunkt des Gültigkeitsintervalls für die Aufzeichnungsinstanz verwenden soll. Die Abfrage gibt eine Zeile für jede Änderung an einer Quellzeile zurück, die innerhalb des gültigen Bereichs der Aufzeichnungsinstanz stattgefunden hat.  
  
### Verwenden der Datetime-Wrapperfunktionen für den Übergang zwischen Aufzeichnungsinstanzen  
 Change Data Capture unterstützt bis zu zwei Aufzeichnungsinstanzen für eine einzelne verfolgte Quelltabelle. Hauptverwendungszweck für diese Funktionalität ist es, einen Übergang zwischen mehreren Aufzeichnungsinstanzen zu ermöglichen, wenn Änderungen der DDL (Data Definition Language, Datendefinitionssprache) der Quelltabelle die Anzahl der für die Verfolgung verfügbaren Spalten erweitern. Um eventuelle Änderungen in den Namen der zugrunde liegenden Abfragefunktionen auf nachfolgenden Anwendungsebenen zu verbergen, kann beim Übergang zu einer neuen Aufzeichnungsinstanz z. B. eine Wrapperfunktion für den eigentlichen Aufruf verwendet werden. Stellen Sie dann sicher, dass der Name der Wrapperfunktion immer gleich bleibt. Sobald der Übergang durchgeführt werden soll, kann die alte Wrapperfunktion gelöscht und eine neue mit demselben Namen erstellt werden, die dann auf die neuen Abfragefunktionen verweist. Indem zuerst das generierte Skript geändert wird, um eine Wrapperfunktion mit demselben Namen zu erstellen, können Sie den Wechsel zu einer neuen Aufzeichnungsinstanz durchführen, ohne dass dies Auswirkungen auf darüber liegende Anwendungsebenen hat.  
  
## Siehe auch  
 [Nachverfolgen von Datenänderungen &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [Über Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [Aktivieren und Deaktivieren von Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)   
 [Verwalten und Überwachen von Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  