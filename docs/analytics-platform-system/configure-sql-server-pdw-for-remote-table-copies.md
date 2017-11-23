---
title: "Konfigurieren von SQLServer PDW für Remotetabelle Kopien (SQLServer PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 496b4214-5891-404c-8237-c2a1e09db6d5
caps.latest.revision: "11"
ms.openlocfilehash: 5daa546ed4cf0eeed1c51713fd9e55aa88515380
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="configure-sql-server-pdw-for-remote-table-copies"></a>Konfigurieren von SQLServer PDW für Kopien der Remotetabelle
Beschreibt das Konfigurieren von SQL Server PDW Verwendung die Funktion zum Kopieren von Remotetabelle um Tabellen SMP SQL Server-Datenbanken auf nicht-Appliance-Servern zu kopieren.  
  
Dieses Thema beschreibt eine der Konfigurationsschritte zum Konfigurieren von remote-Tabelle kopieren. Eine Übersicht über die Konfigurationsschritte finden Sie unter [Remotekopie Tabelle](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Vorbereitungen  
Konfigurieren Sie SQL Server PDW um Remotetabelle Kopie verwenden möchten, müssen Sie folgende Aktionen ausführen:  
  
-   Haben Sie ein Administratorkonto Analytics Platform System mit der Möglichkeit, melden Sie direkt in die  ***Appliance_domain*-AD01** und  ***Appliance_domain*-AD02** Knoten.  
  
-   Kennen Sie den Hostnamen oder die IP-Name des Zielservers an.  
  
## <a name="HowToPDW"></a>Konfigurieren von SQLServer PDW Remotetabelle Kopie: Aktualisieren von Hostnamen in DNS  
Die **CREATE REMOTE TABLE** -Anweisung, zum Remotetabelle Kopien, gibt den Zielserver mithilfe der IP-Adresse oder der IP-Name des Systems SMP-Windows. Um die IP-Namen zu verwenden, müssen Sie Einträge für die erfolgreiche namensauflösung der DNS-Server hinzufügen.  
  
Die folgenden Schritte beschreiben, wie den DNS-Server aktualisiert wird.  
  
1.  Melden Sie sich bei dem aktiven Knoten des AD (normalerweise  ***Appliance_domain*-AD01**).  
  
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
  
