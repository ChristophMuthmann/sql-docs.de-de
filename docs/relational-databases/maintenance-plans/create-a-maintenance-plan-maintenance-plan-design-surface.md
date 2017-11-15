---
title: "Erstellen eines Wartungsplans (Entwurfsoberfläche für Wartungspläne) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Maintenance Plan Design Surface
ms.assetid: 2ef803ee-a9f8-454a-ad63-fedcbe6838d1
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 039e306af582e2bc56559557eea3a5d6d57ec819
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="create-a-maintenance-plan-maintenance-plan-design-surface"></a>Erstellen eines Wartungsplans (Entwurfsoberfläche für Wartungspläne)
  In diesem Thema wird beschrieben, wie für einen einzelnen Server oder mehrere Server mithilfe der Entwurfsoberfläche für Wartungspläne in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]ein Wartungsplan erstellt wird. Der **Wartungsplanungs-Assistent** eignet sich am besten für das Erstellen von grundlegenden Wartungsplänen. Wenn Sie die Entwurfsoberfläche zum Erstellen eines Plans verwenden, können Sie einen erweiterten Workflow nutzen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   [Erstellen eines Wartungsplans mithilfe der Entwurfsoberfläche für Wartungspläne](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn Sie einen Multiserver-Wartungsplan erstellen möchten, muss eine Multiserverumgebung mit einem Masterserver und mindestens einem Zielserver konfiguriert sein. Multiserver-Wartungspläne müssen auf dem Masterserver erstellt und verwaltet werden. Diese Pläne können auf Zielservern zwar angezeigt, jedoch nicht verwaltet werden.  
  
-   Mitglieder der **db_ssisadmin** -Rolle und **dc_admin** -Rolle können ihre Berechtigungen möglicherweise auf **sysadmin**erhöhen. Diese Ausweitung von Berechtigungen ist möglich, da diese Rollen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete ändern können. Diese Pakete können von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe des **sysadmin** -Sicherheitskontexts des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents ausgeführt werden. Konfigurieren Sie als Schutz vor dieser Ausweitung von Berechtigungen beim Ausführen von Wartungsplänen, Datensammlungssätzen und anderen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen Aufträge des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents, die Pakete ausführen, für die Verwendung eines Proxykontos mit eingeschränkten Berechtigungen, oder fügen Sie der **db_ssisadmin** -Rolle und der **dc_admin** -Rolle nur **sysadmin** -Mitglieder hinzu.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen Mitglied der festen Serverrolle **sysadmin** sein, um Wartungspläne erstellen oder verwalten zu können. Im Objekt-Explorer wird der **Wartungspläne** -Knoten nur für Benutzer angezeigt, die Mitglied der festen Serverrolle **sysadmin** sind.  
  
##  <a name="SSMSProcedure"></a> Verwendung der Entwurfsoberfläche für Wartungspläne  
  
#### <a name="to-create-a-maintenance-plan"></a>So erstellen Sie einen Wartungsplan  
  
1.  Klicken Sie im Objekt-Explorer auf das Pluszeichen, um den Server zu erweitern, auf dem Sie einen Wartungsplan erstellen möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Verwaltung** zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner **Wartungspläne** , und klicken Sie anschließend auf **Neuer Wartungsplan**.  
  
4.  Geben Sie im Dialogfeld **Neuer Wartungsplan** im Feld **Name** einen Namen für den Plan ein, und klicken Sie auf **OK**. Die Toolbox und die *maintenance_plan_name* **[Entwurf]** -Oberfläche mit dem **Unterplan_1** im Hauptraster wird angezeigt.  
  
     Die folgenden Optionen sind in der Kopfzeile des Entwurfsbereichs verfügbar.  
  
     **Unterplan hinzufügen**  
     Mit dieser Option fügen Sie einen Unterplan hinzu, den Sie konfigurieren können.  
  
     **Unterplaneigenschaften**  
     Zeigt das Dialogfeld **Unterplaneigenschaften** für den ausgewählten Unterplan im Hauptraster an. Sie können im Raster auch auf einen Unterplan doppelklicken, um das Dialogfeld **Unterplaneigenschaften** anzuzeigen. Weitere Informationen zu diesem Dialogfeld finden Sie unten.  
  
     **Ausgewählten Unterplan löschen**  
     Hiermit löschen Sie den ausgewählten Unterplan.  
  
     **Zeitplan des Unterplans**  
     Zeigt das Dialogfeld **Neuer Auftragszeitplan** für den ausgewählten Unterplan an.  
  
     **Zeitplan entfernen**  
     Mit dieser Option entfernen Sie einen Zeitplan aus dem ausgewählten Unterplan.  
  
     **Verbindungen verwalten**  
     Hiermit zeigen Sie das Dialogfeld **Verbindungen verwalten** an. Es wird verwendet, um dem Wartungsplan zusätzliche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzverbindungen hinzuzufügen. Weitere Informationen zu diesem Dialogfeld finden Sie unten.  
  
     **Berichterstellung und Protokollierung**  
     Zeigt das Dialogfeld **Berichterstellung und Protokollierung** an. Weitere Informationen zu diesem Dialogfeld finden Sie unten.  
  
     **Server**  
     Mit dieser Option zeigen Sie das Dialogfeld **Server** an, das zum Auswählen der Server verwendet wird, auf denen die Unterplantasks ausgeführt werden. Diese Option ist nur auf Masterservern in Umgebungen mit mehreren Servern aktiviert. Weitere Informationen finden Sie unter [Erstellen einer Multiserverumgebung](http://msdn.microsoft.com/library/edc2b60d-15da-40a1-8ba3-f1d473366ee6) und [Wartungsplan &#40;Servers&#41;](../../relational-databases/maintenance-plans/maintenance-plan-servers.md).  
  
     **Name**  
     Hier zeigen Sie den Namen für den Wartungsplan an. Bei neuen Wartungsplänen wird der Name in einem Dialogfeld angegeben, bevor der Designer für den Wartungsplan geöffnet wird. Wenn Sie einen Wartungsplan umbenennen möchten, klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Plan, und klicken Sie anschließend auf **Umbenennen**.  
  
     **Beschreibung**  
     Hier können Sie eine Beschreibung für den Wartungsplan anzeigen oder festlegen. Die maximale Länge für eine Beschreibung beträgt 512 Zeichen.  
  
     **Designeroberfläche**  
     Hiermit können Sie Wartungspläne entwerfen und verwalten. Verwenden Sie die Designeroberfläche, um einem Plan Wartungspläne hinzuzufügen, Tasks aus einem Plan zu entfernen, Rangfolgenlinks zwischen den Tasks anzugeben oder Taskverzweigungen und -parallelausführungen anzuzeigen.  
  
     Ein Rangfolgenlink zwischen zwei Tasks legt eine Beziehung zwischen den Tasks fest. Der zweite Task (der *abhängige Task*) wird nur ausgeführt, wenn das Ausführungsergebnis des ersten Tasks (des *Vorgängertasks*) bestimmte Kriterien erfüllt. Normalerweise ist das angegebene Ausführungsergebnis **Erfolg**, **Fehler**oder **Beendigung**. Weitere Informationen finden Sie unter Schritt **8** .  
  
5.  Doppelklicken Sie in der Kopfzeile des Entwurfsbereichs auf **Unterplan_1** , und geben Sie im Dialogfeld **Unterplaneigenschaften** einen Namen sowie eine Beschreibung für den Unterplan ein.  
  
     Die folgenden Optionen sind im Dialogfeld **Unterplaneigenschaften** verfügbar.  
  
     **Name**  
     Der Name des Unterplans.  
  
     **Beschreibung**  
     Kurze Beschreibung des Unterplans.  
  
     **Zeitplan**  
     Gibt an, nach welchem Zeitplan der Unterplan ausgeführt wird. Klicken Sie auf **Zeitplan des Unterplans** , um das Dialogfeld **Neuer Auftragszeitplan** zu öffnen. Klicken Sie auf **Zeitplan entfernen** , um den Zeitplan aus dem Unterplan zu löschen.  
  
     Liste**Ausführen als**   
     Wählen Sie das Konto aus, das zum Ausführen dieser Unteraufgabe verwendet werden soll.  
  
6.  Klicken Sie auf **Zeitplan des Unterplans** , um die Details zum Zeitplan in das Dialogfeld **Neuer Auftragszeitplan** einzugeben.  
  
7.  Um den Unterplan zu erstellen, ziehen Sie die Tasksteuerungselemente aus der **Toolbox** auf die Planentwurfsoberfläche. Doppelklicken Sie auf Tasks, um Dialogfelder zum Konfigurieren der Taskoptionen zu öffnen.  
  
     Die folgenden Wartungsplantasks sind in der **Toolbox**verfügbar:  
  
    -   **Datenbank sichern (Task)**  
  
    -   **Datenbankintegrität überprüfen (Task)**  
  
    -   **Auftrag des SQL Server-Agents ausführen (Task)**  
  
    -   **T-SQL-Anweisung ausführen (Task)**  
  
    -   **Verlaufscleanup (Task)**  
  
    -   **Wartungscleanup (Task)**  
  
    -   **Operator benachrichtigen (Task)**  
  
    -   **Index neu erstellen (Task)**  
  
    -   **Index neu organisieren (Task)**  
  
    -   **Datenbank verkleinern (Task)**  
  
    -   **Statistiken aktualisieren (Task)**  
  
     So fügen Sie der **Toolbox**Tasks hinzu:  
  
    1.  Klicken Sie im Menü **Extras** auf **Toolboxelemente auswählen**.  
  
    2.  Wählen Sie die Tools aus, die in der **Toolbox**angezeigt werden sollen, und klicken Sie dann auf **OK**.  
  
     Wenn Wartungsplantasks der **Toolbox** hinzugefügt werden, sind diese auch im **Wartungsplanungs-Assistenten**verfügbar. Weitere Informationen zu den einzelnen Tasks finden Sie unter [Verwenden des Wartungsplanungs-Assistenten](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md#SSMSProcedure) im Abschnitt **So starten Sie den Wartungsplanungs-Assistenten**.  
  
8.  So definieren Sie einen Workflow zwischen Tasks:  
  
    1.  Klicken Sie mit der rechten Maustaste auf den Vorgängertask, und wählen Sie **Rangfolgeneinschränkung hinzufügen**aus.  
  
    2.  Wählen Sie im Dialogfeld **Ablaufsteuerung** in der Liste **Zu** den abhängigen Task aus, und klicken Sie auf **OK**.  
  
    3.  Doppelklicken Sie auf den Konnektor zwischen den beiden Tasks, um das Dialogfeld **Rangfolgeneinschränkungs-Editor** zu öffnen.  
  
         Die folgenden Optionen sind im Dialogfeld **Rangfolgeneinschränkungs-Editor** verfügbar.  
  
         **Einschränkungsoption**  
         Definiert, wie eine Einschränkung zwischen zwei Tasks angewendet wird.  
  
         Liste**Auswertungsvorgang**    
         Geben Sie den Auswertungsvorgang an, den die Rangfolgeneinschränkung verwendet. Dazu zählen die folgenden Vorgänge: **Einschränkung**, **Ausdruck**, **Ausdruck und Einschränkung**und **Ausdruck oder Einschränkung**.  
  
         Liste**Wert**   
         Geben Sie den Einschränkungswert an: **Erfolg**, **Fehler**oder **Beendigung**. **Erfolg** ist die Standardeinstellung.  
  
        > [!NOTE]  
        >  Die Rangfolgeneinschränkungszeile wird für **Erfolg**grün, für **Fehler**rot und für **Beendigung**blau angezeigt.  
  
         **Ausdruck**  
         Geben Sie, wenn Sie die Vorgänge **Ausdruck**, **Ausdruck und Einschränkung**oder **Ausdruck oder Einschränkung**verwenden, einen Ausdruck ein. Der Ausdruck muss zu einem booleschen Wert ausgewertet werden.  
  
         **Test**  
         Überprüfen Sie den Ausdruck.  
  
         **Mehrere Einschränkungen**  
         Definieren Sie, wie mehrere Einschränkungen zusammenwirken, um die Ausführung des eingeschränkten Tasks zu steuern.  
  
         **Logisches AND**  
         Damit geben Sie an, dass für die ausführbare Datei mehrere Rangfolgeneinschränkungen gemeinsam überprüft werden müssen. Sämtliche Einschränkungen müssen bei der Auswertung True ergeben. Diese Option ist die Standardeinstellung.  
  
        > [!NOTE]  
        >  Dieser Typ der Rangfolgeneinschränkung wird als durchgehende grüne, rote oder blaue Linie dargestellt.  
  
         **Logisches OR**  
         Damit geben Sie an, dass für die ausführbare Datei mehrere Rangfolgeneinschränkungen gemeinsam überprüft werden müssen. Mindestens eine Einschränkung muss mit True ausgewertet werden.  
  
        > [!NOTE]  
        >  Dieser Typ der Rangfolgeneinschränkung wird als gestrichelte grüne, rote oder blaue Linie dargestellt.  
  
9. Um einen anderen Unterplan mit Tasks hinzuzufügen, die unter einem anderen Zeitplan ausgeführt werden, klicken Sie in der Symbolleiste auf **Unterplan hinzufügen** , um das Dialogfeld **Unterplaneigenschaften** zu öffnen.  
  
10. So fügen Sie Verbindungen zu anderen Servern hinzu:  
  
    1.  Klicken Sie in der Symbolleiste des Entwurfsbereichs auf **Verbindungen verwalten**.  
  
    2.  Klicken Sie im Dialogfeld **Verbindungen verwalten** auf **Hinzufügen**.  
  
    3.  Geben Sie im Dialogfeld **Verbindungseigenschaften** im Feld **Verbindungsname** den Namen der Verbindung ein, die Sie erstellen.  
  
    4.  Geben Sie unter **Geben Sie Folgendes für die Verbindung mit SQL Server-Daten an**im Feld **Wählen Sie einen Servernamen aus, oder geben Sie ihn ein** entweder den Namen des SQL-Servers ein, den Sie verwenden möchten, oder klicken Sie auf die Auslassungspunkte **(…)** , und wählen Sie im Dialogfeld **SQL Server** einen Server aus. Wenn Sie im Dialogfeld **SQL Server** einen Server auswählen, klicken Sie auf **OK**.  
  
    5.  Wählen Sie unter **Geben Sie Informationen zum Anmelden am Server ein**die Option **Integrierte Sicherheit von Windows NT verwenden** oder **SQL Server-Authentifizierung verwenden**aus. Wenn Sie sich für die Verwendung der SQL Server-Authentifizierung entscheiden, geben Sie die entsprechenden Informationen in die Felder **Benutzername** und **Kennwort** ein.  
  
    6.  Klicken Sie im Dialogfeld **Verbindungseigenschaften** auf **OK**.  
  
    7.  Klicken Sie im Dialogfeld **Verbindungen verwalten** auf **Schließen**.  
  
11. So geben Sie Berichtsoptionen an:  
  
    1.  Klicken Sie in der Symbolleiste des Entwurfsbereichs auf **Berichterstellung und Protokollierung**.  
  
    2.  Aktivieren Sie im Dialogfeld **Berichterstellung und Protokollierung** unter **Berichterstellung**die Option **Textdateibericht generieren** oder **Bericht an einen E-Mail-Empfänger senden** oder beide Optionen.  
  
        1.  Wenn Sie **Textdateibericht generieren**auswählen, können Sie entweder **Neue Datei erstellen** oder **An Datei anfügen**auswählen.  
  
        2.  Geben Sie je nach Ihrer Auswahl den Namen und vollständigen Pfad der neuen Datei oder der anzufügenden Datei ein, indem Sie die Informationen im Feld **Ordner** bzw. **Dateiname** angeben. Alternativ dazu können Sie auf die Auslassungspunkte **(…)** klicken und den Pfad zum Ordner oder den Dateinamen in den Dialogfeldern **Ordner suchen –***server_name* oder **Datenbankdateien suchen –***server_name* auswählen.  
  
        3.  Wenn Sie in der Liste **Agentoperator**die Option **Bericht an einen E-Mail-Empfänger senden** auswählen, können Sie den Empfänger des per E-Mail gesendeten Berichts angeben.  
  
            > [!NOTE]  
            >  Der SQL Server-Agent muss für die Verwendung von Datenbank-E-Mail konfiguriert werden, um E-Mails senden zu können. Weitere Informationen finden Sie unter [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md).  
  
    3.  Wählen Sie zum Speichern detaillierter Informationen unter **Protokollierung**die Option **Erweiterte Informationen protokollieren**aus.  
  
    4.  Wählen Sie zum Schreiben von Informationen zu Wartungsplanergebnissen auf einen anderen Server die Option **Auf Remoteserver protokollieren** , und wählen Sie entweder eine Serververbindung aus der Liste **Verbindung** aus, oder klicken Sie auf **Neu** , und geben Sie die Verbindungsinformationen im Dialogfeld **Verbindungseigenschaften** ein.  
  
    5.  Klicken Sie im Dialogfeld **Berichterstellung und Protokollierung** auf **OK**.  
  
12. Wenn Sie die Ergebnisse im Protokolldatei-Viewer anzeigen möchten, klicken Sie im **Objekt-Explorer**mit der rechten Maustaste entweder auf den Ordner **Wartungspläne** oder auf einen bestimmten Wartungsplan, und klicken Sie dann auf **Verlauf anzeigen**.  
  
     Die folgenden Optionen sind im Dialogfeld **Protokolldatei-Viewer –***server_name* verfügbar.  
  
     **Protokoll laden**  
     Öffnen Sie ein Dialogfeld, in dem Sie eine zu ladende Protokolldatei angeben können.  
  
     **Exportieren**  
     Öffnen Sie ein Dialogfeld, in dem Sie die im Raster **Protokolldateizusammenfassung** angezeigten Informationen in eine Textdatei exportieren können.  
  
     **Aktualisieren**  
     Aktualisieren Sie die Anzeige der ausgewählten Protokolle. Beim Übernehmen von Filtereinstellungen werden mithilfe der Schaltfläche **Aktualisieren** die ausgewählten Protokolle erneut vom Zielserver gelesen.  
  
     **Filter**  
     Öffnen Sie ein Dialogfeld, in dem Sie zum Filtern der Protokolldatei verwendete Einstellungen angeben können, z.B. Filterkriterien wie **Verbindung**, **Datum**oder **Allgemein** .  
  
     **Suchen**  
     Durchsuchen Sie die Protokolldatei nach bestimmtem Text. Das Suchen mit Platzhalterzeichen wird nicht unterstützt.  
  
     **Beenden**  
     Beendet das Laden der Protokolldateieinträge. Diese Option können Sie z. B. verwenden, wenn das Laden einer Remote- oder Offline-Protokolldatei eine lange Zeit in Anspruch nimmt und Sie nur die zuletzt erstellten Einträge anzeigen möchten.  
  
     **Protokolldateizusammenfassung**  
     In diesem Informationsbereich wird eine Zusammenfassung der Protokolldateifilterung angezeigt. Wenn die Datei nicht gefiltert wurde, wird folgender Text angezeigt: **Kein Filter angewendet**. Nach Anwendung eines Filters auf das Protokoll wird folgender Text angezeigt: **Protokolleinträge auf diesen Fall filtern:**\<Filterkriterien>.  
  
     **Datum**  
     Zeigt das Datum des Ereignisses an.  
  
     **Quelle**  
     Zeigt die Ausgangsfunktion an, mit dem das Ereignis erstellt wurde, z. B. den Namen des Diensts (z. B. MSSQLSERVER). Dies wird nicht für alle Protokolltypen angezeigt.  
  
     **MessageBox**  
     Zeigt die Meldungen an, die dem Ereignis zugeordnet sind.  
  
     **Protokolltyp**  
     Zeigt den Typ des Protokolls an, zu dem das Ereignis gehört. Alle ausgewählten Protokolle werden im Fenster für die Protokolldateizusammenfassung angezeigt.  
  
     **Protokollquelle**  
     Zeigt eine Beschreibung des Quellprotokolls an, in dem das Ereignis aufgezeichnet wird.  
  
     **Details für die ausgewählte Zeile**  
     Wählen Sie eine Zahl aus, um am unteren Rand der Seite zusätzliche Details zu der ausgewählten Ereigniszeile anzuzeigen. Die Spalten können durch Ziehen an neue Positionen im Raster neu angeordnet werden. Die Breite der Spalten kann durch Ziehen der Spaltentrennbalken in der Kopfzeile des Rasters nach links oder rechts geändert werden. Wenn Sie auf die Spaltentrennbalken in der Kopfzeile des Rasters doppelklicken, wird die Breite der Spalte automatisch an die Breite des Inhalts angepasst.  
  
     **Instanz**  
     Der Name der Instanz, bei der das Ereignis aufgetreten ist. Dieser wird im Format *Computername*\\*Instanzname*.  
  
  
