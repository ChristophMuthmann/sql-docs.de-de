---
title: Installieren von SQL Server 2016 vom Installations-Assistenten aus (Setup) | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing SQL Server, steps
- Setup [SQL Server], steps
- SQL Server, installing
ms.assetid: 6ad23de1-2bab-4933-9122-c09f5565028d
caps.latest.revision: "91"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 41a4945a1d3a709e9fa105e3ebed4c7e010ee957
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="install-sql-server-from-the-installation-wizard-setup"></a>Installieren von SQL Server über den Installations-Assistenten (Setup)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > In diesem Artikel wird erläutert, wie SQL Server mit dem Installations-Assistenten installiert wird. Dies gilt für [!INCLUDE[SQLServer2016](../../includes/sssql15-md.md)] und [!INCLUDE[SQLServer2017](../../includes/sssqlv14-md.md)]. Weitere Informationen, die sich auf vorherige Versionen von SQL Server beziehen, finden Sie unter [Installieren von SQL Server 2014 über den Installations-Assistenten (Setup)](http://msdn.microsoft.com/library/ms143219(SQL.120).aspx).

Dieses Thema stellt Ihnen schrittweise die Installation einer neuen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unter Verwendung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup-Installations-Assistenten vor. Der Installations-Assistent für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält eine einzelne Funktionsstruktur für die Installation sämtlicher [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten, sodass Sie diese nicht einzeln installieren müssen. Weitere Informationen zur individuellen Installation der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Komponenten finden Sie unter [Installieren von SQL Server](../../database-engine/install-windows/install-sql-server.md#how-to-install-individual-components).  

 Die folgenden Themen dokumentieren weitere Möglichkeiten zur Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  

-   [Installieren von SQL Server von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
-   [Installieren von SQL Server mithilfe einer Konfigurationsdatei](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)  
  
-   [Installieren von SQL Server mit SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md)  
  
-   [Erstellen eines neuen SQL Server-Failoverclusters &#40;Setup&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)  
  
-   [Upgrade SQL Server Using the Installation Wizard (Setup) (Upgrade von SQL Server mithilfe des Installations-Assistenten (Setup))](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md) 

## <a name="get-the-installation-media"></a>Abrufen der Installationsmedien

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]
  
## <a name="prerequisites"></a>Voraussetzungen  
 Bevor Sie die Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]durchführen, sollten Sie die Themen in [Planen einer SQL Server-Installation](../../sql-server/install/planning-a-sql-server-installation.md)lesen.  
  
> [!NOTE]  
> Bei lokalen Installationen müssen Sie das Setup als Administrator ausführen. Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einer Remotefreigabe installieren, müssen Sie ein Domänenkonto verwenden, das Lese- und Ausführungsberechtigungen auf der Remotefreigabe hat.  
 
 ###  <a name="bkmk_ga_instalpatch"></a> Installieren einer Patchanforderung 

Microsoft hat ein Problem bei der speziellen Version von Microsoft VC++ 2013 Runtime-Binärdateien erkannt, die von SQL Server als vorausgesetzte Komponenten installiert werden. Wenn dieses Update an den VC++ Runtime-Binärdateien nicht installiert wird, können bei SQL Server in bestimmten Szenarios Stabilitätsprobleme auftreten. Bevor Sie SQL Server installieren, sollten Sie entsprechend den Anweisungen unter [Versionsanmerkungen zu SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) vorgehen, um festzustellen, ob Ihr Computer einen Patch für die VC-Runtime-Binärdateien benötigt.  
  
## <a name="to-install-includessnoversionincludesssnoversion-mdmd"></a>So installieren Sie [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]  
  
1.  Legen Sie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installationsmedium ein. Doppelklicken Sie im Stammordner auf Setup.exe. Wenn Sie eine Installation über eine Netzwerkfreigabe vornehmen möchten, suchen Sie den Stammordner in der Freigabe, und doppelklicken Sie auf setup.exe.  
  
2.  Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installationscenter wird vom Installations-Assistenten ausgeführt. Um eine neue Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu erstellen, klicken Sie im linken Navigationsbereich auf **Installation** und anschließend auf **Neue eigenständige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installation oder Hinzufügen von Funktionen zu einer vorhandenen Installation**.  

3.  Wählen Sie auf der Seite Product Key ein Optionsfeld aus, um anzugeben, ob Sie eine kostenlose Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installieren oder ob Sie über eine Produktionsversion des Produkts mit einem PID-Schlüssel verfügen. Weitere Informationen finden Sie unter [Editionen und unterstützte Funktionen von SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).  
  
     Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  

4.  Lesen Sie auf der Seite Lizenzbedingungen den Lizenzvertrag, und aktivieren Sie das Kontrollkästchen **Ich akzeptiere die Lizenzbedingungen** , wenn Sie diesen zustimmen. Klicken Sie anschließend auf **Weiter**. Falls Sie zur Verbesserung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]beitragen möchten, können Sie auch die Option zur Funktionsverwendung aktivieren und Berichte an [!INCLUDE[msCoName](../../includes/msconame-md.md)]senden.  
  
5.  Im Fenster Globale Regeln wechselt Setup automatisch weiter zum Fenster Produktupdates, sofern keine Regelfehler auftreten.  
  
6.  Die Seite [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update wird als Nächstes angezeigt, wenn das Kontrollkästchen [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update in Systemsteuerung\Alle Systemsteuerungselemente\Windows Update\Einstellungen ändern nicht aktiviert ist. Wenn Sie die Seite [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update mit einem Häkchen markieren, ändern sich die Computereinstellungen, und beim Suchen nach Windows Update werden die neuesten Updates angezeigt.  

7.  Auf der Seite für Produktupdates werden die neuesten verfügbaren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Produktupdates angezeigt. Wenn keine Produktupdates ermittelt wurden, zeigt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup diese Seite nicht an und geht automatisch zur Seite **Setupdateien installieren** über.  

8.  Auf der Seite Setupdateien installieren wird der Status angezeigt, während die Setupdateien heruntergeladen, extrahiert und installiert werden. Wenn ein Update für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup gefunden und angegeben wird, dass das Update eingeschlossen werden soll, wird dieses Update ebenfalls installiert. Wenn kein Update gefunden wird, wird das Setup automatisch fortgefahren. 
  
9. Unter **Installationsregeln** überprüft SQL Server-Setup auf potenzielle Probleme, die beim Ausführen des Setups auftreten können. Wenn Fehler auftreten, klicken Sie für weitere Informationen auf die Spalte **Status**. Klicken Sie andernfalls auf **Weiter**. 

10. Wählen Sie unter **Installationstyp** entweder das Ausführen einer neuen Installation oder das Hinzufügen von Funktionen zu einer bestehenden Installation aus. Klicken Sie auf **Weiter**. 
  
11. Wählen Sie auf der Seite Funktionsauswahl die Komponenten für die Installation aus. Um eine neue Instanz des Datenbankmoduls von SQL Server zu installieren, überprüfen Sie die **Datenbankmoduldienste**.

    Nach Auswahl des Funktionsnamens wird im Abschnitt **Funktionsbeschreibung** eine Beschreibung für die einzelnen Komponentengruppen angezeigt. Sie können jede beliebige Kombination von Kontrollkästchen aktivieren. Weitere Informationen finden Sie unter [Editionen und Komponenten von SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md) und unter [Editionen und unterstützte Funktionen für SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).
  
     Die erforderlichen Komponenten für die ausgewählten Funktionen werden im Abschnitt **Voraussetzungen für ausgewählte Funktionen** angezeigt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup installiert die erforderlichen Komponenten, die nicht bereits während des Installationsschritts installiert werden, der im weiteren Verlauf dieser Prozedur beschrieben wird.  
  
     Sie können auch ein benutzerdefiniertes Verzeichnis für freigegebene Komponenten angeben. Verwenden Sie dazu das Feld unten auf der Seite Funktionsauswahl. Um den Installationspfad für freigegebene Komponenten zu ändern, aktualisieren Sie den Pfadnamen im Feld unten im Dialogfeld, oder klicken Sie auf **Durchsuchen** , um zu einem Installationsverzeichnis zu wechseln. Der Standardinstallationspfad lautet [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)].  
  
     Der Pfad für die freigegebenen Komponenten muss ein absoluter Pfad sein. Der Ordner darf nicht komprimiert oder verschlüsselt werden. Zugeordnete Laufwerke werden nicht unterstützt.  
  
     SQL Server verwendet zwei Verzeichnisse für freigegebene Funktionen:
  
     * Freigegebenes Funktionsverzeichnis  
  
     * Freigegebenes Funktionsverzeichnis (x86)  
  
     Für jeden der oben erwähnten Optionen muss ein anderer Pfad angegeben werden.  
  
12. Im Fenster Funktionsregeln wird automatisch fortgefahren, wenn alle Regeln gültig sind.  
  
13. Geben Sie auf der Seite Instanzkonfiguration an, ob Sie eine Standardinstanz oder eine benannte Instanz installieren möchten. Weitere Informationen finden Sie unter [Instance Configuration](../../sql-server/install/instance-configuration.md#instance-configuration).  
  
     **Instanz-ID** – In der Standardeinstellung wird der Instanzname als Instanz-ID verwendet. So werden Installationsverzeichnisse und Registrierungsschlüssel für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]identifiziert. Dies ist der Fall für Standardinstanzen und benannte Instanzen. Bei einer Standardinstanz lauten Instanzname und Instanz-ID MSSQLSERVER. Um eine nicht standardmäßige Instanz-ID zu verwenden, geben Sie einen anderen Wert in das Feld **Instanz-ID** ein.  
  
    > [!NOTE]  
    >  Typische eigenständige Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]– sowohl Standardinstanzen als auch benannte Instanzen – verwenden keine Nichtstandardwerte für das Feld **Instanz-ID**.  
  
     Alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Service Packs und Updates werden für jede Komponente einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]übernommen.  
  
     **Installierte Instanzen** – Im Raster werden Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angezeigt, die sich auf dem Computer befinden, auf dem Setup ausgeführt wird. Wenn bereits eine Standardinstanz auf dem Computer installiert ist, muss eine benannte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]installiert werden.  
  
     Der Workflow für die weitere Installation ist von den Funktionen abhängig, die Sie für die Installation angegeben haben. Je nach Auswahl werden möglicherweise nicht alle Seiten angezeigt.  
  
14. Geben Sie auf der Seite Serverkonfiguration – Dienstkonten Anmeldekonten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste an. Welche Dienste tatsächlich auf dieser Seite konfiguriert werden, ist von den Funktionen abhängig, die Sie für die Installation ausgewählt haben.  
  
     Sie können allen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Diensten dasselbe Anmeldekonto zuweisen, oder Sie können jedes Dienstkonto einzeln konfigurieren. Außerdem können Sie angeben, ob Dienste automatisch starten sollen, manuell gestartet werden oder deaktiviert sind. [!INCLUDE[msCoName](../../includes/msconame-md.md)] , die Dienstkonten einzeln zu konfigurieren, um möglichst geringe Rechte für jeden Dienst bereitzustellen. Dabei erhalten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste die Berechtigungen, die mindestens erforderlich ist, um ihre Tasks auszuführen. Weitere Informationen finden Sie unter [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
     Um für alle Dienstkonten in dieser Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dasselbe Anmeldekonto anzugeben, geben Sie in den Feldern unten auf dieser Seite die entsprechenden Anmeldeinformationen ein.  
  
    > [!IMPORTANT]  
    > [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
    
    > [!NOTE]
    > Für Versionen ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]: Aktivieren Sie das Kontrollkästchen *SQL Server Database Engine Services Berechtigung zum Ausführen von Volumewartungstasks zuweisen*, um dem Dienstkonto [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] die Verwendung der [schnellen Dateiinitialisierung für Datenbanken](../../relational-databases/databases/database-instant-file-initialization.md) zu ermöglichen.
  
     Verwenden Sie die Seite Serverkonfiguration - Sortierung, um nicht standardmäßige Sortierungen für das [!INCLUDE[ssDE](../../includes/ssde-md.md)] und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]anzugeben. Weitere Informationen finden Sie unter [Sortierungen und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md).  
  
15. Geben Sie auf der Seite für die [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Konfiguration - Serverkonfiguration folgende Informationen an:  
  
    -   Sicherheitsmodus — Wählen Sie für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]die Windows-Authentifizierung oder die Authentifizierung im gemischten Modus aus. Bei Auswahl des gemischten Authentifizierungsmodus müssen Sie ein sicheres Kennwort für das integrierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemadministratorkonto angeben.  
  
         Nachdem ein Gerät erfolgreich eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt hat, wird für die Windows-Authentifizierung und den gemischten Modus derselbe Sicherheitsmechanismus verwendet. Weitere Informationen finden Sie unter [Konfiguration des Datenbankmoduls – Serverkonfiguration](../../sql-server/install/instance-configuration.md#database-engine-configuration---server-configuration).  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Administratoren – Sie müssen wenigstens einen Systemadministrator für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]angeben. Um das Konto hinzuzufügen, unter dem das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup ausgeführt werden soll, klicken Sie auf **Aktuellen Benutzer hinzufügen**. Um Konten zur Liste der Systemadministratoren hinzuzufügen bzw. daraus zu entfernen, klicken Sie auf **Hinzufügen** bzw. **Entfernen**, und bearbeiten Sie anschließend die Liste der Benutzer, Gruppen bzw. Computer, die Administratorrechte für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz haben sollen.  
  
     Verwenden Sie die Seite „ [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Konfiguration – Datenverzeichnisse“, um nicht standardmäßige Installationsverzeichnisse anzugeben. Wenn die Installation in Standardverzeichnissen erfolgen soll, klicken Sie auf **Weiter**.  
  
    > [!IMPORTANT]  
    > Wenn Sie keine Standardverzeichnisse angeben, sollten Sie sicherstellen, dass die Installationsordner nur für die Instanz [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden. Keines der Verzeichnisse in diesem Dialogfeld sollte gemeinsam mit Verzeichnissen anderer Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]genutzt werden.  
  
     Weitere Informationen finden Sie unter [Konfiguration des Datenbankmoduls – Serverkonfiguration](../../sql-server/install/instance-configuration.md#database-engine-configuration---data-directories).  
  
     Aktivieren Sie auf der Seite „ [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Konfiguration – FILESTREAM“ den FILESTREAM für Ihre Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [Konfiguration des Datenbankmoduls - Filestream](../../sql-server/install/instance-configuration.md#database-engine-configuration---filestream).  
  
     Verwenden Sie die Seite „ [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Konfiguration – TempDB“, um die Dateigröße, Anzahl der Dateien, nicht standardmäßige Installationsverzeichnisse und Dateiwachstumseinstellungen für TempDB zu konfigurieren. Weitere Informationen finden Sie unter [Datenbankmodulkonfiguration – tempDB](../../sql-server/install/instance-configuration.md#database-engine-configuration---tempdb).  
  
16. Verwenden Sie die Seite [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Konfiguration – Kontenbereitstellung-Konfiguration – Kontenbereitstellung, um den Servermodus und die Benutzer oder Konten anzugeben, die über Administratorberechtigungen für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]verfügen sollen. Durch den Servermodus wird bestimmt, welcher Arbeitsspeicher und welche Speichersubsysteme auf dem Server verwendet werden. Die unterschiedlichen Projektmappentypen werden in verschiedenen Servermodi ausgeführt. Wenn Sie beabsichtigen, mehrdimensionale Cubedatenbanken auf dem Server auszuführen, wählen Sie die Standardoption, den mehrdimensionalen und Data Mining-Servermodus, aus. Damit Administratorberechtigungen vorhanden sind, müssen Sie mindestens einen Systemadministrator für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]angeben. Um das Konto hinzuzufügen, unter dem das SQL Server-Setup ausgeführt wird, klicken Sie auf **Aktuellen Benutzer hinzufügen**. Um Konten zur Liste der Systemadministratoren hinzuzufügen bzw. daraus zu entfernen, klicken Sie auf **Hinzufügen** bzw. **Entfernen**, und bearbeiten Sie anschließend die Liste der Benutzer, Gruppen bzw. Computer, die Administratorrechte für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]haben sollen. Weitere Informationen zu Servermodus und Administratorberechtigungen finden Sie unter [Analysis Services-Konfiguration – Kontobereitstellung](../../sql-server/install/instance-configuration.md#analysis-services-configuration---account-provisioning).  

   Wenn Sie die Bearbeitung der Liste abgeschlossen haben, klicken Sie auf **OK**. Überprüfen Sie die Liste der Administratoren im Konfigurationsdialogfeld. Sobald die Liste vollständig ist, klicken Sie auf **Weiter**.
   
   Geben Sie ggf. auf der Seite [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Konfiguration – Datenverzeichnisse andere Installationsverzeichnisse als das Standardinstallationsverzeichnis an. Wenn die Installation in Standardverzeichnissen erfolgen soll, klicken Sie auf **Weiter**.  
   
   > [!IMPORTANT]  
   > Wenn Sie bei der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]für INSTANCEDIR und SQLUSERDBDIR denselben Verzeichnispfad angeben, starten der SQL Server-Agent und die Volltextsuche aufgrund fehlender Berechtigungen nicht.  
   >  
   > Wenn Sie keine Standardverzeichnisse angeben, sollten Sie sicherstellen, dass die Installationsordner nur für die Instanz [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden. Keines der Verzeichnisse in diesem Dialogfeld sollte gemeinsam mit Verzeichnissen anderer Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]genutzt werden.  
   
   Weitere Informationen finden Sie unter [Konfigurationseigenschaften von Analysis Services – Datenverzeichnisse](../../sql-server/install/instance-configuration.md#analysis-services-configuration---data-directories).  
   
17. Verwenden Sie die Seite für die Distributed Replay Controller-Konfiguration, um die Benutzer anzugeben, denen Sie Administratorberechtigungen für den Distributed Replay Controller-Dienst erteilen möchten. Benutzer, die über Administratorberechtigungen verfügen, besitzen unbeschränkten Zugriff auf den Distributed Replay Controller-Dienst.  
  
     Klicken Sie auf die Schaltfläche **Aktuellen Benutzer hinzufügen** , um die Benutzer hinzuzufügen, denen Sie Zugriffsberechtigungen für den Distributed Replay Controller-Dienst erteilen möchten. Klicken Sie auf die Schaltfläche **Hinzufügen** , um Zugriffsberechtigungen für den Distributed Replay Controller-Dienst hinzuzufügen. Klicken Sie auf die Schaltfläche **Entfernen** , um Zugriffsberechtigungen für den Distributed Replay Controller-Dienst zu entfernen.  
  
     Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
18. Verwenden Sie die Seite für die Distributed Replay Client-Konfiguration, um die Benutzer anzugeben, denen Sie Administratorberechtigungen für den Distributed Replay Client-Dienst erteilen möchten. Benutzer, die über Administratorberechtigungen verfügen, besitzen unbeschränkten Zugriff auf den Distributed Replay Client-Dienst.  
  
     **Controllername** ist ein optionaler Parameter, und der Standardwert ist \<*leer*>. Geben Sie den Namen des Controllers ein, mit dem der Clientcomputer für den Distributed Replay Client-Dienst kommuniziert. Beachten Sie Folgendes:  
  
    -   Wenn Sie bereits einen Controller eingerichtet haben, geben Sie den Namen des Controllers beim Konfigurieren jedes Clients ein.  
  
    -   Wenn Sie noch keinen Controller eingerichtet haben, können Sie das Feld für den Controllernamen leer lassen. Sie müssen den Controllernamen jedoch in der **Clientkonfigurationsdatei** manuell eingeben.  
  
     Geben Sie das **Arbeitsverzeichnis** für den Distributed Replay Client-Dienst an. Das Standardarbeitsverzeichnis ist \<*Laufwerkbuchstabe*>:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\.  
  
     Geben Sie das **Ergebnisverzeichnis** für den Distributed Replay Client-Dienst an. Das Standardergebnisverzeichnis ist \<*Laufwerkbuchstabe*>:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\.  
  
     Klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.  
  
19. Auf der Seite Installationsbereit wird eine Strukturansicht der Installationsoptionen angezeigt, die während des Setups angegeben wurden. Auf dieser Setupseite ist neben der letzten Updateversion auch angegeben, ob die Produktupdatefunktion aktiviert oder deaktiviert ist.  
  
     Klicken Sie zum Fortsetzen des Vorgangs auf **Installieren**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup installiert zuerst die erforderlichen Komponenten für die ausgewählten Funktionen und dann die Funktionen.  
  
20. Während der Installation wird auf der Seite Installationsstatus der Status angezeigt, sodass Sie während der Installation den Installationsstatus überwachen können.  
  
21. Nach der Installation bietet die Seite Abgeschlossen einen Link zur zusammenfassenden Protokolldatei für die Installation und andere wichtige Hinweise. Klicken Sie auf **Schließen** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um die Installation von abzuschließen.  
  
22. Starten Sie den Computer neu, falls Sie dazu aufgefordert werden. Wenn Sie den Setupvorgang abgeschlossen haben, sollten Sie unbedingt die vom Installations-Assistenten angezeigte Meldung lesen. Weitere Informationen finden Sie unter [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
## <a name="next-steps"></a>Nächste Schritte  
 Konfigurieren Sie die neue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installation.  
  
 Zum Reduzieren der Angriffsfläche eines Systems werden zentrale Dienste und Funktionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selektiv installiert und aktiviert. Weitere Informationen finden Sie unter [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Überprüfen einer SQL Server-Installation](../../database-engine/install-windows/validate-a-sql-server-installation.md)   
 [Reparieren von Fehlern bei einer SQL Server 2016-Installation](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)   
 [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [Aktualisieren auf SQL Server 2016 mithilfe des Installations-Assistenten &#40;Setup&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Installieren von SQL Server 2016 von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  
