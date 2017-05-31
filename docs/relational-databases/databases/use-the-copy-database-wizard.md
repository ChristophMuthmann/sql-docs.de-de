---
title: Verwenden des Assistenten zum Kopieren von Datenbanken | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.cdw.packageconfiguration.f1
- sql13.swb.cdw.schedule.f1
- sql13.swb.cdw.transfermethod.f1
- sql13.swb.cdw.databases.f1
- sql13.swb.cdw.destinationconfiguration.f1
- sql13.swb.cdw.destination.f1
- sql13.swb.cdw.locationofsourcedbfiles.f1
- sql13.swb.cdw.source.f1
- sql13.swb.cdw.selectdatabaseobjects.f1
- sql13.swb.cdw.complete.f1
- sql13.swb.cdw.welcome.f1
helpviewer_keywords:
- Copy Database Wizard
- starting Copy Database Wizard
ms.assetid: 7a999fc7-0a26-4a0d-9eeb-db6fc794f3cb
caps.latest.revision: 64
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 26b3c7967d7549f6f192afcac64888dcb68d6c7c
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="use-the-copy-database-wizard"></a>Verwenden des Assistenten zum Kopieren von Datenbanken
Der Assistent zum Kopieren von Datenbanken verschiebt oder kopiert Datenbanken und bestimmte Serverobjekte ohne Serverausfallzeiten problemlos von einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz zu einer anderen. Mit diesem Assistenten können Sie folgende Aktionen ausführen: 
  
-   Einen Quell- und Zielserver auswählen.  
  
-   Datenbank(en) zum Verschieben oder Kopieren auswählen.  
  
-   Den Dateispeicherort für die Datenbank(en) angeben.  
  
-   Anmeldungen auf den Zielserver kopieren.  
  
-   Zusätzliche unterstützende Objekte, Aufträge, benutzerdefinierte gespeicherte Prozeduren und Fehlermeldungen kopieren.  
  
-   Zeitpunkt zum Verschieben oder Kopieren der Datenbank(en) planen.  
  

  
##  <a name="Restrictions"></a> Einschränkungen  
  
-   Der Assistent zum Kopieren von Datenbanken ist nicht in der Express Edition verfügbar.  
  
-   Der Assistent zum Kopieren von Datenbanken kann nicht zum Kopieren oder Verschieben von Datenbanken verwendet werden, für die Folgendes gilt:
  
    -   Es handelt sich um Systemdatenbanken.
  
    -   Es handelt sich um für die Replikation markierte Datenbanken.
  
    -   Es handelt sich um Datenbanken, die als „Kein Zugriff“, „Lädt“, „Offline“, „Wird wiederhergestellt“, „Fehlerverdächtig“ oder „Notfallmodus“ markiert sind.
    
    -   Es handelt sich um Datenbanken, die Daten oder Protokolldateien in Microsoft Azure-Speicher speichern.
  
-   Eine Datenbank kann nicht zu einer früheren Version von SQL Server verschoben oder kopiert werden.
  
-   Wenn Sie die Option **Verschieben** auswählen, wird die Quelldatenbank nach dem Verschieben der Datenbank automatisch vom Assistenten gelöscht. Wenn Sie die Option **Kopieren** auswählen, wird die Quelldatenbank vom Assistenten zum Kopieren von Datenbanken nicht gelöscht.  Darüber hinaus werden ausgewählte Serverobjekte eher an das Ziel kopiert als verschoben. Die Datenbank ist das einzige Objekt, das tatsächlich verschoben wird.
  
-   Wenn Sie den Volltextkatalog mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object-Methode verschieben, müssen Sie den Index nach dem Verschieben wieder auffüllen.  
  
-   Die Methode zum **Trennen und Anfügen** trennt die Datenbank, verschiebt oder kopiert die MDF-, NDF- und LDF-Dateien der Datenbank und fügt die Datenbank am neuen Zielort wieder an. Bei der Methode zum **Trennen und Anfügen** können zur Vermeidung von Datenverlust und Inkonsistenzen keine aktiven Sitzungen an die verschobene oder kopierte Datenbank angefügt werden. Bei der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object-Methode werden aktive Sitzungen zugelassen, da die Datenbank nie offline gesetzt wird.  

-    Das Übertragen von SQL Server-Agentaufträgen, die auf Datenbanken verweisen, die nicht bereits auf dem Zielserver vorhanden sind, führen zum Fehlschlagen des gesamten Vorgangs.  Der Assistent versucht, einen SQL Server-Agentauftrag zu erstellen, bevor die Datenbank erstellt wurde.  Problemumgehung:
     1.    Erstellen Sie eine Shelldatenbank auf dem Zielserver mit demselben Namen wie die zu verschiebende oder zu kopierende Datenbank.  Weitere Informationen finden Sie unter [Erstellen einer Datenbank](../../relational-databases/databases/create-a-database.md).
     
     2.    Wählen Sie auf der Seite **Zieldatenbank konfigurieren** die Option **Löschen Sie jede auf dem Zielserver vorhandene Datenbank, die denselben Namen hat, und setzen Sie dann die Datenbankübertragung fort, wobei vorhandene Datenbankdateien überschrieben werden**aus.

> **WICHTIG!** Die Methode zum **Trennen und Anfügen** bewirkt, dass für den Besitz der Quell- und Zieldatenbank die Anmeldung festgelegt wird, die den **Assistenten zum Kopieren der Datenbank**ausführt.  Informationen zum Ändern des Besitzes einer Datenbank finden Sie unter [ALTER AUTHORIZATION (Transact-SQL)](../../t-sql/statements/alter-authorization-transact-sql.md) .
  
  
##  <a name="Prerequisites"></a> Voraussetzungen  
-   Stellen Sie sicher, dass SQL Server-Agent auf dem Zielserver gestartet wird.  

-   Stellen Sie sicher, dass die Daten- und Protokolldateiverzeichnisse auf dem Quellserver über den Zielserver erreicht werden können.

-   Unter der Methode zum **Trennen und Anfügen** muss ein Proxy für den SQL Server-Agent für das SSIS-Subsystem auf dem Zielserver mit Anmeldeinformationen vorhanden sein, mit denen auf die Dateisysteme von Quell- und Zielserver zugegriffen werden kann. Weitere Informationen zu Proxys finden Sie unter [Erstellen eines Proxys für den SQL Server-Agent](~/ssms/agent/create-a-sql-server-agent-proxy.md).

> **WICHTIG!** Unter der Methode zum **Trennen und Anfügen** -Methode tritt ein Fehler beim Kopieren oder Verschieben auf, wenn kein Integration Services-Proxykonto verwendet wird.  In bestimmten Situationen wird die Quelldatenbank nicht erneut an den Quellserver angefügt und alle NTFS-Sicherheitsberechtigungen werden aus den Daten- und Protokolldateien entfernt.  Navigieren Sie in diesem Fall zu den Dateien, wenden Sie die entsprechenden Berechtigungen erneut an, und fügen Sie die Datenbank anschließend erneut an Ihre Instanz von SQL Server an.
  
##  <a name="Recommendations"></a> Empfehlungen  
  
-   Um die optimale Leistung einer aktualisierten Datenbank sicherzustellen, führen Sie [sp_updatestats (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md) (Statistikupdate) für die aktualisierte Datenbank aus.  
  
-   Wenn Sie eine Datenbank auf eine andere Serverinstanz verschieben oder kopieren, müssen Sie möglicherweise einen Teil oder auch alle Metadaten für die Datenbank, wie Anmeldenamen und Aufträge, auf der anderen Serverinstanz erneut erstellen, um Benutzern und Anwendungen ein konsistentes Verhalten zu bieten. Weitere Informationen finden Sie unter [Verwalten von Metadaten beim Bereitstellen einer Datenbank auf einer anderen Serverinstanz &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  

  
###  <a name="Permissions"></a> Berechtigungen  
 Sie müssen auf dem Quell- und Zielserver ein Mitglied der festen Serverrolle **sysadmin** sein.  
  
##  <a name="Overview"></a> Seiten des Assistenten zum Kopieren von Datenbanken 
Starten Sie den **Assistenten zum Kopieren von Datenbanken** in SQL Server Management Studio über den **Objekt-Explorer** , und erweitern Sie dann die Option **Datenbanken**.  Klicken Sie mit der rechten Maustaste auf eine Datenbank, zeigen Sie auf **Tasks**, und klicken Sie dann auf **Datenbank kopieren**.  Wenn die Seite **Willkommen des Assistenten zum Kopieren von Datenbanken** angezeigt wird, klicken Sie auf **Weiter**.


### <a name="select-a-source-server"></a>Quellserver auswählen
Diese Seite wurde dazu verwendet, um den Server anzugeben, auf dem sich die zu verschiebende oder kopierende Datenbank befindet, und die Anmeldeinformationen einzugeben.  Nach der Auswahl der Authentifizierungsmethode und der Eingabe der Anmeldeinformationen, klicken Sie auf **Weiter** , um die Verbindung zum Quellserver herzustellen.  Diese Verbindung bleibt während der ganzen Sitzung bestehen.

-    **Quellserver**  
Diese Option wurde dazu verwendet, um den Namen des Servers zu identifizieren, auf dem sich die zu verschiebenden oder zu kopierenden Datenbanken befinden.  Nehmen Sie die Eingabe manuell vor, oder klicken Sie auf die Auslassungspunkte, um zum gewünschten Server zu navigieren.  Der Server muss mindestens SQL Server 2005 entsprechen.

-    **Windows-Authentifizierung verwenden**  
Ermöglicht den Benutzern eine Verbindung über ein Microsoft Windows-Benutzerkonto.

-    **SQL Server-Authentifizierung verwenden**  
Ermöglicht den Benutzern, mithilfe eines Benutzernamens und eines Kennworts für die SQL Server-Authentifizierung eine Verbindung aufzubauen.

     -    **Benutzername**  
Diese Option wurde dazu verwendet, um den Benutzernamen für die Verbindung einzugeben. Diese Option ist nur verfügbar, wenn Sie die **SQL Server-Authentifizierung**für die Verbindungsherstellung ausgewählt haben.

     -    **Kennwort**  
Diese Option wurde dazu verwendet, um das Kennwort für die Anmeldung einzugeben. Diese Option ist nur verfügbar, wenn Sie die **SQL Server-Authentifizierung**für die Verbindungsherstellung ausgewählt haben.

###  <a name="select-a-destination-server"></a>Zielserver auswählen
Mithilfe dieser Seite wurde der Server angegeben, auf den die Datenbank verschoben oder kopiert wird.  Wenn Quell- und Zielserver auf derselben Serverinstanz eingerichtet sind, wird eine Kopie der Datenbank erstellt.  In diesem Fall müssen Sie die Datenbank zu einem späteren Zeitpunkt im Assistenten umbenennen.  Der Name der Quelldatenbank kann nur für die kopierte oder verschobene Datenbank verwendet werden, wenn keine Namenskonflikte auf dem Zielserver bestehen.  Wenn Namenskonflikte bestehen, müssen Sie diese manuell auf dem Zielserver lösen, bevor Sie den Namen der Quelldatenbank verwenden können.
  
-    **Zielserver**  
Diese Option wurde dazu verwendet, um den Namen des Servers zu identifizieren, auf dem sich die zu verschiebenden oder zu kopierenden Datenbanken befinden sollen.  Nehmen Sie die Eingabe manuell vor, oder klicken Sie auf die Auslassungspunkte, um zum gewünschten Server zu navigieren.  Der Server muss mindestens SQL Server 2005 entsprechen.

     >**HINWEIS:** Sie können einen gruppierten Server als Ziel verwenden. Mit dem Assistenten zum Kopieren von Datenbanken wird sichergestellt, dass Sie nur freigegebene Laufwerke auf einem gruppierten Zielserver auswählen.

-    **Windows-Authentifizierung verwenden**  
Ermöglicht den Benutzern eine Verbindung über ein Microsoft Windows-Benutzerkonto.

-    **SQL Server-Authentifizierung verwenden**  
Ermöglicht den Benutzern, mithilfe eines Benutzernamens und eines Kennworts für die SQL Server-Authentifizierung eine Verbindung aufzubauen.

     -    **Benutzername**  
Diese Option wurde dazu verwendet, um den Benutzernamen für die Verbindung einzugeben. Diese Option ist nur verfügbar, wenn Sie die **SQL Server-Authentifizierung**für die Verbindungsherstellung ausgewählt haben.

     -    **Kennwort**  
Diese Option wurde dazu verwendet, um das Kennwort für die Anmeldung einzugeben. Diese Option ist nur verfügbar, wenn Sie die **SQL Server-Authentifizierung**für die Verbindungsherstellung ausgewählt haben.

###  <a name="select-the-transfer-method"></a>Übertragungsmethode auswählen
 
-    **Methode zum Trennen und Anfügen verwenden**  
Trennt die Datenbank vom Quellserver, kopiert die Datenbankdateien (MDF, NDF und LDF) auf den Zielserver und fügt die Datenbank dem Zielserver hinzu. Diese Methode ist normalerweise die schnellere, weil die Hauptarbeit im Lesen des Quelldatenträgers und im Schreiben auf den Zieldatenträger besteht. Es ist keine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Logik zum Erstellen von Objekten innerhalb der Datenbank oder zum Erstellen von Datenspeicherstrukturen erforderlich. Diese Methode kann zeitaufwändiger sein, wenn die Datenbank große zugeordnete, aber nicht verwendete Speicherbereiche enthält. Bei einer neuen und fast leeren Datenbank, die mit zugeordnetem Speicher von 100 MB erstellt wurde, werden beispielsweise die gesamten 100 MB kopiert, auch wenn nur 5 MB belegt sind.

     > **HINWEIS:** Bei dieser Methode ist die Datenbank während der Übertragung für die Benutzer nicht verfügbar.

     -    **Bei Auftreten eines Fehlers Quelldatenbank erneut anfügen**  
     Wenn eine Datenbank kopiert wird, werden die ursprünglichen Datenbankdateien immer erneut an den Quellserver angefügt. Verwenden Sie dieses Feld, um ursprüngliche Dateien erneut an die Quelldatenbank anzufügen, wenn eine Datenbankverschiebung nicht beendet werden kann. 
  
-    **SMO-Methode (SQL Management Object) verwenden**  
     Diese Methode liest die Definition jedes Datenbankobjekts in der Quelldatenbank und erstellt alle Objekte in der Zieldatenbank. Dann werden die Daten aus den Quelltabellen in die Zieltabellen übertragen, wobei Indizes und Metadaten neu erstellt werden.
  
     > [!NOTE]
     >  Datenbankbenutzer können während der Übertragung weiter auf die Datenbank zugreifen. 
  
###  <a name="select-database"></a>Datenbank auswählen
Wählen Sie die Datenbank(en) aus, die vom Quellserver auf den Zielserver kopiert oder verschoben werden soll(en).  Weitere Informationen finden Sie unter [Einschränkungen](#Restrictions) am Anfang dieses Themas.  
  
-    **Verschieben**  
Verschiebt die Datenbank auf den Zielserver.

-    **Kopieren**  
Kopiert die Datenbank auf den Zielserver.

-    **Quelle**  
Zeigt die auf dem Quellserver vorhandenen Datenbanken an.

-    **Status**  
Zeigt verschiedene Informationen zur Quelldatenbank an.

-    **Aktualisieren**  
Aktualisiert die Liste der Datenbanken.
  
### <a name="configure-destination-database"></a>Zieldatenbank konfigurieren
Ändern Sie ggf. den Datenbanknamen, und geben Sie den Speicherort sowie die Namen der Datenbankdateien an.  Diese Seite wird einmal für jede Datenbank angezeigt, die verschoben oder kopiert wird.

-    **Quelldatenbank**  
Der Name der Quelldatenbank.  Das Textfeld kann nicht bearbeitet werden.

-    **Zieldatenbank**  
Der Name der zu erstellenden Zieldatenbank, der nach Bedarf geändert werden kann.

-    **Zieldatenbankdateien:**  
     
     -    **Filename**  
Der Name der zu erstellenden Zieldatenbankdatei, der nach Bedarf geändert werden kann.

     -    **Größe (MB)**  
Die Größe der Zieldateidatenbankdatei in Megabyte.

     -    **Zielordner**  
Der Ordner auf dem Zielserver, der als Host für die Zieldatenbankdatei dient und nach Bedarf geändert werden kann.

     -    **Status**  
Status

-    **Wenn die Zieldatenbank bereits vorhanden ist:**  
     Entscheiden Sie, welche Aktion ausgeführt werden soll, wenn die Zieldatenbank bereits vorhanden ist.

     -    **Beenden Sie die Übertragung, wenn am Ziel eine Datenbank oder Datei vorhanden ist, die denselben Namen hat.**

     -    **Löschen Sie jede auf dem Zielserver vorhandene Datenbank, die denselben Namen hat, und setzen Sie dann die Datenbankübertragung fort, wobei vorhandene Datenbankdateien überschrieben werden.**

###  <a name="select-server-objects"></a>Serverobjekte auswählen 
Diese Seite ist nur verfügbar, wenn Quelle und Ziel verschiedene Server sind.  
  
-    **Verfügbare verbundene Objekte**  
Listet die zum Übertragen auf die Zielserver verfügbaren Objekte auf.  Wenn Sie ein Objekt einfügen möchten, klicken Sie im Feld **Verfügbare verbundene Objekte** auf den Objektnamen und dann auf die Schaltfläche **>>** , um das Objekt in das Feld **Ausgewählte verbundene Objekte** zu verschieben. 

-    **Ausgewählte verbundene Objekte**  
Listet Objekte auf, die auf den Zielserver übertragen werden.  Wenn Sie ein Objekt ausschließen möchten, klicken Sie im Feld **Ausgewählte verbundene Objekte** auf den Objektnamen und dann auf die Schaltfläche **<\<** , um das Objekt in das Feld **Verfügbare verbundene Objekte** zu verschieben.  Standardmäßig werden alle Objekte aller ausgewählten Typen übertragen. Wenn Sie einzelne Objekte beliebiger Typen auswählen möchten, klicken Sie auf die Schaltfläche mit den drei Punkten (...) neben dem entsprechenden Objekttyp im Feld **Ausgewählte verbundene Objekte** .  Dadurch wird ein Dialogfeld geöffnet, in dem Sie einzelne Objekte auswählen können.

-    **Liste der Serverobjekte** 

      -    **Anmeldungen (standardmäßig ausgewählt)** 
  
     -    **Aufträge des SQL Server-Agents**  
  
     -    **Benutzerdefinierte Fehlermeldungen**  
  
     -    **Endpunkte**  
  
     -    **Volltextkatalog** 
  
     -    **SSIS-Paket**  
     
     -    **Gespeicherte Prozeduren aus der master-Datenbank** 
          >**HINWEIS:** Erweiterte gespeicherte Prozeduren und deren zugeordnete DLLs sind vom automatischen Kopieren ausgenommen.  
    
  
###   <a name="location-of-source-database-files"></a>Speicherort der Quelldatenbankdateien
Diese Seite ist nur verfügbar, wenn Quelle und Ziel verschiedene Server sind.  Geben Sie eine Dateisystemfreigabe an, die die Datenbankdateien auf dem Quellserver enthält.
  
-    **Datenbank**  
     Zeigt die Namen der Datenbanken an, die verschoben werden.  
  
-    **Speicherort des Ordners**  
Der Ordnerspeicherort der Datenbankdateien auf dem Quellserver.
Beispiel: `C:\Program Files\Microsoft SQL Server\MSSQL110.MSSQLSERVER\MSSQL\DATA`

  
-    **Dateifreigabe auf dem Quellserver**  
Die Dateifreigabe, die die Datenbankdateien auf dem Quellserver enthält.  Geben Sie die Freigabe manuell ein, oder klicken Sie auf die Auslassungspunkte, um zur Freigabe zu navigieren.
Beispiel: `\\server_name\C$\Program Files\Microsoft SQL Server\MSSQL110.MSSQLSERVER\MSSQL\Data`

### <a name="configure-the-package"></a>Paket konfigurieren
Der Assistent zum Kopieren von Datenbanken erstellt ein SSIS-Paket für die Übertragung der Datenbank.

-    **Paketspeicherort**  
Zeigt an, wohin das SSIS-Paket geschrieben wird.

-    **Paketname**  
Es wird ein Standardname für das SSIS-Paket erstellt, der nach Bedarf geändert werden kann.

-    **Protokollierungsoptionen**  
Wählen Sie aus, ob die Protokollierungsinformationen im Windows-Ereignisprotokoll oder in einer Textdatei gespeichert werden sollen.

-    **Fehlerprotokollpfad**  
Diese Option ist nur bei ausgewählter Option zum Protokollieren der Textdatei verfügbar.  Stellen Sie einen Pfad für den Speicherort der Protokolldatei bereit. 

### <a name="schedule-the-package"></a>Zeitplan für Paket
Geben Sie den Zeitpunkt für den Beginn des Kopier- oder Verschiebungsvorgangs an.  Wenn Sie kein Systemadministrator sind, müssen Sie ein Proxykonto für den SQL Server-Agent angeben, das Zugriff auf das Subsystem zur Integration Services-Paketausführung (SSIS) hat.

> **WICHTIG!** Ein Integration Services-Proxykonto muss unter der Methode zum **Trennen und Anfügen** verwendet werden.  

-    **Sofort ausführen**  
     Das SSIS-Paket wird nach Abschluss des Assistenten ausgeführt.
  
-    **Zeitplan**  
     Das SSIS-Paket wird nach einem Zeitplan ausgeführt. 
  
     -    **Zeitplan ändern**   
Öffnet das Dialogfeld **Neuer Auftragszeitplan** .  Nehmen Sie die Konfiguration nach Bedarf vor.  Wenn Sie fertig sind, klicken Sie auf **OK** .


-    **Integration Services-Proxykonto** Wählen Sie ein verfügbares Proxykonto aus der Dropdownliste aus.  Wenn Sie die Übertragung planen möchten, muss für den Benutzer mindestens ein Proxykonto verfügbar sein, das mit der Berechtigung für das Subsystem **SSIS-Paketausführung**konfiguriert ist.

        Wenn Sie ein Proxykonto für die SSIS-Paketausführung erstellen möchten, erweitern Sie im **Objekt-Explorer**den **SQL Server-Agent**, erweitern Sie **Proxys**, klicken Sie mit der rechten Maustaste auf **SSIS-Paketausführung**, und klicken Sie dann auf **Neuer Proxy**.

### <a name="complete-the-wizard"></a>Assistenten abschließen
Zeigt eine Zusammenfassung der ausgewählten Optionen an.  Klicken Sie auf **Zurück** , um eine Option zu ändern.  Klicken Sie auf **Fertig stellen** , um das SSIS-Paket zu erstellen. Die Statusinformationen zum Ausführen des **Assistenten zum Kopieren von Datenbanken** werden auf der Seite **Vorgang wird ausgeführt**überwacht.

-    **Aktion**  
 Listet jede Aktion auf, die ausgeführt wird.

-    **Status**  
 Gibt an, ob die Aktion insgesamt erfolgreich war oder fehlgeschlagen ist.

-    **MessageBox**  
Stellt alle von jedem Schritt zurückgegebenen Meldungen bereit.

##  <a name="Examples"></a> Beispiele
### <a name="common-steps"></a>**Allgemeine Schritte** 
Unabhängig davon, ob Sie sich für **Verschieben** oder **Kopieren**, **Trennen und Anfügen** oder **SMO**entscheiden, sind die unten aufgeführten fünf Schritte identisch.  Aus Gründen der Übersichtlichkeit sind die Schritte hier einmal aufgelistet und alle Beispiele beginnen mit **Schritt 6**.

1.    Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz des SQL Server-Datenbankmoduls her, und erweitern Sie anschließend diese Instanz.

2.    Erweitern Sie **Datenbanken**, klicken Sie mit der rechten Maustaste auf die gewünschte Datenbank, zeigen Sie auf **Tasks**, und klicken Sie anschließend auf **Datenbank kopieren...**.

3.    Wenn die Seite **Willkommen des Assistenten zum Kopieren von Datenbanken** angezeigt wird, klicken Sie auf **Weiter**.

4.    Seite**Quellserver auswählen** : Geben Sie den Server an, auf dem sich die zu verschiebende oder zu kopierende Datenbank befindet.  Wählen Sie die Authentifizierungsmethode aus.  Wenn **SQL Server-Authentifizierung verwenden** ausgewählt wird, müssen Sie Ihre Anmeldeinformationen eingeben.  Klicken Sie auf **Weiter** , um die Verbindung mit dem Quellserver herzustellen.  Diese Verbindung bleibt während der ganzen Sitzung bestehen.

5.    Seite**Zielserver auswählen** : Geben Sie den Server an, auf den die Datenbank verschoben oder kopiert werden soll.  Wählen Sie die Authentifizierungsmethode aus.  Wenn **SQL Server-Authentifizierung verwenden** ausgewählt wird, müssen Sie Ihre Anmeldeinformationen eingeben.  Klicken Sie auf **Weiter** , um die Verbindung mit dem Quellserver herzustellen.  Diese Verbindung bleibt während der ganzen Sitzung bestehen.

     > **HINWEIS:** Sie können den Assistenten zum Kopieren von Datenbanken über eine beliebige Datenbank starten.  Sie können den Assistenten zum Kopieren von Datenbanken entweder auf dem Quell- oder Zielserver starten.
  
### <a name="a--move-database-using-detach-and-attach-method-to-an-instance-on-a-different-physical-server--a-login-and-sql-server-agent-job-will-be-moved-as-well"></a>**A.  Verschieben Sie die Datenbank mithilfe der Methode zum Trennen und Anfügen in eine Instanz auf einem anderen physischen Server.  Ebenso werden eine Anmeldung und ein SQL Server-Agentauftrag verschoben.**  
Im folgenden Beispiel wird die `Sales` -Datenbank, eine Windows-Anmeldung namens `contoso\Jennie` und ein SQL Server-Agentauftrag namens `Jennie’s Report` aus einer Instanz von SQL Server 2008 auf `Server1` in eine Instanz von SQL Server 2016 auf `Server2`verschoben.  `Jennie’s Report` verwendet die `Sales` -Datenbank.  `Sales` ist nicht bereits auf dem Zielserver, `Server2`, vorhanden.  `Server1` wird einem anderen Team neu zugewiesen, nachdem die Datenbank verschoben wurde.
  
6.    Wie oben unter [Einschränkungen](#Restrictions)erwähnt, muss beim Übertragen eines SQL Server-Agentauftrags, der auf eine Datenbank verweist, die noch nicht auf dem Zielserver vorhanden ist, eine Shelldatenbank auf dem Zielserver erstellt werden.  Erstellen Sie eine Shelldatenbank namens `Sales` auf dem Zielserver. 

7.    Zurück beim **Assistenten**auf der Seite **Übertragungsmethode auswählen** : Überprüfen und verwalten Sie die Standardwerte.  Klicken Sie auf **Weiter**.
  
8.    Seite**Datenbanken auswählen** : Aktivieren Sie das Kontrollkästchen **Verschieben** für die gewünschte Datenbank, `Sales`.  Klicken Sie auf **Weiter**.
  
9.    Seite**Zieldatenbank konfigurieren** : Der **Assistent** hat erkannt, dass `Sales` bereits auf dem Zielserver vorhanden ist, wie oben in **Schritt 6** erstellt, und hat `_new` an den Namen der **Zieldatenbank** angefügt.  Löschen Sie `_new` aus dem Textfeld **Zieldatenbank** .  Ändern Sie bei Bedarf die Werte für **Dateiname**und **Zielordner**.  Wählen Sie **Löschen Sie jede auf dem Zielserver vorhandene Datenbank, die denselben Namen hat, und setzen Sie dann die Datenbankübertragung fort, wobei vorhandene Datenbankdateien überschrieben werden**aus.  Klicken Sie auf **Weiter**.
  
10.    Seite**Serverobjekte auswählen** : Klicken Sie im Bereich **Ausgewählte verbundene Objekte:** auf die Schaltfläche mit den Auslassungspunkten für **Objektnamenanmeldungen**.  Wählen Sie unter **Kopieroptionen** die Option **Nur die ausgewählten Anmeldenamen kopieren:**aus.  Aktivieren Sie das Kontrollkästchen für **Alle Serveranmeldungen anzeigen**.  Aktivieren Sie das Feld **Anmeldung** für `contoso\Jennie`.  Klicken Sie auf **OK**.  Wählen Sie im Bereich **Verfügbare verbundene Objekte:** die Option **SQL Server-Agentaufträge** aus, und klicken Sie dann auf die Schaltfläche **>** .  Klicken Sie im Bereich **Ausgewählte verbundene Objekte:** auf die Schaltfläche mit den Auslassungspunkten für **SQL Server-Agentaufträge**.  Wählen Sie unter **Kopieroptionen** die Option **Nur die ausgewählten Aufträge kopieren:**aus.  Aktivieren Sie das Kontrollkästchen für `Jennie’s Report`.  Klicken Sie auf **OK**.  Klicken Sie auf **Weiter**.  
  
11.    Seite**Speicherort der Quelldatenbankdateien** : Klicken Sie auf die Schaltfläche mit den Auslassungspunkten für **Dateifreigabe auf dem Quellserver** , und navigieren Sie zum Speicherort für den angegebenen Ordner.  Verwenden Sie z. B. für den Ordnerspeicherort `D:\MSSQL13.MSSQLSERVER\MSSQL\DATA` die Option `\\Server1\D$\MSSQL13.MSSQLSERVER\MSSQL\DATA` für **Dateifreigabe auf dem Quellserver**.  Klicken Sie auf **Weiter**.
  
12.    Seite**Paket konfigurieren** : Geben Sie in das Textfeld **Paketname:**  `SalesFromServer1toServer2_Move`ein.  Aktivieren Sie das Feld **Übertragungsprotokolle speichern?** .  Wählen Sie in der Dropdownliste **Protokollierungsoptionen** die Option **Textdatei**aus.  Beachten Sie den **Pfad der Fehlerprotokolldatei**, und ändern Sie ihn nach Bedarf.  Klicken Sie auf **Weiter**.  
  
     > **HINWEIS:** Der **Pfad der Fehlerprotokolldatei** ist der Pfad auf dem Zielserver.
  
13.    Seite**Zeitplan für Paket** : Wählen Sie den entsprechenden Proxy aus der Dropdownliste **Integration Services-Proxykonto** aus.  Klicken Sie auf **Weiter**.

14.    Seite**Assistenten abschließen** : Überprüfen Sie die Zusammenfassung der ausgewählten Optionen.  Klicken Sie auf **Zurück** , um eine Option zu ändern.  Klicken Sie auf **Fertig stellen** , um den Task auszuführen.  Während der Übertragung werden die Statusinformationen zum Ausführen des **Assistenten** auf der Seite **Vorgang wird ausgeführt**überwacht.

15.    Seite**Vorgang wird ausgeführt** : Wenn der Vorgang erfolgreich ausgeführt wurde, klicken Sie auf **Schließen**.  Wenn der Vorgang nicht erfolgreich ausgeführt wurde, überprüfen Sie das Fehlerprotokoll, und klicken Sie möglicherweise zur weiteren Überprüfung auf **Zurück** .  Klicken Sie andernfalls auf **Schließen**.
  
16.    **Schritte nach dem Verschieben** : Erwägen Sie die Ausführung der folgenden T-SQL-Anweisungen auf dem neuen Host, `Server2`:
  
     ~~~ tsql 
     ALTER AUTHORIZATION ON DATABASE::Sales TO sa;

     ALTER DATABASE Sales 
     SET COMPATIBILITY_LEVEL = 130;

     USE Sales
     GO

     EXEC sp_updatestats;
     ~~~
 
17.    **Bereinigung nach den Schritten zum Verschieben**  
Da `Server1` zu einem anderen Team verschoben wird und der **Verschieben** -Vorgang nicht wiederholt wird, sollten Sie die folgenden Schritte ausführen:
     -    SSIS-Paket `SalesFromServer1toServer2_Move` auf `Server2`löschen.
     -    SQL Server-Agentauftrag `SalesFromServer1toServer2_Move` auf `Server2`löschen.
     -    SQL Server-Agentauftrag `Jennie’s Report` auf `Server1`löschen.
     -    Anmeldename `contoso\Jennie` auf `Server1`löschen.


### <a name="b-----copy-database-using-detach-and-attach-method-to-the-same-instance-and-set-recurring-schedule"></a>**B.     Kopieren der Datenbank mithilfe der Methode zum Trennen und Anfügen auf dieselbe Instanz und Festlegen eines wiederholten Zeitplans.**  
In diesem Beispiel wird die `Sales` -Datenbank als `SalesCopy` auf derselben Instanz kopiert und erstellt.  Danach wird `SalesCopy`wöchentlich neu erstellt.

6.    Seite**Übertragungsmethode auswählen** : Überprüfen und verwalten Sie die Standardwerte.  Klicken Sie auf **Weiter**.

7.    Seite**Datenbanken auswählen** : Aktivieren Sie das Kontrollkästchen **Kopieren** für die `Sales` -Datenbank.  Klicken Sie auf **Weiter**.

8.    Seite**Zieldatenbank konfigurieren** : Ändern Sie den Namen der **Zieldatenbank** in `SalesCopy`.  Ändern Sie bei Bedarf die Werte für **Dateiname**und **Zielordner**.  Wählen Sie **Löschen Sie jede auf dem Zielserver vorhandene Datenbank, die denselben Namen hat, und setzen Sie dann die Datenbankübertragung fort, wobei vorhandene Datenbankdateien überschrieben werden**aus.  Klicken Sie auf **Weiter**.

9.    Seite**Paket konfigurieren** : Geben Sie in das Textfeld **Paketname:**  `SalesCopy Weekly Refresh`ein.  Aktivieren Sie das Feld **Übertragungsprotokolle speichern?** .  Klicken Sie auf **Weiter**.

10.    Seite**Zeitplan für Paket** : Klicken Sie auf das Optionsfeld **Zeitplan:** und dann auf die Schaltfläche **Zeitplan ändern** . 
 
    1. Seite**Neuer Auftragszeitplan** : Geben Sie im Feld **Name** entsprechend `Weekly on Sunday`ein. 
          
    2. Klicken Sie auf **OK**.

11.    Wählen Sie den entsprechenden Proxy aus der Dropdownliste **Integration Services-Proxykonto** aus.  Klicken Sie auf **Weiter**.

12.    Seite**Assistenten abschließen** : Überprüfen Sie die Zusammenfassung der ausgewählten Optionen.  Klicken Sie auf **Zurück** , um eine Option zu ändern.  Klicken Sie auf **Fertig stellen** , um den Task auszuführen.  Während der Paketerstellung werden die Statusinformationen zum Ausführen des **Assistenten** auf der Seite **Vorgang wird ausgeführt**überwacht.

13.    Seite**Vorgang wird ausgeführt** : Wenn der Vorgang erfolgreich ausgeführt wurde, klicken Sie auf **Schließen**.  Wenn der Vorgang nicht erfolgreich ausgeführt wurde, überprüfen Sie das Fehlerprotokoll, und klicken Sie möglicherweise zur weiteren Überprüfung auf **Zurück** .  Klicken Sie andernfalls auf **Schließen**.

14.    Starten Sie den neu erstellten SQL Server-Agentauftrag `SalesCopy weekly refresh`manuell.  Überprüfen Sie den Auftragsverlauf, und stellen Sie sicher, dass `SalesCopy` jetzt auf der Instanz vorhanden ist.

  
##  <a name="FollowUp"></a> Anschlussaktivität: Nach dem Aktualisieren einer Datenbank  
 Nachdem Sie mithilfe des Assistenten zum Kopieren von Datenbanken eine Datenbank von einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]aktualisiert haben, ist die Datenbank sofort verfügbar und wird automatisch aktualisiert. Wenn die Datenbank Volltextindizes aufweist, werden diese beim Upgrade entweder importiert, zurückgesetzt oder neu erstellt, je nach der Einstellung der Servereigenschaft **Volltextupgrade-Option** . Wenn die Upgradeoption auf **Importieren** oder **Neu erstellen**festgelegt ist, sind die Volltextindizes während des Upgrades nicht verfügbar. Je nach Menge der indizierten Daten kann der Importvorgang mehrere Stunden dauern; die Neuerstellung sogar bis zu zehnmal länger. Wenn die Upgradeoption auf **Importieren**festgelegt und kein Volltextkatalog verfügbar ist, werden die zugehörigen Volltextindizes neu erstellt. Informationen zum Anzeigen oder Ändern der Einstellung der Eigenschaft **Volltextupgrade-Option** finden Sie unter [Verwalten und Überwachen der Volltextsuche auf einer Serverinstanz](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md).  
  
 War der Kompatibilitätsgrad einer Benutzerdatenbank vor dem Upgrade 100 oder höher, wird er nach dem Upgrade beibehalten. War der Kompatibilitätsgrad der aktualisierten Datenbank auf 90 festgelegt, wird er auf 100 erhöht, was dem niedrigsten unterstützten Kompatibilitätsgrad in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] entspricht. Weitere Informationen finden Sie unter [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
 
 ## <a name="Post"></a> Überlegungen nach dem Kopieren oder Verschieben
 Erwägen Sie die Ausführung der folgenden Schritte nach dem **Kopieren** oder **Verschieben**:
-    Besitzer der Datenbank(en) ändern, wenn die Methode zum Trennen und Anfügen verwendet wird.
-    Serverobjekte auf dem Quellserver nach dem **Verschieben**löschen.
-    Das vom Assistenten auf dem Zielserver erstellte SSIS-Paket löschen.
-    Den vom Assistenten auf dem Zielserver erstellten SQL Server-Agentauftrag löschen.

  
## <a name="more-information"></a>Weitere Informationen. 
 [Aktualisieren einer Datenbank durch Trennen und Anfügen &#40;Transact-SQL&#41;](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md)   
 [Erstellen eines Proxys für den SQL Server-Agent](http://msdn.microsoft.com/library/142e0c55-a8b9-4669-be49-b9dc602d5988)  
  
  


