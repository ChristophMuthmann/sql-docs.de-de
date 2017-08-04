---
title: "Hohe Verfügbarkeit und Notfallwiederherstellung für Master Data Services | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: sabotta
ms.author: carlasab
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2afbf59101a0605dba2e79f09777160cb4de5cab
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---



# <a name="high-availability-and-disaster-recovery-for-master-data-services"></a>Hohe Verfügbarkeit und Notfallwiederherstellung für Master Data Services

**Zusammenfassung:** Dieser Artikel beschreibt eine Lösung für die Konfiguration von Master Data Services (MDS), gehostet in einer Always On-Verfügbarkeitsgruppe. Der Artikel beschreibt, wie Sie SQL 2016 Master Data Services auf einer SQL 2016 AlwaysOn-Verfügbarkeitsgruppe (availability group, AG) installieren und konfigurieren. Der Hauptzweck dieser Lösung ist die Verbesserung der hohen Verfügbarkeit und der Notfallwiederherstellung von MDS-Back-End-Daten, die auf einer SQL Server-Datenbank gehostet werden.

## <a name="introduction"></a>Einführung


Dieser Artikel beschreibt eine Lösung für Master Data Service (MDS) in der Konfiguration einer AlwaysOn-Verfügbarkeitsgruppe gehostet. Der Artikel beschreibt, wie zum Installieren und Konfigurieren von SQL 2016 MDS auf einer SQL 2016 AlwaysOn-verfügbarkeitsgruppe (AG). Der Hauptzweck dieser Lösung ist die Verbesserung der hohen Verfügbarkeit und der Notfallwiederherstellung von MDS-Back-End-Daten, die auf einer SQL Server-Datenbank gehostet werden.

Um die Lösung zu implementieren, müssen Sie die folgenden Aufgaben in diesem Artikel beschriebene ausführen.

1.  [Installieren und Einrichten von Windows Server Failover Cluster (WSFC)](#windows-server-failover-cluster-wsfc).

2.  [Richten Sie AlwaysOn-Verfügbarkeitsgruppe](#sql-server-alwayson-availability-group).

3.  [Konfigurieren von MDS auf einer wsfc-Knoten ausgeführt](#configure-mds-to-run-on-an-wsfc-node).

In den oben aufgeführten Abschnitten werden die Technologien, gefolgt von Anweisungen kurz vorgestellt. Ausführliche Informationen zu den Technologien finden Sie in den Dokumenten, die in jedem Abschnitt verknüpft.

Diese Lösung, die in diesem Artikel beschriebenen baut auf SQL Server AlwaysOn-Verfügbarkeitsgruppe, in dem jede Datenbank verfügt über mehrere Replikate für synchrone oder asynchrone. Nur ein Replikat die Transaktion akzeptiert (benutzeranforderungen akzeptiert). Dies ist das primäre Replikat.

Jedes Replikat hat seinen eigenen Speicher an, sodass es keine zentralisierte freigegebener Speicher in dieser Lösung ist. Bei einem Softwarefehler oder ein Hardwarefehler Auswirkungen auf dem primären Replikat vorhanden ist, kann das primäre Replikat an ein Replikat für synchrone oder asynchrone Failover ausgeführt werden, die entweder automatisch oder manuell auf die Konfiguration und Situationen basieren. Hohe Verfügbarkeit der Datenbank mit minimaler Unterbrechung für die Benutzer gewährleistet ist.

Asynchrone Replikate werden in der Regel in einem Rechenzentrum gehostet, die in das primäre Replikat-Rechenzentrum remote ausgeführt wird. Bei einem Notfallszenarien kann das primäre Replikat Failover zu einem anderen Rechenzentrum ausgeführt werden. Dadurch wird die Wiederherstellung der Datenbank sichergestellt.

Zu Demonstrationszwecken Zweck verwendet in diesem Artikel beschriebene Lösung die folgenden Versionen der Software. Ältere Versionen sollte identisch mit potenziell geringfügigen Unterschieden funktionieren.

-   Windows Server 2012 R2 mit Server-Failovercluster

-   SQL Server 2016 mit Master Data Services-Funktion

Die Lösung verwendet außerdem zwei VMs **MDS-HA1** und **MDS-HA2**, um zwei Replikate hosten. Solange sie von SQL Server AlwaysOn-Verfügbarkeitsgruppe unterstützt wird, wird MDS nicht wie viele Replikate beschränkt, Sie verwenden können.

In diesem Artikel wird davon ausgegangen, dass Sie über grundlegende Kenntnisse über Windows Server, Windows Server Failover Cluster SQL Server AlwaysOn und SQL Server MDS verfügen.

## <a name="what-is-not-covered"></a>Was wird nicht behandelt.

Dieses Dokument deckt nicht Folgendes:

-   Wie Sie IIS, Web-Hostserver in der Master Data service-Benutzeroberfläche mit hoher Verfügbarkeit, die nach einem Notfall wiederhergestellt. MDS administratorverbindungen werden keine bestimmte Anforderung unter IIS, damit die standardmäßigen Techniken, um IIS hoch verfügbar machen und Lastenausgleich auch hier arbeiten können.

-   Wie Sie SQL Server AlwaysOn-Failovercluster (FCI) zu verwenden, um hohe Verfügbarkeit (HA) auf dem MDS-Back-End zu unterstützen. SQL Server-Failoverclustering ist eine andere Lösung für hohe Verfügbarkeit und wird von SQL Server offiziell unterstützt und funktioniert dies mit MDS.

-   Wie Sie Hybrid-Lösung von SQL Server-Failovercluster (FCI) und AlwaysOn-Verfügbarkeitsgruppe zu verwenden, um hohe Verfügbarkeit auf dem MDS-Back-End zu unterstützen. Die Hybrid-Lösung funktioniert mit MDS.

## <a name="design-consideration"></a>Designüberlegung

Abbildung 1 zeigt eine typische Konfiguration vorwiegend in den AlwaysOn-Verfügbarkeitsgruppe verwendet. Im primären Datencenter es gibt zwei Replikate mit synchronem Commit Beziehung, und beide Replikate die Berechtigung zum Abstimmen. Dies wird hauptsächlich verwendet, um die hohe Verfügbarkeit zu verbessern, für den Fall, dass das primäre Replikat ausfällt.

Im Rechenzentrum Disaster Recovery ist mit einer asynchronen Commit-Beziehung mit dem primären Replikat ein sekundäres Replikat vorhanden. Rechenzentrum ist in der Regel in einer geografischen Region anders als das primäre Rechenzentrum. Das sekundäre Replikat besitzt nicht die Stimme-Berechtigung.

Diese Konfiguration wird verwendet, um die Wiederherstellung zu erzielen, für den Fall, dass das primäre Rechenzentrum in einem Notfall, z. B. ein Brand, Erdbeben usw. ist. Die Konfiguration bietet sowohl hohe Verfügbarkeit und Disaster Recovery mit relativ geringen Kosten.

![Standardkonfiguration für AlwaysOn-Verfügbarkeitsgruppe.](media/Fig1_TypicalConfig.png)

Abbildung 1. Eine Typische AlwaysOn Availability Group-Konfiguration

Wenn Sie nicht zur Wiederherstellung im Notfall berücksichtigen müssen, müssen Sie ein Replikat in einem zweiten Rechenzentrum haben. Wenn Sie hohe Verfügbarkeit zu verbessern möchten, können Sie weitere synchroner Replikate in primären Rechenzentrums mit verfügen.

Daher ist es wichtig, müssen Sie berücksichtigen, die Szenarien und Anforderungen, und wählen wie viele asynchrone und synchrone Replikate, und welches Rechenzentrum Sie sollten in.

## <a name="windows-server-failover-cluster-wsfc"></a>Windows Server-Failovercluster (WSFC)

In diesem Abschnitt werden die folgenden Aufgaben behandelt.

1.  [Installieren Sie Windows-Failovercluster-Features](#install-failover-cluster-feature).

2.  [Erstellen eines Windows Server-Failoverclusters](#create-a-windows-server-failover-cluster).

Wie in Abbildung 1 im vorherigen Abschnitt gezeigt, enthält die Projektmappe, die in diesem Artikel beschriebene Windows Server-Failovercluster (WSFC). Wir müssen WSFC eingerichtet werden, da SQL-AlwaysOn von WFSC für fehlererkennung und Failover abhängt.

WSFC ist ein Feature, mit hoher Verfügbarkeit von Anwendungen und Dienste zu verbessern. Es besteht aus einer Gruppe von unabhängigen Windows Server-Instanzen mit Microsoft-Failoverclusterdiensts ausgeführt werden, auf den Instanzen. Die Windows Server-Instanzen (oder Knoten, wie sie manchmal aufgerufen werden) verbunden sind, sodass sie miteinander kommunizieren können und die fehlererkennung möglich ist. WSFC geben Fehler Erkennung und automatisches Failover-Funktionen. Wenn Sie einen Knoten oder ein Dienst im Cluster ausfällt, klicken Sie dann den Fehler erkannt hat, und einen anderen Knoten automatisch oder manuell startet, um die auf den fehlerhaften Knoten gehosteten Dienste bereitzustellen. Als solche Benutzer nur minimalen Unterbrechungen in Dienste auftreten, und zur Verbesserung der Verfügbarkeit des Diensts.  

### <a name="prerequisites"></a>Erforderliche Komponenten

Für alle Instanzen der Windows Server-Betriebssystem installiert ist, und alle Updates gepatcht werden.

>[!NOTE] 
>Es ist **empfohlen** die Installation von der gleichen Windows-Version und die gleiche Funktion in allen Instanzen festgelegt wird, um alle möglichen Kompatibilitätsproblemen zu vermeiden.

### <a name="install-failover-cluster-feature"></a>Failoverclusterfunktion installieren

Die folgenden Schritte für jede Windows Server-Instanz, die wsfc-Funktion für jede Instanz zu installieren. Sie benötigen Administratorberechtigungen.

1.  Open **Server-Manager** in Windows Server, und klicken Sie auf **Hinzufügen von Rollen und Features** im rechten Bereich. Hierdurch wird die **Hinzufügen von Rollen und Features Assistenten**.

2.  Klicken Sie auf **Weiter** , bis Sie zum Abrufen der **Funktionen** Seite.

3.  Wählen Sie die **Failoverclustering** Kontrollkästchen, und klicken Sie dann auf **Weiter** um die Installation abzuschließen. Siehe Abbildung 2.

    Wenn Sie, für die Bestätigung zur gefragt werden **Hinzufügen von Funktionen, die für das Failoverclustering erforderlich sind**, klicken Sie auf **Features hinzufügen**. Siehe Abbildung 3.

    ![Hinzufügen von Rollen und Features Assistenten Failover-Clusterunterstützung](media/Fig2_SelectFeatures.png)

    Abbildung 2

    ![Hinzufügen von Rollen und Features-Assistenten für Failover-Cluster erforderlich sind](media/Fig3_RequiredFeaturesFailover.png)

    Abbildung 3

4.  Auf der **Bestätigung** auf **installieren** Feature Failoverclustering installiert.

5.  Auf der **Ergebnis** Seite, stellen Sie sicher, dass alles wurde ohne Fehler und Warnungen erfolgreich installiert wurde.

### <a name="create-a-windows-server-failover-cluster"></a>Erstellen eines Windows Server-Failoverclusters

Nachdem die wsfc-Funktion auf alle Instanzen installiert ist, können Sie WSFC konfigurieren. Sie müssen nur diese auf einem Knoten vorgenommen werden.

1.  Open **Server-Manager** in Windows Server, und klicken Sie auf **Failovercluster-Manager** auf die **Tool** Menü in der oberen rechten Ecke auf den Manager zu starten.

2.  In **Failovercluster-Manager**, klicken Sie auf **Konfiguration überprüfen** im rechten Bereich. Siehe Abbildung 4.

    ![Überprüfen Sie Failovercluster-Manager die Konfiguration](media/Fig4_ValidateConfig.png)

    Abbildung 4

3.  In der **Konfiguration überprüfen** **Assistenten**, klicken Sie auf **Weiter**.

4.  In der **wählen Sie Server oder Cluster** Dialogfeld Feld, fügen Sie den Servernamen, die SQL Server gehostet werden, und klicken Sie dann auf **Weiter**. Siehe Abbildung 5.

    In diesem Beispiel haben wir zwei Instanzen, MDS-HA1 und MDS-HA2 hinzugefügt.

    ![Überprüfen Sie einen Konfigurations-Assistenten, Server auswählen oder eine Seite "Cluster"](media/Fig5_AddServer.png)

    Abbildung 5

5.  Auf der **Testoptionen** auf **Ausführen aller Tests**, und klicken Sie dann auf **Weiter**.

6.  Klicken Sie auf **Weiter** um die Überprüfung abzuschließen.

    Die **Validating** Seite zeigt den Fortschritt und die **Zusammenfassung** Seite zeigt die Zusammenfassung der Validierung. Finden Sie in Abbildung 6 und 7.

7.  Auf der **Zusammenfassung** Seite, überprüfen Sie alle Warn- oder Fehlermeldungen.

    Fehler müssen behoben werden. Warnungen möglicherweise ein Problem jedoch nicht. Eine Warnmeldung bedeutet, dass "das getestete Element kann die Anforderung erfüllen, aber etwas geprüft werden sollten". Beispielsweise Abbildung 7 zeigt ein "Überprüfen Datenträgerlatenz-Zugriff", die möglicherweise aufgrund des Datenträgers wird vorübergehend auf andere Vorgänge ausgelastet und kann ignoriert werden, es "Warnung" und. Sie sollte dem folgenden Onlinedokument für jede Warnung und Fehlermeldung für weitere Details überprüfen. Siehe Abbildung 7.
 
    ![Überprüfen Sie die Konfigurations-Assistent, Seite "Überprüfung"](media/Fig6_ValidationTests.png)

    Abbildung 6

    ![Konfigurationsüberprüfungs-Assistent, Seite "Zusammenfassung"](media/Fig7_ValidationSummary.png)

    Abbildung 7

8.  Auf der **Zusammenfassung** Seite sicher, dass die **Cluster jetzt unter Verwendung der überprüften Knoten erstellen** aktiviert ist, und klicken Sie dann auf **Fertig stellen** zum Starten der **Clustererstellungs** **Assistenten**.

9.  In der **Clustererstellungs** **Assistenten**, klicken Sie auf **Weiter**.

10. Auf der **Zugriffspunkt für die Clusterverwaltung** Seite Geben Sie den Namen des wsfc-Cluster, und klicken Sie dann auf **Weiter**. In diesem Beispiel verwenden wir "MDS-HA" als Namen des Clusters. Siehe Abbildung 8.

    ![Geben Sie den Namen des Clusters](media/Fig8_EnterClusterName.png)

    Abbildung 8

11. Klicken Sie auf Weiter **Weiter** zum Abschließen der Erstellung des Clusters. Die **Zusammenfassung der Cluster MDS-HA** Abschnitt zeigt die Clusterinformationen. Siehe Abbildung 9.

    ![Anzeigen von Zusammenfassungsinformationen für den Cluster](media/Fig9_ClusterSummary.png)

    Abbildung 9

    Wenn Sie später einen Knoten hinzufügen möchten, klicken Sie auf **AddNode** Aktion im rechten Bereich in **Failovercluster-Manager**.

Hinweise:

-   Die wsfc-Funktion kann nicht in allen Editionen von Windows Server zur Verfügung. Stellen Sie sicher, dass Ihre Edition über diese Funktion verfügt.

-   Stellen Sie sicher, dass Sie die erforderlichen Berechtigungen zum Einrichten von WSFC in active Directory verfügen. Wenn Probleme sind, finden Sie unter [schrittweise Anleitung für Failovercluster: Konfigurieren von Konten in Active Directory](https://technet.microsoft.com/library/cc731002(v=ws.10).aspx).

Ausführlichere Informationen zu wsfc-finden Sie unter [Failoverclustern](https://technet.microsoft.com/library/cc732488(v=ws.10).aspx).

## <a name="sql-server-alwayson-availability-group"></a>SQL Server AlwaysOn-Verfügbarkeitsgruppe

In diesem Abschnitt werden die folgenden Aufgaben behandelt.

1.  [Enable SQL Server AlwaysOn-Verfügbarkeitsgruppe](#enable-sql-server-alwayson-availability-group-on-every-sql-server-instance).

2.  [Erstellen einer Verfügbarkeitsgruppe](#create-an-availability-group).

3.  [Überprüfen und Testen Sie die Verfügbarkeitsgruppe](#validation-and-test-the-availability-group).

SQLServer AlwaysOn-Lösung bietet hohe Verfügbarkeit und Wiederherstellung im Notfall für SQL Server-Datenbanken. AlwaysOn hat zwei mögliche Lösungen.
Beide basieren auf WSFC.

-   AlwaysOn-Verfügbarkeitsgruppen (VG)

-   AlwaysOn-Failoverclusterinstanzen (FCI).

AG verbessert die hohe Verfügbarkeit auf Datenbankebene. Die AG (ein Satz von Benutzerdatenbanken) und den Namen des virtuellen Netzwerks werden als Ressourcen in WSFC registriert.

FCI verbessert die hohe Verfügbarkeit auf Instanzebene. SQL Server-Dienst und die zugehörigen Dienste werden als Ressourcen in WSFC registriert. Zudem dass, die FCI-Lösung symmetrischen freigegebenen Festplattenspeicher, z. B. SAN oder SMB-Dateifreigaben, die für alle Knoten in einem WFC-Cluster verfügbar sein muss.


### <a name="prerequisites"></a>Erforderliche Komponenten

-   Installieren von SQL Server auf allen Knoten. Weitere Informationen finden Sie unter [Installieren von SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server).

-   (Empfohlen) Installieren Sie die genaue denselben Funktionsumfang von SQL Server und die Version auf jedem Knoten an. Insbesondere muss MDS installiert sein.

-   (Empfohlen) Verwenden Sie die gleiche Konfiguration auf jeder SQL Server-Instanz. Insbesondere muss die gleiche Server-Sortierung für alle SQL Server-Instanzen konfiguriert werden.

-   (Empfohlen) Verwenden Sie das gleiche Dienstkonto Jeder SQL Server-Instanz ausgeführt. Andernfalls müssen Sie gewähren der Berechtigung für jede SQL Server-Instanz, um sicherzustellen, dass der SQL Server-Instanzen, die miteinander kommunizieren können.

-   Vergewissern Sie sich, dass die Windows-Firewall-Einstellung der SQL Server-Instanzen, die miteinander kommunizieren kann.

### <a name="enable-sql-server-alwayson-availability-group-on-every-sql-server-instance"></a>Enable SQL Server AlwaysOn-Verfügbarkeitsgruppe auf jeder SQL Server-Instanz

1.  In der **SQL Server-Konfigurations-Manager** klicken Sie auf **SQL Server-Dienst** im linken Bereich mit der Maustaste **SQL Server** im rechten Bereich, und klicken Sie dann auf **Eigenschaften**. Siehe Abbildung 10.

    ![Fenster "Eigenschaften von SQL Server"](media/Fig10_SQLServerProperties.png)

    Abbildung 10

2.  In der **SQL Server (MSSQLSERVER)** **Eigenschaften** (Dialogfeld), klicken Sie auf die **hohe Verfügbarkeit mit AlwaysOn** Registerkarte, und wählen Sie dann die **AlwaysOn-Verfügbarkeitsgruppen aktivieren** Kontrollkästchen. Wenn ein Wert angezeigt, der **Name des Windows-Failoverclusters** Textfeld, klicken Sie auf **OK** um den Vorgang fortzusetzen. Siehe Abbildung 11.

    ![Aktivieren Sie AlwaysOn-Verfügbarkeitsgruppen-option](media/Fig11_EnableAlwaysOn.png)

    Abbildung 11

3.  Wenn eine Seite "Warnungen" angezeigt wird, klicken Sie auf **OK** um den Vorgang fortzusetzen. Siehe Abbildung 12.

    ![Bestätigen Sie zum Beenden und Neustarten des Diensts](media/Fig12_WarningServiceStopStart.png)

    Abbildung 12

4.  Klicken Sie auf **neu starten**, um den Neustart der **SQL Server** service, und stellen Sie diese Änderung wirksam. Siehe Abbildung 10.

>[!NOTE] 
>Sie können ändern, dass das Dienstkonto ausgeführt wird, den SQL Server-Dienst mithilfe der **SQL Server-Konfigurations-Manager**. Klicken Sie auf die **anmelden** Registerkarte der **SQL Server (MSSQLSERVER)** **Eigenschaften** (Dialogfeld). Siehe Abbildung 11.

### <a name="create-an-availability-group"></a>Erstellen einer Verfügbarkeitsgruppe

Nachdem die Funktion "AlwaysOn" in allen Instanzen von SQL Server aktiviert ist, erstellen Sie eine neue VGS, die die MDS-Datenbank auf einem Knoten enthält.

AG kann nur für bestehende Datenbanken erstellt werden. So erstellen Sie eine MDS-Datenbank auf einem Knoten oder eine temporäre Datenbank erstellen und dann die temporäre Datenbank löschen. In diesem Beispiel haben wir eine EmptyMDS-Datenbank erstellen und eine AG in dieser MDS-Datenbank erstellen.

1.  Starten Sie **SQL Server Management Studio** (**SSMS**) auf einem Knoten und Herstellen einer Verbindung mit der lokalen SQL Server-Instanz mit entsprechenden Anmeldeinformationen.

2.  Öffnen Sie in SSMS eine **neue Abfrage** Fenster, und führen Sie das folgende Skript, um eine leere Datenbank zu erstellen. Ersetzen Sie "c:"\\durch den Speicherort der temporären, das Sie verwenden, um eine vollständige Sicherung ausführen möchten.

    ```
    CREATE DATABASE MDS\_Sample
    GO
    BACKUP DATABASE MDS\_Sample TO DISK='C:\\temp'
    GO
    ```

    >[!NOTE] 
    >Eine vollständige Sicherung ist erforderlich zum Erstellen der Verfügbarkeitsgruppe für diese Datenbank.

3.  In der **Objekt-Explorer**, erweitern Sie die **hohe Verfügbarkeit mit AlwaysOn** Ordner, und klicken Sie auf **Assistenten für neue Verfügbarkeitsgruppen** zum Starten der **Assistenten für neue Verfügbarkeitsgruppen**. Siehe Abbildung 13.

    ![Assistent für neue Verfügbarkeitsgruppen starten](media/Fig13_AvailabilityGroupsFolder.png)

    Abbildung 13

4.  In der **neue Verfügbarkeitsgruppe** -Assistenten klicken Sie auf **Weiter** zum Anzeigen der **angeben** Seite. Geben Sie einen Namen für die Verfügbarkeitsgruppe, und klicken Sie dann auf **Weiter**. Finden Sie unter Abbildung 14.

    ![Geben Sie den Namen der Verfügbarkeitsgruppe.](media/Fig14_AvailabilityGroupName.png)

    Abbildung 14

5.  Klicken Sie auf die Datenbank, die Sie gerade erstellt haben, auf die **Datenbank auswählen** Seite, und klicken Sie dann auf **Weiter**. Finden Sie unter Abbildung 15.

    ![Wählen Sie die Datenbank](media/Fig15_AvailabilityGroupSelectDatabase.png)

    Abbildung 15

6.  Auf der **Replikate angeben** Seite, fügen Sie einem anderen Replikat, indem Sie auf **Hinzufügen von Replikaten**. Diese Seite enthält bereits die aktuellen, lokalen SQL Server-Instanzen als Replikat. Finden Sie unter Abbildung 16.

7.  In der **Verbindung mit Server herstellen** Dialogfeld Feld, fügen Sie die entsprechenden Anmeldeinformationen aus, und klicken Sie auf **verbinden**.

    ![Herstellen einer Verbindung mit einer SQL Server-Instanz](media/Fig16_AddReplicaConnectServer.png)

    Abbildung 16

    Nun sollten zwei Replikate in der Liste angezeigt werden. Wiederholen Sie diesen Schritt, um die anderen Knoten als Replikate hinzuzufügen. Finden Sie unter Abbildung 17.

    ![Liste der Replikate anzeigen](media/Fig17_AvailabilityGroupSQLReplicas.png)

    Abbildung 17

    Konfigurieren Sie für jedes Replikat Folgendes **synchroner Commit**, **automatisches Failover**, und **lesbare sekundäre Replikate** Einstellungen. Siehe Abbildung
17.

    **Synchroner Commit**: Dadurch wird sichergestellt, dass eine Transaktion auf dem primären Replikat einer Datenbank ein Commit ausgeführt wird, klicken Sie dann die Transaktion auch auf alle synchronen Replikate ausgeführt wird. Asynchroner Commit garantiert dies jedoch nicht, und es hinter dem primären Replikat liegen kann.

    Nur, wenn die zwei Knoten im selben Rechenzentrum befinden, sollten Sie in der Regel synchronen Commit aktivieren. Wenn sie sich in unterschiedlichen Rechenzentren befinden, kann die Leistung der Datenbank synchroner Commit verlangsamen.

    Wenn dieses Kontrollkästchen nicht aktiviert ist, wird die asynchroner Commit verwendet.

    **Automatisches Failover:** , wenn das primäre Replikat nicht ausgeführt wird, die Verfügbarkeitsgruppe wird automatisch Failover auf das sekundäre Replikat Wenn Automatisches Failover aktiviert ist. Dies kann nur auf den Replikaten mit synchronen Commits aktiviert werden.

    **Lesbare sekundäre Rolle:** standardmäßig Benutzer keine Verbindung alle sekundären Replikate. Dadurch können Benutzer eine Verbindung mit dem sekundären Replikat mit nur-Lese-Zugriff herstellen.

8.  Auf der **Replikate angeben** auf die **Listener** Registerkarte, und führen Sie die folgenden Schritte. Finden Sie unter Abbildung 18.

    A.  Klicken Sie auf **erstellen ein verfügbarkeitsgruppenlisteners** So richten Sie einen verfügbarkeitsgruppenlistener für die Verbindung mit der MDS-Datenbank ein.

    B.  Geben Sie einen **Listener DNS-Namen**, z. B. MDSSQLServer.

    c.  Geben Sie die Standard-SQL-Port 1433, in der **Port** Textfeld.

    d.  Geben Sie DHCP in der **Netzwerkmodus** Textfeld, und klicken Sie dann auf **Weiter** um den Vorgang fortzusetzen.

    >[!NOTE] 
    >Optional können Sie "Statische IP-Adresse" entscheiden, wie die **Netzwerkmodus** , und geben Sie eine statische IP-Adresse. Sie können auch einen anderen Port als 1433 eingeben. 

    ![Konfigurieren Sie den Listener](media/Fig18_AvailabilityGroupCreateListener.png)

    Abbildung 18

9.  Auf der **Datensynchronisierung auswählen** auf **vollständige**, und geben Sie eine Netzwerkfreigabe, die alle Knoten zugreifen können. Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen. Finden Sie unter Abbildung 19.

    Diese Netzwerkfreigabe dienen zum Speichern der datenbanksicherung zum Erstellen von sekundärer Replikats. Wenn diese nicht für Ihre Organisation verfügbar sind, wählen Sie eine andere Einstellung für die datensynchronisierung aus. Verweisen auf [SQL Server 2016 AlwaysOn Availability Group](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server) zum anderen Optionen verwenden, um die sekundären Replikate zu erstellen. Die Abbildung 17 sind auch andere Optionen aufgeführt.

    ![Konfigurieren der datensynchronisierung](media/Fig19_AvailabilityGroupDataSync.png)

    Abbildung 19 

10. Auf der **Überprüfung** Seite, stellen Sie sicher, dass alle Überprüfungen erfolgreich übergeben, und beheben Sie alle Fehler. Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.

11. Auf der **Zusammenfassung** Seite, überprüfen Sie die Konfigurationseinstellungen, und klicken Sie auf **Fertig stellen**. Dadurch wird die verfügbarkeitsgruppe erstellen und konfigurieren.

12. Auf der **Ergebnis** Seite, vergewissern Sie sich, dass alle notwendigen Schritte abgeschlossen wurden.

### <a name="validation-and-test-the-availability-group"></a>Prüf- und Testparameter Verfügbarkeitsgruppe.

1.  Öffnen Sie SSMS und Herstellen einer Verbindung mit den DNS-Listenernamen, die Sie gerade erstellt, in haben der [Erstellen einer Verfügbarkeitsgruppe](#create-an-availability-group) Abschnitt. In diesem Beispiel ist es MDSSQLServer.

2.  In **Objekt-Explorer**, erweitern Sie die **hohe Verfügbarkeit mit AlwaysOn** Ordner, mit der rechten Maustaste in die Verfügbarkeitsgruppe, die Sie gerade erstellt die [Erstellen einer Verfügbarkeitsgruppe](#create-an-availability-group) Abschnitt, und klicken Sie dann auf **Dashboard anzeigen**. Finden Sie unter Abbildung 20. Der Status der neuen Verfügbarkeitsgruppe und ihrer Replikate angezeigt wird.

    ![Zeigen Sie das dashboard](media/Fig20_ShowDashboard.png)

    Abbildung 20 

3.  Klicken Sie auf **Failover** , führen Sie ein Failover auf ein synchrones Replikat und ein asynchrones Replikat. Dies ist zu überprüfen, ob dieses Failover ohne Probleme ordnungsgemäß erfolgt.

 Die AlwaysOn-Setup abgeschlossen ist.

Weitere Informationen zu AlwaysOn-Availability Group, finden Sie unter [SQL Server 2016 AlwaysOn Availability Group](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server).

## <a name="configure-mds-to-run-on-an-wsfc-node"></a>Konfigurieren von MDS für die Ausführung auf einem wsfc-Knoten

Diese Lösung, die in diesem Artikel vorgestellten erfordert nur die MDS-Back-End-Datenbank für wsfc-Cluster ausgeführt wird. Andere Teile von MDS, z. B. Webanwendungen und MDS-Konfigurations-Manager können entweder auf den Knoten im wsfc- oder außerhalb der WSFC ausgeführt werden, solange die AG MDS herstellen können.

1.  Open **Konfigurations-Manager für Master Data Service** auf einem Knoten, klicken Sie auf **Datenbankkonfiguration**, und klicken Sie dann auf **Create Database** zum Starten der **Assistenten zum Erstellen von Datenbanken**.

2.  Auf der **Datenbankserver** Seite, geben Sie den AG-Listener DNS-Namen in der **SQL Server-Instanz** Textfeld, klicken Sie auf **Testverbindung**, und klicken Sie dann auf **Weiter**. Finden Sie unter Abbildung 21.

    ![Konfigurieren des Datenbankservers mit AG-listener](media/Fig21_MDSDatabaseServerListener.png)

    Abbildung 21

3.  Auf der **Datenbank** Seite, geben Sie den Namen der Datenbank, die Sie in erstellt die [Erstellen einer Verfügbarkeitsgruppe](#create-an-availability-group) Abschnitt, und klicken Sie dann auf **Weiter**. Finden Sie unter Abbildung 22.

    ![Erstellen und Konfigurieren der Datenbank](media/Fig22_MDSCreateDatabase.png)

    Abbildung 22

4.  Führen Sie die **-Datenbankerstellung** **Assistenten**. Weitere Informationen finden Sie unter [Master Data Services-Installation und Konfiguration](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration).

5.  Klicken Sie auf **Webanwendungen** in **Konfigurations-Manager für Master Data Service** die Webanwendung konfigurieren, und klicken Sie dann auf **übernehmen** zum Anwenden der Einstellungen in MDS. Finden Sie unter Abbildung 23. Weitere Informationen finden Sie unter [Master Data Services-Installation und Konfiguration](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration).

    ![Die Webanwendung konfigurieren](media/Fig23_MDSWebApplication.png)

    Abbildung 23

    Die MDS-Setup abgeschlossen ist. Wiederholen Sie die oben genannten Schritte, um MDS einzurichten, führen Sie auf allen Knoten. Die Back-End-Datenbank ist in der gleichen Verfügbarkeitsgruppe identisch.

6.  Wenn zuvor eine temporäre Datenbank erstellt (siehe [Erstellen einer Verfügbarkeitsgruppe](#create-an-availability-group) Abschnitt) um AlwaysOn-Verfügbarkeitsgruppe zu erstellen, klicken Sie dann Sie sollten die temporäre Datenbank löschen

    Weitere Informationen zu Master Data Services, finden Sie unter [Master Data Services](https://docs.microsoft.com/sql/master-data-services/master-data-services-overview-mds).

## <a name="conclusion"></a>Fazit

In diesem Whitepaper haben wir gesehen, einrichten und konfigurieren die Master Data Services Back-End-Datenbank auf SQL Server AlwaysOn-Verfügbarkeitsgruppe. Diese Konfiguration bietet hohe Verfügbarkeit und notfallwiederherstellung für die Master Data Services-Back-End-Datenbank. Um diese Konfiguration zu implementieren, müssen Sie zum Installieren und Konfigurieren von Windows Server Failover Cluster, SQL Server AlwaysOn-Verfügbarkeitsgruppe und Master Data Services.

## <a name="feedback"></a>Feedback

War dieses Dokument hilfreich? Bitte senden Sie uns Ihr Feedback durch Klicken auf **Kommentare** am Anfang des Artikels. 

Ihr Feedback hilft uns die Verbesserung der Qualität des Whitepapers unserer. 


