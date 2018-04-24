---
title: Konfigurieren Sie InfiniBand - Analyseplattformsystem | Microsoft Docs
description: Beschreibt, wie die InfiniBand-Netzwerkadapter auf einem nicht-Appliance Clientserver für die Verbindung mit dem Steuerungsknoten auf Parallel Data Warehouse (PDW) konfigurieren. Verwenden Sie diese Anweisungen für grundlegende Konnektivität und hohe Verfügbarkeit, sodass laden, Sicherung und andere Prozesse automatisch mit dem aktiven InfiniBand-Netzwerk verbunden.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 8e67d63e7bb4bded0bd19e5db4a0b7faddb80977
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>InfiniBand-Netzwerkadapter für Analytics Platform System konfigurieren
Beschreibt, wie die InfiniBand-Netzwerkadapter auf einem nicht-Appliance Clientserver für die Verbindung mit dem Steuerungsknoten auf Parallel Data Warehouse (PDW) konfigurieren. Verwenden Sie diese Anweisungen für grundlegende Konnektivität und hohe Verfügbarkeit, sodass laden, Sicherung und andere Prozesse automatisch mit dem aktiven InfiniBand-Netzwerk verbunden.  
  
## <a name="Basics"></a>Beschreibung  
Diese Anweisungen zeigen, wie zum Suchen, und legen Sie dann die richtige InfiniBand IP-Adressen und Subnetzmasken auf Ihrem Server InfiniBand verbunden. Sie wird auch erläutert, wie Festlegen von einem Server in der APS-Appliance DNS verwenden, damit die Verbindung mit dem aktiven InfiniBand-Netzwerk aufgelöst wird.  
  
Für hohe Verfügbarkeit hat APS zwei InfiniBand-Netzwerke, ein aktives und einer passiven. Jedes InfiniBand-Netzwerk verfügt über eine andere IP-Adresse für den Knoten "Zugriffssteuerung". Fällt der aktive InfiniBand-Netzwerk aus, wird der passive InfiniBand-Netzwerk das aktive Netzwerk an. In diesem Fall verbindet sich ein Skript oder der Prozess automatisch mit dem aktiven InfiniBand-Netzwerk ohne Änderung der Skriptparameter.  
  
Insbesondere in diesem Artikel Sie:  
  
1.  Suchen Sie die InfiniBand IP-Adressen von der APS-DNS-Servern (Appliance_domain AD01 und Appliance_domain *-AD02). Zu diesem Zweck melden Sie sich bei den Servern AD01 und AD02 und rufen Sie die IP-Adressen für jedes InfiniBand-Netzwerk. Die InfiniBand IP-Adressen auf dem AD-Knoten sind die DNS IP-Adressen.  
  
2.  Konfigurieren Sie jeden Netzwerkadapter, um eine verfügbare IP-Adresse auf APS InfiniBand-Netzwerke verwenden.  
  
    1.  Wenn Sie zwei InfiniBand-Netzwerkadapter haben, konfigurieren Sie einen Adapter einer verfügbaren IP-Adresse in das erste InfiniBand-Netzwerk TeamIB1 und der andere Adapter mit einer verfügbaren IP-Adresse in das zweite InfiniBand-Netzwerk heißt der TeamIB2 aufgerufen wird. Verwenden der Appliance_domain AD01 TeamIB1 IP-Adresse als bevorzugter DNS-Server und Appliance_domain AD02 TeamIB1 IP-Adresse wie der alternativen DNS-Server für den Netzwerkadapter-TeamIB1. Verwenden der Appliance_domain AD01 TeamIB2 IP-Adresse als bevorzugter DNS-Server und Appliance_domain AD02 TeamIB2 IP-Adresse als alternativen DNS-Server für TeamIB2-Netzwerkadapter.  
  
    2.  Wenn Sie nur einen InfiniBand-Netzwerkadapter verfügen, konfigurieren Sie den Adapter mit einer verfügbaren IP-Adresse eines InfiniBand-Netzwerke. Anschließend konfigurieren Sie die bevorzugte und alternative DNS-Server auf diesem Adapter Appliance_domain AD01 TeamIB1 und Appliance_domain AD02 TeamIB1 oder Appliance_domain AD01 TeamIB2 und Appliance_domain AD02 TeamIB2 je nachdem, was auf dem gleichen ist Netzwerk-bzw. als der konfigurierte Adapter als der bevorzugte und alternative DNS-Server.  
  
3.  Konfigurieren Sie Ihre InfiniBand-Netzwerkadapter zur APS DNS-Server verwenden, um die Verbindung mit dem aktiven InfiniBand-Netzwerk zu beheben.  
  
    1.  Um diese Konfiguration verwenden Sie die erweiterte TCP/IP-Einstellungen die Appliance DNS-Domänensuffix am Anfang der Liste der DNS-Suffixe auf Ihrem Clientserver hinzuzufügen. Dies muss nur auf einem Netzwerkadapter konfiguriert werden; die Einstellung gilt für beide Adapter.  
  
Nach dem Konfigurieren der InfiniBand-Netzwerkadapter, Clientprozesse können eine Verbindung mit dem Steuerungsknoten im InfiniBand-Netzwerk `PDW_region-SQLCTL01` für die Adresse des Servers. Der Server Fügt das Analytics Platform System, DNS-Suffix an, oder die vollständige Adresse also eingeben `PDW_region-SQLCTL01.appliance_domain.pdw.local`.  
  
Beispielsweise ist, wenn der Name der PDW-Region MyPDW ist und der Gerätename MyAPS ist, Dwloader Serverspezifikation zum Laden von Daten eine der folgenden:  
  
-   `dwloader –S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader –S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>Vorbereitungen  
  
### <a name="requirements"></a>Anforderungen  
Sie benötigen ein Domänenkonto für APS Appliance, auf den Knoten AD01 anzumelden. Beispielsweise F12345 * \Administrator.  
  
Sie benötigen ein Windowskonto auf dem Clientserver, der Berechtigung zur Konfiguration der Netzwerkadapter verfügt.  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
Diese Anweisungen gehen davon aus, die Clientserver bereits Verkabeln und der Appliance InfiniBand-Netzwerk verbunden ist. Racks und Verkabelung Anweisungen finden Sie in [erwerben und Konfigurieren eines Servers geladen](acquire-and-configure-loading-server.md).  
  
### <a name="general-remarks"></a>Allgemeine Hinweise  
Mithilfe von SQLCTL01 verbindet das Analytics Platform System DNS mit dem Steuerungsknoten Ihre Clientserver mithilfe des aktiven InfiniBand-Netzwerks an. Dies gilt nur für das Herstellen einer Verbindung zur; Wenn das InfiniBand-Netzwerk während eines Auslastungstests ausfällt oder sichern, Sie den Prozess neu zu starten müssen.  
  
Um Ihren eigenen geschäftsanforderungen zu erfüllen, können Sie die Clientserver auch Ihre eigenen nicht-Appliance Arbeitsgruppe oder einer Windows-Domäne verknüpfen.  
  
## <a name="Sec1"></a>Schritt 1: Abrufen der Appliance InfiniBand-Netzwerkeinstellungen  
*Um die Appliance InfiniBand-Netzwerkeinstellungen abrufen*  
  
1.  Melden Sie sich an die Appliance AD01 Knoten mit dem Appliance_domain\Administrator an.  
  
2.  Klicken Sie auf dem Gerät AD01-Knoten öffnen Sie die Systemsteuerung, wählen Sie Netzwerk und Internet, wählen Sie Netzwerk- und Freigabe Center aus *, und wählen Sie die Adaptereinstellungen ändern.  
  
3.  Klicken Sie im Fenster Netzwerkverbindungen mit der rechten Maustaste auf das Team IB1, und wählen Sie Eigenschaften aus.  
  
    ![InfiniBand-Verbindungen auf dem Verwaltungsknoten](media/network-teamib.png "InfiniBand-Verbindungen auf den Knoten "Management"")  
  
4.  Im Fenster Eigenschaften von Internetprotokoll Version 4 (TCP/IPv4) Notieren Sie sich die Werte für die **IP-Adresse** und **Subnetzmaske**.  Die IP-Adresse der ***Appliance_domain *-AD01** Knoten ist die IP-Adresse des Analytics Platform System, DNS-Servers.  
  
5.  Wiederholen Sie die Schritte 1 bis 5 oben für den Adapter TeamIB1 auf ***Appliance_domain *-AD02** Server.  
  
    ![PDW-Knoten InfiniBand 1 Verwaltungseigenschaften](media/network-ip1-properties.png "PDW Verwaltungseigenschaften Knoten InfiniBand 1")  
  
6.  Klicken Sie auf "Abbrechen", um das Fenster zu schließen.  
  
7.  Suchen Sie eine nicht verwendete IP-Adresse im Netzwerk TeamIB1, und notieren Sie ihn.  
  
    Öffnen Sie ein Befehlsfenster, und versuchen Sie ping IP-Adressen innerhalb des Bereichs von Adressen für Ihre Anwendung, um eine nicht verwendete IP-Adresse zu suchen. In diesem Beispiel wird die IP-Adresse des Netzwerks TeamIB1 172.16.14.30. Suchen Sie eine IP-Adresse, die mit 172.16.14 beginnt, das verwendet wird. Geben Sie über die Befehlszeile z. B. "ping 172.16.14.254". Wenn der Ping-Anforderung nicht erfolgreich ist, ist die IP-Adresse verfügbar.  
  
8.  Führen Sie dieselben Schritte für TeamIB2. In der * Netzwerkverbindungen-Fenster mit der rechten Maustaste auf das Team IB2 und wählen Sie Eigenschaften aus.  
  
9. Notieren Sie im Fenster Eigenschaften von Internetprotokoll Version 4 (TCP/IPv4) sich die Werte für die IP-Adresse und Subnetzmaske, für TeamIB2.  
  
10. Wiederholen Sie die Schritte 8 und 9 oben für den Adapter TeamIB2 auf Appliance_domain AD02-Server.  
  
    ![Eigenschaften für TeamIB2](media/network-ip2-properties.png "Eigenschaften für TeamIB2")  
  
11. Suchen Sie eine nicht verwendete IP-Adresse auf dem **TeamIB2** Netzwerk, und notieren Sie ihn.  
  
    Öffnen Sie ein Befehlsfenster, und versuchen Sie ping IP-Adressen innerhalb des Bereichs von Adressen für Ihre Anwendung, um eine nicht verwendete IP-Adresse zu suchen. In diesem Beispiel wird die IP-Adresse des Netzwerks TeamIB2 172.16.18.30. Suchen Sie eine IP-Adresse, die mit 172.16.18 beginnt, das verwendet wird. Geben Sie über die Befehlszeile z. B. "ping 172.16.18.254". Wenn der Ping-Anforderung nicht erfolgreich ist, ist die IP-Adresse verfügbar.  
  
## <a name="Sec2"></a>Schritt 2: Konfigurieren der Einstellungen für InfiniBand-Netzwerkadapter auf dem Clientserver  

### <a name="notes"></a>Hinweise  
  
-   Diese Schritte veranschaulichen, wie zum Registrieren Ihres Servers mit der APS DNS-Servern.  
  
-   Um Ihren eigenen netzwerkanforderungen zu erfüllen, können Sie die Clientserver auch Ihre eigenen nicht-Appliance Arbeitsgruppe oder einer Windows-Domäne verknüpfen.  
  
-   Die Anweisungen schrittweise durchlaufen die Konfiguration von zwei Netzwerkadaptern auf jedem Server.  Wenn Sie nur einen Netzwerkadapter verfügen, wählen Sie eine der Netzwerke an, auf dem Netzwerkadapter konfigurieren, und klicken Sie dann die zweite DNS IP-Adresse als alternativen DNS-Server hinzufügen.  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>So konfigurieren Sie die InfiniBand-Einstellungen des Netzwerkadapters auf dem Clientserver  
  
1.  Melden Sie sich als Windows-Administrator, Ihr laden Sicherung oder andere Clientserver, auf dem Gerät InfiniBand-Netzwerk.  
  
2.  Öffnen Sie das Steuerelement Bereich *, wählen Sie, Netzwerk- und Freigabecenter, und wählen Sie die Adaptereinstellungen ändern.  
  
### <a name="to-configure-the-first-network-adapter"></a>So konfigurieren Sie die erste Netzwerkkarte  
  
1.  Klicken Sie im Fenster Netzwerkverbindungen mit der rechten Maustaste auf einen der Slots nicht identifizierte Netzwerk für den Mellanox-Adapter, und wählen Sie Eigenschaften aus.  
  
    ![Wählen Sie die InfiniBand-Netzwerke](media/network-connections.png "InfiniBand-Netzwerke auswählen")  
  
2.  Im Eigenschaftenfenster  
  
    1.  Legen Sie auf der Registerkarte "Allgemein" die IP-Adresse der IP-Adresse, die Sie als "frei" in der Ping-Test für TeamIB1 überprüft. Für die Beispielwerte in diesem Artikel verwendet wird Geben Sie 172.16.14.254.  
  
    2.  Legen Sie die Subnetzmaske, auf die Subnetzmaske, die Sie für TeamIB1 notiert.  
  
    3.  Legen Sie den bevorzugten DNS-Server die IP-Adresse, die zuvor von Appliance_domain * notiert TeamIB1-AD01-Knoten.  
  
    4.  Legen Sie den alternativen DNS-Server die IP-Adresse, die zuvor von Appliance_domain * notiert TeamIB1-AD02-Knoten.  
  
        ![InfiniBand 1 Netzwerkadaptereigenschaften](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  Klicken Sie auf OK, um die Änderungen zu übernehmen.  
  
### <a name="to-configure-the-second-network-adapter"></a>So konfigurieren Sie die zweite Netzwerkkarte  
  
1.  Überspringen Sie diesen Abschnitt, wenn Sie nur einen Netzwerkadapter verfügen.  
  
2.  Klicken Sie im Fenster Netzwerkverbindungen mit der rechten Maustaste im zweiten Steckplatz der nicht identifizierten Netzwerk für den Mellanox-Adapter, und wählen Sie Eigenschaften aus.  
  
    ![Wählen Sie die InfiniBand-Netzwerke](media/network-connections.png "InfiniBand-Netzwerke auswählen")  
  
3.  Im Eigenschaftenfenster  
  
    1.  Legen Sie auf der Registerkarte "Allgemein" die IP-Adresse der IP-Adresse, die Sie als "frei" in der Ping-Test für TeamIB2 überprüft. Für die Beispielwerte in diesem Artikel verwendet wird Geben Sie 172.16.18.254.  
  
    2.  Legen Sie die Subnetzmaske, auf die Subnetzmaske, die Sie für TeamIB2 notiert.  
  
    3.  Legen Sie den bevorzugten DNS-Server die IP-Adresse, die zuvor von Appliance_domain * notiert TeamIB2-AD01-Knoten.  
  
    4.  Legen Sie den alternativen DNS-Server die IP-Adresse, die zuvor von Appliance_domain * notiert TeamIB2-AD02-Knoten.  
  
        > [!NOTE]  
        > Wenn Sie nur über einen Netzwerkadapter, der bevorzugte und alternative DNS-Server mithilfe der Appliance AD01 TeamIB1 und der Appliance AD02 TeamIB1 als der bevorzugte und alternative DNS-Server konfigurieren oder verwenden Sie die Einheit AD01 TeamIB2 und Appliance AD02 TeamIB2 als der bevorzugte und alternative DNS-Server durch, je nachdem, ob hat der virtuelle AD-Computer ein Failover ausgeführt.  
  
        ![InfiniBand 1 Netzwerkadaptereigenschaften](media/network-ib1-properties.png "InfiniBand 1 Netzwerkadaptereigenschaften")  
  
    5.  Klicken Sie auf OK, um die Änderungen zu übernehmen.  
  
### <a name="to-configure-the-dns-suffix"></a>So konfigurieren Sie das DNS-suffix  
  
1.  Klicken Sie im Fenster Netzwerkverbindungen mit der rechten Maustaste auf einen der Slots Netzwerk für den Mellanox-Adapter, und wählen Sie Eigenschaften aus.  
  
2.  Klicken Sie auf den erweiterten... aus.  
  
3.  Im Fenster Erweiterte TCP/IP-Einstellungen, wenn das Anfügen dieser DNS-Suffixe (in entsprechender Reihenfolge)-Option nicht, abgeblendet ist überprüfen Sie das Feld aufgerufen diese DNS-Suffixe anhängen (in Reihenfolge): Wählen Sie das Domänensuffix Einheit, und klicken Sie auf Hinzufügen... Das Gerät Domänensuffix `appliance_domain.local`  
  
4.  Wenn der Anfügevorgang diese DNS-Suffixe (in entsprechender Reihenfolge): Option abgeblendet ist, Sie können die APS-Domäne mit diesem Server hinzufügen, indem Sie den Registrierungsschlüssel HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\DNSClient ändern.  
  
    ![TCP/IP-Einstellungen](media/network-tcpip.png "TCP/IP-Einstellungen")  
  
5.  Schnellere Adressauflösung wird empfohlen, die Appliance-Suffix an den Anfang der Liste verschieben.  
  
6.  Klicken Sie auf OK.  
  
7.  Sie können nun mit dem Gerät Infiniband-Netzwerk verbinden, indem Sie mit `PDW_region-SQLCTL01.appliance_domain.local`, oder einfach `appliance_domain-SQLCTL01`. Die Verbindung möglicherweise schneller eingerichtet werden, wenn Sie eine mit den vollständigen Namen und die DNS-Suffix Verbindung.  
  
    Beispiele für eine Einheit benannt MyAPS mit einem MyPDW PDW-Region an:  
  
    -   MyPDW-SQLCTL01.MyAPS.local  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>Siehe auch  
[Erwerben und Konfigurieren eines Servers geladen ](acquire-and-configure-loading-server.md)  
  
