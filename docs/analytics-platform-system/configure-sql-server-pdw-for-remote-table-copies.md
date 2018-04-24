---
title: Parallel Data Warehouse für die Remotetabelle Kopien konfigurieren | Microsoft Docs
description: Beschreibt, wie so konfigurieren Sie Parallel Data Warehouse, um die Remotetabelle Copy-Funktion verwenden, um Tabellen in SMP SQL Server-Datenbanken auf nicht-Appliance-Servern zu kopieren.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3f71a0c67639918820bca8f6f8f38b9f354154f3
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>Konfigurieren Sie für die Remotetabelle Kopien Parallel Data Warehouse
Beschreibt das Konfigurieren von SQL Server PDW Verwendung die Funktion zum Kopieren von Remotetabelle um Tabellen SMP SQL Server-Datenbanken auf nicht-Appliance-Servern zu kopieren.  
  
Dieses Thema beschreibt eine der Konfigurationsschritte zum Konfigurieren von remote-Tabelle kopieren. Eine Übersicht über die Konfigurationsschritte finden Sie unter [Remotekopie Tabelle](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Vorbereitungen  
Konfigurieren Sie SQL Server PDW um Remotetabelle Kopie verwenden möchten, müssen Sie folgende Aktionen ausführen:  
  
-   Haben Sie ein Administratorkonto Analytics Platform System mit der Möglichkeit, melden Sie direkt in der ***Appliance_domain *-AD01** und ***Appliance_domain *-AD02** Knoten.  
  
-   Kennen Sie den Hostnamen oder die IP-Name des Zielservers an.  
  
## <a name="HowToPDW"></a>Konfigurieren von SQLServer PDW Remotetabelle Kopie: Aktualisieren von Hostnamen in DNS  
Die **CREATE REMOTE TABLE** -Anweisung, zum Remotetabelle Kopien, gibt den Zielserver mithilfe der IP-Adresse oder der IP-Name des Systems SMP-Windows. Um die IP-Namen zu verwenden, müssen Sie Einträge für die erfolgreiche namensauflösung der DNS-Server hinzufügen.  
  
Die folgenden Schritte beschreiben, wie den DNS-Server aktualisiert wird.  
  
1.  Melden Sie sich bei dem aktiven Knoten des AD (normalerweise ***Appliance_domain *-AD01**).  
  
2.  Öffnen Sie den DNS-Manager. Diese befindet sich unter **Verwaltung** in der **starten** Menü.  
  
3.  Verwenden Sie die DNS-Manager, um die IP-Namen hinzuzufügen.  
  
## <a name="see-also"></a>Siehe auch  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Verwenden Sie nicht-Appliance DNS-Namen auflösen einer DNS-Weiterleitungsservers](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
