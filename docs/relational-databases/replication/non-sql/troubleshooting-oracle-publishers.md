---
title: Problembehandlung bei Oracle-Verlegern | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], troubleshooting
- troubleshooting [SQL Server replication], Oracle publishing
ms.assetid: be94f1c1-816b-4b1d-83f6-2fd6f5807ab7
caps.latest.revision: 62
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f6b52a9fc10c8dae7a0b01a6a615076bcc257104
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="troubleshooting-oracle-publishers"></a>Problembehandlung bei Oracle-Verlegern
  In diesem Thema wird eine Reihe von Problemen aufgeführt, die bei der Konfiguration und Verwendung von Oracle-Verlegern auftreten können.  
  
## <a name="an-error-is-raised-regarding-oracle-client-and-networking-software"></a>Fehler bezüglich Oracle-Client- und Netzwerksoftware  
 Dem Konto, unter dem [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf dem Verteiler ausgeführt wird, müssen Lese- und Ausführungsberechtigungen für das Verzeichnis (und alle Unterverzeichnisse) erteilt werden, in dem die Oracle-Clientnetzwerksoftware installiert ist. Wenn diese Berechtigungen nicht erteilt worden sind oder die Oracle-Clientkomponenten nicht ordnungsgemäß installiert sind, wird eine Fehlermeldung ähnlich der folgenden angezeigt:  
  
 "Fehler bei der Serververbindung mit [Microsoft OLE DB-Anbieter für Oracle]. Oracle Client- und Netzwerkverbindung konnten nicht gefunden werden. Diese Komponenten werden von der Oracle Corporation geliefert und mit der Clientsoftware von Oracle, Version 7.3.3 oder höher, installiert. Sie müssen diese Komponenten installieren, um den Provider verwenden zu können."  
  
 Wenn ein entsprechender Oracle-Client auf dem Verteiler installiert wurde, stellen Sie sicher, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] angehalten wurde, und dann nach Abschluss der Clientinstallation erneut gestartet wird. Dies ist erforderlich, damit die Clientkomponenten von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] erkannt werden.  
  
 Wenn die Berechtigungen tatsächlich erteilt und die Komponenten ordnungsgemäß installiert sind und der Fehler trotzdem weiterhin angezeigt wird, sollten Sie die Registrierungseinstellungen unter HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDTC\MTxOCI überprüfen:  
  
-   Für Oracle 10g gelten folgende Einstellungen:  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql10.dll  
  
    -   OracleXaLib = oraclient10.dll  
  
-   Für Oracle 9i gelten folgende Einstellungen:  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql9.dll  
  
    -   OracleXaLib = oraclient9.dll  
  
## <a name="the-sql-server-distributor-cannot-connect-to-the-oracle-database-instance"></a>Verbindung zwischen SQL Server-Verteiler und Oracle-Datenbankinstanz nicht möglich  
 Wenn der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler keine Verbindung mit dem Oracle-Verleger herstellen kann, sollten Sie sicherstellen, dass die folgenden Anforderungen erfüllt sind:  
  
-   Auf dem Verteiler ist die notwendige Oracle-Software installiert.  
  
-   Die Oracle-Datenbank ist online, und Sie können mit einem Tool wie SQL*Plus eine Verbindung mit der Datenbank herstellen.  
  
-   Der Anmeldename, den die Replikation zur Herstellung einer Verbindung mit dem Oracle-Verleger verwendet, verfügt über ausreichende Berechtigungen. Weitere Informationen finden Sie unter [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
-   Die während der Konfiguration des Oracle-Verteilers definierten TNS-Namen sind in der Datei tnsnames.ora aufgeführt.  
  
-   Das richtige Oracle Home-Verzeichnis und der entsprechende Pfad werden verwendet. Auch wenn Sie nur einen einzigen Satz von Oracle-Binärdateien auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler installiert haben, muss sichergestellt sein, dass die Umgebungsvariablen für das Oracle Home-Verzeichnis ordnungsgemäß festgelegt wurden. Wenn Sie Werte für Umgebungsvariablen ändern, müssen Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] beenden und neu starten, damit die Änderungen wirksam werden.  
  
 Weitere Informationen zum Konfigurieren und Testen der Konnektivität finden Sie im Abschnitt zum „Installieren und Konfigurieren der Oracle-Clientnetzwerksoftware auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Verteiler“ in [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="the-oracle-publisher-is-associated-with-another-distributor"></a>Oracle-Verleger ist mit anderem Verteiler verknüpft  
 Jeder Oracle-Verleger kann immer nur mit einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler verknüpft sein. Wenn der Oracle-Verleger bereits mit einem anderen Verteiler verknüpft ist, muss diese Zuordnung gelöscht werden, bevor ein anderer Verteiler verwendet werden kann. Wird die Zuordnung des Verteilers nicht gelöscht, wird eine der folgenden Fehlermeldungen angezeigt:  
  
-   „Die Oracle-Serverinstanz '\<*OracleVerlegerName*>' wurde zum Verwenden von '\<*SQLServerDistributorName*>' als Verteiler konfiguriert. Um mit dem Verwenden von '\<*NewSQLServerDistributorName*>' als Verteiler zu beginnen, müssen Sie die aktuelle Replikationskonfiguration auf der Oracle-Serverinstanz entfernen. Hierbei werden alle Veröffentlichungen auf dieser Serverinstanz gelöscht.“  
  
-   „Der Oracle-Server '\<*OracleServerName*>' ist bereits als Verleger '\<*OracleVerlegerName*>' auf dem Verteiler '\<*SQLServerDistributorName*>.*\<VerteilungsdatenbankName>*' definiert. Löschen Sie die Zuordnung des Verlegers, oder löschen Sie das öffentliche Synonym '*\<SynonymName>*' zur erneuten Erstellung.“  
  
 Wenn die Zuordnung eines Oracle-Verlegers gelöscht wird, werden die Replikationsobjekte in der Oracle-Datenbank automatisch bereinigt. In einigen Fällen ist jedoch auch eine manuelle Bereinigung der Oracle-Replikationsobjekte erforderlich. So bereinigen Sie die durch die Replikation erstellten Oracle-Replikationsobjekte manuell:  
  
1.  Stellen Sie eine Verbindung mit dem Oracle-Verleger mit DBA-Berechtigungen her.  
  
2.  Führen Sie den SQL-Befehl `DROP PUBLIC SYNONYM MSSQLSERVERDISTRIBUTOR;`aus.  
  
3.  Führen Sie den SQL-Befehl `DROP USER <replication_administrative_user_schema>``CASCADE;`aus.  
  
## <a name="sql-server-error-21663-is-raised-regarding-the-lack-of-a-primary-key"></a>SQL Server-Fehler 21663 (Fehlen des Primärschlüssels) wurde ausgelöst  
 Artikel in Transaktionsveröffentlichungen müssen über einen gültigen Primärschlüssel verfügen. Fehlt dieser Primärschlüssel, finden Sie beim Versuch, den Artikel hinzuzufügen, die folgende Fehlermeldung:  
  
 „Für die [\<*TableOwner*>].[\<*TableName*>]-Quelltabelle wurde kein gültiger Primärschlüssel gefunden.“  
  
 Informationen zu den Anforderungen für Primärschlüssel finden Sie im Abschnitt zu eindeutigen Indizes und Einschränkungen im Thema [Design Considerations and Limitations for Oracle Publishers](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md).  
  
## <a name="sql-server-error-21642-is-raised-regarding-a-duplicate-linked-server-login"></a>SQL Server-Fehler 21642 (Verbindungsserver bereits vorhanden) wurde ausgelöst  
 Wenn ein Oracle-Verleger zum ersten Mal konfiguriert wird, wird für die Verbindung zwischen dem Verleger und dem Verteiler ein Verbindungsservereintrag erstellt. Der Verbindungsserver hat denselben Namen wie der Oracle-TNS-Dienst. Wenn Sie versuchen, einen Verbindungsserver mit demselben Namen zu erstellen, wird die folgende Fehlermeldung angezeigt:  
  
 "Für heterogene Verleger ist ein Verbindungsserver erforderlich. Ein Verbindungsserver mit dem Namen '*\<LinkedServerName>*' ist bereits vorhanden. Entfernen Sie den Verbindungsserver, oder wählen Sie einen anderen Verlegernamen aus."  
  
 Dieser Fehler kann auftreten, wenn Sie versuchen, den Verbindungsserver direkt zu erstellen, oder die Beziehung zwischen dem Oracle-Verleger und dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler zuvor gelöscht haben und jetzt versuchen, diese Beziehung neu zu konfigurieren. Wenn Sie beim Neukonfigurieren des Verlegers diese Fehlermeldung erhalten, löschen Sie den Verbindungsserver mit [sp_dropserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md).  
  
 Wenn Sie über eine Verbindungsserververbindung eine Verbindung mit dem Oracle-Verleger herstellen müssen, erstellen Sie einen anderen TNS-Dienstnamen, und verwenden Sie dann für den Aufruf von [sp_addlinkedserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) diesen Namen. Informationen zum Erstellen von TNS-Dienstnamen finden Sie in der Oracle-Dokumentation.  
  
## <a name="sql-server-error-21617-is-raised"></a>SQL Server-Fehler 21617 wurde ausgelöst  
 Für das Veröffentlichen mit Oracle wird die Oracle-Anwendung SQL*PLUS verwendet, um das Paket mit Unterstützungscode für den Verleger in die Oracle-Datenbank herunterzuladen. Bevor der Oracle-Verleger konfiguriert wird, überprüft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ob auf SQL\*PLUS über den Systempfad auf dem Verteiler zugegriffen werden kann. Wenn SQL\*PLUS nicht geladen werden kann, wird die folgende Meldung angezeigt:  
  
 "SQL*PLUS konnte nicht ausgeführt werden. Stellen Sie sicher, dass die aktuelle Version des Oracle-Clientcodes auf dem Verteiler installiert ist."  
  
 Suchen Sie nach SQL\*PLUS auf dem Verteiler. Bei einer Oracle 10g-Clientinstallation lautet der Name dieser ausführbaren Datei sqlplus.exe. Sie ist normalerweise in %ORACLE_HOME%/bin installiert. Um zu überprüfen, ob der Pfad von SQL\*PLUS im Systempfad angezeigt wird, untersuchen Sie den Wert der Systemvariablen **Path**:  
  
1.  Klicken Sie mit der rechten Maustaste auf **Arbeitsplatz**, und klicken Sie dann auf **Eigenschaften**.  
  
2.  Klicken Sie auf die Registerkarte **Erweitert** , und klicken Sie dann auf **Umgebungsvariablen**.  
  
3.  Wählen Sie im Dialogfeld **Umgebungsvariablen** in der Liste **Systemvariablen** die Variable **Path** aus, und klicken Sie dann auf **Bearbeiten**.  
  
4.  Wenn im Dialogfeld **Systemvariable bearbeiten** der Pfad des Ordners, in dem sqlplus.exe enthalten ist, nicht im Textfeld **Wert der Variablen** vorhanden ist, bearbeiten Sie die Zeichenfolge entsprechend.  
  
5.  Klicken Sie in jedem geöffneten Dialogfeld auf **OK** , um den Vorgang zu beenden und die Änderungen zu speichern.  
  
 Wenn Sie sqlplus.exe auf dem Verteiler nicht finden können, installieren Sie die aktuelle Version der Oracle-Clientsoftware auf dem Verteiler. Weitere Informationen finden Sie unter [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="sql-server-error-21620-is-raised"></a>SQL Server-Fehler 21620 wurde ausgelöst  
 Wenn Sie eine Verbindung mit einer Oracle-Datenbank vor Version 8.1 herstellen, muss für die Oracle-Veröffentlichung mindestens die Version 9 der Oracle-Clientsoftware auf dem Verteiler installiert sein. Wenn Sie eine Verbindung mit einer Oracle-Datenbank der Version 8.1 oder höher herstellen, wird empfohlen, mindestens die Version 10 der Oracle-Clientsoftware zu verwenden.  
  
 Bevor der Oracle-Verleger konfiguriert wird, wird beim Veröffentlichen mit Oracle überprüft, ob es sich bei der Version von SQL*PLUS, auf die über den Systempfad auf dem Verteiler zugegriffen werden kann, um Version 9 oder höher handelt. Ist dies nicht der Fall, wird die folgende Meldung angezeigt:  
  
 "Die Version von SQL*PLUS, auf die über die Systemvariable 'Path' zugegriffen wird, ist nicht aktuell genug, um die Veröffentlichung mit Oracle zu unterstützen. Stellen Sie sicher, dass die aktuelle Version des Oracle-Clientcodes auf dem Verteiler installiert ist."  
  
 Wenn Sie mehrere Versionen der Oracle-Clientsoftware auf dem Verteiler installiert haben, müssen Sie sicherstellen, dass es sich bei der aktuellsten Version mindestens um Version 9 handelt und dass die Systemvariable Path zuerst auf diese Version verweist (sofern die neueste Version zuerst angezeigt wird, können auch Verweise auf andere Versionen angezeigt werden). Weitere Informationen zum Bearbeiten der Systemvariable Path finden Sie im Abschnitt "SQL Server-Fehler 21617 wurde ausgelöst" weiter oben in diesem Thema.  
  
## <a name="sql-server-error-21624-or-error-21629-is-raised"></a>SQL Server-Fehler 21624 oder 21629 wurde ausgelöst  
 Bei 64-Bit-Verteilern wird für das Veröffentlichen mit Oracle der OLE DB-Anbieter von Oracle (OraOLEDB.Oracle) verwendet. Stellen Sie sicher, dass der OLE DB-Anbieter von Oracle auf dem Verteiler installiert und registriert ist. Wenn der Anbieter nicht installiert und registriert ist, werden eine oder beide der folgenden Fehlermeldungen angezeigt:  
  
-   "Der registrierte OLE DB-Anbieter von Oracle, OraOLEDB.Oracle, wurde auf dem Verteiler '%s' nicht gefunden. Stellen Sie sicher, dass die aktuelle Version des OLE DB-Anbieters von Oracle auf dem Verteiler installiert und registriert ist."  
  
-   "Der CLSID-Registrierungsschlüssel, der anzeigt, dass der OLE DB-Anbieter von Oracle, OraOLEDB.Oracle, registriert wurde, ist auf dem Verteiler nicht vorhanden. Stellen Sie sicher, dass der OLE DB-Anbieter von Oracle auf dem Verteiler installiert und registriert ist."  
  
 Wenn Sie die Version 10g der Oracle-Clientsoftware verwenden, lautet der Dateiname des Anbieters OraOLEDB10.dll. Für Version 9i lautet er OraOLEDB.dll. Der Anbieter wird in %ORACLE_HOME%\BIN installiert (beispielsweise C:\oracle\product\10.1.0\Client_1\bin). Wenn Sie feststellen, dass der OLE DB-Anbieter von Oracle nicht auf dem Verteiler installiert ist, installieren Sie ihn über die von Oracle bereitgestellte Installations-CD mit der Oracle-Clientsoftware. Weitere Informationen finden Sie unter [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
 Wenn der OLE DB-Anbieter von Oracle installiert ist, stellen Sie sicher, dass er registriert ist. Führen Sie zum Registrieren der Anbieter-DLL den folgenden Befehl in dem Verzeichnis aus, in dem die DLL installiert ist. Beenden Sie die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz, und starten Sie sie dann erneut:  
  
1.  `regsvr32 OraOLEDB10.dll` oder `regsvr32 OraOLEDB.dll`.  
  
## <a name="sql-server-error-21626-or-error-21627-is-raised"></a>SQL Server-Fehler 21626 oder 21627 wurde ausgelöst  
 Um zu überprüfen, ob die Umgebung zum Veröffentlichen mit Oracle ordnungsgemäß konfiguriert ist, versucht [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mit den Anmeldeinformationen, die Sie während der Konfiguration angegeben haben, eine Verbindung mit dem Oracle-Verleger herzustellen. Wenn der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteiler keine Verbindung mit dem Oracle-Verleger herstellen kann, wird die folgende Fehlermeldung angezeigt:  
  
-   "Die Verbindung mit dem Oracle-Datenbankserver '%s' kann mithilfe des OLE DB-Anbieters von Oracle, OraOLEDB.Oracle, nicht hergestellt werden."  
  
 Wenn diese Fehlermeldung angezeigt wird, überprüfen Sie die Verbindung mit der Oracle-Datenbank, indem Sie SQL*PLUS direkt mit der gleichen Anmeldung und dem gleichen Kennwort ausführen, wie während der Konfiguration des Oracle-Verlegers angegeben. Weitere Informationen finden Sie im Abschnitt "Verbindung zwischen SQL Server-Verteiler und Oracle-Datenbankinstanz nicht möglich" weiter oben in diesem Thema.  
  
## <a name="sql-server-error-21628-is-raised"></a>SQL Server-Fehler 21628 wurde ausgelöst  
 Bei 64-Bit-Verteilern wird für das Veröffentlichen mit Oracle der OLE DB-Anbieter von Oracle (OraOLEDB.Oracle) verwendet. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] erstellt einen Registrierungseintrag, damit der Oracle-Anbieter in einem Prozess mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ausgeführt werden kann. Wenn beim Lesen oder Schreiben dieses Registrierungseintrags ein Problem auftritt, wird die folgende Fehlermeldung angezeigt:  
  
 "Die Registrierung des Verteilers '%s' kann nicht so aktualisiert werden, dass der OLE DB-Anbieter von Oracle, OraOLEDB.Oracle, in einem Prozess mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ausgeführt werden kann. Stellen Sie sicher, dass der aktuelle Anmeldename autorisiert ist, Registrierungsschlüssel im Besitz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] zu ändern."  
  
 Für das Veröffentlichen mit Oracle muss der Registrierungseintrag für 64-Bit-Verteiler vorhanden und auf **1** festgelegt sein. Wenn der Eintrag nicht vorhanden ist, versucht [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , ihn zu erstellen. Wenn der Eintrag vorhanden ist, aber auf **0**festgelegt wurde, wird die Einstellung nicht geändert. Die Konfiguration des Oracle-Verlegers erzeugt dann einen Fehler.  
  
 So zeigen Sie die Registrierungseinstellung an und ändern sie  
  
1.  Klicken Sie im **Startmenü**auf **Ausführen**.  
  
2.  Geben Sie **regedit** im Dialogfeld **Ausführen**ein, und klicken Sie dann auf **OK**.  
  
3.  Navigieren Sie zu HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\*\<InstanceName>*\Providers.  
  
     Unter Providers sollte sich ein Ordner mit dem Namen OraOLEDB.Oracle befinden. In diesem Ordner sollte sich der DWORD-Wert mit dem Namen **AllowInProcess**und dem Wert **1**befinden.  
  
4.  Wenn Sie feststellen, dass für **AllowInProcess** der Wert **0**festgelegt ist, ändern Sie den Registrierungseintrag auf **1**:  
  
    1.  Klicken Sie mit der rechten Maustaste auf den Eintrag, und klicken Sie dann auf **Ändern**.  
  
    2.  Geben Sie im Dialogfeld **Zeichenfolge bearbeiten** in das Feld **Wert** den Wert **1** ein.  
  
## <a name="sql-server-error-21684-is-raised"></a>SQL Server-Fehler 21684 wurde ausgelöst  
 Wenn das administrative Benutzerkonto nicht über ausreichende Berechtigungen verfügt, wird die folgende Fehlermeldung angezeigt:  
  
 "Der Administratoranmeldung für den '%s'-Oracle-Verleger sind unzureichende Berechtigungen zugeordnet."  
  
 Führen Sie zum Überprüfen der dem Benutzer erteilten Berechtigungen die folgende Abfrage aus: `SELECT * from session_privs`. Die Ausgabe sollte ähnlich der Folgenden aussehen:  
  
 `PRIVILEGE`  
  
 `------------------`  
  
 `CREATE SESSION`  
  
 `CREATE TABLE`  
  
 `CREATE PUBLIC SYNONYM`  
  
 `DROP PUBLIC SYNONYM`  
  
 `CREATE VIEW`  
  
 `CREATE SEQUENCE`  
  
 `CREATE PROCEDURE`  
  
 `CREATE TRIGGER`  
  
## <a name="you-encounter-permissions-issues-for-the-replication-user-schema"></a>Berechtigungsprobleme beim Benutzerschema für die Replikation  
 Das Benutzerschema für die Replikation muss über die im Abschnitt zum manuellen Erstellen des Benutzerschemas in [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md) beschriebenen Berechtigungen verfügen.  
  
## <a name="oracle-error-ora-01000"></a>Oracle-Fehler ORA-01000  
 Die Replikation verwendet für das Hinzufügen von Artikeln zu einer Veröffentlichung Cursor auf dem Oracle-Verleger. Während dieses Vorgangs kann es passieren, dass die Höchstzahl der auf dem Verleger verfügbaren Cursor überstiegen wird. In diesem Fall wird der folgende Fehler ausgelöst:  
  
 "ORA-01000: maximum open cursors exceeded"  
  
 Um dieses Problem zu vermeiden, sollten Sie für die Einstellung **max_open_cursors** in den Oracle-Datenbanken einen ausreichend großen Wert (mindestens 1000) sicherstellen. Weitere Informationen zu dieser Einstellung finden Sie in der Oracle-Dokumentation.  
  
## <a name="oracle-error-ora-01555"></a>Oracle-Fehler ORA-01555  
 Die folgende Oracle-Datenbankfehlermeldung bezieht sich nicht auf die Snapshotreplikation, sondern darauf, wie Oracle lesekonsistente Datensichten konstruiert:  
  
 "ORA-01555: Snapshot too old"  
  
 Oracle verwendet so genannte Rollbacksegmente, um lesekonsistente Datensichten zu erstellen, die den Stand zum Zeitpunkt der Ausführung einer SQL-Anweisung wiedergeben. Die Fehlermeldung "snapshot too old" (Snapshot zu alt) kann angezeigt werden, wenn die Rollbackinformationen von anderen gleichzeitigen Sitzungen überschrieben werden. Vor Oracle 9i wurde empfohlen, die Häufigkeit dieser Fehlermeldung durch Erhöhen der Größe und/oder Anzahl der Rollbacksegmente und Zuweisen großer Transaktionen zu einem bestimmten Rollbacksegment zu reduzieren.  
  
 Seit Oracle 9i gibt es das UNDO-Tabellenbereichskonzept, das an die Stelle der Rollbacksegmente getreten ist. Zur Vermeidung der Fehlermeldung "snapshot too old" in Oracle 9i sollten Sie wie folgt vorgehen:  
  
-   Erstellen Sie einen UNDO-Tabellenbereich mit ausreichend freiem Speicherplatz.  
  
-   Legen Sie für den Tabellenbereich die den Wert für Retention Guarantee fest (ab Oracle 10G).  
  
-   Konfigurieren Sie die Oracle-Initialisierungsparameter UNDO_MANAGEMENT und UNDO_RETENTION.  
  
 Weitere Informationen zur Fehlermeldung "snapshot too old" finden Sie in der Oracle-Dokumentation.  
  
## <a name="oracle-error-ora-22285"></a>Oracle-Fehler ORA-22285  
 Wenn eine Tabelle eine BFILE-Spalte enthält, werden die Daten für die Spalte im Dateisystem gespeichert. Dem Administratorkonto für die Replikation muss Zugriff auf das Verzeichnis gewährt werden, in dem die Daten gespeichert sind. Dabei ist die folgende Syntax zu verwenden:  
  
 `GRANT READ ON DIRECTORY <directory_name> TO <replication_administrative_user_schema>`  
  
 Wenn kein Zugriff gewährt wird, gibt der Protokolllese-Agent die folgende Fehlermeldung aus:  
  
 "ORA-22285: non-existent directory or file for FILEOPEN operation"  
  
## <a name="changes-are-made-that-require-reconfiguration-of-the-publisher"></a>Verleger muss aufgrund von Änderungen neu konfiguriert werden  
 Aufgrund von Änderungen der Metadatentabellen oder der Prozeduren für die Replikation muss die Zuordnung des Verlegers gelöscht oder neu konfiguriert werden. Wenn Sie den Verleger neu konfigurieren möchten, müssen Sie die Zuordnung löschen und dann mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], Transact-SQL oder RMO neu konfigurieren. Informationen zum Konfigurieren des Verlegers finden Sie unter [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
 **So löschen Sie einen Oracle-Verleger (**SQL Server Management Studio**)**  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] eine Verbindung mit dem Verteiler für den Oracle-Verleger her, und erweitern Sie dann den Serverknoten.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Replikation**, und klicken Sie dann auf **Verteilereigenschaften**.  
  
3.  Deaktivieren Sie auf der Seite **Verleger** des Dialogfelds **Verteilereigenschaften** das Kontrollkästchen für den Oracle-Verleger.  
  
4.  Klicken Sie auf **OK**.  
  
 **So löschen Sie die Zuordnung eines Oracle-Verlegers (Transact-SQL)**  
  
-   Führen Sie **sp_dropdistpublisher**aus. Weitere Informationen finden Sie unter [Sp_dropdistpublisher &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren eines Oracle-Verlegers](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
