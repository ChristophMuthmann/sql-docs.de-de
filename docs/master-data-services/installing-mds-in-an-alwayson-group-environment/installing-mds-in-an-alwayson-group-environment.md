---
title: "Hochverfügbarkeit und Notfallwiederherstellung für Master Data Services | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/28/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: installing-mds-in-an-alwayson-group-environment
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: f5cebe2ba32765cc5f4bddc974ee62b3ed3b8915
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---



# <a name="high-availability-and-disaster-recovery-for-master-data-services"></a>Hochverfügbarkeit und Notfallwiederherstellung für Master Data Services

**Zusammenfassung:** Dieser Artikel beschreibt eine Lösung für die Konfiguration von Master Data Services (MDS), gehostet in einer Always On-Verfügbarkeitsgruppe. Der Artikel beschreibt, wie Sie SQL 2016 Master Data Services auf einer SQL 2016 AlwaysOn-Verfügbarkeitsgruppe (availability group, AG) installieren und konfigurieren. Der Hauptzweck dieser Lösung ist die Verbesserung der hohen Verfügbarkeit und der Notfallwiederherstellung von MDS-Back-End-Daten, die auf einer SQL Server-Datenbank gehostet werden.

## <a name="introduction"></a>Einführung


Dieser Artikel beschreibt eine Lösung für die Konfiguration von Master Data Services (MDS), gehostet auf einer Always On-Verfügbarkeitsgruppe. Der Artikel beschreibt, wie Sie SQL 2016 MDS auf einer SQL 2016 Always On-Verfügbarkeitsgruppe (Availability Group, AG) installieren und konfigurieren. Der Hauptzweck dieser Lösung ist die Verbesserung der hohen Verfügbarkeit und der Notfallwiederherstellung von MDS-Back-End-Daten, die auf einer SQL Server-Datenbank gehostet werden.

Um die Lösung zu implementieren, müssen Sie die folgenden Aufgaben, die in diesem Artikel beschrieben sind, ausführen.

1.  [Installieren und Einrichten des Windows Server Failover Clusters (WSFC)](#windows-server-failover-cluster-wsfc)

2.  [Einrichten der Always On-Verfügbarkeitsgruppe](#sql-server-alwayson-availability-group)

3.  [Konfigurieren von MDS zur Ausführung auf einem WSFC-Knoten](#configure-mds-to-run-on-an-wsfc-node)

In den oben aufgeführten Abschnitten werden die Technologien kurz vorgestellt und Anweisungen folgen. Ausführliche Informationen zu den Technologien finden Sie in den Dokumenten, die mit jedem Abschnitt verknüpft sind.

Die in diesem Artikel beschriebene Lösung basiert auf der SQL Server Always On-Verfügbarkeitsgruppe, in der jede Datenbank über mehrere synchrone oder asynchrone Replikate verfügt. Nur ein Replikat akzeptiert die Transaktion (akzeptiert Benutzeranfragen). Dies ist das primäre Replikat.

Jedes Replikat hat seinen eigenen Speicher, deshalb gibt es keinen zentralen freigegebenen Speicher in dieser Lösung. Wenn ein Software- oder Hardwarefehler Auswirkungen auf das primäre Replikat hat, kann auf Grundlage der Konfiguration oder der gegebenen Situation entweder automatisch oder manuell ein Failover für das primäre Replikat auf ein synchrones oder asynchrones Replikat ausgeführt werden. Dadurch kann die Hochverfügbarkeit der Datenbank mit nur minimaler Unterbrechung für den Benutzer sichergestellt werden.

Asynchrone Replikate werden in der Regel in einem Rechenzentrum gehostet, das sich im Bezug auf das Rechenzentrum des primären Replikats an einem Remotestandort befindet. Im Falle von Notfallszenarios kann auf das primäre Replikat ein Failover auf ein anderes Rechenzentrum ausgeführt werden. So wird die Notfallwiederherstellung der Datenbank sichergestellt.

Zu Demonstrationszwecken verwendet die in diesem Artikel beschriebene Lösung die folgenden Versionen der Software. Ältere Versionen sollten genauso funktionieren und nur minimale Unterschiede aufweisen.

-   Windows Server 2012R2 mit Server-Failovercluster

-   SQL Server 2016 mit Master Data Services-Funktion

Die Lösung verwendet außerdem zwei VMs, **MDS-HA1** und **MDS-HA2**, um zwei Replikate zu hosten. Solange sie von der SQL Server Always On-Verfügbarkeitsgruppe unterstützt wird, beschränkt MDS nicht, wie viele Replikate Sie verwenden können.

In diesem Artikel wird davon ausgegangen, dass Sie über grundlegende Kenntnisse über Windows Server, Windows Server-Failovercluster, SQL Server Always On und SQL Server MDS verfügen.

## <a name="what-is-not-covered"></a>Was nicht behandelt wird

Dieses Dokument deckt folgende Themen nicht ab:

-   Wie Sie IIS und den Webserver zum Hosten der Master Data Service-Benutzeroberfläche nach einem Notfall hoch verfügbar und wiederherstellbar machen. MDS legt keine bestimmten Anforderungen an IIS fest, deshalb können die Standardtechniken, IIS hoch verfügbar und geeignet für den Lastenausgleich zu machen, hier auch funktionieren.

-   Wie Sie den SQL Server Always On-Failovercluster (FCI) verwenden können, um Hochverfügbarkeit auf dem MDS-Back-End zu unterstützen. SQL Server-Failoverclustering ist eine andere Lösung für hohe Verfügbarkeit, wird von SQL Server offiziell unterstützt und funktioniert mit MDS.

-   Wie Sie eine Hybridlösung des SQL Server-Failoverclusters und der Always On-Verfügbarkeitsgruppe verwenden, um Hochverfügbarkeit auf dem MDS-Back-End zu unterstützen. Die Hybridlösung funktioniert mit MDS.

## <a name="design-consideration"></a>Entwurfsaspekt

Abbildung 1 zeigt eine typische Konfiguration, die vorwiegend in der Always On-Verfügbarkeitsgruppe verwendet wird. Im primären Rechenzentrum gibt es zwei Replikate mit einer synchronen Commit-Beziehung, und beide Replikate besitzen die Berechtigung zum Abstimmen (VOTE). Diese Methode wird meistens zur Verbesserung der Hochverfügbarkeit verwendet, falls das primäre Replikat fehlschlägt.

Im Rechenzentrum für die Notfallwiederherstellung gibt es ein sekundäres Replikat mit einer asynchronen Commit-Beziehung zum primären Replikat. Dieses Rechenzentrum befindet sich in der Regel in einem anderen geografischen Raum als das erste Rechenzentrum. Das sekundäre Replikat besitzt nicht die Berechtigung zum Abstimmen (VOTE).

Diese Konfiguration wird verwendet, um die Wiederherstellung zu erzielen, für den Fall, dass sich das primäre Rechenzentrum in einem Notfall befindet, z.B. ein Brand, Erdbeben usw. Die Konfiguration kann mit relativ niedrigen Kosten hohe Verfügbarkeit und Notfallwiederherstellung erzielen.

![Typische Konfiguration für eine Always On-Verfügarkeitsgruppe](media/Fig1_TypicalConfig.png)

Abbildung 1. Eine typische Always On-Verfügbarkeitsgruppenkonfiguration

Wenn Sie die Notfallwiederherstellung nicht in Erwägung ziehen müssen, benötigen Sie kein Replikat in einem sekundären Rechenzentrum. Wenn Sie die Hochverfügbarkeit verbessern müssen, können Sie mehrere synchrone Replikate im selben primären Rechenzentrum besitzen.

Daher ist es wichtig, dass Sie Ihre Szenarios und Anforderungen im Hinterkopf behalten und wählen, wie viele asynchrone und synchrone Replikate Sie benötigen und in welches Rechenzentrum Sie diese einfügen müssen.

## <a name="windows-server-failover-cluster-wsfc"></a>Windows Server-Failovercluster (WSFC)

In diesem Abschnitt werden die folgenden Aufgaben behandelt.

1.  [Installieren der Windows-Failoverclusterfunktion](#install-failover-cluster-feature)

2.  [Erstellen eines Windows Server-Failoverclusters](#create-a-windows-server-failover-cluster)

Wie in Abbildung 1 im vorherigen Abschnitt gezeigt, enthält die in diesem Artikel beschriebene Projektmappe den Windows Server-Failovercluster (WSFC). Wir müssen das WSFC einrichten, da SQL Always On immer auf WFSC für die Fehlererkennung und das Failover baut.

WSFC ist ein Feature, das die Hochverfügbarkeit von Anwendungen und Diensten verbessert. Es besteht aus einer Gruppe unabhängiger Windows Server-Instanzen, auf denen der Microsoft-Failoverclusterdienst ausgeführt wird. Die Windows Server-Instanzen (oder Knoten, wie sie manchmal genannt werden) sind miteinander verbunden, sodass sie kommunizieren können und so die Fehlererkennung möglich machen. Der WSFC stellt die Fehlererkennung und Failoverfunktionen bereit. Wenn ein Knoten oder Dienst im Cluster einen Fehler ausgibt, wird der Fehler erkannt, und ein anderer Knoten stellt automatisch oder manuell die auf dem fehlgeschlagenen Knoten gehosteten Dienste bereit. So erfahren Benutzer nur eine minimale Unterbrechung des Diensts, und die Verfügbarkeit des Diensts wird verbessert.  

### <a name="prerequisites"></a>Erforderliche Komponenten

Das Windows Server-Betriebssystem wird auf allen Instanzen installiert, und alle Updates werden gepatcht.

>[!NOTE] 
>Es wird **unbedingt empfohlen**, die gleiche Windows-Version und den gleichen Satz von Funktionen auf allen Instanzen zu installieren, damit potenzielle Probleme mit Inkompatibilität vermieden werden können.

### <a name="install-failover-cluster-feature"></a>Installieren der Windows-Failoverclusterfunktion

Schließen Sie die folgenden Schritte für jede Windows Server-Instanz ab, um die WSFC-Funktion auf jeder Instanz zu installieren. Sie benötigen Administratorberechtigungen.

1.  Öffnen Sie in Windows Server die Option **Server-Manager**, und klicken Sie im rechten Bereich auf **Rollen und Features hinzufügen**. Hierdurch wir der **Assistent zum Hinzufügen von Rollen und Features** gestartet.

2.  Klicken Sie auf **Weiter**, bis Sie auf die Seite **Features** gelangen.

3.  Aktivieren Sie das Kontrollkästchen **Failoverclustering**, und klicken Sie auf **Weiter**, um die Installation abzuschließen. Weitere Informationen in Abbildung 2.

    Wenn Sie zur Bestätigung zum **Hinzufügen von Features, die für das Failoverclustering erforderlich sind**, aufgefordert werden, klicken Sie auf **Features hinzufügen**. Weitere Informationen in Abbildung 3.

    ![Assistent zum Hinzufügen von Rollen und Features, Failoverclustering](media/Fig2_SelectFeatures.png)

    Abbildung 2

    ![Assistent zum Hinzufügen von Rollen und Features, benötigt für das Failoverclustering](media/Fig3_RequiredFeaturesFailover.png)

    Abbildung 3

4.  Klicken Sie auf der Seite **Bestätigung** auf **Installieren**, um das Feature für das Failoverclustering zu installieren.

5.  Stellen Sie auf der Seite **Ergebnis** sicher, dass alles erfolgreich ohne Fehler und Warnungen installiert wurde.

### <a name="create-a-windows-server-failover-cluster"></a>Erstellen eines Windows Server-Failoverclusters

Sobald das WSFC-Feature auf allen Instanzen installiert ist, können Sie den WSFC konfigurieren. Dies müsste nur auf einem Knoten vorgenommen werden.

1.  Öffnen Sie **Server-Manager** in Windows Server, und klicken Sie im Menü **Tool** auf **Failovercluster-Manager** in der rechten oberen Ecke, um den Manager zu starten.

2.  Klicken Sie im **Failovercluster-Manager** im rechten Bereich auf **Konfiguration überprüfen**. Weitere Informationen in Abbildung 4.

    ![Failovercluster-Manager, Konfiguration überprüfen](media/Fig4_ValidateConfig.png)

    Abbildung 4

3.  Klicken Sie im **Assistent** zum **Überprüfen einer Konfiguration** auf **Weiter**.

4.  Fügen Sie im Dialogfeld **Server oder Cluster auswählen** die Servernamen ein, die SQL Server hosten werden, und klicken Sie anschließend auf **Weiter**. Weitere Informationen in Abbildung 5.

    In diesem Beispiel haben wir zwei Instanzen, MDS-HA1 und MDS-HA2, hinzugefügt.

    ![Assistent zum Überprüfen einer Konfiguration, Seite zum Auswählen eines Servers oder Clusters](media/Fig5_AddServer.png)

    Abbildung 5

5.  Klicken Sie auf der Seite **Testoptionen** auf **Alle Tests ausführen** und anschließend auf **Weiter**.

6.  Klicken Sie auf **Weiter**, um die Überprüfung abzuschließen.

    Auf der Seite **Überprüfung** ist der Status dargestellt, und die Seite **Zusammenfassung** zeigt Ihnen die Zusammenfassung der Überprüfung. Informationen dazu finden Sie in Abbildung 6 und 7.

7.  Überprüfen Sie die Seite **Zusammenfassung** auf Warnungen oder Fehlermeldungen.

    Fehler müssen behoben werden. Warnungen stellen möglicherweise jedoch kein Problem dar. Eine Warnmeldung bedeutet nur, dass „das geprüfte Element womöglich den Anforderungen entspricht, jedoch gibt es etwas, das Sie überprüfen sollten“. Abbildung 7 zeigt beispielsweise die Warnung „Wartezeit beim Datenträgerzugriff überprüfen“, die aufgrund dessen angezeigt werden könnte, dass der Datenträger derzeit auf andere Aufgaben fokussiert ist. Diese Warnung können Sie ignorieren. Suchen Sie im Onlinedokument für jede Warnung oder Fehlermeldung nach weiteren Informationen. Weitere Informationen in Abbildung 7.
 
    ![Assistent zum Überprüfen der Konfiguration, Seite „Überprüfung“](media/Fig6_ValidationTests.png)

    Abbildung 6

    ![Assistent zum Überprüfen der Konfiguration, Seite „Zusammenfassung“](media/Fig7_ValidationSummary.png)

    Abbildung 7

8.  Bestätigen Sie auf der Seite **Zusammenfassung**, dass das Kontrollkästchen **Cluster jetzt unter Verwendung der überprüften Knoten erstellen...** aktiviert ist, und klicken Sie dann auf **Beenden**, um den **Assistenten** „**Cluster erstellen**“ zu starten.

9.  Klicken Sie im **Cluster erstellen**-**Assistent** auf **Weiter**.

10. Geben Sie auf der Seite **Zugriffspunkt für die Clusterverwaltung** den Namen des WSFC-Clusters ein, und klicken Sie auf **Weiter**. In diesem Beispiel verwenden wir „MDS-HA“ als Namen des Clusters. Weitere Informationen in Abbildung 8.

    ![Eingeben des Clusternamens](media/Fig8_EnterClusterName.png)

    Abbildung 8

11. Klicken Sie so lange auf **Weiter**, bis die Erstellung des Clusters abgeschlossen ist. Der Abschnitt **Summary of Cluster MDS-HA** (Zusammenfassung des Clusters MDS-HA) zeigt die Clusterinformationen an. Weitere Informationen in Abbildung 9.

    ![Anzeigen von Zusammenfassungsinformationen für den Cluster](media/Fig9_ClusterSummary.png)

    Abbildung 9

    Wenn Sie später einen Knoten hinzufügen möchten, klicken Sie auf die Aktion **Knoten hinzufügen** im rechten Bereich im **Failovercluster-Manager**.

Hinweise:

-   Das WSFC-Feature ist womöglich nicht in allen Editionen von Windows Server verfügbar. Stellen Sie sicher, dass Ihre Edition über diese Funktion verfügt.

-   Stellen Sie sicher, dass Sie über die erforderlichen Berechtigungen zum Einrichten von WSFC in Active Directory verfügen. Sehen Sie sich bei Problemen die Seite [Failover Cluster Step-by-Step Guide: Configure Accounts in Active Directory (Ausführliche Anleitung für den Failovercluster: Konfigurieren von Konten in Active Directory)](https://technet.microsoft.com/library/cc731002(v=ws.10).aspx) an.

Ausführlichere Informationen zum WSFC finden Sie unter [Failover Clusters (Failovercluster)](https://technet.microsoft.com/library/cc732488(v=ws.10).aspx).

## <a name="sql-server-alwayson-availability-group"></a>SQL Server AlwaysOn-Verfügbarkeitsgruppe

In diesem Abschnitt werden die folgenden Aufgaben behandelt.

1.  [Aktivieren der SQL Server Always On-Verfügbarkeitsgruppe](#enable-sql-server-alwayson-availability-group-on-every-sql-server-instance)

2.  [Erstellen einer Verfügbarkeitsgruppe](#create-an-availability-group)

3.  [Überprüfen und Testen der Verfügbarkeitsgruppe](#validation-and-test-the-availability-group)

SQL Server Always On-Lösungen bieten hohe Verfügbarkeit und Wiederherstellung im Notfall für SQL Server-Datenbanken. Always On bietet zwei mögliche Lösungen.
Beide basieren auf WSFC.

-   Always On-Verfügbarkeitsgruppen (Availability Groups, AG)

-   Always On-Failoverclusterinstanzen (Failover Cluster Instances, FCI)

Verfügbarkeitsgruppen verbessern die hohe Verfügbarkeit auf Datenbankebene. Die Verfügbarkeitsgruppe (ein Satz von Benutzerdatenbanken) und deren virtueller Netzwerkname sind als Ressourcen im WSFC registriert.

Failoverclusterinstanzen verbessern die Hochverfügbarkeit auf Instanzebene. Der SQL Server-Dienst sowie die damit verbundenen Dienste sind als Ressourcen im WSFC registriert. Die Failoverclusterinstanz-Lösung erfordert zudem symmetrischen freigegebenen Festplattenspeicher, z.B. SAN- oder SMB-Dateifreigaben, die für alle Knoten im WFC-Cluster verfügbar sein müssen.


### <a name="prerequisites"></a>Erforderliche Komponenten

-   Installieren Sie SQL Server auf allen Knoten. Weitere Informationen finden Sie unter [Installieren von SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server).

-   (Empfohlen) Installieren Sie genau denselben Satz von SQL Server-Funktionen und die gleiche Version auf jedem Knoten. Insbesondere muss MDS installiert sein.

-   (Empfohlen) Verwenden Sie die gleiche Konfiguration auf jeder SQL Server-Instanz. Insbesondere muss die gleiche Serversortierung für alle SQL Server-Instanzen konfiguriert werden.

-   (Empfohlen) Verwenden Sie dasselbe Dienstkonto, um jede SQL Server-Instanz auszuführen. Andernfalls müssen Sie jeder SQL Server-Instanz Berechtigungen gewähren, um sicherzustellen, dass SQL Server-Instanzen miteinander kommunizieren können.

-   Vergewissern Sie sich, dass die Windows-Firewalleinstellung zulässt, dass SQL Server-Instanzen miteinander kommunizieren können.

### <a name="enable-sql-server-alwayson-availability-group-on-every-sql-server-instance"></a>Aktivieren einer SQL Server Always On-Verfügbarkeitsgruppe auf jeder SQL Server-Instanz

1.  Klicken Sie im **SQL Server-Konfigurations-Manager** auf **SQL Server-Dienst** im linken Bereich, klicken Sie anschließend mit der rechten Maustaste auf **SQL Server** im rechten Bereich und dann auf **Eigenschaften**. Weitere Informationen in Abbildung 10.

    ![Fenster der Eigenschaften von SQL Server](media/Fig10_SQLServerProperties.png)

    Abbildung 10

2.  Klicken Sie im Fenster **Eigenschaften** von **SQL Server (MSSQLSERVER)** auf die Registerkarte **Hohe Verfügbarkeit mit Always On**, und aktivieren Sie dann das Kontrollkästchen **Always On-Verfügbarkeitsgruppen aktivieren**. Wenn ein Wert im Textfeld **Name des Windows-Failoverclusters** angezeigt wird, klicken Sie auf **OK**, um fortzufahren. Weitere Informationen in Abbildung 11.

    ![Option „Always On-Verfügbarkeitsgruppen aktivieren“](media/Fig11_EnableAlwaysOn.png)

    Abbildung 11

3.  Wenn eine Seite „Warnungen“ angezeigt wird, klicken Sie auf **OK**, um den Vorgang fortzusetzen. Weitere Informationen in Abbildung 12.

    ![Zum Anhalten und Neustart des Diensts bestätigen](media/Fig12_WarningServiceStopStart.png)

    Abbildung 12

4.  Klicken Sie auf **Neustart**, um den **SQL Server**-Dienst neu zu starten und diese Änderung wirksam zu machen. Weitere Informationen in Abbildung 10.

>[!NOTE] 
>Sie können das Dienstkonto, das den SQL Server-Dienst ausführt, mithilfe des **SQL Server-Konfigurations-Managers** ändern. Klicken Sie auf der Registerkarte **Anmelden** auf das Dialogfeld **SQL Server (MSSQLSERVER)** **Eigenschaften**. Weitere Informationen in Abbildung 11.

### <a name="create-an-availability-group"></a>Erstellen einer Verfügbarkeitsgruppe

Nachdem die Always On-Funktion für alle SQL Server-Instanzen aktiviert wurde, erstellen Sie eine neue Verfügbarkeitsgruppe, die die MDS-Datenbank auf einem Knoten enthält.

Die Verfügbarkeitsgruppe kann nur auf vorhandenen Datenbanken erstellt werden. Sie erstellen also entweder eine MDS-Datenbank auf dem Knoten oder erstellen alternativ eine temporäre Datenbank und löschen die temporäre Datenbank anschließend. In diesem Beispiel erstellen wir eine leere MDS-Datenbank und eine Verfügbarkeitsgruppe auf dieser Datenbank.

1.  Starten Sie **SQL Server Management Studio** (**SSMS**) auf einem Knoten,und stellen Sie eine Verbindung mit der lokalen SQL Server-Instanz mit entsprechenden Anmeldeinformationen her.

2.  Öffnen Sie in SSMS ein Fenster **Neue Abfrage**, und führen Sie das folgende Skript aus, um eine leere Datenbank zu erstellen. Ersetzen Sie C:\\temp mit dem Speicherort, den Sie zur Ausführung einer vollständigen Sicherung verwenden möchten.

    ```
    CREATE DATABASE MDS\_Sample
    GO
    BACKUP DATABASE MDS\_Sample TO DISK='C:\\temp'
    GO
    ```

    >[!NOTE] 
    >Eine vollständige Sicherung ist zum Erstellen der Verfügbarkeitsgruppe auf diese Datenbank erforderlich.

3.  Erweitern Sie im **Objekt-Explorer** den Ordner **Hohe Verfügbarkeit mit Always On**, und klicken Sie auf **Assistent für neue Verfügbarkeitsgruppen**, um den **Assistent für neue Verfügbarkeitsgruppen** zu starten. Weitere Informationen in Abbildung 13.

    ![Assistent zum Starten neuer Verfügbarkeitsgruppen](media/Fig13_AvailabilityGroupsFolder.png)

    Abbildung 13

4.  Klicken Sie im Assistent **Neue Verfügbarkeitsgruppe** auf **Weiter**, um die Seite **Namen angeben** anzuzeigen. Geben Sie einen Namen für die Verfügbarkeitsgruppe ein, und klicken Sie dann auf **Weiter**. Weitere Informationen in Abbildung 14.

    ![Eingeben des Namens der Verfügbarkeitsgruppe](media/Fig14_AvailabilityGroupName.png)

    Abbildung 14

5.  Klicken Sie auf die Datenbank, die Sie gerade auf der Seite **Datenbank auswählen** erstellt haben, und klicken Sie dann auf **Weiter**. Weitere Informationen in Abbildung 15.

    ![Datenbank auswählen](media/Fig15_AvailabilityGroupSelectDatabase.png)

    Abbildung 15

6.  Fügen Sie auf der Seite **Replikate angeben** ein weiteres Replikat hinzu, indem Sie auf **Replikat hinzufügen** klicken. Diese Seite enthält bereits die aktuellen lokalen SQL Server-Instanzen als Replikat. Weitere Informationen in Abbildung 16.

7.  Geben Sie im Dialogfeld **Mit Server verbinden** die entsprechenden Anmeldeinformationen ein, und klicken Sie dann auf **Verbinden**.

    ![Eine Verbindung mit einer SQL Server-Instanz herstellen](media/Fig16_AddReplicaConnectServer.png)

    Abbildung 16

    Nun sollten zwei Replikate in der Liste angezeigt werden. Wiederholen Sie diesen Schritt, um die anderen Knoten als Replikate hinzuzufügen. Weitere Informationen in Abbildung 17.

    ![Liste der Replikate anzeigen](media/Fig17_AvailabilityGroupSQLReplicas.png)

    Abbildung 17

    Konfigurieren Sie für jedes Replikat die folgenden Einstellungen für **Synchroner Commit**, **Automatisches Failover** und **Lesbares sekundäres Replikat**. Weitere Informationen in der Abbildung
17.

    **Synchroner Commit**: Dadurch wird sichergestellt, dass wenn für eine Transaktion auf dem primären Replikat der Datenbank ein Commit ausgeführt wird, ebenfalls ein Commit für die Transaktion auf allen anderen synchronen Replikaten ausgeführt wird. Ein asynchroner Commit kann dies jedoch nicht garantieren und kann hinter dem primären Replikat liegen.

    Sie müssen normalerweise das synchrone Commit nur aktivieren, wenn sich zwei Knoten im selben Rechenzentrum befinden. Wenn sie sich in unterschiedlichen Rechenzentren befinden, kann ein synchroner Commit die Leistung der Datenbank verlangsamen.

    Wenn dieses Kontrollkästchen nicht aktiviert ist, wird ein asynchroner Commit verwendet.

    **Automatisches Failover:** Wenn das primäre Replikat ausgefallen ist, wird für die Verfügbarkeitsgruppe automatisch ein Failover auf das sekundäre Replikat ausgeführt, wenn das automatische Failover ausgewählt ist. Dies kann nur auf den Replikaten mit synchronen Commits aktiviert werden.

    **Lesbares sekundäres Replikat:** Benutzer können standardmäßig keine Verbindung mit sekundären Replikaten herstellen. Dadurch können Benutzer eine Verbindung mit dem sekundären Replikat mit schreibgeschütztem Zugriff herstellen.

8.  Klicken Sie auf der Seite **Replikate angeben** auf die Registerkarte **Listener** und tun Sie Folgendes: Weitere Informationen in Abbildung 18.

    a.  Klicken Sie auf **Verfügbarkeitsgruppenlistener erstellen**, um einen Verfügbarkeitsgruppenlistener für die MDS-Datenbankverbindung einzurichten.

    b.  Geben Sie einen **DNS-Namen des Listeners** ein, z.B. MDSSQLServer.

    c.  Geben Sie den Standard-SQL-Port „1433“ im Textfeld **Port** ein.

    d.  Geben Sie im Textfeld **Netzwerkmodus** „DHCP“ ein, und klicken Sie auf **Weiter**, um den Vorgang fortzusetzen.

    >[!NOTE] 
    >Optional können Sie „Statische IP“ als **Netzwerkmodus** auswählen und als statische IP eingeben. Sie können auch einen anderen Port als 1433 eingeben. 

    ![Konfigurieren des Listeners](media/Fig18_AvailabilityGroupCreateListener.png)

    Abbildung 18

9.  Klicken Sie auf der Seite **Datensynchronisierung auswählen** auf **Vollständig**, und geben Sie eine Netzwerkfreigabe an, auf die jeder Knoten zugreifen kann. Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen. Weitere Informationen in Abbildung 19.

    Diese Netzwerkfreigabe dient zum Speichern der Datenbanksicherung zum Erstellen von sekundären Replikaten. Wenn diese nicht für Ihre Organisation verfügbar ist, wählen Sie eine andere Einstellung für die Datensynchronisierung aus. Beziehen Sie sich auf [SQL Server 2016 Always On-Verfügbarkeitsgruppe](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server) für Informationen zur Verwendung anderer Optionen für die Erstellung sekundärer Replikate. In der Abbildung 17 sind auch andere Optionen aufgeführt.

    ![Konfigurieren der Datensynchronisierung](media/Fig19_AvailabilityGroupDataSync.png)

    Abbildung 19 

10. Stellen Sie auf der Seite **Überprüfung** sicher, dass Überprüfungen erfolgreich übergeben werden, und beheben Sie aufgetretene Fehler. Klicken Sie auf **Weiter** , um den Vorgang fortzusetzen.

11. Überprüfen Sie auf der Seite **Zusammenfassung** alle Konfigurationseinstellungen, und klicken Sie dann auf **Beenden**. Dadurch wird die Verfügbarkeitsgruppe erstellt und konfiguriert.

12. Bestätigen Sie auf der Seite **Ergebnis**, dass alle erforderlichen Schritte ausgeführt wurden.

### <a name="validation-and-test-the-availability-group"></a>Überprüfen und Testen der Verfügbarkeitsgruppe

1.  Öffnen Sie SSMS, und stellen Sie eine Verbindung mit dem DNS-Listenernamen her, die Sie gerade im Abschnitt [Erstellen einer Verfügbarkeitsgruppe](#create-an-availability-group) erstellt haben. In diesem Beispiel ist es MDSSQLServer.

2.  Erweitern Sie im **Objekt-Explorer** den Ordner **Hohe Verfügbarkeit mit Always On**, klicken Sie mit der rechten Maustaste auf die soeben im Abschnitt [Erstellen einer Verfügbarkeitsgruppe](#create-an-availability-group) erstellte Verfügbarkeitsgruppe, und klicken Sie dann auf **Dashboard anzeigen**. Weitere Informationen in Abbildung 20. Der Status der neuen Verfügbarkeitsgruppe und ihrer Replikate wird angezeigt.

    ![Dashboard anzeigen](media/Fig20_ShowDashboard.png)

    Abbildung 20 

3.  Klicken Sie auf **Failover**, um ein Failover auf ein synchrones und ein asynchrones Replikat auszuführen. So können Sie überprüfen, ob ein Failover ohne Probleme ausgeführt werden kann.

 Die Always On-Einrichtung ist abgeschlossen.

Weitere Informationen zur Always On-Verfügbarkeitsgruppe finden Sie unter [Always On-Verfügbarkeitsgruppen (SQL Server)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server).

## <a name="configure-mds-to-run-on-an-wsfc-node"></a>Konfigurieren von MDS zur Ausführung auf einem WSFC-Knoten

Die in diesem Artikel vorgestellte Lösung erfordert nur, dass die Datenbank des MDS-Back-Ends auf dem WSFC ausgeführt wird. Andere Teile von MDS, z.B. Webanwendungen und der MDS-Konfigurations-Manager können entweder auf dem Knoten im WSFC oder außerhalb des WSFC ausgeführt werden, solange MDS eine Verbindung zur Verfügbarkeitsgruppe herstellen kann.

1.  Öffnen Sie den **Master Data Service-Konfigurations-Manager** auf dem Knoten, klicken Sie auf **Datenbankkonfiguration** und anschließend auf **Datenbank erstellen**, um **Datenbank erstellen (Assistent)** zu starten.

2.  Geben Sie auf der Seite **Datenbankserver** den DNS-Namen des Verfügbarkeitsgruppenlisteners in das Textfeld **SQL Server-Instanz** ein, klicken Sie auf **Verbindung testen** und anschließend auf **Weiter**. Weitere Informationen in Abbildung 21.

    ![Konfigurieren des Datenbankservers mit dem Verfügbarkeitslistener](media/Fig21_MDSDatabaseServerListener.png)

    Abbildung 21

3.  Geben Sie auf der **Datenbank**-Seite den Namen der im Abschnitt [Erstellen einer Verfügbarkeitsgruppe](#create-an-availability-group) erstellten Datenbank ein, und klicken Sie anschließend auf **Weiter**. Weitere Informationen in Abbildung 22.

    ![Erstellen und Konfigurieren der Datenbank](media/Fig22_MDSCreateDatabase.png)

    Abbildung 22

4.  Schließen Sie den **Assistenten** **Datenbank erstellen** ab. Weitere Informationen finden Sie unter [Master Data Services – Installation und Konfiguration](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration).

5.  Klicken Sie im **Master Data Service-Konfigurations-Manager** auf **Webanwendungen**, um die Webanwendung zu erstellen. Klicken Sie anschließend auf **Anwenden**, um die Einstellungen für MDS anzuwenden. Weitere Informationen in Abbildung 23. Weitere Informationen finden Sie unter [Master Data Services – Installation und Konfiguration](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration).

    ![Konfigurieren der Webanwendung](media/Fig23_MDSWebApplication.png)

    Abbildung 23

    Die MDS-Einrichtung ist abgeschlossen. Sie können die oben genannten Schritte wiederholen, um MDS für die Ausführung aller Knoten einzurichten. Die Back-End-Datenbank ist in der gleichen Verfügbarkeitsgruppe identisch.

6.  Wenn Sie zuvor eine temporäre Datenbank erstellt haben(siehe Abschnitt [Erstellen einer Verfügbarkeitsgruppe](#create-an-availability-group)), um eine Always On-Verfügbarkeitsgruppe zu erstellen, sollten Sie die temporäre Datenbank löschen.

    Weitere Informationen zu Master Data Services, finden Sie unter [Master Data Services](https://docs.microsoft.com/sql/master-data-services/master-data-services-overview-mds).

## <a name="conclusion"></a>Fazit

In diesem Whitepaper wird erläutert, wie die Master Data Services-Back-End-Datenbank basierend auf der SQL Server Always On-Verfügbarkeitsgruppe konfiguriert wird. Diese Konfiguration bietet hohe Verfügbarkeit und Notfallwiederherstellung für die Master Data Services-Back-End-Datenbank. Um diese Konfiguration zu implementieren, müssen Sie den Windows Server-Failovercluster, die SQL Server Always On-Verfügbarkeitsgruppe und Master Data Services installieren und konfigurieren.

## <a name="feedback"></a>Feedback

War dieses Dokument hilfreich? Senden Sie uns Ihr Feedback, indem Sie auf oben im Artikel auf **Kommentare** klicken. 

Ihr Feedback unterstützt uns bei der Verbesserung der Qualität unserer Whitepaper. 


