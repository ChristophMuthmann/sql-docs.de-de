---
title: "Konfigurieren von mehreren Subnetzen AlwaysOn-Verfügbarkeitsgruppen und Failoverclusterinstanzen unter Linux | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/1/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: df5182d374e41b68fe35333c6e4ab59714d8241d
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>Konfigurieren von mehreren Subnetzen AlwaysOn-Verfügbarkeitsgruppen und Failoverclusterinstanzen

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Wenn eine immer auf Availability Group (AG) oder ein Failover-Clusterinstanz (FCI) mehr als ein Standort, der jeder Standort in der Regel umfasst verfügt über eigene Netzwerke aus. Dies bedeutet häufig, dass jeder Standort verfügt über eine eigene IP-Adressierung. Starten Sie Standortadressen A z. B. mit 192.168.1. *x* und Standort B-Adressen mit 192.168.2 beginnen. *X*, wobei *x* ist der Teil der IP-Adresse, die mit dem Server eindeutig ist. Ohne irgendeine auf Netzwerkebene direktes Routing werden dieser Server nicht miteinander kommunizieren können. Es gibt zwei Möglichkeiten, dieses Szenario zu behandeln: ein Netzwerk, das die zwei unterschiedlichen Subnetzen befinden, bekannt als ein VLAN verbindet einrichten oder konfigurieren Sie das routing zwischen den Subnetzen.

## <a name="vlan-based-solution"></a>VLAN-basierte Lösung
 
**Erforderliche**: für ein VLAN-basierten Lösung jeder Server Teil einer Verfügbarkeitsgruppe oder einer FCI benötigt zwei Netzwerkkarten (NICs) für eine ordnungsgemäße Verfügbarkeit (ein dualer-Port NIC wäre eine einzelne Fehlerquelle auf einem physischen Server), damit sie IP-Adressen zugewiesen werden kann die systemeigene Subnetz als auch auf das VLAN. Dies erfolgt zusätzlich zu anderen netzwerkanforderungen, z. B. iSCSI, das auch ein eigenes Netzwerk benötigt.

Die Erstellung der IP-Adresse für die Verfügbarkeitsgruppe oder einer FCI erfolgt im VLAN. Im folgenden Beispiel wurde das VLAN einem Subnetz 192.168.3. *x*, sodass die IP-Adresse für die AG oder FCI erstellt 192.168.3.104 ist. Keine weiteren Aktionen erforderlich konfiguriert werden, da es eine einzelne IP-Adresse, die dem AG oder der FCI zugewiesen ist.

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Mit der Schrittmacher

In der Windows-Welt wird ein Windows Server Failover Cluster (WSFC) systemintern mehrere Subnetze unterstützt, und mehrere IP-Adressen über einen OR-Abhängigkeit der IP-Adresse behandelt. Unter Linux keine OR-Abhängigkeit vorhanden ist, aber es gibt eine Möglichkeit, eine ordnungsgemäße multisubnetz systemintern mit Schrittmacher, erzielen, wie im folgenden Beispiel dargestellt. Sie können nicht so vorgehen mithilfe der normalen Schrittmacher Befehlszeile einfach, um eine Ressource zu ändern. Sie müssen die Clusterinformationen Basis (CIB) zu ändern. Die CIB ist eine XML-Datei mit der Schrittmacher-Konfiguration.

![](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>Aktualisieren Sie die CIB

1.  Exportieren Sie die CIB.

    **Red Hat Enterprise Linux (RHEL) und Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server (SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    Wobei *Filename* ist der Name der CIB aufgerufen werden soll.

2.  Bearbeiten Sie die Datei, die generiert wurde. Suchen Sie nach der `<resources>` Abschnitt. Daraufhin werden die verschiedenen Ressourcen, die für die Verfügbarkeitsgruppe oder einer FCI erstellt wurden. Suchen Sie eine der IP-Adresse zugeordnet. Hinzufügen einer `<instance attributes>` im Abschnitt mit den Informationen für die zweite IP-Adresse oberhalb oder unterhalb der vorhandenen Dateigruppe, jedoch bevor `<operations>`. Es sieht in etwa wie die folgende Syntax:

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    wobei *NameForAttribute* ist der eindeutige Name für dieses Attribut *Score* wird die zugewiesene Nummer an das Attribut, das höher als die primären Subnetzes sein muss, *RuleName*ist der Name der Regel *ExpressionName* ist der Name des Ausdrucks *NodeNameInSubnet2* ist der Name des Knotens in den anderen Subnetzen *NameForSecondIP* ist der Name der zweiten IP-Adresse zugeordnet *IP-Adresse* ist die IP-Adresse für das zweite Subnetz *NameForSecondIPNetmask* ist der Name der Netzmaske zugeordnet und *Netzmaske* die Netzmaske für das zweite Subnetz ist.
    
    Das folgende zeigt Beispiel.
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

3.  Importieren Sie die geänderte CIB und konfigurieren Sie Schrittmacher.

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    wobei *Filename* ist der Name der Datei mit der geänderten IP-Adressinformationen CIB.

### <a name="check-and-verify-failover"></a>Überprüfen Sie, und Überprüfen des Failovers

1.  Nachdem die CIB mit der aktualisierten Konfiguration erfolgreich angewendet wurde, Pingen Sie den DNS-Namen der IP-Adressressource in Schrittmacher zugeordnet. Sie sollten die IP-Adresse, die dem Subnetz derzeit gehostet wird, die Verfügbarkeitsgruppe oder einer FCI zugeordnet widerspiegeln.
2.  Fehl, die Verfügbarkeitsgruppe oder einer FCI zum anderen Subnetz.
3.  Nachdem der AG oder einer FCI vollständig online ist, Pingen Sie den DNS-Namen der IP-Adresse zugeordnet. Die IP-Adresse in das zweite Subnetz sollten berücksichtigt werden.
4.  Falls gewünscht, werden die AG oder einer FCI wieder mit dem ursprünglichen Subnetz fehl.
