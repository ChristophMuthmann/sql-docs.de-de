---
title: Bereitstellen ein Clusters Schrittmacher für SQL Server on Linux | Microsoft Docs
description: Dieses Lernprogramm zeigt, wie einen Cluster Schrittmacher für SQL Server on Linux bereitstellen.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/11/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: 6080c2bb4a430b25bdaa8605b4fd9473cf766fdd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>Bereitstellen eines Clusters Schrittmacher für SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

In diesem Lernprogramm werden die erforderlichen Aufgaben zum Bereitstellen eines Clusters Linux Schrittmacher für eine [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Always On-verfügbarkeitsgruppe (AG) oder einer Failoverclusterinstanz (FCI). Im Gegensatz zu eng gekoppelten WindowsServer /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Stapel, Schrittmacher Clustererstellung sowie verfügbarkeitsgruppenkonfiguration (AG) unter Linux kann durchgeführt werden, vor oder nach der Installation von [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Die Integration und Konfiguration von Ressourcen für den Schrittmacher Teil einer Verfügbarkeitsgruppe oder einer FCI-Bereitstellung wird ausgeführt, nachdem der Cluster konfiguriert ist.
> [!IMPORTANT]
> Ist eine AG mit einem Cluster keine *nicht* muss einen Cluster Schrittmacher, noch können sie von Schrittmacher verwaltet werden. 

> [!div class="checklist"]
> * Installieren Sie das Add-on für hohe Verfügbarkeit und installieren Sie Schrittmacher.
> * Bereiten Sie die Knoten für Schrittmacher (RHEL und Ubuntu nur) vor.
> * Erstellen Sie den Schrittmacher-Cluster.
> * Installieren Sie die SQL Server mit hoher Verfügbarkeit und SQL Server-Agent-Pakete.
 
## <a name="prerequisite"></a>Voraussetzung
[Installieren von SQLServer 2017](sql-server-linux-setup.md).

## <a name="install-the-high-availability-add-on"></a>Installieren Sie das Add-on für hohe Verfügbarkeit
Verwenden Sie die folgende Syntax zum Installieren der Pakete, die die hohe Verfügbarkeit (HA)-Add-On für jede Verteilung von Linux bilden. 

**Red Hat Enterprise Linux (RHEL)**
1.  Registrieren Sie den Server, die mithilfe der folgenden Syntax an. Sie werden für einen gültigen Benutzernamen und Kennwort aufgefordert.
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  Liste der verfügbaren Pools für die Registrierung.
    
    ```bash
    sudo subscription-manager list --available
3.  Run the following command to associate RHEL high availability with the subscription
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    wobei *PoolId* ist die Pool-ID für das Abonnement hohe Verfügbarkeit aus dem vorherigen Schritt.
    
4.  Aktivieren Sie das Repository, damit das Add-on für hohe Verfügbarkeit verwendet werden.
    
    ```bash
    sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
    ```
    
5.  Installieren Sie Schrittmacher.
    
    ```bash
    sudo yum install pacemaker pcs fence-agents-all resource-agents
    ```

**Ubuntu**

```bash
sudo apt-get install pacemaker pcs fence-agents resource-agents
```

**SUSE Linux Enterprise Server (SLES)**

Installieren Sie das Muster für hohe Verfügbarkeit in YaST, oder führen Sie ihn als Teil der Basisinstallation des Servers. Die Installation kann mit einer ISO/DVD als Quelle oder indem Sie es online abrufen erfolgen.
> [!NOTE]
> Auf SLES ruft der HA-Add-On initialisiert, wenn es sich bei der Erstellung des Clusters.

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>Vorbereiten der Knoten für Schrittmacher (RHEL und nur Ubuntu)
Schrittmacher selbst mithilfe einen vom Benutzer auf die Verteilung, die mit dem Namen *Hacluster*. Der Benutzer wird erstellt, wenn die HA-Add-On für RHEL und Ubuntu installiert ist.
1. Erstellen Sie auf jedem Server, die als Knoten des Clusters Schrittmacher fungieren soll das Kennwort für einen Benutzer, die vom Cluster verwendet werden. Der Name in den Beispielen verwendete *Hacluster*, aber einen beliebigen Namen verwendet werden kann. Den Namen und das Kennwort müssen auf allen Knoten, die Teil des Clusters Schrittmacher identisch sein.
   
    ```bash
    sudo passwd hacluster
    ```
    
2. Aktivieren Sie auf jedem Knoten, die Teil des Clusters Schrittmacher werden, und starten die `pcsd` -Dienst mit den folgenden Befehlen (RHEL und Ubuntu):

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   Führen Sie dann
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   um sicherzustellen, dass `pcsd` gestartet wird.
3. Aktivieren der Schrittmacher-Dienst auf jeder mögliche Knoten des Clusters Schrittmacher.
   
   ```bash
   sudo systemctl start pacemaker
   ```

   Auf Ubuntu wird ein Fehler angezeigt:
   
   *Schrittmacher Standard Boot-enthält keine Ausführungsstufe, abgebrochen wird.*
   
   Dieser Fehler ist ein bekanntes Problem. Trotz des Fehlers Aktivieren des Diensts Schrittmacher erfolgreich ist, und dieser Fehler wird in der Zukunft irgendwann behoben werden.
   
4. Als Nächstes erstellen Sie und starten Sie den Cluster Schrittmacher. Es gibt einen Unterschied zwischen RHEL und Ubuntu an diesem Punkt ein. Klicken Sie auf beiden Verteilungen installieren `pcs` konfiguriert eine standardmäßige Konfigurationsdatei für Cluster Schrittmacher RHEL, diesen Befehl ausführen, eine vorhandene Konfiguration zerstört und erstellt einen neuen Cluster.

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>Erstellen des Clusters Schrittmacher 
Dieser Abschnitt beschreibt das Erstellen und konfigurieren Sie für jede Verteilung auf dem Linux-Cluster.

**RHEL**

1. Autorisieren Sie die Knoten
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 … NodeN> -u hacluster
   ```
   
   wobei *NodeX* ist der Name des Knotens.
2. Erstellen des Clusters
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   wobei *PMClusterName* ist der Name für den Cluster Schrittmacher zugewiesen und *Nodelist* ist die Liste der Namen der Knoten, die durch ein Leerzeichen getrennt.

**Ubuntu**

Konfigurieren von Ubuntu ähnelt dem RHEL. Es ist jedoch ein wesentlicher Unterschied: Installieren der Pakete Schrittmacher erstellt eine Basiskonfiguration für die Cluster, und aktiviert und startet `pcsd`. Wenn Sie versuchen, den Schrittmacher-Cluster mithilfe der RHEL Anweisungen genau zu konfigurieren, erhalten Sie eine Fehlermeldung an. Um dieses Problem zu beheben, führen Sie die folgenden Schritte aus: 
1. Entfernen Sie die Standardkonfiguration Schrittmacher auf jedem Knoten.
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. Führen Sie die Schritte im Abschnitt zum Erstellen des Clusters Schrittmacher RHEL aus.

**SLES**

Der Prozess zum Erstellen eines Clusters Schrittmacher unterscheidet sich vollständig auf SLES, als dies für RHEL und Ubuntu. Gewusst wie: Erstellen eines Clusters mit SLES zu dokumentieren die folgenden Schritte aus.
1. Starten Sie den Cluster Konfigurationsprozess durch Ausführen 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   auf einem der Knoten. Sie werden möglicherweise aufgefordert, dass NTP nicht konfiguriert ist und kein Watchdog-Gerät gefunden wird. Die eignet sich gut für erste Dinge einrichten und ausführen. Watchdog bezieht sich auf STONITH bei Verwendung SLESs integrierte Zäune, die Speicher-basiert ist. NTP und Watchdog kann später konfiguriert werden.
   
2. Sie werden aufgefordert, Corosync konfigurieren. Sie werden für die Netzwerkadresse sowie die Multicastadresse und den Port Bindung aufgefordert. Die Netzwerkadresse ist das Subnetz, das Sie verwenden. Beispielsweise 192.191.190.0. Sie können akzeptieren Sie die Standardeinstellungen an jeder Eingabeaufforderung oder bei Bedarf ändern.
   
3. Als Nächstes werden Sie aufgefordert, wenn SBD, konfigurieren Sie also die datenträgerbasierten Fencing werden sollen. Diese Konfiguration kann bei Bedarf später erfolgen. SBD ist nicht konfiguriert, im Gegensatz zu RHEL und Ubuntu, `stonith-enabled` wird standardmäßig auf "false" festgelegt.
   
4. Abschließend werden Sie aufgefordert, wenn Sie eine IP-Adresse für die Verwaltung konfigurieren möchten. Diese IP-Adresse ist optional, aber funktioniert ähnlich wie die IP-Adresse für einen Windows Server-Failovercluster (WSFC) in dem Sinne, die eine IP-Adresse im Cluster verwendet werden, für die Verbindung herstellt, über virtuelle Maschinen mit hoher Web Konsole (HAWK) erstellt. Diese Konfiguration ist ebenfalls optional.
   
5. Stellen Sie sicher, dass der Cluster durch ausgeben einsatzbereit ist 
   ```bash
   sudo crm status
   ```
   
6. Ändern der *Hacluster* mit Kennwort 
   ```bash
   sudo passwd hacluster
   ```
   
7. Wenn Sie eine IP-Adresse für die Verwaltung konfiguriert haben, können Sie testen in einem Browser eingeben, die auch die Änderung des Kennworts für testet *Hacluster*.
   ![](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. Führen Sie auf einem anderen SLES-Server, der einem Knoten des Clusters sein wird, 
   ```bash
   sudo ha-cluster-join
   ```
   
9. Wenn Sie aufgefordert werden, geben Sie den Namen oder die IP-Adresse des Servers, der als erster Knoten des Clusters in den vorherigen Schritten konfiguriert wurde. Der Server wird als Knoten zum vorhandenen Cluster hinzugefügt.
   
10. Stellen Sie sicher, dass der Knoten durch ausgeben hinzugefügt wurde 
   ```bash
   sudo crm status
   ```
   
11. Ändern der *Hacluster* mit Kennwort 
   ```bash
   sudo passwd hacluster
   ```
   
12. Wiederholen Sie die Schritte 8 bis 11 für alle anderen Server, auf dem Cluster hinzugefügt werden.

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>Installieren Sie die SQL Server mit hoher Verfügbarkeit und SQL Server-Agent-Pakete
Verwenden Sie die folgenden Befehle zum Installieren des SQL Server-HA-Pakets und [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -Agent, wenn sie nicht bereits installiert sind. Installieren die HA-Paket nach der Installation von [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] erfordert einen Neustart des [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] dafür verwendet werden. Diese Anweisungen gehen davon aus, dass die Repositorys für die Microsoft-Pakete bereits seit eingerichtet wurden haben [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] zu diesem Zeitpunkt installiert werden soll.
> [!NOTE]
> - Wenn Sie nicht verwenden möchten [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -Agent für den Protokollversand oder jegliche andere Zwecke, er muss nicht installiert werden, so verpacken *Mssql-Server-Agent* können übersprungen werden.
> - Die optionalen Pakete für [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] unter Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Volltextsuche (*Mssql-Server-Fts*) und [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*Mssql Server ist*), sind nicht für hohe Verfügbarkeit für eine FCI oder einer AG erforderlich.

**RHEL**

```bash
sudo yum install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**Ubuntu**

```bash
sudo apt-get install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**SLES**

```bash
sudo zypper install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

## <a name="next-steps"></a>Nächste Schritte

In diesem Lernprogramm haben Sie gelernt, einen Cluster Schrittmacher für SQL Server on Linux bereitstellen. Sie haben gelernt, wie auf:
> [!div class="checklist"]
> * Installieren Sie das Add-on für hohe Verfügbarkeit und installieren Sie Schrittmacher.
> * Bereiten Sie die Knoten für Schrittmacher (RHEL und Ubuntu nur) vor.
> * Erstellen Sie den Schrittmacher-Cluster.
> * Installieren Sie die SQL Server mit hoher Verfügbarkeit und SQL Server-Agent-Pakete.

Erstellen und Konfigurieren einer verfügbarkeitsgruppe für SQL Server on Linux, finden Sie unter:

> [!div class="nextstepaction"]
> [Erstellen und konfigurieren eine verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-create-availability-group.md).

