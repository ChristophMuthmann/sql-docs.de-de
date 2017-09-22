---
title: SQL Server Agent Jobs for Packages | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [Integration Services]
- automatic package execution
- scheduling packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 009c30b7f14fe10099257c97a5a310aa41df71b0
ms.contentlocale: de-de
ms.lasthandoff: 09/21/2017

---
# <a name="sql-server-agent-jobs-for-packages"></a>Aufträge des SQL Server-Agents für Pakete
  Sie können die Ausführung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen automatisieren und planen, indem Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent verwenden. Sie können Pakete planen, die auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitgestellt und in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher und im Dateisystem gespeichert werden.  
  
## <a name="sections-in-this-topic"></a>Kapitel in diesem Thema  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [Planen von Aufträgen in SQL Server-Agent](#jobs)  
  
-   [Planen von Integration Services-Paketen](#packages)  
  
-   [Problembehandlung von geplanten Paketen](#trouble)  
  
##  <a name="jobs"></a> Scheduling Jobs in SQL Server Agent  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent ist ein Dienst, der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert wird und mit dem Sie Aufgaben durch Ausführen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Aufträgen automatisieren und planen können. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst muss ausgeführt werden, um die automatische Ausführung von Aufträgen zu ermöglichen. Weitere Informationen finden Sie unter [Configure SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/configure-sql-server-agent).  
  
 Der Knoten **SQL Server-Agent** wird im Objekt-Explorer in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] angezeigt, wenn Sie eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]herstellen.  
  
 Erstellen Sie einen Auftrag im Dialogfeld **Neuer Auftrag** , um eine sich wiederholende Aufgabe zu automatisieren. Weitere Informationen finden Sie unter [Implementieren von Aufträgen](https://docs.microsoft.com/sql/ssms/agent/implement-jobs).  
  
 Nachdem Sie den Auftrag erstellt haben, müssen Sie mindestens einen Schritt hinzufügen. Ein Auftrag kann mehrere Schritte enthalten, und in jedem Schritt kann eine andere Aufgabe ausgeführt werden. Weitere Informationen finden Sie unter [Manage Job Steps](https://docs.microsoft.com/sql/ssms/agent/manage-job-steps).  
  
 Nachdem Sie den Auftrag und die Auftragsschritte erstellt haben, können Sie einen Zeitplan zur Ausführung des Auftrags erstellen. Sie können jedoch auch einen ungeplanten Auftrag erstellen und manuell ausführen. Weitere Informationen finden Sie unter [Anlegen und Zuweisen von Zeitplänen zu Aufträgen](https://docs.microsoft.com/sql/ssms/agent/create-and-attach-schedules-to-jobs).  
  
 Sie können den Auftrag durch Benachrichtigungsoptionen erweitern, z. B. indem Sie einen Operator zum Senden einer E-Mail-Nachricht beim Abschluss des Auftrags festlegen oder Warnungen hinzufügen. Weitere Informationen finden Sie unter [Warnungen](https://docs.microsoft.com/sql/ssms/agent/alerts).  
  
##  <a name="packages"></a> Scheduling Integration Services Packages  
 Nachdem Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftrag erstellt haben, um [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete zu planen, müssen Sie mindestens einen Schritt hinzufügen und den Typ des Schrittes als **SQL Server Integration Services-Paket**definieren. Ein Auftrag kann mehrere Schritte enthalten, und in jedem Schritt kann ein anderes Paket ausgeführt werden.  
  
 Das Ausführen eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakets mit einem Auftragsschritt entspricht dem Ausführen eines Pakets mit den Hilfsprogrammen **dtexec** (dtexec.exe) und **DTExecUI** (dtexecui.exe). Anstatt die Laufzeitoptionen für ein Paket jedoch über Befehlszeilenoptionen oder das Dialogfeld **Paketausführungs-Hilfsprogramm** festzulegen, geschieht dies hier mit dem Dialogfeld **Neuer Auftragsschritt** . Weitere Informationen zu den Optionen zum Ausführen eines Pakets finden Sie unter [dtexec Utility](../../integration-services/packages/dtexec-utility.md).  
  
 Weitere Informationen finden Sie unter [Planen eines Pakets mit dem SQL Server-Agent](#schedule).  
  
 In der MSDN Library auf der Videohomepage unter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Vorgehensweise: Automatisieren der Paketausführung mit SQL Server-Agent (SQL Server-Video) [können Sie ein Video abspielen, in dem das Ausführen eines Pakets mit dem](http://go.microsoft.com/fwlink/?LinkId=141771)-Agent veranschaulicht wird.  
  
##  <a name="trouble"></a> Problembehandlung  
 Es kann vorkommen, dass ein Paket durch einen Auftragsschritt des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents nicht gestartet werden kann, obwohl das Paket in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] sowie über die Befehlszeile erfolgreich ausgeführt wird. Es gibt einige häufige Ursachen für dieses Problem und mehrere empfohlene Lösungen. Weitere Informationen finden Sie in den folgenden Ressourcen.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base-Artikel [Beim Aufrufen aus einem SQL Server-Agentauftragsschritt wird ein SSIS-Paket nicht ausgeführt](http://support.microsoft.com/kb/918760)  
  
-   Video [Problembehandlung: Paketausführung mit SQL Server-Agent (SQL Server-Video)](http://go.microsoft.com/fwlink/?LinkId=141772)in der MSDN Library.  
  
 Nachdem ein Paket durch einen Auftragsschritt des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents gestartet wurde, tritt bei der Paketausführung u. U. ein Fehler auf, oder das Paket wird zwar erfolgreich, aber mit unerwarteten Ergebnissen ausgeführt. Diese Probleme können mithilfe der folgenden Tools behandelt werden.  
  
-   Bei Paketen, die in der MSDB-Datenbank von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher oder in einem Ordner auf dem lokalen Computer gespeichert sind, können Sie neben dem **Protokolldatei-Viewer** alle Protokolle und Debugdumpdateien verwenden, die während der Ausführung des Pakets generiert wurden.  
  
     **Gehen Sie zur Verwendung des Protokolldatei-Viewers wie folgt vor.**  
  
    1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftrag, und klicken Sie dann auf **Verlauf anzeigen**.  
  
    2.  Suchen Sie im Feld **Protokolldateizusammenfassung** die Auftragsausführung, für die in der Spalte **Meldung** die Meldung **Auftragsfehler** angezeigt wird.  
  
    3.  Erweitern Sie den Auftragsknoten, und klicken Sie auf den Auftragsschritt, um im Bereich unter dem Feld **Protokolldateizusammenfassung** Details zur Meldung anzuzeigen.  
  
-   Bei Paketen, die in der SSISDB-Datenbank gespeichert sind, können Sie ebenfalls den **Protokolldatei-Viewer** und alle Protokolle und Debugdumpdateien verwenden, die während der Ausführung des Pakets generiert wurden. Darüber hinaus können Sie die Berichte für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server verwenden.  
  
     **Um die Berichte für die Paketausführung nach Informationen zu einer Auftragsausführung zu durchsuchen, verfahren Sie wie folgt.**  
  
    1.  Führen Sie die oben angegebenen Schritte aus, um die Details der Meldung zum Auftragsschritt einzublenden.  
  
    2.  Suchen Sie die Ausführungs-ID, die in der Meldung aufgeführt ist.  
  
    3.  Erweitern Sie den Knoten Integration Services-Katalog im Objekt-Explorer.  
  
    4.  Klicken Sie mit der rechten Maustaste auf SSISDB, zeigen Sie auf Berichte, dann auf Standardberichte, und klicken Sie auf Alle Ausführungen.  
  
    5.  Suchen Sie im Bericht **Alle Ausführungen** die Ausführungs-ID in der Spalte **ID** . Klicken Sie auf **Übersicht**, **Alle Meldungen**oder **Ausführungsleistung** , um Informationen zu dieser Paketausführung anzuzeigen.  
  
    Weitere Informationen zu den Berichten Übersicht, Alle Meldungen und Ausführungsleistung finden Sie unter [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  

## <a name="schedule"></a> Planen eines Pakets mit dem SQL Server-Agent
  Im Folgenden werden Schritte beschrieben, mit denen die Ausführung eines Pakets automatisiert werden kann, indem das Paket unter Verwendung eines Auftragsschritts des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents ausgeführt wird.  
  
### <a name="to-automate-package-execution-by-using-sql-server-agent"></a>So automatisieren Sie die Paketausführung mithilfe des SQL Server-Agents  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung zu der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her, in der Sie einen Auftrag erstellen möchten, oder zu der Instanz, die den Auftrag enthält, dem Sie einen Schritt hinzufügen möchten.  
  
2.  Erweitern Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Knoten im Objekt-Explorer, und führen Sie eine der folgenden Aufgaben aus:  
  
    -   Klicken Sie zum Erstellen eines neuen Auftrags mit der rechten Maustaste auf **Aufträge** , und klicken Sie anschließend auf **Neuer Auftrag**.  
  
    -   Erweitern Sie **Aufträge**, klicken Sie mit der rechten Maustaste auf den Auftrag, und klicken Sie anschließend auf **Eigenschaften**,um einem bereits vorhandenen Auftrag einen Schritt hinzuzufügen.  
  
3.  Geben Sie beim Erstellen eines neuen Auftrags auf der Seite **Allgemein** einen Auftragsnamen an, wählen Sie einen Besitzer und eine Auftragskategorie aus, und geben Sie wahlweise eine Auftragsbeschreibung ein.  
  
4.  Um den Auftrag für die Planung verfügbar zu machen, wählen Sie **Aktiviert**aus.  
  
5.  Um einen Auftragsschritt für das zu planende Paket zu erstellen, klicken Sie auf **Schritte**und anschließend auf **Neu**.  
  
6.  Wählen Sie **Integration Services-Paket** als Typ für den Auftragsschritt aus.  
  
7.  Wählen Sie in der Liste **Ausführen als** die Option **Konto des SQL Server-Agent-Diensts** aus. Alternativ können Sie ein Proxykonto auswählen, das über die Anmeldeinformationen verfügt, die vom Auftragsschritt verwendet werden. Informationen zum Erstellen eines Proxykontos finden Sie unter [Erstellen eines Proxys für den SQL Server-Agent](http://msdn.microsoft.com/library/142e0c55-a8b9-4669-be49-b9dc602d5988).  
  
     Durch die Verwendung eines Proxykontos anstelle der Option **Konto des SQL Server-Agent-Diensts** können u.U. allgemeine Probleme behoben werden, die bei der Ausführung eines Pakets mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents auftreten können. Weitere Informationen zu diesen Problemen finden Sie im [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base-Artikel [Beim Aufrufen aus einem SQL Server-Agentauftragsschritt wird ein SSIS-Paket nicht ausgeführt](http://support.microsoft.com/kb/918760).  
  
    > **HINWEIS:** Wenn das Kennwort für die vom Proxykonto verwendeten Anmeldeinformationen geändert wird, muss das Kennwort in den Anmeldeinformationen aktualisiert werden. Andernfalls verursacht der Auftragsschritt einen Fehler.  
  
     Informationen zum Konfigurieren des SQL Server-Agent-Dienstkontos finden Sie unter [Festlegen des Dienststartkontos für den SQL Server-Agent &#40;SQL Server-Konfigurations-Manager&#41;](http://msdn.microsoft.com/library/46ffe818-ebb5-43a0-840b-923f219a2472).  
  
8.  Klicken Sie im Listenfeld **Paketquelle** auf die Quelle des Pakets, und konfigurieren Sie anschließend die Optionen für den Auftragsschritt.  
  
     **In der folgenden Tabelle sind die möglichen Paketquellen beschrieben.**  
  
    |Paketquelle|Description|  
    |--------------------|-----------------|  
    |**SSIS-Katalog**|Pakete, die in der SSISDB-Datenbank gespeichert sind. Die Pakete sind in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekten enthalten, die auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitgestellt werden.|  
    |**SQL Server**|Pakete, die in der MSDB-Datenbank gespeichert sind. Sie verwenden den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst, um diese Pakete zu verwalten.|  
    |**SSIS-Paketspeicher**|Pakete, die im Standardordner auf dem Computer gespeichert sind. Der Standardordner ist * \<Laufwerk >*: \Programme\Microsoft SQL Server\110\DTS\Packages. Sie verwenden den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst, um diese Pakete zu verwalten.<br /><br /> Hinweis: Sie können einen anderen Ordner oder zusätzliche Ordner im Dateisystem angeben, die vom [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst verwaltet werden sollen, indem Sie die Konfigurationsdatei für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]ändern. Weitere Informationen finden Sie unter [Integration Services-Dienst &#40;SSIS-Dienst&#41;](../../integration-services/service/integration-services-service-ssis-service.md).|  
    |**Dateisystem**|Pakete, die in einem beliebigen Ordner auf dem lokalen Computer gespeichert sind.|  
  
     **In den folgenden Tabellen werden die Konfigurationsoptionen beschrieben, die je nach ausgewählter Paketquelle für den Auftragsschritt verfügbar sind.**  
  
    > **WICHTIG** : Wenn Sie beim Klicken auf eine der Registerkarten (außer der Registerkarte **Paket** ) auf der Seite **Allgemein** im Dialogfeld **Neuer Auftragsschritt** feststellen, dass das Paket kennwortgeschützt ist, müssen Sie das Kennwort im eingeblendeten Dialogfeld **Paketkennwort** eingeben. Andernfalls kann das Paket vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agentauftrag nicht ausgeführt werden.  
  
     **Paketquelle**: SSIS-Katalog  
  
    |Registerkarte|enthalten|  
    |---------|-------------|  
    |**Neuer Auftragsschritt**|**Server**<br /><br /> Geben Sie den Namen der Datenbankserver-Instanz ein, die den SSISDB-Katalog hostet, oder wählen Sie den Namen aus.<br /><br /> Wenn die Paketquelle **SSIS-Katalog** lautet, können Sie sich nur unter Verwendung eines Microsoft Windows-Benutzerkontos beim Server anmelden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung ist nicht verfügbar.|  
    ||**Neuer Auftragsschritt**<br /><br /> Klicken Sie auf die Schaltfläche mit den Auslassungspunkten, und wählen Sie ein Paket aus.<br /><br /> Sie wählen ein Paket in einem Ordner unter dem Knoten **Integration Services-Kataloge** im **Objekt-Explorer**aus.|  
    |**Parameter**<br /><br /> Auf der Registerkarte **Konfiguration** .|Mithilfe des **Assistenten zum Konvertieren von Integration Services-Projekten** können Sie Paketkonfigurationen durch Parameter ersetzen.<br /><br /> Auf der Registerkarte **Parameter** werden Parameter angezeigt, die Sie beim Entwerfen des Pakets, beispielsweise mit [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], hinzugefügt haben. Außerdem werden auf der Registerkarte Parameter angezeigt, die dem Paket hinzugefügt wurden, als Sie das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt aus dem Paketbereitstellungsmodell in das Projektbereitstellungsmodell konvertiert haben. Geben Sie neue Werte für Parameter ein, die im Paket enthalten sind. Sie können einen Literalwert eingeben oder den Wert verwenden, der in einer Serverumgebungsvariable enthalten ist, die Sie dem Parameter bereits zugeordnet haben.<br /><br /> Um den Literalwert einzugeben, klicken Sie neben einem Parameter auf die Schaltfläche mit den Auslassungspunkten. Das Dialogfeld **Literalwert für die Ausführung bearbeiten** wird angezeigt.<br /><br /> Um eine Umgebungsvariable zu verwenden, klicken Sie auf **Umgebung** und wählen dann die Umgebung aus, in der die gewünschte Variable enthalten ist.<br /><br /> **\*\* Wichtig \*\*** Wenn Sie mehrere Parameter und/oder Eigenschaften des Verbindungs-Managers Variablen zugeordnet haben, die in mehreren Umgebungen enthalten sind, zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent eine Fehlermeldung an. Ein Paket kann jeweils nur mit den Werten ausgeführt werden, die in einer einzelnen Serverumgebung enthalten sind.<br /><br /> Informationen zum Erstellen eines Servers Umgebung und die Zuordnung einer Variablen auf einen Parameter, finden Sie unter [Bereitstellen von Integration Services (SSIS)-Projekten und Paketen](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).|  
    |**Verbindungs-Manager**<br /><br /> Auf der Registerkarte **Konfiguration** .|Ändern Sie Werte von Eigenschaften des Verbindungs-Managers. Beispielsweise können Sie den Servernamen ändern. Parameter für die Eigenschaften des Verbindungs-Managers werden automatisch auf dem SSIS-Server generiert. Um einen Eigenschaftswert zu ändern, können Sie einen Literalwert eingeben oder den Wert verwenden, der in einer Serverumgebungsvariablen enthalten ist, die Sie der Eigenschaft des Verbindungs-Managers bereits zugeordnet haben.<br /><br /> Um den Literalwert einzugeben, klicken Sie neben einem Parameter auf die Schaltfläche mit den Auslassungspunkten. Das Dialogfeld **Literalwert für die Ausführung bearbeiten** wird angezeigt.<br /><br /> Um eine Umgebungsvariable zu verwenden, klicken Sie auf **Umgebung** und wählen dann die Umgebung aus, in der die gewünschte Variable enthalten ist.<br /><br /> **\*\* Wichtig \*\*** Wenn Sie mehrere Parameter und/oder Eigenschaften des Verbindungs-Managers Variablen zugeordnet haben, die in mehreren Umgebungen enthalten sind, zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent eine Fehlermeldung an. Ein Paket kann jeweils nur mit den Werten ausgeführt werden, die in einer einzelnen Serverumgebung enthalten sind.<br /><br /> Informationen zum Erstellen einer serverumgebung, und ordnen Sie einer Variable zu einer Eigenschaft des Verbindungs-Manager finden Sie unter [Bereitstellen von Integration Services (SSIS)-Projekten und Paketen](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).|  
    |**Erweitert**<br /><br /> Auf der Registerkarte **Konfiguration** .|Konfigurieren Sie die folgenden zusätzlichen Einstellungen für die Paketausführung:|  
    ||**Eigenschaftenüberschreibungen**:<br /><br /> Klicken Sie auf **Hinzufügen** , um einen neuen Wert für eine Paketeigenschaft einzugeben, den Eigenschaftspfad festzulegen und anzugeben, ob der Eigenschaftswert sensibel ist. Sensible Daten werden vom [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server verschlüsselt. Um die Einstellungen für eine Eigenschaft zu bearbeiten oder zu entfernen, klicken Sie im Feld **Eigenschaftenüberschreibungen** auf eine Zeile und klicken anschließend auf **Bearbeiten** oder **Entfernen**. Sie können den Eigenschaftspfad wie folgt ermitteln:<br /><br /> – Kopieren Sie den Eigenschaftspfad aus der XML-Konfigurationsdatei (\*.dtsconfig). Der Pfad ist im Konfigurationsabschnitt der Datei als Wert des Pfadattributs aufgeführt. Im folgenden Beispiel ist der Pfad für die MaximumErrorCount-Eigenschaft dargestellt: \Package.Properties[MaximumErrorCount]<br /><br /> – Führen Sie den **Paketkonfigurations-Assistenten** aus, und kopieren Sie die Eigenschaftspfade von der letzten Seite **Assistenten abschließen** . Dann können Sie den Assistenten abbrechen.<br /><br /> <br /><br /> Hinweis: Die Option **Eigenschaftenüberschreibungen** ist für Pakete mit Konfigurationen vorgesehen, die von einer früheren Version von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]aktualisiert wurden. Pakete, die Sie mit [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] erstellen und für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitstellen, verwenden Parameter anstelle von Konfigurationen.|  
    ||**Protokolliergrad**<br /><br /> Wählen Sie einen der folgenden Protokolliergrade für die Paketausführung aus. Beachten Sie, dass sich die Auswahl des Protokolliergrads **Leistung** oder **Ausführlich** auf die Leistung der Paketausführung auswirken kann.<br /><br /> **Keine**:<br />                          Die Protokollierung ist deaktiviert. Nur der Status der Ausführung von Paketen wird protokolliert.<br /><br /> **Standard**:<br />                          Alle Ereignisse werden protokolliert, außer benutzerdefinierten und Diagnose-Ereignissen. Dies ist der Standardwert für den Protokolliergrad.<br /><br /> **Leistung**:<br />                          Nur Leistungsstatistiken sowie OnError- und OnWarning-Ereignisse werden protokolliert.<br /><br /> **Ausführlich**:<br />                          Alle Ereignisse werden protokolliert, einschließlich benutzerdefinierter Ereignisse und Diagnose-Ereignissen.<br /><br /> Der ausgewählte Protokolliergrad bestimmt, welche Informationen in SSISDB-Sichten und Berichten für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server angezeigt werden. Weitere Informationen finden Sie unter [Integration Services-Protokollierung (SSIS)](../../integration-services/performance/integration-services-ssis-logging.md).|  
    ||**Speichern bei Fehlern**<br /><br /> Geben Sie an, ob Debugdumpdateien generiert werden, wenn während der Ausführung des Pakets ein Fehler auftritt. Die Dateien enthalten Informationen zur Ausführung des Pakets, die Unterstützung beim Beheben von Problemen bieten. Wenn Sie diese Option auswählen und bei der Ausführung ein Fehler auftritt, erstellt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eine MDMP-Datei (Binärdatei) sowie eine TMP-Datei (Textdatei). Standardmäßig [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] speichert die Dateien in den * \<Laufwerk >:*Ordner "\Programme\Microsoft SQL Server\110\Shared\ErrorDumps".|  
    ||**32-Bit-Laufzeit**<br /><br /> Geben Sie an, ob das Paket mit der 32-Bit-Version des Hilfsprogramms dtexec auf einem 64-Bit-Computer ausgeführt werden soll, auf dem die 64-Bit-Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent installiert sind.<br /><br /> Möglicherweise müssen Sie das Paket mithilfe der 32-Bit-Version von dtexec ausführen, beispielsweise, wenn das Paket einen systemeigenen OLE DB-Anbieter verwendet, der in einer 64-Bit-Version nicht verfügbar ist. Weitere Informationen finden Sie unter [Überlegungen zu Integration Services auf 64-Bit-Computern](http://msdn.microsoft.com/library/ms141766\(SQL.105\).aspx).<br /><br /> Wenn Sie den Auftragsschritt vom Typ **SQL Server Integration Services-Paket** auswählen, führt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent das Paket standardmäßig unter Verwendung der Version des Hilfsprogramms „dtexec“ aus, die automatisch vom System aufgerufen wird. Das System ruft abhängig vom Computerprozessor sowie der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Version, die auf dem Computer ausgeführt wird, entweder die 32-Bit- oder 64-Bit-Version des Hilfsprogramms auf.|  
  
     **Paketquelle**: SQL Server, SSIS-Paketspeicher oder Dateisystem  
  
     Viele Optionen, die Sie für die in SQL Server, im SSIS-Paketspeicher oder im Dateisystem gespeicherten Pakete festlegen können, entsprechen den Befehlszeilenoptionen für das Eingabeaufforderungs-Hilfsprogramm **dtexec** . Weitere Informationen zum Hilfsprogramm und den Befehlszeilenoptionen finden Sie unter [dtexec (Hilfsprogramm)](../../integration-services/packages/dtexec-utility.md).  
  
    |Registerkarte|enthalten|  
    |---------|-------------|  
    |**Neuer Auftragsschritt**<br /><br /> Diese Registerkartenoptionen sind auf Pakete anwendbar, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher gespeichert sind.|**Server**<br /><br /> Geben Sie den Namen der Datenbankserver-Instanz für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst ein, oder wählen Sie den Namen aus.|  
    ||**Windows-Authentifizierung verwenden**<br /><br /> Wählen Sie diese Option aus, um sich unter Verwendung eines Microsoft Windows-Benutzerkontos beim Server anzumelden.|  
    ||**SQL Server-Authentifizierung verwenden**<br /><br /> Wenn ein Benutzer eine Verbindung mit einem angegebenen Benutzernamen und einem Kennwort von einer nicht vertrauenswürdigen Verbindung herstellt, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Authentifizierung aus, indem überprüft wird, ob ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldekonto eingerichtet wurde und ob das angegebene Kennwort mit dem zuvor aufgezeichneten übereinstimmt. Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das Anmeldekonto nicht finden kann, schlägt die Authentifizierung fehl und der Benutzer erhält eine Fehlermeldung.|  
    ||**Benutzername**|  
    ||**Kennwort**|  
    ||**Neuer Auftragsschritt**<br /><br /> Klicken Sie auf die Schaltfläche mit den Auslassungspunkten, und wählen Sie das Paket aus.<br /><br /> Sie wählen ein Paket in einem Ordner unter dem Knoten **Gespeicherte Pakete** im **Objekt-Explorer**aus.|  
    |**Neuer Auftragsschritt**<br /><br /> Diese Registerkartenoptionen sind auf Pakete anwendbar, die im Dateisystem gespeichert sind.|**Neuer Auftragsschritt**<br /><br /> Geben Sie den vollständigen Pfad für die Paketdatei ein, oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten, um das Paket auszuwählen.|  
    |**Konfigurationen**|Fügen Sie eine XML-Konfigurationsdatei hinzu, um das Paket mit einer bestimmten Konfiguration auszuführen. Sie verwenden eine Paketkonfiguration, um die Werte von Paketeigenschaften zur Laufzeit zu aktualisieren.<br /><br /> Diese Option entspricht der Option **/ConfigFile** für **dtexec**.<br /><br /> Weitere Informationen zur Anwendung von Paketkonfigurationen finden Sie unter [Paketkonfigurationen](../../integration-services/packages/package-configurations.md). Informationen zum Erstellen von Paketkonfigurationen finden Sie unter [Erstellen von Paketkonfigurationen](../../integration-services/packages/create-package-configurations.md).|  
    |**Befehlsdateien**|Geben Sie weitere Optionen, die Sie mit **dtexec**ausführen möchten, in einer separaten Datei an.<br /><br /> Beispielsweise können Sie eine Datei einschließen, die die Option /Dump *errorcode* enthält, um Debugdumpdateien zu generieren, wenn während der Paketausführung eines oder mehrere angegebene Ereignisse auftreten.<br /><br /> Sie können ein Paket mit unterschiedlichen Gruppen von Optionen ausführen, indem Sie mehrere Dateien erstellen und anschließend die entsprechende Datei mithilfe der Option **Befehlsdateien** angeben.<br /><br /> Die Option **Befehlsdateien** entspricht der Option **/CommandFile** für **dtexec**.|  
    |**Datenquellen**|Zeigen Sie die im Paket enthaltenen Verbindungs-Manager an. Um eine Verbindungszeichenfolge zu ändern, klicken Sie auf den Verbindungs-Manager und dann auf die Verbindungszeichenfolge.<br /><br /> Diese Option entspricht der Option **/Connection** für **dtexec**.|  
    |**Ausführungsoptionen**|**Paket bei Überprüfungswarnungen als fehlerhaft kennzeichnen**<br /> Gibt an, ob eine Warnmeldung als Fehler angesehen wird. Wenn Sie diese Option auswählen und während der Überprüfung eine Warnung ausgegeben wird, verursacht das Paket während der Überprüfung einen Fehler. Diese Option entspricht der Option **/WarnAsError** für **dtexec**.<br /><br /> **Paket ohne Ausführung überprüfen**<br /> Gibt an, ob die Paketausführung nach der Überprüfungsphase beendet wird, ohne das Paket tatsächlich auszuführen. Diese Option entspricht der Option **/Validate** für **dtexec**.<br /><br /> **MaxConcurrentExecutables-Eigenschaft überschreiben**<br /> Gibt die Anzahl von ausführbaren Dateien an, die das Paket gleichzeitig ausführen kann. Der Wert "-1" bedeutet, dass vom Paket maximal so viele ausführbare Dateien plus zwei Dateien ausgeführt werden können, wie Prozessoren auf dem Computer vorhanden sind, auf dem das Paket ausgeführt wird. Diese Option entspricht der Option **/MaxConcurrent** für **dtexec**.<br /><br /> **Paketprüfpunkte aktivieren**<br /> Gibt an, ob das Paket Prüfpunkte bei der Paketausführung verwendet. Weitere Informationen finden Sie unter [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).<br /><br /> Diese Option entspricht der Option **/CheckPointing** für **dtexec**.<br /><br /> **Neustartoptionen überschreiben**<br /> Gibt an, ob ein neuer Wert für die **CheckpointUsage** -Eigenschaft des Pakets festgelegt ist. Wählen Sie einen Wert aus dem Listenfeld **Neustartoption** aus.<br /><br /> Diese Option entspricht der Option **/Restart** für **dtexec**.<br /><br /> **32-Bit-Laufzeitumgebung verwenden**<br /> Geben Sie an, ob das Paket mit der 32-Bit-Version des Hilfsprogramms dtexec auf einem 64-Bit-Computer ausgeführt werden soll, auf dem die 64-Bit-Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent installiert sind.<br /><br /> Möglicherweise müssen Sie das Paket mithilfe der 32-Bit-Version von dtexec ausführen, beispielsweise, wenn das Paket einen systemeigenen OLE DB-Anbieter verwendet, der in einer 64-Bit-Version nicht verfügbar ist. Weitere Informationen finden Sie unter [Überlegungen zu Integration Services auf 64-Bit-Computern](http://msdn.microsoft.com/library/ms141766\(SQL.105\).aspx).<br /><br /> Wenn Sie den Auftragsschritt vom Typ **SQL Server Integration Services-Paket** auswählen, führt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent das Paket standardmäßig unter Verwendung der Version des Hilfsprogramms „dtexec“ aus, die automatisch vom System aufgerufen wird. Das System ruft abhängig vom Computerprozessor sowie der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Version, die auf dem Computer ausgeführt wird, entweder die 32-Bit- oder 64-Bit-Version des Hilfsprogramms auf.|  
    |**Protokollierung**|Ordnen Sie der Paketausführung einen Protokollanbieter zu.<br /><br /> **SSIS-Protokollanbieter für Textdateien**<br /> Schreibt Protokolleinträge in ASCII-Textdateien.<br /><br /> **SSIS-Protokollanbieter für SQL Server**<br /> Schreibt Protokolleinträge in die sysssislog-Tabelle der MSDB-Datenbank.<br /><br /> **SSIS-Protokollanbieter für SQL Server Profiler**<br /> Schreibt Ablaufverfolgungen, die Sie mit SQL Server Profiler anzeigen können.<br /><br /> **SSIS-Protokollanbieter für das Windows-Ereignisprotokoll**<br /> Schreibt Protokolleinträge in das Anwendungsprotokoll im Windows-Ereignisprotokoll.<br /><br /> **SSIS-Protokollanbieter für XML-Dateien**<br /> Schreibt Protokolldateien in eine XML-Datei.<br /><br /> Für die Textdatei, die XML-Datei und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler-Protokollanbieter wählen Sie Dateiverbindungs-Manager aus, die im Paket enthalten sind. Für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Protokollanbieter wählen Sie einen OLE DB-Verbindungs-Manager aus, der im Paket enthalten ist.<br /><br /> Diese Option entspricht der Option **/Logger** für **dtexec**.|  
    |**Werte festlegen**|Überschreiben Sie Einstellungen für Paketeigenschaften. Geben Sie im Feld **Eigenschaften** Werte in den Spalten **Eigenschaftspfad** und **Wert** ein. Nachdem Sie Werte für eine Eigenschaft eingegeben haben, wird im Feld **Eigenschaften** eine leere Zeile eingeblendet, damit Sie Werte für eine weitere Eigenschaft eingeben können.<br /><br /> Klicken Sie auf die Zeile und anschließend auf **Entfernen**, um eine Eigenschaft aus dem Feld Eigenschaften zu entfernen.<br /><br /> Sie können den Eigenschaftspfad wie folgt ermitteln:<br /><br /> – Kopieren Sie den Eigenschaftspfad aus der XML-Konfigurationsdatei (\*.dtsconfig). Der Pfad ist im Konfigurationsabschnitt der Datei als Wert des Pfadattributs aufgeführt. Im folgenden Beispiel ist der Pfad für die MaximumErrorCount-Eigenschaft dargestellt: \Package.Properties[MaximumErrorCount]<br /><br /> – Führen Sie den **Paketkonfigurations-Assistenten** aus, und kopieren Sie die Eigenschaftspfade von der letzten Seite **Assistenten abschließen** . Dann können Sie den Assistenten abbrechen.|  
    |**Überprüfung**|**Nur signierte Pakete ausführen**<br /> Gibt an, ob die Paketsignatur überprüft wird. Wenn das Paket nicht signiert oder die Signatur nicht gültig ist, schlägt das Paket fehl. Diese Option entspricht der Option **/VerifySigned** für **dtexec**.<br /><br /> **Paketbuild überprüfen**<br /> Gibt an, ob die Buildnummer des Pakets anhand der Buildnummer überprüft wird, die in das Feld **Build** neben dieser Option eingegeben wird. Stimmen die Buildnummern nicht überein, wird das Paket nicht ausgeführt. Diese Option entspricht der Option **/VerifyBuild** für **dtexec**.<br /><br /> **Paket-ID überprüfen**<br /> Gibt an, ob die GUID des Pakets überprüft wird, indem sie mit der im Feld **Paket-ID** neben dieser Option eingegebenen Paket-ID verglichen wird. Diese Option entspricht der Option **/VerifyPackageID** für **dtexec**.<br /><br /> **Versions-ID überprüfen**<br /> Gibt an, ob die Versions-GUID des Pakets überprüft wird, indem sie mit der im Feld **Versions-ID** neben dieser Option eingegebenen Versions-ID verglichen wird. Diese Option entspricht der Option **/VerifyVersionID** für **dtexec**.|  
    |**Befehlszeile**|Ändern Sie die Befehlszeilenoptionen für dtexec. Weitere Informationen zu den Optionen finden Sie unter [dtexec (Hilfsprogramm)](../../integration-services/packages/dtexec-utility.md).<br /><br /> **Die ursprünglichen Optionen wiederherstellen**<br /> Verwenden Sie die Befehlszeilenoptionen, die Sie auf den Registerkarten **Paket**, **Konfigurationen**, **Befehlsdateien**, **Datenquellen**, **Ausführungsoptionen**, **Protokollierung**, **Werte festlegen**und **Überprüfung** des Dialogfelds **Auftragsschritt-Eigenschaften** festgelegt haben.<br /><br /> **Befehlszeile manuell bearbeiten**<br /> Geben Sie zusätzliche Befehlszeilenoptionen im Feld **Befehlszeile** ein.<br /><br /> Bevor Sie auf **OK** klicken, um die Änderungen am Auftragsschritt zu speichern, können Sie alle zusätzlichen Optionen entfernen, die Sie in das Feld **Befehlszeile** eingegeben haben, indem Sie auf **Ursprüngliche Optionen wiederherstellen**klicken.<br /><br /> **\*\* Tipp \*\*** Sie können die Befehlszeile in ein Eingabeaufforderungsfenster kopieren, `dtexec`hinzufügen und das Paket über die Befehlszeile ausführen. Dies ist eine einfache Methode zum Generieren des Befehlszeilentexts.|  
  
9. Klicken Sie auf **OK** , um die Einstellungen zu speichern und das Dialogfeld **Neuer Auftragsschritt** zu schließen.  
  
    > **HINWEIS:** Bei Paketen, die im **SSIS-Katalog**gespeichert sind, wird die Schaltfläche **OK** deaktiviert, wenn eine nicht aufgelöste Parametereinstellung oder Eigenschafteneinstellung des Verbindungs-Managers vorliegt. Eine nicht aufgelöste Einstellung liegt vor, wenn Sie einen in einer Serverumgebungsvariablen enthaltenen Wert verwenden, um den Parameter oder die Eigenschaft festzulegen, und eine der folgenden Bedingungen zutrifft:  
    >   
    >  Das Kontrollkästchen **Umgebung** auf der Registerkarte **Konfiguration** ist nicht aktiviert.  
    >   
    >  Die Serverumgebung, in der die Variable enthalten ist, ist im Listenfeld auf der Registerkarte **Konfiguration** nicht ausgewählt.  
  
10. Klicken Sie im Bereich **Seite auswählen** auf **Zeitpläne** , um einen Zeitplan für einen Auftragsschritt zu erstellen. Informationen zum Konfigurieren eines Zeitplans finden Sie unter [Planen eines Auftrags](http://msdn.microsoft.com/library/f626390a-a3df-4970-b7a7-a0529e4a109c).  
  
    > [!TIP]  
    >  Zur Benennung des Zeitplans sollten Sie einen eindeutigen und aussagekräftigen Namen verwenden, damit sich der Zeitplan leichter von anderen Zeitplänen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents unterscheiden lässt.  

## <a name="see-also"></a>Siehe auch  
 [Ausführung von Projekten und Paketen](/sql-docs/docs/integration-services/packages/deploy-integration-services-ssis-projects-and-packages)  

## <a name="external-resources"></a>Externe Ressourcen  
  
-   Knowledge Base-Artikel [Beim Aufrufen aus einem SQL Server-Agentauftragsschritt wird ein SSIS-Paket nicht ausgeführt](http://support.microsoft.com/kb/918760)auf der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Website  
  
-   Video [Problembehandlung: Paketausführung mit SQL Server-Agent (SQL Server-Video)](http://go.microsoft.com/fwlink/?LinkId=141772)in der MSDN Library  
  
-   Video [Vorgehensweise: Automatisieren der Paketausführung mit dem SQL Server-Agent (SQL Server-Video)](http://go.microsoft.com/fwlink/?LinkId=141771)in der MSDN Library  
  
-   Technischer Artikel [Überprüfen von Aufträgen des SQL Server-Agents mit Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=165675)auf mssqltips.com  
  
-   Technischer Artikel, [Auto alert for SQL Agent jobs when they are enabled or disabled](http://go.microsoft.com/fwlink/?LinkId=165676), auf mssqltips.com  
  
-   Blogeintrag [Konfigurieren von SQL-Agentaufträgen für das Schreiben in das Windows-Ereignisprotokoll](http://go.microsoft.com/fwlink/?LinkId=220745)auf mssqltips.com  
  
  
