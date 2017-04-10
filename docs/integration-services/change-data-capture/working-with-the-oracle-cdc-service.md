---
title: "Arbeiten mit dem Oracle CDC Service | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 04be5896-2301-45f5-a8ce-5f4ef2b69aa5
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# Arbeiten mit dem Oracle CDC Service
  In diesem Abschnitt werden einige wichtige Begriffe des Oracle CDC Service beschrieben. Es werden die folgenden Begriffe behandelt:  
  
-   [MSXDBCDC-Datenbank](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_MSXDBCDC)  
  
     In diesem Abschnitt werden die Tabellen beschrieben, die in dieser Datenbank enthalten sind, und welche Bedeutung sie für CDC haben.  
  
-   [CDC-Datenbanken](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_CDCdatabase)  
  
     Dieser Abschnitt enthält eine kurze Beschreibung der CDC-Datenbanken. Diese Datenbanken werden mit der Oracle CDC Designer Console erstellt. Weitere Informationen zu CDC-Datenbanken finden Sie in der Dokumentation, die im Installationsumfang der CDC Designer Console enthalten ist.  
  
-   [Verwenden der Befehlszeile zum Konfigurieren des CDC Service](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_CommandConfigCDC)  
  
     In diesem Abschnitt werden die Befehlszeilenbefehle beschrieben, die zum Konfigurieren des Oracle CDC Service verwendet werden.  
  
##  <a name="BKMK_MSXDBCDC"></a> MSXDBCDC-Datenbank  
 Bei der MSXDBCDC-Datenbank (Microsoft External-Database CDC) handelt es sich um eine spezielle Datenbank, die beim Verwenden des CDC Service mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz erforderlich ist.  
  
 Der Name dieser Datenbank kann nicht geändert werden. Wenn eine Datenbank mit dem Namen MSXDBCDC auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hostinstanz vorhanden ist und andere Tabellen enthält, als vom CDC Service for Oracle definiert wurden, kann die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hostinstanz nicht verwendet werden.  
  
 Die hauptsächlichen Verwendungen für diese Datenbank sind:  
  
-   Dient als Registrierung von Oracle CDC Services, die einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz zugeordnet sind. Diese Informationen werden für die Dienstkonfiguration und Entwurfskomponenten sowie als Unterstützung der Koordination mehrerer CDC-Dienste gleichen Namens auf anderen Knoten verwendet, wenn ermittelt werden muss, welcher Dienst aktiv ist.  
  
-   Dient als Registrierung der Oracle CDC-Instanzen, die in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz enthalten sind, des CDC-Diensts, der die einzelnen Instanzen behandelt, und der jeweils verwendeten Konfigurationsversion. Diese Informationen entsprechen den Informationen in der Spalte **is_cdc_enabled** der Tabelle **sys.databases** der master-Datenbank. Der CDC-Dienst scannt die Tabelle **dbo.xdbcdc_databases** in regelmäßigen Abständen, um an der CDC-Konfiguration oder der Liste der aufgezeichneten Instanzen vorgenommene Änderungen zu ermitteln.  
  
-   Vorhalten von im Besitz von **sysadmin** befindlichen gespeicherten Prozeduren, die zum Erstellen und Verwalten von CDC-Instanzen verwendet werden. Diese ähneln den Systemprozeduren, die für die Implementierung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC-Funktion verwendet werden.  
  
### Erstellen der MSXDBCDC-Datenbank  
 Eine MSXDBCDC-Datenbank muss erstellt werden, bevor der Oracle CDC Service definiert werden kann. Sie können auf einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz nur eine MSXDBCDC-Datenbank erstellen. Die MSXDBCDC-Datenbank wird erstellt, wenn Sie eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank für Oracle CDC vorbereiten. Dazu können Sie die Oracle CDC Service Configuration Console verwenden oder ein Erstellungsskript ausführen, das mithilfe der CDC Service Configuration Console generiert wird.  
  
 Der Besitzer dieser Datenbank ist der Oracle CDC Service-Administrator, der alle unter der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz gehosteten Oracle CDC-Instanzen steuern kann.  
  
 **Siehe auch:**  
  
 [Vorbereiten von SQL Server für CDC](../../integration-services/change-data-capture/how-to-prepare-sql-server-for-cdc.md)  
  
### MSXDBCDC-Datenbanktabellen  
 In diesem Abschnitt werden die folgenden Tabellen in der MSXDBCDC-Datenbank beschrieben.  
  
-   [dbo.xdbcdc_trace](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_trace)  
  
-   [dbo.xdbcdc_databases](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_databases)  
  
-   [dbo.xdbcdc_services](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_services)  
  
###  <a name="BKMK_dboxdbcdc_trace"></a> dbo.xdbcdc_trace  
 In dieser Tabelle werden die Ablaufverfolgungsinformationen für den Oracle CDC Service gespeichert. Zu den in dieser Tabelle gespeicherten Informationen zählen wichtige Statusänderungen und Ablaufverfolgungsdatensätze.  
  
 Der Oracle CDC Service schreibt Fehlerdatensätze und einige Informationsdatensätze sowohl in das Windows-Ereignisprotokoll als auch in die Ablaufverfolgungstabelle. In einigen Fällen kann ggf. nicht auf die Ablaufverfolgungstabelle zugegriffen werden. Auf die Fehlerinformationen kann dann über das Ereignisprotokoll zugegriffen werden.  
  
 Im Folgenden werden die Elemente beschrieben, die in der Tabelle **dbo.xdbcdc_trace** enthalten sind.  
  
|Element|Description|  
|----------|-----------------|  
|timestamp|Der genaue UTC-Zeitstempel mit der Uhrzeit, zu der der Ablaufverfolgungsdatensatz geschrieben wurde.|  
|Typ|Enthält einen der folgenden Werte.<br /><br /> ERROR<br /><br /> INFO<br /><br /> TRACE|  
|Knoten|Der Name des Knotens, unter dem der Datensatz geschrieben wurde.|  
|status|Der Statuscode, der von der Statustabelle verwendet wird.|  
|sub_status|Der Unterstatuscode, der von der Statustabelle verwendet wird.|  
|status_message|Die Statusmeldung, die von der Statustabelle verwendet wird.|  
|Quelle|Der Name der Oracle CDC-Komponente, die den Ablaufverfolgungsdatensatz erzeugt hat.|  
|text_data|Weitere Textdaten für Fälle, in denen der Fehler oder Ablaufverfolgungsdatensatz eine Textnutzlast enthält.|  
|binary_data|Weitere Binärdaten für Fälle, in denen der Fehler oder der Ablaufverfolgungsdatensatz eine binäre Nutzlast enthält.|  
  
 Die Oracle CDC-Instanz löscht veraltete Ablaufverfolgungstabellenzeilen gemäß der Beibehaltungsrichtlinie für Änderungstabellen.  
  
###  <a name="BKMK_dboxdbcdc_databases"></a> dbo.xdbcdc_databases  
 Diese Tabelle enthält die Namen der CDC Service for Oracle-CDC-Datenbanken in der aktuellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz. Jede Datenbank entspricht einer Oracle CDC-Instanz. Der Oracle CDC Service ermittelt anhand dieser Tabelle, welche Instanzen gestartet oder beendet und welche Instanzen neu konfiguriert werden sollen.  
  
 In der folgenden Tabelle werden die Elemente beschrieben, die in der Tabelle **dbo.xdbcdc_databases** enthalten sind.  
  
|Element|Description|  
|----------|-----------------|  
|name|Der Name der Oracle-Datenbank in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz.|  
|config_version|Der Zeitstempel (UTC) für die letzte Änderung in der entsprechenden **xdbcdc_config**-Tabelle der CDC-Datenbank oder der Zeitstempel der aktuellen Zeile in dieser Tabelle.<br /><br /> Der UPDATE-Trigger erzwingt für dieses Element den Wert GETUTCDATE(). Mithilfe von **config_version** kann der CDC-Dienst die CDC-Instanz ermitteln, die auf eine Konfigurationsänderung geprüft oder die aktiviert/deaktiviert werden muss.|  
|cdc_service_name|Dieses Element bestimmt, welcher Oracle CDC Service die ausgewählte Oracle-Datenbank behandelt.|  
|aktiviert|Gibt an, ob die Oracle CDC-Instanz aktiviert (1) oder deaktiviert (0) ist. Wenn der Oracle CDC Service gestartet wird, werden nur die als aktiviert (1) markierten Instanzen gestartet.<br /><br /> **Hinweis**: Eine Oracle CDC-Instanz kann aufgrund eines Fehlers deaktiviert werden, der nicht wiederholbar ist. In diesem Fall muss die Instanz manuell neu gestartet werden, nachdem der Fehler behoben wurde.|  
  
###  <a name="BKMK_dboxdbcdc_services"></a> dbo.xdbcdc_services  
 In dieser Tabelle sind die CDC-Dienste aufgeführt, die der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hostinstanz zugeordnet sind. Diese Tabelle wird von der CDC Designer Console verwendet, um die Liste der CDC-Dienste zu bestimmen, die für die lokale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz konfiguriert werden. Außerdem wird sie vom CDC-Dienst verwendet, um sicherzustellen, dass nur ein ausgeführter Windows-Dienst jeweils einen bestimmten Oracle CDC Service-Namen behandelt.  
  
 Im Folgenden sind die Aufzeichnungsstatuselemente beschrieben, die in der Tabelle **dbo.xdbcdc_databases** enthalten sind.  
  
|Element|Description|  
|----------|-----------------|  
|cdc_service_name|Der Name des Oracle CDC Service (Name des Windows-Diensts).|  
|cdc_service_sql_login|Der Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung, die vom Oracle CDC Service zum Herstellen der Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz verwendet wird. Es wird ein neuer SQL-Benutzer mit dem Namen cdc_service erstellt und diesem Anmeldenamen zugeordnet. Anschließend wird er als Mitglied der festen Datenbankrollen db_ddladmin, db_datareader und db_datawriter für jede CDC-Datenbank hinzugefügt, die vom Dienst behandelt wird.|  
|ref_count|Dieses Element zählt die Anzahl von Computern, auf denen der gleiche Oracle CDC Service installiert ist. Es wird mit jeder Hinzufügung des gleichnamigen Oracle CDC Service inkrementiert. Es wird entsprechend dekrementiert, wenn ein Dienst entfernt wird. Wenn der Indikator 0 (null) erreicht, wird diese Zeile gelöscht.|  
|active_service_node|Der Name des Windows-Knotens, der den CDC-Dienst momentan behandelt. Wenn der Dienst ordnungsgemäß beendet wird, wird diese Spalte auf NULL festgelegt, um anzugeben, dass kein aktiver Dienst mehr vorhanden ist.|  
|active_service_heartbeat|Dieses Element verfolgt den aktuellen CDC-Dienst, um zu ermitteln, ob er noch aktiv ist.<br /><br /> Dieses Element wird in regelmäßigen Abständen mit dem aktuellen Datenbankzeitstempel (UTC) für den aktiven CDC-Dienst aktualisiert. Das Standardintervall beträgt 30 Sekunden, aber Sie können diesen Wert anpassen.<br /><br /> Wenn ein ausstehender CDC-Dienst erkennt, dass der Takt nicht aktualisiert wurde, nachdem das konfigurierte Intervall verstrichen ist, versucht der ausstehende Dienst, die aktive CDC-Dienst-Rolle zu übernehmen.|  
|options|Dieses Element gibt die sekundären Optionen an, z. B. Ablaufverfolgung oder Optimierung. Es hat die Form **name[=Wert][; ]**. Für die Zeichenfolge options wird die gleiche Semantik wie für die ODBC-Verbindungszeichenfolge verwendet. Wenn die Option ein boolescher Wert ist (ja/nein), kann der Wert nur den Namen enthalten.<br /><br /> Die Ablaufverfolgung (trace) hat die folgenden möglichen Werte.<br /><br /> **true**<br /><br /> **on**<br /><br /> **false**<br /><br /> **off**<br /><br /> **\<Klassenname>[,Klassenname>]**<br /><br /> <br /><br /> Der Standardwert ist **false**.<br /><br /> **service_heartbeat_interval** ist das Zeitintervall (in Sekunden), nach dem der Dienst die Spalte „active_service_heartbeat“ aktualisiert. Der Standardwert ist **30**. Der Maximalwert ist **3600**.<br /><br /> **service_config_polling_interval** ist das Abrufintervall (in Sekunden), nach dem der CDC-Dienst eine Überprüfung auf Konfigurationsänderungen durchführt. Der Standardwert ist **30**. Der Maximalwert ist **3600**.<br /><br /> **sql_command_timeout** ist das Befehlstimeout für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Der Standardwert ist **1**. Der Maximalwert ist **3600**.|  
||  
  
### Gespeicherte Prozeduren der MSXDBCDC-Datenbank  
 In diesem Abschnitt werden die folgenden gespeicherten Prozeduren der MSXDBCDC-Datenbank beschrieben.  
  
-   [dbo.xcbcdc_reset_db(Datenbankname)](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxcbcdc_reset_db)  
  
-   [dbo.xdbcdc_disable_db(dbname)](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_disable_db)  
  
-   [dbo.xcbcdc_add_service(svcname,sqlusr)](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxcbcdc_add_service)  
  
-   [dbo.xdbcdc_start(dbname)](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_start)  
  
-   [dbo.xdbcdc_stop(dbname)](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_dboxdbcdc_stop)  
  
###  <a name="BKMK_dboxcbcdc_reset_db"></a> dbo.xcbcdc_reset_db(Datenbankname)  
 Bei dieser Prozedur werden die Daten einer Oracle CDC-Instanz gelöscht. Verwendung:  
  
-   Zum Neustarten der Aufzeichnung von Daten ohne Berücksichtigung der vorherigen Daten, z. B. nach der Wiederherstellung einer Quelldatenbank oder nach einem Zeitraum der Inaktivität, in dem einige Oracle-Transaktionsprotokolle nicht verfügbar sind.  
  
-   Bei einer Beschädigung im CDC-Status (vor allem in den cdc.*tables-Daten).  
  
 Bei der Prozedur **dbo.xcbcdc_reset_db** werden die folgenden Tasks ausgeführt:  
  
-   Beendet die CDC-Instanz (falls sie aktiv ist).  
  
-   Schneidet die Änderungstabellen, die Tabelle **cdc_lsn_mapping** und die Tabelle **cdc_ddl_history** ab.  
  
-   Löscht die Tabelle **cdc_xdbcdc_state**.  
  
-   Löscht die Spalte „start_lsn“ für jede Zeile von **cdc_change_table**.  
  
 Zum Verwenden der Prozedur **dbo.xcbcdc_reset_db** muss der Benutzer Mitglied der Datenbankrolle **db_owner** für die genannte CDC-Instanzdatenbank oder alternativ dazu Mitglied der festen Serverrolle **sysadmin** oder **serveradmin** sein.  
  
 Weitere Informationen zu den CDC-Tabellen finden Sie im Hilfesystem in der CDC Designer Console unter *CDC-Datenbanken*.  
  
###  <a name="BKMK_dboxdbcdc_disable_db"></a> dbo.xdbcdc_disable_db(dbname)  
 Bei der Prozedur **dbo.xcbcdc_disable_db** wird der folgende Task ausgeführt:  
  
-   Entfernt den Eintrag für die ausgewählte CDC-Datenbank in der Tabelle MSXDBCDC.xdbcdc_databases.  
  
 Zum Verwenden der Prozedur **dbo.xcbcdc_disable_db** muss der Benutzer Mitglied der Datenbankrolle **db_owner** für die genannte CDC-Instanz oder Mitglied der festen Serverrolle **sysadmin** oder **serveradmin** sein.  
  
 Weitere Informationen zu den CDC-Tabellen finden Sie im Hilfesystem in der CDC Designer Console unter CDC-Datenbanken.  
  
###  <a name="BKMK_dboxcbcdc_add_service"></a> dbo.xcbcdc_add_service(svcname,sqlusr)  
 Bei der Prozedur **dbo.xcbcdc_add_service** wird der Tabelle **MSXDBCDC.xdbcdc_services** ein Eintrag hinzugefügt, und es wird ein Inkrement von 1 der Spalte „ref_count“ für den Dienstnamen in der Tabelle **MSXDBCDC.xdbcdc_services** hinzugefügt. Wenn der **ref_count** 0 ist, wird die Zeile gelöscht.  
  
 Zum Verwenden der Prozedur **dbo.xcbcdc_add_service\<Dienstname, Benutzername>** muss der Benutzer Mitglied der Datenbankrolle **db_owner** für die genannte CDC-Instanzdatenbank oder Mitglied der festen Serverrolle **sysadmin** oder **serveradmin** sein.  
  
###  <a name="BKMK_dboxdbcdc_start"></a> dbo.xdbcdc_start(dbname)  
 Bei der Prozedur **dbo.xdbcdc_start** wird eine Startanforderung an den CDC-Dienst gesendet, der die ausgewählte CDC-Instanz behandelt, um die Änderungsverarbeitung zu starten.  
  
 Zum Verwenden der Prozedur **dbo.xcdcdc_start** muss der Benutzer Mitglied der Datenbankrolle **db_owner** für die CDC-Datenbank oder Mitglied der Rolle **sysadmin** oder **serveradmin** für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz sein.  
  
###  <a name="BKMK_dboxdbcdc_stop"></a> dbo.xdbcdc_stop(dbname)  
 Bei der Prozedur **dbo.xdbcdc_stop** wird eine Stoppanforderung an den CDC-Dienst gesendet, der die ausgewählte CDC-Instanz behandelt, um die Änderungsverarbeitung zu beenden.  
  
 Zum Verwenden der Prozedur **dbo.xcdcdc_stop** muss der Benutzer Mitglied der Datenbankrolle **db_owner** für die CDC-Datenbank oder Mitglied der Rolle **sysadmin** oder **serveradmin** für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz sein.  
  
##  <a name="BKMK_CDCdatabase"></a> CDC-Datenbanken  
 Jede in einem CDC-Dienst verwendete Oracle CDC-Instanz ist einer bestimmten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank zugeordnet, die als CDC-Datenbank bezeichnet wird. Diese [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank wird auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz gehostet, die dem Oracle CDC Service zugeordnet ist.  
  
 Die CDC-Datenbank enthält ein spezielles CDC-Schema. Der Oracle CDC Service verwendet dieses Schema in Verbindung mit Tabellennamen mit dem Präfix **xdbcdc_**. Dieses Schema wird zu Sicherheits- und Konsistenzzwecken verwendet.  
  
 Sowohl die Oracle CDC-Instanz als auch die CDC-Datenbanken werden mit der Oracle CDC Designer Console erstellt. Weitere Informationen zu den CDC-Datenbanken finden Sie in der Dokumentation, die im Installationsumfang der Oracle CDC Designer Console enthalten ist.  
  
##  <a name="BKMK_CommandConfigCDC"></a> Verwenden der Befehlszeile zum Konfigurieren des CDC Service  
 Sie können das Oracle CDC Service-Programm (xdbcdcsvc.exe) über die Befehlszeile bedienen. Das CDC Service-Programm ist eine systemeigene ausführbare Windows-Datei (32 oder 64 Bit).  
  
 **Siehe auch**  
  
 [Verwenden der CDC Service-Befehlszeilenschnittstelle](../../integration-services/change-data-capture/how-to-use-the-cdc-service-command-line-interface.md)  
  
### Dienstprogrammbefehle  
 Im folgenden Abschnitt werden die folgenden Befehle beschrieben, die zum Konfigurieren des CDC-Diensts verwendet werden.  
  
-   [Config](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_config)  
  
-   [Create](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_create)  
  
-   [Delete](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_delete)  
  
###  <a name="BKMK_config"></a> Config  
 Verwenden Sie `Config`, um eine Oracle CDC Service-Konfiguration über ein Skript zu aktualisieren. Der Befehl kann verwendet werden, um nur bestimmte Teile der CDC-Dienstkonfiguration zu aktualisieren (z. B. nur die Verbindungszeichenfolge ohne Kenntnis des asymmetrischen Schlüsselkennworts). Der Befehl muss von einem Computeradministrator ausgeführt werden. Unten ist ein Beispiel für den Befehl `Config` angegeben.  
  
```  
"<path>xdbcdcsvc.exe" config  
     <cdc-service-name>  
     [connect= <sql-server-connection-string>]  
     [key= <asym-key-password>]  
     [svcacct= <windows-account> <windows-password>]  
     [sqlacct= <sql-username> <sql-password>]  
  
```  
  
 Erläuterungen:  
  
 **cdc-service-name** ist der Name des zu aktualisierenden CDC-Diensts. Dies ist ein erforderlicher Parameter.  
  
 **sql-server-connection-string** ist die zu aktualisierende Verbindungszeichenfolge. Wenn die Verbindungszeichenfolge Leerzeichen oder Anführungszeichen enthält, muss sie in doppelte Anführungszeichen (") gesetzt werden. Eingebettete Anführungszeichen werden mit Escapezeichen versehen, indem die Anführungszeichen verdoppelt werden.  
  
 **asym-key-password** ist das zu aktualisierende Kennwort.  
  
 **windows-account** und **windows-password** sind die Anmeldeinformationen für das Windows-Konto des Diensts, der aktualisiert wird.  
  
 **sql-username** und **sql-password** sind die zu aktualisierenden Anmeldeinformationen für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung. Wenn sqlacct sowohl einen leeren Benutzernamen als auch ein leeres Kennwort aufweist, stellt der Oracle CDC Service mithilfe der Windows-Authentifizierung eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her.  
  
 **Hinweis**: Alle Parameter, die Leerzeichen oder doppelte Anführungszeichen enthalten, müssen in doppelte Anführungszeichen (") gesetzt werden. Eingebettete doppelte Anführungszeichen müssen verdoppelt werden (geben Sie zum Verwenden von **"A#B" D** als Kennwort z.B. **""A#B"" D"** ein).  
  
###  <a name="BKMK_create"></a> Create  
 Verwenden Sie `Create`, um einen Oracle CDC Service aus einem Skript zu erstellen. Der Befehl muss von einem Computeradministrator ausgeführt werden. Unten ist ein Beispiel für den Befehl `Create` angegeben:  
  
```  
"<path>xdbcdcsvc.exe" create  
     <cdc-service-name>  
     [connect= "<sql-server-connection-string>"]  
     [key= <asym-key-password>]  
     [svcacct <windows-account> <windows-password>]  
     [sqlacct <sql-username> <sql-password>]  
```  
  
 Erläuterungen:  
  
 **cdc-service-name** ist der Name des neu erstellten Diensts. Wenn bereits ein Dienst mit diesem Namen vorhanden ist, gibt das Programm einen Fehler zurück. Sie sollten keine langen Namen oder Namen mit Leerzeichen verwenden. Die Zeichen "/" und "\\" sind für einen Dienstnamen keine gültigen Zeichen. Dies ist ein erforderlicher Parameter.  
  
 **sql-server-connection-string** ist die Verbindungszeichenfolge, mit der die Verbindung zur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz hergestellt wird, die dem neuen Oracle CDC Service zugeordnet ist.  
  
 **asym-key-password** ist das Kennwort, mit dem der asymmetrische Schlüssel geschützt wird, der zum Speichern der Log Mining-Anmeldeinformationen der Quelldatenbank verwendet wird.  
  
 **windows-account** und **windows-password** sind der Kontoname bzw. das Kennwort, der bzw. das dem erstellten Oracle CDC Service zugeordnet ist.  
  
 **sql-username** und **sql-password** sind der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Kontoname bzw. das Kennwort, der bzw. das zum Herstellen der Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz verwendet wird. Wenn beide Parameter leer sind, stellt CDC Service for Oracle mithilfe der Windows-Authentifizierung eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her.  
  
 **Hinweis**: Alle Parameter, die Leerzeichen oder doppelte Anführungszeichen enthalten, müssen in doppelte Anführungszeichen (") gesetzt werden. Eingebettete doppelte Anführungszeichen müssen verdoppelt werden (geben Sie zum Verwenden von **"A#B" D** als Kennwort z.B. **""A#B"" D"** ein).  
  
###  <a name="BKMK_delete"></a> Delete  
 Verwenden Sie `Delete`, um den Oracle CDC Service sauber aus einem Skript zu löschen. Dieser Befehl muss von einem Computeradministrator ausgeführt werden. Unten ist ein Beispiel für den Befehl `Delete` angegeben.  
  
```  
"<path>xdbcdcsvc.exe" delete  
    <cdc-service-name>  
  
```  
  
 Erläuterungen:  
  
 **cdc-service-name** ist der Name des zu löschenden CDC-Diensts.  
  
 **Hinweis**: Alle Parameter, die Leerzeichen oder doppelte Anführungszeichen enthalten, müssen in doppelte Anführungszeichen (") gesetzt werden. Eingebettete doppelte Anführungszeichen müssen verdoppelt werden (geben Sie zum Verwenden von **"A#B" D** als Kennwort z.B. **""A#B"" D"** ein).  
  
## Siehe auch  
 [Verwenden der CDC Service-Befehlszeilenschnittstelle](../../integration-services/change-data-capture/how-to-use-the-cdc-service-command-line-interface.md)   
 [Vorbereiten von SQL Server für CDC](../../integration-services/change-data-capture/how-to-prepare-sql-server-for-cdc.md)  
  
  