---
title: Verwenden Sie eine DNS-Weiterleitung in Analytics Platform System | Microsoft Docs"
description: Verwenden Sie eine DNS-Weiterleitung zum Auflösen von nicht-Appliance DNS-Namen in Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2f707d4c681c695105daf23d5fc640279bb83658
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names-in-analytics-platform-system"></a>Verwenden Sie nicht Appliance DNS-Namen in Analytics Platform System Auflösen einer DNS-Weiterleitungsservers
DNS-Weiterleitung für die Active Directory-Domänendienste-Knoten konfiguriert werden kann (***Appliance_domain *-AD01** und ***Appliance_domain *-AD02**) der Appliance Analytics Platform System zu ermöglichen Skripts und softwareanwendungen auf externe Servern zugreifen.  
  
## <a name="ResolveDNS"></a>Mithilfe einer DNS-Weiterleitungsservers  
Das Analytics Platform System-Gerät ist konfiguriert, um zu verhindern, Auflösen von DNS-Namen der Server, die nicht in der Einheit befinden. Einige Prozesse, z. B. Windows Software Update Services (WSUS) müssen auf Servern außerhalb der Appliance zugreifen. Um dieses Verwendungsszenario das Analytics Platform System DNS unterstützen können konfiguriert werden um eine externen Namen-Weiterleitung zu unterstützen, die Analytics Platform System-Hosts und virtuellen Computern (VMs), externen DNS-Server zum Auflösen von Namen außerhalb der Anwendung verwendet werden kann. Benutzerdefinierte Konfiguration von DNS-Suffixe wird nicht unterstützt, was bedeutet, dass Sie vollständig qualifizierte Domänennamen verwenden müssen, um einen nicht-Appliance-Servernamen zu beheben.  
  
**So erstellen Sie DNS-Weiterleitung mit der DNS-GUI**  
  
1.  Melden Sie sich an den ***Appliance_domain *-AD01** Knoten.  
  
2.  Öffnen Sie den DNS-Manager (**dnsmgmt.msc**).  
  
3.  Mit der rechten Maustaste in des Namens des Servers, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Auf der **erweitert** Registerkarte, heben Sie die Auswahl der **Rekursion (Weiterleitungen) deaktivieren** aus, und klicken Sie dann auf **übernehmen**.)  
  
5.  Klicken Sie auf die **Weiterleitungen** Registerkarte, und klicken Sie dann auf **bearbeiten**.  
  
6.  Geben Sie die IP-Adresse für den externen DNS-Server, der die namensauflösung bereitstellen. Der virtuelle Computer und Servern (Hosts) in der Einheit verbindet mit externen Servern mit vollqualifizierten Domänennamen.  
  
7.  Wiederholen Sie die Schritte 1 bis 6 für die ***Appliance_domain *-AD02** Knoten  
  
**So erstellen Sie eine DNS-Weiterleitung mit Windows PowerShell**  
  
1.  Melden Sie sich an den ***Appliance_domain *-AD01**Knoten.  
  
2.  Führen Sie das folgende Windows PowerShell-Skript aus der ***Appliance_domain *-AD01** Knoten. Ersetzen Sie vor dem Ausführen der Windows PowerShell-Skript, IP-Adressen mit der IP-Adressen Ihrer DNS-Server von nicht-Appliance.  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  Führen Sie den gleichen Befehl auf dem ***Appliance_domain *-AD02** Knoten.  
  
## <a name="configuring-dns-resolution-for-wsus"></a>Konfigurieren von DNS-Auflösung für WSUS  
SQL Server PDW 2012 bietet integrierte Wartung und Patchen Funktionalität. SQL Server PDW verwendet Microsoft Update und andere Microsoft-Technologien Wartung. Um Updates zu aktivieren muss die Anwendung entweder in einem Unternehmen WSUS-Repository oder den öffentlichen Microsoft-WSUS-Repository herstellen.  
  
Für Kunden, die das Gerät zum Suchen nach Updates auf die öffentlichen Microsoft-WSUS-Repositorys konfigurieren, festgelegt in den folgenden Anweisungen die richtigen Konfigurationsdetails auf dem Gerät an.  
  
> [!NOTE]  
> Der Netzwerkadministrator Kunden muss die IP-Adresse angeben, für den Unternehmens-DNS-Server, die am Namen auflösen kann **"Microsoft.com"**.  
  
1.  Mithilfe des Remotedesktops, melden Sie sich bei der VMM-VM (<fabric domain>– VMM) mit dem Fabric-Domänenadministratorkonto.  
  
2.  Öffnen Sie die Systemsteuerung, klicken Sie auf **Netzwerk und Internet**, und klicken Sie dann auf **Netzwerk- und Freigabecenter**.  
  
3.  Klicken Sie in der Liste der dienstanwendungsverbindungen auf **VMSEthernet**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Wählen Sie **Internet Protocol Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**.  
  
5.  In der **alternativer DNS-Server** hinzu, und die IP-Adresse, die vom Netzwerkadministrator Kunden bereitgestellt.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
