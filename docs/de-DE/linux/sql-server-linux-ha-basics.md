---
title: Grundlagen der SQL Server-Verfügbarkeit für Linux-Bereitstellungen | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: a7c2cbcf904b575f84bd461a0b0ab6c7854140d0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>Grundlagen der SQL Server-Verfügbarkeit für Linux-Bereitstellungen

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Beginnend mit [!INCLUDE[sssql17-md](../includes/sssql17-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] wird unter Linux und Windows unterstützt. Wie Sie die Windows-basierten [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Bereitstellungen [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Datenbanken und Instanzen unter Linux hochverfügbar sein müssen. Dieser Artikel behandelt die technischen Aspekte der Planung und Bereitstellung von hoch verfügbaren Linux-basierte [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Datenbanken und Instanzen sowie einige der Unterschiede zu Windows-basierten Installationen. Da [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] möglicherweise für Linux-Experten und Linux möglicherweise neu für neue [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -Experten, die Artikel Zeiten werden Konzepte vorgestellt, die möglicherweise auf einige vertraut sind und nicht an andere Personen vertraut.

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Verfügbarkeitsoptionen für Linux-Bereitstellungen
Neben dem Sichern und Wiederherstellen stehen die gleichen drei Verfügbarkeitsfunktionen unter Linux wie für Windows-basierte Bereitstellungen:
-   Always On-Verfügbarkeitsgruppen (Testreihen)
-   Always On-Failoverclusterinstanzen (FCIs)
-   [Protokollversand](sql-server-linux-use-log-shipping.md)

Bei Windows erfordern FCIs immer einem zugrunde liegenden Windows Server-Failovercluster (WSFC). Abhängig vom Bereitstellungsszenario, eine AG erfordert normalerweise einem zugrunde liegenden WSFC, mit der Ausnahme, wird die neue keine Variante in [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Einem WSFC unter Linux ist nicht vorhanden. Im Abschnitt erläutert wird Clustering Implementierung unter Linux [Schrittmacher für AlwaysOn-Verfügbarkeitsgruppen und Failover-Cluster-Instanzen unter Linux](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux).

## <a name="a-quick-linux-primer"></a>Eine schnelle Linux-Einführung
Während einige Linux-Installationen mit einer Schnittstelle installiert werden können, sind die meisten nicht, was bedeutet, dass nahezu alles auf der Betriebssystemebene über die Befehlszeile ausgeführt wird. Der allgemeine Begriff für diese Befehlszeile in der Linux-Welt ist ein *bash-Shell*.

Unter Linux müssen viele Befehle mit erhöhten Rechten ausgeführt werden, ähnlich wie viele Dinge in Windows Server als Administrator ausgeführt werden müssen. Es gibt zwei Hauptmethoden zum mit erhöhten Rechten ausführen:
1. Im Kontext des entsprechenden Benutzers ausgeführt. Um einem anderen Benutzer zu ändern, verwenden Sie den Befehl `su`. Wenn `su` selbst ausgeführt wird ohne einen Benutzernamen, solange Sie das Kennwort kennen Sie werden in einer Shell als *Root*.
   
2. Die weitere allgemeine und Sicherheit die Möglichkeit zum bewusste auszuführende Aufgaben ist die Verwendung `sudo` vor der Ausführung nichts. In vielen der Beispiele in diesem Artikel verwenden `sudo`.

Einige häufig verwendete Befehle, von denen jedes über verschiedene Schalter und Optionen, die online untersucht werden können:
-   `cd` – Ändern Sie das Verzeichnis
-   `chmod` – Ändern Sie die Berechtigungen von einer Datei oder eines Verzeichnisses
-   `chown` – Ändern des Besitzers einer Datei oder eines Verzeichnisses
-   `ls` – Anzeigen der Inhalte eines Verzeichnisses
-   `mkdir` – Erstellen Sie einen Ordner (Verzeichnis) auf einem Laufwerk
-   `mv` – eine Datei von einem Speicherort zu einem anderen verschieben
-   `ps` – alle Prozesse arbeiten anzeigen
-   `rm` – Löschen Sie eine Datei lokal auf einem Server
-   `rmdir` – Löschen eines Ordners (Verzeichnis)
-   `systemctl` – Starten, beenden oder Aktivieren von Diensten
-   Text-Editor-Befehle. Unter Linux stehen Ihnen verschiedene Text-Editor-Optionen, z. B. vi und Emacs.

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>Allgemeine Aufgaben bei der von Verfügbarkeitskonfigurationen von [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] unter Linux
Dieser Abschnitt enthält Aufgaben, die für alle Linux-basierten gelten [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Bereitstellungen.

### <a name="ensure-that-files-can-be-copied"></a>Stellen Sie sicher, dass die Dateien kopiert werden können
Kopieren von Dateien von einem Server in eine andere ist eine Aufgabe, die alle mit [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] unter Linux sollte ausgeführt werden können. Diese Aufgabe ist sehr wichtig für die AG-Konfigurationen.

Dinge Berechtigungsprobleme können für Linux und Windows-basierten Installationen vorhanden sein. Allerdings vertraut sind, mit der Vorgehensweise beim Kopieren zwischen Servern unter Windows möglicherweise nicht vertraut, wie unter Linux erfolgt. Eine gängige Methode ist die Verwendung des Befehlszeilen-Hilfsprogramms `scp`, dem steht für sichere kopieren. Im Hintergrund `scp` OpenSSH verwendet. SSH steht für secure Shell. Abhängig von der Linux-Distribution OpenSSH selbst möglicherweise nicht installiert werden. Wenn sie nicht der Fall ist, muss OpenSSH zuerst installiert werden. Weitere Informationen zum Konfigurieren von OpenSSH finden Sie die Informationen unter den folgenden Links für jede Verteilung:
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-OpenSSH.html)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

Bei Verwendung `scp`, Sie müssen die Anmeldeinformationen des Servers angeben, wenn es sich nicht um die Quelle oder das Ziel ist. Beispiel für die Verwendung

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

kopiert die Datei MyAGCert.cer zu dem Ordner auf dem anderen Server. Beachten Sie, dass Sie benötigen Berechtigungen – und möglicherweise den Besitz der Datei, also kopieren `chown` müssen möglicherweise auch vor dem Kopieren eingesetzt werden. Auf ähnliche Weise benötigt die richtige Benutzer auf der Empfängerseite wird genauso, Zugriff auf die Datei bearbeiten. Beispielsweise, um diese Zertifikatdatei Wiederherstellen der `mssql` Benutzer muss darauf zugreifen.

Samba, d. h. die Linux-Variante von Server Message Block (SMB), kann auch verwendet werden, zum Erstellen von Freigaben, z. B. von UNC-Pfade zugegriffen `\\SERVERNAME\SHARE`. Weitere Informationen zum Konfigurieren von Samba finden Sie die Informationen unter den folgenden Links für jede Verteilung:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

Windows-basierten SMB-Freigaben können auch verwendet werden. SMB-Freigaben erübrigt sich die Linux-basierte, werden so lange der Clientteil der Samba auf den Linux-Server hostet ordnungsgemäß konfiguriert ist [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] und die Freigabe hat die richtige Zugriffsrechte. Für Entitäten in einer gemischten Umgebung, wäre dies eine Möglichkeit, nutzen vorhandene Infrastrukturen für Linux-basierte [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Bereitstellungen.

Aufpassen, die wichtig ist, dass die Version der bereitgestellten Samba SMB 3.0 kompatibel sein soll. Wenn die Unterstützung von SMB in hinzugefügt wurde [!INCLUDE[sssql11-md](../includes/sssql11-md.md)], es erforderlich, dass alle Freigaben zur Unterstützung von SMB 3.0. Wenn Samba für die Freigabe und nicht Windows Server verwenden, sollte die Freigabe Samba-basierte Samba 4.0 oder höher, und im Idealfall 4.3 oder höher, verwenden die SMB 3.1.1 unterstützt. Ist eine gute Informationsquelle für SMB- und Linux [SMB3 in Samba](http://events.linuxfoundation.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf).

Schließlich ist das Verwenden einer Dateifreigabe im Netzwerk-System (NFS) eine Option aus. Verwenden Sie stattdessen NFS ist keine Option auf Windows-basierten Bereitstellungen von [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], und kann nur für Linux-basierten Bereitstellungen verwendet werden.

### <a name="configure-the-firewall"></a>Konfigurieren der firewall
Ähnlich wie bei Windows, Linux-Distributionen haben eine integrierte Firewall. Wenn Ihr Unternehmen eine externe Firewall auf dem Server verwendet wird, akzeptabel deaktivieren die Firewalls unter Linux. Allerdings unabhängig davon, in dem die Firewall aktiviert ist, müssen die Ports geöffnet werden. Die folgende Tabelle beschreibt die allgemeine Ports für hoch verfügbare [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Bereitstellungen unter Linux.

| Portnummer | Typ     | Description                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS – `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | Samba (sofern verwendet) – Endpunkt-Mapper                                                                                          |
| 137         | UDP      | Samba (sofern verwendet) – NetBIOS-Namensdienst                                                                                      |
| 138         | UDP      | Samba (sofern verwendet) – NetBIOS-Datagramm                                                                                          |
| 139         | TCP      | Samba (sofern verwendet) – NetBIOS-Sitzung                                                                                           |
| 445         | TCP      | Samba (sofern verwendet) – SMB über TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] – Der Standardport; Falls gewünscht, können mit ändern. `mssql-conf set network.tcpport <portnumber>`                       |
| 2049        | TCP, UDP | NFS (sofern verwendet)                                                                                                               |
| 2224        | TCP      | Schrittmacher – verwendet von `pcsd`                                                                                                |
| 3121        | TCP      | Schrittmacher – erforderlich, wenn Schrittmacher entfernten Knoten vorhanden sind                                                                    |
| 3260        | TCP      | iSCSI-Initiator (sofern verwendet) – kann geändert werden, `/etc/iscsi/iscsid.config` (RHEL), aber der Port des iSCSI-Ziels übereinstimmen |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -Der Standardport für einen Endpunkt AG verwendet kann geändert werden, beim Erstellen des Endpunktes                                |
| 5403        | TCP      | Schrittmacher                                                                                                                   |
| 5404        | UDP      | Schrittmacher – Corosync ggf. mithilfe von multicast-UDP                                                                     |
| 5405        | UDP      | Schrittmacher – Corosync erforderlich                                                                                            |
| 21064       | TCP      | Schrittmacher – von Ressourcen mithilfe von DLM erforderlich                                                                                 |
| Variable    | TCP      | AG Endpunktport; Standardmäßig ist 5022                                                                                           |
| Variable    | TCP      | NFS – port für `LOCKD_TCPPORT` (im gefunden `/etc/sysconfig/nfs` auf RHEL)                                              |
| Variable    | UDP      | NFS – port für `LOCKD_UDPPORT` (im gefunden `/etc/sysconfig/nfs` auf RHEL)                                              |
| Variable    | TCP/UDP  | NFS – port für `MOUNTD_PORT` (im gefunden `/etc/sysconfig/nfs` auf RHEL)                                                |
| Variable    | TCP/UDP  | NFS – port für `STATD_PORT` (im gefunden `/etc/sysconfig/nfs` auf RHEL)                                                 |

Zusätzliche Ports, die ggf. von Samba verwendet werden, finden Sie unter [Samba Portverwendung](https://wiki.samba.org/index.php/Samba_Port_Usage).

Im Gegensatz dazu kann der Name des Diensts unter Linux auch als Ausnahme anstelle des Ports hinzugefügt werden; z. B. `high-availability` für Schrittmacher. Finden Sie auf den Verteilungspunkt für die Namen, ist dies die Richtung, die Sie verfolgen möchten. Beispielsweise ist für RHEL Befehls Schrittmacher hinzufügen

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**Dokumentation der Firewall:**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>Installieren Sie [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Pakete für Verfügbarkeit
Auf einem Windows-basierten [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Installation, einige Komponenten sind auch in einer grundlegenden Engine-Installation, andere hingegen nicht installiert. Unter Linux, nur die [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Modul als Teil des Installationsvorgangs installiert ist. Alles ist optional. Für hoch verfügbare [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Instanzen unter Linux, zwei Pakete installiert werden mit [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]: [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent (*Mssql-Server-Agent*) und die hohe Verfügbarkeit (HA) Paket ( *MSSQL-Server-ha*). Während [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -Agent ist technisch optional, es ist [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]der Planer für Aufträge und Protokollversand, erforderlich, damit die Installation empfohlen wird. Auf Windows basierenden Installationen [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -Agent ist nicht optional.

>[!NOTE]
>Für diejenigen, die noch nicht mit [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -Agent ist [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]des integrierten Auftragsplaner. Dies ist eine allgemeine Möglichkeit für Datenbankadministratoren planen, z. B. Sicherungen und andere [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Wartung. Im Gegensatz zu einer Windows-basierten Installation von [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] , in denen [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent ist ein völlig anderen Dienst, unter Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -Agent ausgeführt wird, im Kontext der [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] selbst.

Bei Testreihen oder FCIs einer Windows-basierten Konfiguration konfiguriert werden, sind sie clusterfähige. Clusterinformationen bedeutet, dass [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] bestimmten Ressourcen-DLLs, die einem WSFC ("sqagtres.dll" und sqsrvres.dll für FCIs hadrres.dll für Testreihen) bekannt ist, und werden durch den die WSFC verwendet, um sicherzustellen, dass die [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] gruppierten Funktionen, ausgeführt wird, und ordnungsgemäß funktioniert. Da clustering externen nicht nur zu ist [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] aber Linux selbst, Microsoft, das Äquivalent zu einer Ressourcen-DLL für Linux-basierte AG und FCI-Bereitstellungen zu codieren. Dies ist die *Mssql-Server-ha* Verpacken, auch bekannt als die [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Ressource-Agent für Schrittmacher. So installieren Sie die *Mssql-Server-ha* Verpacken, finden Sie unter [installieren Sie die hohe Verfügbarkeit und SQL Server-Agent-Pakete](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages).

Die optionalen Pakete für [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] unter Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Volltextsuche (*Mssql-Server-Fts*) und [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*Mssql Server ist*), sind nicht für hohe Verfügbarkeit für eine FCI oder einer AG erforderlich.

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Schrittmacher für AlwaysOn-Verfügbarkeitsgruppen und Failoverclusterinstanzen unter Linux
Als vorherige erwähnt, der nur clustering-Mechanismus, die derzeit für Testreihen und Failoverclusterinstanzen (fcis) von Microsoft unterstützt Schrittmacher mit Corosync ist. Dieser Abschnitt enthält die grundlegende Informationen zum Verständnis der Lösung sowie zum Planen und Bereitstellen für [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Konfigurationen.

### <a name="ha-add-onextension-basics"></a>Grundlagen der HA-add-on/Erweiterung
Alle derzeit unterstützten Verteilungen liefern eine hohe Verfügbarkeit add-on/Erweiterung, die auf den Stapel clustering Schrittmacher basiert. Dieser Stapel umfasst zwei Hauptkomponenten: Schrittmacher und Corosync. Alle Komponenten des Stapels sind:
-   Schrittmacher – die Core-Komponente, die Dinge Koordinate für die Clustercomputer wird clustering.
-   Corosync – ein Framework und den Satz von APIs, z. B. Quorum, die Möglichkeit, Fehler beim Neustart Prozesse usw. bereitstellt.
-   LibQB – stellt Aufgaben wie die Protokollierung.
-   Ressource-Agent – bestimmte Funktionen bereitgestellt, damit eine Anwendung Schrittmacher abgestimmt werden kann.
-   Zaun-Agent – Skripts/Funktionen, die bei der Isolierung von Knoten und mit ihnen behandelt werden, wenn sie die Probleme auftreten.
    
> [!NOTE]
> Die Cluster-Stapel wird häufig als Schrittmacher Linux weltweit bezeichnet.

Diese Lösung ist in gewisser Hinsicht ähnelt, aber in vielerlei Hinsicht unterscheiden Clusterkonfigurationen mit Windows bereitstellen. In Windows basiert die Verfügbarkeit-Art des Clusterings, einen Windows Server-Failovercluster (WSFC), aufgerufen in das Betriebssystem und die Funktion, die die Erstellung eines wsfc-Failover-Clusterunterstützung ermöglicht, ist standardmäßig deaktiviert. In Windows Testreihen FCIs baut auf einem WSFC und freigeben enge Integration aufgrund einer bestimmten Ressourcen-DLL, die von bereitgestellten [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Diese eng gekoppelten Lösung ist im großen und möglich, da es von einem Hersteller ist.

![](./media/sql-server-linux-ha-basics/image1.png)

Unter Linux während jede unterstützte Verteilungspunkte Schrittmacher verfügbar ist, hat kann jedes Verteilungspunkts angepasst und verfügen über geringfügig Implementierungen und Versionen. Einige der Unterschiede werden in den Anweisungen in diesem Artikel berücksichtigt. Die clustering-Schicht ist eine open Source, damit, obwohl es in die Distributionen enthalten ist, es nicht auf die gleiche Weise eng ist einem WSFC unter Windows. Daher verändert sich Microsoft bietet *Mssql-Server-ha*, sodass [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] und im Stapel Schrittmacher bieten nahe an, jedoch nicht genau die gleiche, Erfahrung für Testreihen und Failoverclusterinstanzen (fcis) unter Windows.

Eine vollständige Dokumentation Schrittmacher darunter eine nähere Erläuterung, was das alles mit vollständigen Verweisinformationen, für RHEL und SLES ist:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Eine Anleitung für die Verfügbarkeit keinen Ubuntu.

Weitere Informationen zu den gesamten Stapel, auch finden Sie unter den offiziellen [Schrittmacher Dokumentationsseite](http://clusterlabs.org/doc/) auf der Website Clusterlabs.

### <a name="pacemaker-concepts-and-terminology"></a>Schrittmacher Konzepte und Terminologie
In diesem Abschnitt dokumentiert die allgemeinen Konzepte und Terminologie für eine Schrittmacher-Implementierung.

#### <a name="node"></a>Node
Ein Knoten ist ein Teil des Clusters. Ein Cluster Schrittmacher unterstützt bis zu 16 Knoten. Diese Zahl kann überschritten werden, wenn Corosync wird nicht auf zusätzlichen Knoten ausgeführt, aber Corosync erforderlich, damit ist [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Aus diesem Grund die maximale Anzahl von Knoten, die über einen Cluster kann für eine beliebige [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-Basis Konfiguration ist 16; Dies ist der Grenzwert Schrittmacher und hat nichts mit maximale Einschränkungen für Testreihen oder FCIs benennungsbeschränkungen [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. 

#### <a name="resource"></a>Ressource
Einem WSFC und einem Cluster Schrittmacher haben das Konzept einer Ressource. Eine Ressource ist, bestimmte Funktionen, die im Kontext des Clusters, z. B. ein Datenträger oder eine IP-Adresse ausgeführt wird. Beispielsweise unter Schrittmacher können FCI und AG-Ressourcen erstellt. Dies ist kein Punkt von was in einem WSFC erfolgt, in dem Sie sehen eine [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] für eine FCI oder eine Ressource AG beim Konfigurieren einer Verfügbarkeitsgruppe, wird jedoch nicht genau die gleiche aufgrund der zugrunde liegenden Unterschiede bei der Art [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Schrittmacher integriert.

Schrittmacher hat Standard und Clone-Ressourcen. Klon-Ressourcen sind Argumente, die auf allen Knoten gleichzeitig ausgeführt werden. Ein Beispiel wäre eine IP-Adresse, die auf mehreren Knoten für den Lastenausgleich Zwecke ausgeführt wird. Alle Ressourcen, die für Failoverclusterinstanzen (fcis) erstellt wird verwendet eine standard-Ressource, da nur ein Knoten zu einem beliebigen Zeitpunkt eine FCI gehostet werden kann.

Wenn eine Verfügbarkeitsgruppe erstellt wird, erfordert sie eine spezielle Form einer Klon-Ressource eine Ressource mit mehreren Zustand aufgerufen. Während eine Verfügbarkeitsgruppe nur ein primäres Replikat verfügt, wird die AG selbst in allen Knoten ausgeführt, die sie für die Zusammenarbeit auf konfiguriert ist und potenziell möglich, z. B. nur-Lese-Zugriff. Da dies eine "live" Verwendung des Knotens ist, wird durch die Ressourcen verfügen, das Konzept von zwei Status: Master "und" Slave. Weitere Informationen finden Sie unter [Ressourcen mit mehreren Zuständen: Ressourcen, die mehrere Modi haben](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html).

#### <a name="resource-groupssets"></a>Gruppen/Ressourcensätze
Ähnlich wie Rollen in einem WSFC, verfügt über ein Cluster Schrittmacher das Konzept einer Ressourcengruppe. Eine Ressourcengruppe (eine Gruppe im SLES bezeichnet) handelt es sich um eine Auflistung von Ressourcen, die zusammen funktionieren und ein Failover von einem Knoten zu einem anderen als einzelne Einheit. Ressourcengruppen können keine Ressourcen enthalten, die als Master/Slave konfiguriert sind; Daher können sie für Testreihen verwendet werden. Während eine Ressourcengruppe für Failoverclusterinstanzen (fcis) verwendet werden kann, ist es nicht in der Regel eine empfohlene Konfiguration.

#### <a name="constraints"></a>Einschränkungen
WSFCs haben verschiedene Parameter für die Ressourcen sowie z. B. Abhängigkeiten, die mit den WSFC der über-/unterordnungsbeziehung zwischen zwei verschiedene Ressourcen zu erkennen. Eine Abhängigkeit ist nur eine Regel, die dem WSFC mitteilen, welche Ressource muss zuerst online sein.

Ein Cluster Schrittmacher verfügt nicht über das Konzept der Abhängigkeiten, aber es gibt Einschränkungen. Es gibt drei Arten von Einschränkungen: Zusammenstellung, den Speicherort und Reihenfolge.
-   Eine Zusammenstellung Einschränkung erzwingt, und zwar unabhängig davon, ob zwei Ressourcen auf demselben Knoten ausgeführt werden sollte.
-   Eine standorteinschränkung wird die Schrittmacher-Cluster, in dem eine Ressource ausgeführt werden kann (oder nicht).
-   Eine Sortierung Einschränkung wird der Schrittmacher-Cluster die Reihenfolge, in der die Ressourcen gestartet werden soll.

> [!NOTE]
> Zusammenstellung Einschränkungen sind nicht für Ressourcen in einer Ressourcengruppe erforderlich, da all diese als einzelne Einheit gelten.

#### <a name="quorum-fence-agents-and-stonith"></a>Quorum Fence Agents und STONITH
Quorum unter Schrittmacher ähnelt einem WSFC Konzept. Der gesamte Mechanismus für einen Cluster-Quorum dient, stellen Sie sicher, dass der Cluster aktiv bleibt. Wsfc- und die HA-Add-Ons für die Linux-Distributionen haben das Konzept der abstimmen, wobei Aktivierungsdiensten wird für jeden Knoten Quorum. Soll eine Mehrheit der stimmen gestartet wurde, andernfalls im schlimmsten Fall, wird der Cluster heruntergefahren werden.

Im Gegensatz zu einem WSFC gibt es keine Zeugenressource mit Quorum arbeiten. Wie einem WSFC besteht das Ziel darin, behalten Sie die Anzahl der Wähler ungerade. Quorumkonfiguration verfügt über verschiedene Überlegungen zum Testreihen als FCIs.

WSFCs Überwachen des Status von beteiligten Knoten und behandelt werden, wenn ein Problem auftritt. Spätere Versionen von WSFCs bieten Funktionen wie gesäubert einen Knoten, der fehlerhafte oder nicht verfügbar ist (Knoten befindet sich nicht auf, die Netzwerkkommunikation ist unten usw.). Auf der Seite Linux wird diese Art von Funktion von einem Fence-Agent bereitgestellt. Das Konzept wird manchmal als Fencing bezeichnet. Diese Agents Fence im Allgemeinen gelten für die Bereitstellung und häufig vom Hardwarehersteller und einige Softwarehersteller, z. B. solche, die Hypervisoren anbieten bereitgestellt. VMware enthält beispielsweise einen Fence-Agent, der für virtuelle Linux-Computer mithilfe von vSphere virtualisiert verwendet werden kann.

Quorum und Zauns Ties in ein anderes Konzept STONITH aufgerufen oder der andere Knoten im Kopf gehen. STONITH ist erforderlich, um einen unterstützten Schrittmacher Cluster für alle Linux-Distributionen haben. Weitere Informationen finden Sie unter [in einem Red Hat hohe Verfügbarkeit Cluster Zauns](https://access.redhat.com/solutions/15575) (RHEL).

#### <a name="corosyncconf"></a>corosync.conf
Die `corosync.conf` Datei enthält die Konfiguration des Clusters. Befindet sich im `/etc/corosync`. Im Verlauf der normalen alltäglichen müssen diese Datei nie in bearbeitet werden, wenn der Cluster ordnungsgemäß eingerichtet ist.

#### <a name="cluster-log-location"></a>Protokollspeicherort der Cluster
Protokollspeicherorte für Schrittmacher Cluster unterscheiden sich abhängig von der Verteilung.
-   RHEL "und" SLES- `/var/log/cluster/corosync.log`
-   Ubuntu: `/var/log/corosync/corosync.log`

Um den Standardspeicherort für die Protokollierung zu ändern, ändern `corosync.conf`.

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Planen der Schrittmacher-Cluster [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Dieser Abschnitt beschreibt die Planung wichtigen Punkte bei einem Cluster mit Schrittmacher.

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Virtualisierung von Linux-basierten Schrittmacher Cluster für [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Verwenden von virtuellen Computern zum Bereitstellen von Linux-basierten [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Bereitstellungen für Testreihen und Failoverclusterinstanzen (fcis) wird über die gleichen Regeln wie für den jeweiligen Entsprechungen der Windows-basierten behandelt. Es gibt ein grundlegender Satz von Regeln für unterstützbarkeit von virtualisierten [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Bereitstellungen von Microsoft bereitgestellten [Microsoft Support-KB-956893](https://support.microsoft.com/en-us/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment). Andere Hypervisoren z. B. Microsoft Hyper-V und VMware ESXi möglicherweise unterschiedliche Varianzen oben auf dieser, aufgrund von Unterschieden in den Plattformen selbst.

Bei Testreihen und FCIs unter Virtualisierung betrifft, stellen Sie sicher, dass für die Knoten eines bestimmten Clusters Schrittmacher antiaffinität festgelegt ist. Wenn für eine hohe Verfügbarkeit in einer Verfügbarkeitsgruppe oder einer FCI-Konfiguration, die virtuellen Computer hostet konfiguriert [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] sollte nie auf demselben hypervisorhost ausgeführt werden. Z. B. wenn eine FCI zwei Knoten bereitgestellt wird, gibt es müssten werden *mindestens* drei Hypervisor-Hosts, die an einer beliebigen Stelle für eine der virtuellen Computer hostet einen Knoten im Fall eines Fehlers Host wechseln besteht vor allem, wenn Sie Funktionen verwenden, wie z. B. Live Migration oder "vMotion".

Weitere Einzelheiten finden Sie in:
-   Hyper-V-Dokumentation – [Verwenden von Gastclustering für hohe Verfügbarkeit](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   Whitepaper (geschrieben für Windows-basierte Bereitstellungen, aber die meisten Konzepte, die noch anwenden) – [Planung mit hoher Verfügbarkeit, unternehmenswichtige kritische SQL Server-Bereitstellungen mit VMware vSphere](http://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)

>[!NOTE]
>RHEL mit einem Cluster Schrittmacher mit STONITH wird von Hyper-V noch nicht unterstützt. Bis die unterstützt wird, Weitere Informationen und Updates, wenden Sie sich an [Richtlinien zur Unterstützung für RHEL Cluster für hohe Verfügbarkeit](https://access.redhat.com/articles/29440#3physical_host_mixing).

### <a name="networking"></a>Netzwerk
Im Gegensatz zu einem WSFC erfordert Schrittmacher keinen dedizierten Namen oder mindestens eine dedizierte IP-Adresse für den Schrittmacher Cluster selbst. Testreihen und FCIs IP-Adressen (siehe die Dokumentation für jede weitere Informationen) benötigen, aber nicht Namen, da es ist keine Netzwerk-Namensressource. SLES lässt die Konfiguration einer IP-Adresse für Verwaltungszwecke, aber es ist nicht erforderlich, wie in der dargestellt werden können [Erstellen des Clusters Schrittmacher](sql-server-linux-deploy-pacemaker-cluster.md#create).

Wie einem WSFC Schrittmacher verwenden möchten redundante Networking, d. h. unterschiedlichen Netzwerkkarten (NICs oder pNICs für physischen) müssen einzelne IP-Adressen. Im Hinblick auf die Clusterkonfiguration müsste jede IP-Adresse was als eigene Ring bekannt ist. Allerdings mit WSFCs heute verschiedensten Implementierungen virtualisiert werden oder in der öffentlichen Cloud, in dem es wirklich ist virtualisiert nur einer einzelnes NIC (vNIC) an den Server angezeigt. Wenn alle pNICs und eine mit dem gleichen physischen oder virtuellen Switch verbunden sind, ist es keine echte Redundanz auf der Netzwerkebene konfigurieren mehrere NICs einem gewissen Grad Illusion an den virtuellen Computer. Netzwerkredundanz wird normalerweise in der Hypervisor für virtualisierte Bereitstellungen erstellt, und der öffentlichen Cloud definitiv integriert ist.

Ein besteht Unterschied mit mehreren NICs und Schrittmacher im Vergleich zu einem WSFC darin, dass Schrittmacher mehrere IP-Adressen im gleichen Subnetz kann während ein WSFC nicht der Fall ist. Weitere Informationen über mehrere Subnetze und Linux-Cluster finden Sie im Artikel [konfigurieren Sie mehrere Subnetze](sql-server-linux-configure-multiple-subnet.md).

### <a name="quorum-and-stonith"></a>Quorum und STONITH
Quorumkonfiguration und Anforderungen beziehen sich auf AG oder FCI-spezifische Bereitstellungen von [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

STONITH ist für einen unterstützten Schrittmacher Cluster erforderlich. Verwenden Sie die Dokumentation über die Verteilungspunkteigenschaften STONITH konfigurieren. Ein Beispiel ist am [Fencing Speicher basierende](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html) für SLES. Es gibt auch ein STONITH-Agent für VMware vCenter für ESXI-basierte Lösungen. Weitere Informationen finden Sie unter [Stonith-Plug-in-Agent für VMWare VM VCenter SOAP-Zauns (Unofficial)](https://github.com/olafrv/fence_vmware_soap).

> [!NOTE]
> Zum Zeitpunkt der Verfassung dieses Artikels, weist Hyper-V keine Lösung für STONITH auf. Dies ist "true" für die bei lokalen Bereitstellungen und wirkt sich auch auf bestimmte Verteilungen z. B. RHEL mit Azure-basierten Schrittmacher-Bereitstellungen.

### <a name="interoperability"></a>Interoperabilität
Dieser Abschnitt beschreibt, wie auf ein Linux-basierten Cluster mit einem WSFC oder andere Linux-Distributionen interagieren kann.

#### <a name="wsfc"></a>WSFC
Derzeit besteht keine direkte Möglichkeit für einen wsfc- und einem Cluster Schrittmacher zusammenarbeiten. Dies bedeutet, dass es gibt keine Möglichkeit zum Erstellen einer AG oder einer FCI, die über ein wsfc- und Schrittmacher funktioniert. Es gibt jedoch zwei Interoperabilität-Lösungen, die beide zur Testreihen vorgesehen sind. Die einzige Möglichkeit, die eine plattformübergreifende Konfiguration eine FCI teilnehmen kann ist, wenn es als eine Instanz einer dieser beiden Szenarien ist:
-   Eine Verfügbarkeitsgruppe mit einem Clustertyp ' None '. Weitere Informationen finden Sie unter Windows [Verfügbarkeitsgruppen Dokumentation](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).
-   Eine verteilte AG, also eine besondere Art von verfügbarkeitsgruppe, die zwei verschiedenen Testreihen als ihre eigenen verfügbarkeitsgruppe konfiguriert werden können. Weitere Informationen zu verteilten Testreihen, finden Sie in der Dokumentation [von verteilten Verfügbarkeitsgruppen](../database-engine/availability-groups/windows/distributed-availability-groups.md).

#### <a name="other-linux-distributions"></a>Andere Linux-Distributionen
Alle Knoten eines Clusters Schrittmacher muss unter Linux auf die gleiche Verteilung verwendet wird. Beispielsweise bedeutet dies, dass ein Knoten RHEL Teil eines Clusters Schrittmacher sein kann, die ein SLES-Knoten hat. Der Hauptgrund dafür wurde bereits erwähnt: die Verteilungen möglicherweise unterschiedliche Versionen und Funktionalität, sodass Dinge nicht ordnungsgemäß ausgeführt werden konnte. Mischen von Verteilungen hat den gleichen Text wie das Mischen von WSFCs und Linux: Verwenden Sie keine oder Testreihen verteilt.

## <a name="next-steps"></a>Nächste Schritte
[Bereitstellen eines Clusters Schrittmacher für SQL Server on Linux](sql-server-linux-deploy-pacemaker-cluster.md)
