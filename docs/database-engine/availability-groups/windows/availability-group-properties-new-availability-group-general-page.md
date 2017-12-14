---
title: "Eigenschaften der Verfügbarkeitsgruppe: Neue Verfügbarkeitsgruppe (Seite „Allgemein“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.availabilitygroupproperties.general.f1
ms.assetid: 9af5379f-91b8-4729-9f75-4a80242a30e9
caps.latest.revision: "15"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 49b34cb2867b26be38f9d6c9086f5ea038d8cbdc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="availability-group-properties-new-availability-group-general-page"></a>Eigenschaften der Verfügbarkeitsgruppe: Neue Verfügbarkeitsgruppe (Seite Allgemein)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Dieses Thema gilt für die Registerkarte **Allgemein** des Dialogfelds **Neue Verfügbarkeitsgruppe** und des Dialogfelds **Eigenschaften der Verfügbarkeitsgruppe**.  Das Dialogfeld **Neue Verfügbarkeitsgruppe** ermöglicht es Ihnen, eine neue Verfügbarkeitsgruppe zu erstellen, ohne den [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]zu verwenden. Das Dialogfeld **Eigenschaften der Verfügbarkeitsgruppe** ermöglicht es Ihnen, die Konfiguration einer vorhandenen Verfügbarkeitsgruppe anzuzeigen und zu ändern.  
  
 **So zeigen Sie Verfügbarkeitsgruppeneigenschaften an**  
  
-   [Anzeigen von Verfügbarkeitsgruppeneigenschaften &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
-   [Verwenden des Always On-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
 **Name der Verfügbarkeitsgruppe**  
 Der Name der Verfügbarkeitsgruppe. Dies ist ein vom Benutzer angegebener Name, der innerhalb des Windows Server-Failoverclusters (WSFC) eindeutig sein muss.  
  
## <a name="availability-databases"></a>Verfügbarkeitsdatenbanken  
 **Datenbankname**  
 Name einer Datenbank, die der Verfügbarkeitsgruppe hinzugefügt wurde.  
  
 **Hinzufügen**  
 Klicken Sie, um der Verfügbarkeitsgruppe eine Datenbank hinzuzufügen.  
  
 **Entfernen**  
 Klicken Sie, um eine ausgewählte Datenbank aus der Verfügbarkeitsgruppe zu entfernen.  
  
## <a name="availability-replicas"></a>Verfügbarkeitsreplikate  
 **Serverinstanz**  
 Entspricht dem Servernamen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz, die dieses Replikat hostet, sowie bei einer nicht standardmäßigen Instanz dem Instanznamen.  
  
 **Rolle**  
 **Primär**  
 Derzeit das primäre Replikat.  
  
 **Secondary**  
 Derzeit ein sekundäres Replikat.  
  
 **Wird aufgelöst**  
 Die Replikatrolle wird derzeit zur primären oder sekundären Rolle aufgelöst.  
  
 **Verfügbarkeitsmodus**  
 Der Verfügbarkeitsmodus des Replikats. Folgende Werte sind möglich:  
  
 **Asynchroner Commit**  
 Das primäre Replikat kann einen Commit für Transaktionen ausführen, ohne das Schreiben des Protokolls auf den Datenträger durch das sekundäre Replikat abzuwarten.  
  
 **Synchroner Commit**  
 Das primäre Replikat wartet mit dem Ausführen des Commits für eine bestimmte Transaktion, bis das sekundäre Replikat die Transaktion auf den Datenträger geschrieben hat.  
  
 Weitere Informationen finden Sie unter [Verfügbarkeitsmodi &#40;Always On-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)ausgeführt wird.  
  
 **Failovermodus**  
 Der Failovermodus des Replikats. Folgende Werte sind möglich:  
  
 **Automatisch**  
 Automatisches Failover. Das Replikat ist ein Ziel für automatische Failover. Diese Option wird nur unterstützt, wenn der Verfügbarkeitsmodus auf synchrone Commits festgelegt wird.  
  
 **Manuell**  
 Manuelles Failover. Ein Failover des Replikats kann nur manuell vom Datenbankadministrator ausgeführt werden.  
  
 **Verbindungen in primärer Rolle**  
 Der unterstützte Clientverbindungstyp, wenn das Replikat die primäre Rolle besitzt.  
  
 **Alle Verbindungen zulassen**  
 Für die Datenbanken im primären Replikat sind alle Verbindungen zugelassen. Dies ist die Standardeinstellung.  
  
 **Verbindungen mit Lese-/Schreibzugriff zulassen**  
 Verbindungen, bei denen die Verbindungseigenschaft für den Anwendungszweck auf **ReadOnly** festgelegt ist, werden nicht zugelassen. Wenn die Eigenschaft für die Anwendungsabsicht auf **ReadWrite** festgelegt ist oder keine Verbindungseigenschaft für die Anwendungsabsicht festgelegt wurde, wird die Verbindung zugelassen. Weitere Informationen zur Verbindungseigenschaft für die Anwendungsabsicht finden Sie unter [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 **Lesbares sekundäres Replikat**  
 Gibt an, ob ein Verfügbarkeitsreplikat, das die sekundäre Rolle ausführt (also einem sekundären Replikat entspricht), Verbindungen von Clients zulassen kann. Folgende Werte sind möglich:  
  
 **Nein**  
 Es werden keine direkten Verbindungen mit sekundären Datenbanken dieses Replikats zugelassen. Sie sind für den Lesezugriff nicht verfügbar. Dies ist die Standardeinstellung.  
  
 **Nur beabsichtigte Lesevorgänge**  
 Es sind nur direkte, schreibgeschützte Verbindungen mit sekundären Datenbanken dieses Replikats zulässig. Die sekundären Datenbanken sind alle für Lesezugriff verfügbar.  
  
 **ja**  
 Alle Verbindungen zu sekundären Datenbanken dieses Replikats sind zugelassen, aber nur für Lesezugriff. Die sekundären Datenbanken sind alle für Lesezugriff verfügbar.  
  
 **Sitzungstimeout (Sekunden)**  
 Die Anzahl der Sekunden für das Sitzungstimeout auf diesem Replikat.  
  
 **Endpunkt-URL**  
 Die URL des Endpunkts. Informationen über das Format dieser URLs finden Sie unter [Angeben der Endpunkt-URL beim Hinzufügen oder Ändern eines Verfügbarkeitsreplikats &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md).  
  
 **Hinzufügen**  
 Klicken Sie, um ein sekundäres Replikat zur Verfügbarkeitsgruppe hinzuzufügen.  
  
 **Entfernen**  
 Klicken Sie, um ein sekundäres Replikat aus der Verfügbarkeitsgruppe zu entfernen.  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
