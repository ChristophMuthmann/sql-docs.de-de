---
title: "Oracle CDC-Datenbanken | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a96486e9-f79b-4b24-bfaf-56203dd0e435
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 17
---
# Oracle CDC-Datenbanken
  Eine Oracle CDC-Instanz wird einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank mit dem gleichen Namen auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz zugeordnet. Diese Datenbank wird als Oracle CDC-Datenbank (oder kurz CDC-Datenbank) bezeichnet.  
  
 Die CDC-Datenbank wird mit der Oracle CDC Designer Console erstellt und konfiguriert und enthält die folgenden Elemente:  
  
-   Ein `cdc` -Schema, das erstellt wird, indem die Datenbank für SQL Server CDC aktiviert wird.  
  
-   Ein Satz von **cdc.xdbcdc_xxxx** -Tabellen, die von der Oracle CDC-Instanz verwendet werden.  
  
-   Ein Satz leerer Spiegeltabellen mit den Definitionen der aufgezeichneten Tabellen in der Oracle-Quelldatenbank.  
  
-   Einen Satz von Änderungstabellen und Änderungszugriffsfunktionen, die vom SQL Server CDC-Mechanismus generiert werden und identisch mit den Elementen sind, die beim normalen SQL Server CDC-Vorgang (nicht Oracle) verwendet werden.  
  
 Anfänglich können nur die Mitglieder der festen Datenbankrolle `cdc` dbowner **auf das** -Schema zugreifen. Der Zugriff auf die Änderungstabellen und Änderungsfunktionen wird über das gleiche Sicherheitsmodell wie für SQL Server CDC gesteuert. Weitere Informationen zum Sicherheitsmodell finden Sie unter [Sicherheitsmodell](http://go.microsoft.com/fwlink/?LinkId=231151).  
  
## <a name="creating-the-cdc-database"></a>Erstellen der CDC-Datenbank  
 In den meisten Fällen wird die CDC-Datenbank über die CDC Designer Console erstellt, aber sie kann auch mithilfe eines CDC-Bereitstellungsskripts erstellt werden, das mit der CDC Designer Console generiert wird. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemadministrator kann die Datenbankeinstellungen bei Bedarf ändern (z. B. in Bezug auf Speicherung, Sicherheit oder Verfügbarkeit).  
  
 Weitere Informationen zum Erstellen der Datenbanktabellen und der erforderlichen Skripts mithilfe der CDC Designer Console finden Sie unter [Verwenden des Assistenten für neue Instanzen](../../integration-services/change-data-capture/use-the-new-instance-wizard.md).  
  
## <a name="cdc-database-user-roles"></a>Rollen von CDC-Datenbankbenutzern  
 Wenn eine CDC-Datenbank erstellt und für CDC aktiviert wird, wird in der CDC-Datenbank ein Datenbankbenutzer mit dem Namen **cdc_service** erstellt und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung zugeordnet, mit der der Oracle CDC Service konfiguriert wurde. Dieser Benutzer wird zum Mitglied der Datenbankrollen **db_datareader**, **db_datawriter**und **db_ddladmin** gemacht. Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung auch dem `dbo` -Benutzer zugeordnet ist, wird der **cdc_service** nicht erstellt.  
  
 Diese Rollenzuweisung ermöglicht es dem Oracle CDC Service, die Tabellen unter dem `cdc` -Schema mit aufgezeichneten Daten und Steuerinformationen zu aktualisieren.  
  
 Wenn eine CDC-Datenbank erstellt wird und Oracle CDC-Quelltabellen eingerichtet werden, kann der CDC-Datenbankbesitzer die SELECT-Berechtigung für Spiegeltabellen gewähren und SQL Server CDC-Gatingrollen definieren, um zu steuern, welche Benutzer auf die Änderungsdaten zugreifen können.  
  
## <a name="mirror-tables"></a>Spiegeltabellen  
 Für jede aufgezeichnete Tabelle der Form <Schemaname>.<Tabellenname> in der Oracle-Quelldatenbank wird in der CDC-Datenbank eine ähnliche leere Tabelle erstellt, die das gleiche Schema und den gleichen Tabellennamen aufweist. Oracle-Quelltabellen mit dem Schemanamen `cdc` (Groß-/Kleinschreibung nicht berücksichtigt) können nicht aufgezeichnet werden, da das Schema `cdc` unter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die SQL Server CDC reserviert ist.  
  
 Die Spiegeltabellen sind leer. Darin werden keine Daten gespeichert. Sie werden verwendet, um die standardmäßige SQL Server CDC-Infrastruktur zu aktivieren, die von der Oracle CDC-Instanz verwendet wird. Um zu verhindern, dass Daten in die Spiegeltabellen eingefügt oder darin aktualisiert werden, werden alle UPDATE-, DELETE- und INSERT-Vorgänge für PUBLIC verweigert. Dadurch wird sichergestellt, dass die Daten nicht geändert werden können.  
  
## <a name="access-to-change-data"></a>Zugreifen auf Änderungsdaten  
 Aufgrund des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherheitsmodells, das zur Erlangung des Zugriffs auf die Änderungsdaten verwendet wird, die einer Aufzeichnungsinstanz zugeordnet sind, muss dem Benutzer der `select` -Zugriff auf alle aufgezeichneten Spalten der zugeordneten Spiegeltabelle gewährt werden (Zugriffsberechtigungen für die ursprünglichen Oracle-Tabellen bieten keinen Zugriff auf die Änderungstabellen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Informationen zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherheitsmodell finden Sie unter [Sicherheitsmodell](http://go.microsoft.com/fwlink/?LinkId=231151).  
  
 Wenn bei Erstellung der Aufzeichnungsinstanz eine Gatingrolle angegeben wird, muss der Aufrufer außerdem Mitglied der angegebenen Gatingrolle sein. Andere allgemeine Change Data Capture-Funktionen für den Zugriff auf Metadaten stehen für alle Datenbankbenutzer mit der Rolle PUBLIC zur Verfügung. Der Zugriff auf die zurückgegebenen Metadaten wird jedoch in der Regel auch hier durch die Zugriffsberechtigungen auf die zugrunde liegenden Quelltabellen und die Mitgliedschaft in definierten Gatingrollen beschränkt.  
  
 Änderungsdaten können gelesen werden, indem spezielle tabellenbasierte Funktionen aufgerufen werden, die von der SQL Server CDC-Komponente beim Erstellen einer Aufzeichnungsinstanz generiert werden. Weitere Informationen zu diesen Funktionen finden Sie unter [Change Data Capture-Funktionen (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=231152).  
  
 Der Zugriff auf die CDC-Daten über die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] CDC-Quellkomponente unterliegt den gleichen Regeln.  
  
## <a name="the-cdc-database-tables"></a>CDC-Datenbanktabellen  
 In diesem Abschnitt werden die folgenden Tabellen in der CDC-Datenbank beschrieben.  
  
-   [Änderungstabellen (_CT)](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_Change_Tables_CT)  
  
-   [cdc.lsn_time_mapping](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdclsn_time_mapping)  
  
-   [cdc.xdbcdc_config](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_config)  
  
-   [cdc.xdbcdc_state](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_state)  
  
-   [cdc.xdbcdc_trace](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_trace)  
  
-   [cdc.xdbcdc_staged_transactions](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_staged_transactions)  
  
###  <a name="a-namebkmkchangetablescta-change-tables-ct"></a><a name="BKMK_Change_Tables_CT"></a> Änderungstabellen (_CT)  
 Die Änderungstabellen werden aus den Spiegeltabellen erstellt. Sie enthalten die Änderungsdaten, die in der Oracle-Datenbank aufgezeichnet werden. Die Tabellen werden nach der folgenden Konvention benannt:  
  
 **[cdc].[<Aufzeichnungsinstanz>_CT]**  
  
 Wenn die Aufzeichnung anfänglich für die Tabelle `<schema-name>.<table-name>`aktiviert ist, ist der Standardname der Aufzeichnungsinstanz `<schema-name>_<table-name>`. Der Standardname der Aufzeichnungsinstanz für die Oracle-Tabelle HR.EMPLOYEES ist z. B. HR_EMPLOYEES, und die zugeordnete Änderungstabelle ist [cdc]. [HR_EMPLOYEES_CT].  
  
 In die Aufzeichnungstabellen wird von der Oracle CDC-Instanz geschrieben. Sie werden mit speziellen Tabellenwertfunktionen gelesen, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Erstellen der Aufzeichnungsinstanz generiert werden. Beispiel: `fn_cdc_get_all_changes_HR_EMPLOYEES`. Weitere Informationen zu diesen CDC-Funktionen finden Sie unter [Change Data Capture-Funktionen (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=231152).  
  
###  <a name="a-namebkmkcdclsntimemappinga-cdclsntimemapping"></a><a name="BKMK_cdclsn_time_mapping"></a> cdc.lsn_time_mapping  
 Die Tabelle **[cdc].[lsn_time_mapping]** wird von der SQL Server-CDC-Komponente generiert. Sie wird in Verbindung mit Oracle CDC anders als sonst verwendet.  
  
 Für Oracle CDC basieren die in dieser Tabelle gespeicherten LSN-Werte auf dem Oracle System Change Number (SCN)-Wert, der der Änderung zugeordnet ist. Die ersten 6 Bytes des LSN-Werts stehen für die ursprüngliche Oracle SCN-Nummer.  
  
 In den Zeitspalten (`tran_begin_time` und `tran_end_time`) wird auch bei Verwendung von Oracle CDC die UTC-Zeit der Änderung gespeichert, und nicht die Ortszeit, wie dies bei der normalen SQL Server CDC der Fall ist. Dadurch wird sichergestellt, dass sich Sommerzeitänderungen nicht auf die unter lsn_time_mapping gespeicherten Daten auswirken.  
  
###  <a name="a-namebkmkcdcxdbcdcconfiga-cdcxdbcdcconfig"></a><a name="BKMK_cdcxdbcdc_config"></a> cdc.xdbcdc_config  
 Diese Tabelle enthält die Konfigurationsdaten für die Oracle CDC-Instanz. Sie wird mit der CDC Designer Console aktualisiert. Diese Tabelle hat nur eine Zeile.  
  
 In der folgenden Tabelle werden die Spalten der Tabelle **cdc.xdbcdc_config** beschrieben.  
  
|Element|Description|  
|----------|-----------------|  
|version|Hiermit wird die Version der CDC-Instanzkonfiguration verfolgt. Sie wird bei jeder Aktualisierung der Tabelle und bei jeder Hinzufügung einer neuen Aufzeichnungsinstanz oder Entfernung einer vorhandenen Aufzeichnungsinstanz aktualisiert.|  
|connect_string|Eine Oracle-Verbindungszeichenfolge. Ein grundlegendes Beispiel ist:<br /><br /> `<server>:<port>/<instance>` (z. B. `erp.contoso.com:1521/orcl`).<br /><br /> In der Verbindungszeichenfolge kann auch ein Oracle Net-Verbindungsdeskriptor angegeben werden, z. B. `(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp) (HOST=erp.contoso.com) (PORT=1521)) (CONNECT_DATA=(SERVICE_NAME=orcl)))`.<br /><br /> Wenn Sie einen Verzeichnisserver oder tnsnames verwenden, kann die Verbindungszeichenfolge der Name der Verbindung sein.<br /><br /> Weitere Informationen zu Oracle-Verbindungszeichenfolgen finden Sie unter [http://go.microsoft.com/fwlink/?LinkId=231153](http://go.microsoft.com/fwlink/?LinkId=231153) . Sie erhalten ausführliche Informationen zu Oracle-Datenbankverbindungszeichenfolgen für den Oracle Instant Client, der vom Oracle CDC Service verwendet wird.|  
|use_windows_authentication|Ein boolescher Wert, der die folgenden Werte haben kann:<br /><br /> **0**: Ein Oracle-Benutzername und ein dazugehöriges Kennwort werden zur Authentifizierung bereitgestellt (Standardeinstellung).<br /><br /> **1**: Zum Herstellen einer Verbindung mit der Oracle-Datenbank wird die Windows-Authentifizierung verwendet. Sie können diese Option nur verwenden, wenn die Oracle-Datenbank für die Nutzung der Windows-Authentifizierung konfiguriert ist.|  
|username|Der Name des Oracle-Datenbankbenutzers mit Log Mining-Berechtigung. Diese Angabe ist nur obligatorisch, wenn Folgendes gilt: **use_windows_authentication = 0**.|  
|Kennwort|Das Kennwort für den Oracle Datenbankbenutzer mit Log Mining-Berechtigung. Diese Angabe ist nur obligatorisch, wenn Folgendes gilt: **use_windows_authentication = 0**.|  
|transaction_staging_timeout|Der Zeitraum in Sekunden, während dessen eine nicht mit Commit bestätigte Oracle-Transaktion im Arbeitsspeicher verbleibt, bevor sie in die Tabelle **cdc.xdbcdc_staged_transactions** geschrieben wird. Der Standardwert ist 120 Sekunden.|  
|memory_limit|Der Arbeitsspeicher-Höchstwert in MB, der zum Zwischenspeichern von Daten im Arbeitsspeicher verwendet werden kann. Ein niedrigere Einstellung führt dazu, dass mehr Transaktionen in die Tabelle **cdc.xdbcdc_staged_transactions** geschrieben werden. Die Standardeinstellung ist 50 MB.|  
|Optionen|Eine Liste der Optionen der Form name[=value][; ]. Wird zum Angeben von sekundären Optionen verwendet (z. B. Ablaufverfolgung, Optimierung). Eine Beschreibung der verfügbaren Optionen finden Sie unten in der Tabelle.|  
  
 In der folgenden Tabelle werden die verfügbaren Optionen beschrieben.  
  
|Name|Standardwert|Min|Max|STATIC-Cursor|Description|  
|----------|-------------|---------|---------|------------|-----------------|  
|Ablaufverfolgung|False|-|-|False|Die verfügbaren Werte sind:<br /><br /> Wahr<br /><br /> False<br /><br /> on<br /><br /> off|  
|cdc_update_state_interval|10|1|120|False|Die Größe von Arbeitsspeichersegmenten (in KB), die für eine Transaktion zugeordnet werden (eine Transaktion kann mehr als ein Segment zuordnen). Siehe Spalte „memory_limit“ in der [cdc.xdbcdc_config](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_config) -Tabelle.|  
|target_max_batched_transactions|100|1|1000|Wahr|Die maximale Anzahl von Oracle-Transaktionen, die beim Update von SQL Server CT-Tabellen zusammengefasst zu einer Transaktion verarbeitet werden können.|  
|target_idle_lsn_update_interval|10|0|1|False|Das Intervall (in Sekunden) zum Aktualisieren der Tabelle **lsn_time_mapping** , wenn die aufgezeichneten Tabellen keine Aktivität aufweisen.|  
|trace_retention_period|24|1|24*31|False|Der Zeitraum (in Stunden), wie lange Meldungen in der Ablaufverfolgungstabelle beibehalten werden.|  
|sql_reconnect_interval|2|2|3600|False|Der Zeitraum (in Sekunden), wie lange gewartet wird, bevor eine neue Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt wird. Dieses Intervall wird zusätzlich zum Verbindungstimeout des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Clients verwendet.|  
|sql_reconnect_limit|-1|-1|-1|False|Die maximale Anzahl von erneuten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verbindungsversuchen. Die Standardeinstellung -1 bedeutet, dass der Prozess so lange versucht, erneut eine Verbindung herzustellen, bis er beendet wird.|  
|cdc_restart_limit|6|-1|3600|False|In den meisten Fällen startet der CDC-Dienst eine abnormal beendete CDC-Instanz automatisch neu. Diese Eigenschaft definiert, nach wie vielen Fehlern pro Stunde der Dienst das Neustarten der Instanz beendet. Der Wert -1 bedeutet, dass die Instanz immer neu gestartet werden soll.<br /><br /> Der Dienst fährt dann nach jedem Update der Konfigurationstabelle damit fort, die Instanz neu zu starten.|  
|cdc_memory_report|0|0|1000|False|Wenn der Wert des Parameters geändert wurde, gibt die CDC-Instanz den zugehörigen Arbeitsspeicherbericht in der Ablaufverfolgungstabelle aus.|  
|target_command_timeout|600|1|3600|False|Befehlstimeout bei Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|source_character_set|-|-|-|Wahr|Kann auf eine bestimmte Oracle-Codierung festgelegt werden, die anstelle der Codepage der Oracle-Datenbank verwendet werden soll. Dies kann nützlich sein, wenn sich die tatsächliche Codierung, die für die Zeichendaten verwendet wird, von der Codierung unterscheidet, die von der Codepage der Oracle-Datenbank vorgegeben wird.|  
|source_error_retry_interval|30|1|3600|False|Wird bei mehreren Fehlern verwendet, z. B. einem Verbindungsfehler oder einer vorübergehenden fehlenden Synchronisierung zwischen Systemtabellen, bevor der Vorgang wiederholt wird.|  
|source_prefetch_size|100|1|10000|Wahr|Größe des Vorabruf-Batch.|  
|source_max_tables_in_query|100|1|10000|Wahr|Maximale Anzahl von Tabellen in der WHERE-Klausel, bevor zum Lesen des Oracle-Protokolls ohne Tabellenfilterung gewechselt wird.|  
|source_read_retry_interval|2|1|3600|False|Der Zeitraum, wie lange die Quelle wartet, bis sie versucht, die Oracle-Transaktionsprotokolle bei EOF erneut zu lesen.|  
|source_reconnect_interval|30|1|3600|False|Der Zeitraum (in Sekunden), wie lange vor dem Versuch, eine neue Verbindung mit der Quelldatenbank herzustellen, gewartet wird.|  
|source_reconnect_limit|-1|-1||False|Die maximale Anzahl der versuchten Verbindungsversuche mit der Quelldatenbank. Die Standardeinstellung -1 bedeutet, dass der Prozess so lange versucht, erneut eine Verbindung herzustellen, bis er beendet wird.|  
|source_command_timeout|30|1|3600|False|Verbindungstimeout beim Verwenden von Oracle.|  
|source_connection_timeout|30|1|3600|False|Verbindungstimeout bei Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|trace_data_errors|Wahr|-|-|False|Boolesch. **True** gibt an, dass Fehler beim Konvertieren und Abschneiden von Daten protokolliert werden.|  
|CDC_stop_on_breaking_schema_changes|False|-|-|False|Boolesch. **True** gibt an, dass der Vorgang beendet werden soll, wenn fehlerhafte Schemaänderungen erkannt werden.<br /><br /> **False** gibt an, dass die Spiegeltabelle und die Aufzeichnungsinstanz gelöscht werden sollen.|  
|source_oracle_home||-|-|False|Kann auf einen bestimmten Oracle Home-Pfad oder einen Oracle Home-Namen festgelegt werden, der von der CDC-Instanz zum Herstellen einer Verbindung zu Oracle verwendet wird.|  
  
###  <a name="a-namebkmkcdcxdbcdcstatea-cdcxdbcdcstate"></a><a name="BKMK_cdcxdbcdc_state"></a> cdc.xdbcdc_state  
 Diese Tabelle enthält Informationen zum permanenten Status der Oracle CDC-Instanz. Der Aufzeichnungsstatus wird bei Wiederherstellungs- und Failoverszenarien sowie für die Systemüberwachung verwendet.  
  
 In der folgenden Tabelle werden die Spalten der Tabelle **cdc.xdbcdc_state** beschrieben.  
  
|Element|Description|  
|----------|-----------------|  
|status|Der aktuelle Statuscode für die aktuelle Oracle CDC-Instanz. Der Status beschreibt den aktuellen Zustand für die CDC.|  
|sub_status|Status der zweiten Ebene, der zusätzliche Informationen zum aktuellen Status liefert.|  
|active|Ein boolescher Wert, der die folgenden Werte haben kann:<br /><br /> **0**: Der Oracle CDC-Instanzprozess ist nicht aktiv.<br /><br /> **1**: Der Oracle CDC-Instanzprozess ist aktiv.|  
|Fehler|Ein boolescher Wert, der die folgenden Werte haben kann:<br /><br /> **0**: Der Oracle CDC-Instanzprozess befindet sich nicht in einem Fehlerzustand.<br /><br /> **1**: Die Oracle CDC-Instanz befindet sich in einem Fehlerzustand.|  
|status_message|Eine Zeichenfolge, die eine Beschreibung des Fehlers oder des Status darstellt.|  
|timestamp|Der Zeitstempel mit der Uhrzeit (UTC), zu der der Aufzeichnungsstatus zuletzt aktualisiert wurde.|  
|active_capture_node|Der Name des Hosts (der Host kann ein Knoten auf einem Cluster sein), auf dem momentan der Oracle CDC Service und die Oracle CDC-Instanz (auf der die Oracle-Transaktionsprotokolle verarbeitet werden) ausgeführt werden.|  
|last_transaction_timestamp|Ein Zeitstempel mit der Uhrzeit (UTC), zu der die letzte Transaktion in die Änderungstabellen geschrieben wurde.|  
|last_change_timestamp|Ein Zeitstempel mit der Uhrzeit (UTC), zu der der letzte Änderungsdatensatz aus dem Oracle-Quelltransaktionsprotokoll gelesen wurde. Anhand dieses Zeitstempels können Sie die aktuelle Latenzzeit des CDC-Prozesses ermitteln.|  
|transaction_log_head_cn|Die letzte Änderungsnummer (CN), die aus dem Oracle-Transaktionsprotokoll gelesen wurde.|  
|transaction_log_tail_cn|Die Änderungsnummer (CN) im Oracle-Transaktionsprotokoll, auf das die Oracle CDC-Instanz bei einem Neustart oder einer Wiederherstellung zurückgreift.|  
|current_cn|Die letzte bekannte Änderungsnummer (CN) in der Quelldatenbank.|  
|software_version|Die interne Version des Oracle CDC Service.|  
|completed_transactions|Die Anzahl der Transaktionen, die seit der letzten CDC-Zurücksetzung verarbeitet wurden.|  
|written_changes|Die Anzahl der Änderungsdatensätze, die in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Änderungstabellen geschrieben werden.|  
|read_changes|Die Anzahl der Änderungsdatensätze, die aus dem Oracle-Quelltransaktionsprotokoll gelesen werden.|  
|staged_transactions|Die Anzahl der momentan aktiven Transaktionen, die in der Tabelle **cdc.xdbcdc_staged_transactions** bereitgestellt werden.|  
  
###  <a name="a-namebkmkcdcxdbcdctracea-cdcxdbcdctrace"></a><a name="BKMK_cdcxdbcdc_trace"></a> cdc.xdbcdc_trace  
 Diese Tabelle enthält Informationen zum Betrieb der CDC-Instanz. Zu den in dieser Tabelle gespeicherten Informationen zählen Fehlerdatensätze, wichtige Statusänderungen und Ablaufverfolgungsdatensätze. Fehlerinformationen werden auch in das Windows-Ereignisprotokoll geschrieben, um sicherzustellen, dass auf die Informationen zugegriffen werden kann, wenn die Tabelle **cdc.xcbcdc_trace** nicht verfügbar ist.  
  
 In der folgenden Tabelle werden die Spalten der Tabelle cdc.xdbcdc_trace beschrieben.  
  
|Element|Description|  
|----------|-----------------|  
|timestamp|Der genaue UTC-Zeitstempel mit der Uhrzeit, zu der der Ablaufverfolgungsdatensatz geschrieben wurde.|  
|Typ|Enthält einen der folgenden Werte.<br /><br /> Fehler<br /><br /> INFO<br /><br /> Ablaufverfolgung|  
|Knoten|Der Name des Knotens, unter dem der Datensatz geschrieben wurde.|  
|status|Der Statuscode, der von der Statustabelle verwendet wird.|  
|sub_status|Der Unterstatuscode, der von der Statustabelle verwendet wird.|  
|status_message|Die Statusmeldung, die von der Statustabelle verwendet wird.|  
|data|Zusätzliche Daten für Fälle, in denen der Fehler oder der Ablaufverfolgungsdatensatz eine Nutzlast enthält (z. B. einen beschädigten Protokolldatensatz).|  
  
###  <a name="a-namebkmkcdcxdbcdcstagedtransactionsa-cdcxdbcdcstagedtransactions"></a><a name="BKMK_cdcxdbcdc_staged_transactions"></a> cdc.xdbcdc_staged_transactions  
 In dieser Tabelle werden Änderungsdatensätze für große Transaktionen oder Transaktionen mit langer Laufzeit gespeichert, bis der Transaktionscommit oder das Rollbackereignis aufgezeichnet wird. Der Oracle CDC Service sortiert aufgezeichnete Protokolldatensätze für jede Transaktion nach Transaktionscommit-Zeitpunkt und dann nach der chronologischen Reihenfolge. Protokolldatensätze für dieselbe Transaktion werden im Arbeitsspeicher gespeichert, bis die Transaktion endet, und dann in die Änderungszieltabelle geschrieben oder verworfen (bei einem Rollback). Da nur eine begrenzte Menge an Arbeitsspeicher vorhanden ist, werden große Transaktionen in die Tabelle **cdc.xdbcdc_staged_transactions** geschrieben, bis die Transaktion abgeschlossen ist. Transaktionen werden auch in die Stagingtabelle geschrieben, wenn die Ausführung lange dauert. Daher müssen die alten Änderungen beim Neustarten der Oracle CDC-Instanz nicht neu aus den Oracle-Transaktionsprotokollen gelesen werden.  
  
 In der folgenden Tabelle werden die Spalten der Tabelle **cdc.xdbcdc_staged_transactions** beschrieben.  
  
|Element|Description|  
|----------|-----------------|  
|transaction_id|Der eindeutige Transaktionsbezeichner der bereitgestellten Transaktion.|  
|seq_num|Die Nummer der Zeile **xcbcdc_staged_transactions** für die aktuelle Transaktion (beginnend mit 0).|  
|data_start_cn|Die Änderungsnummer (CN) für die erste Änderung der Daten in dieser Zeile.|  
|data_end_cn|Die Änderungsnummer (CN) für die letzte Änderung der Daten in dieser Zeile.|  
|data|Die bereitgestellten Änderungen für die Transaktion in BLOB-Form.|  
  
## <a name="see-also"></a>Siehe auch  
 [Change Data Capture Designer für Oracle von Attunity](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)  
  
  