---
title: "Verwenden des Assistenten zum Hinzufügen von Azure-Replikaten (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.addreplicawizard.azurereplica.f1
ms.assetid: b89cc41b-07b4-49f3-82cc-bc42b2e793ae
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 24b3e9ec3cded630a18fef353ccaad3b5a2912b1
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="use-the-add-azure-replica-wizard-sql-server"></a>Verwenden des Assistenten zum Hinzufügen von Azure-Replikaten (SQL Server)
  Der Assistent zum Hinzufügen von Azure-Replikaten unterstützt Sie dabei, einen neuen virtuellen Microsoft Azure-Computer in einer hybriden IT-Umgebung zu erstellen und als sekundäres Replikat für eine neue oder vorhandene Always On-Verfügbarkeitsgruppe zu konfigurieren.  
  
-   **Vorbereitungen:**  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Sicherheit](#Security)  
  
-   **Fügen Sie ein Replikat hinzu mit:**  [Assistent zum Hinzufügen von Azure-Replikaten (SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
 Wenn Sie einer Verfügbarkeitsgruppe noch kein Verfügbarkeitsreplikat hinzugefügt haben, sollten Sie sich zuvor im Thema [Voraussetzungen, Einschränkungen und Empfehlungen für Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)in den Abschnitten „Serverinstanzen“ und „Verfügbarkeitsgruppen und -replikate“ informieren.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Sie müssen mit der Serverinstanz verbunden sein, auf der das aktuelle primäre Replikat gehostet wird.  
  
-   Sie benötigen eine hybride IT-Umgebung, in der das lokale Subnetz über ein Standort-zu-Standort-VPN mit Windows Azure verbunden ist. Weitere Informationen finden Sie unter [Konfigurieren eines Standort-zu-Standort-VPNs im Verwaltungsportal](https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-site-to-site-create).  
  
-   Ihre Verfügbarkeitsgruppe muss lokale Verfügbarkeitsreplikate enthalten.  
  
-   Clients des Verfügbarkeitsgruppenlisteners müssen über Internetverbindungen verfügen, falls sie mit dem Listener verbunden bleiben sollen, wenn für die Verfügbarkeitsgruppe ein Failover auf ein Windows Azure-Replikat ausgeführt wird.  
  
-   **Voraussetzungen für die Verwendung der vollständigen anfänglichen Datensynchronisierung** : Sie müssen eine Netzwerkfreigabe angeben, damit der Assistent Sicherungen erstellen und darauf zugreifen kann. Für das primäre Replikat kann das zum Starten von [!INCLUDE[ssDE](../../../includes/ssde-md.md)] verwendete Konto über Lese- und Schreibberechtigungen für das Dateisystem in einer Netzwerkfreigabe verfügen. Bei sekundären Replikaten muss das Konto über eine Leseberechtigung für die Netzwerkfreigabe verfügen.  
  
     Wenn Sie nicht den Assistenten für eine vollständige anfängliche Datensynchronisierung verwenden können, müssen Sie die sekundären Datenbanken manuell vorbereiten. Dies ist vor oder nach dem Ausführen des Assistenten möglich. Weitere Informationen finden Sie unter [Manuelles Vorbereiten einer sekundären Datenbank auf eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)erstellt und konfiguriert wird.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Siehe [Security](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md#Security)  
  
##  <a name="SSMSProcedure"></a> Verwenden des Assistenten zum Hinzufügen von Azure-Replikaten (SQL Server Management Studio)  
 Der Assistent zum Hinzufügen von Azure-Replikaten kann auf der Seite [Replikate angeben](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md)gestartet werden. Die Seite kann auf zwei Weisen aufgerufen werden:  
  
-   [Verwenden des Assistenten für Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Verwenden des Assistenten zum Hinzufügen von Replikaten zu Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 Nachdem Sie den Assistenten zum Hinzufügen von Azure-Replikaten gestartet haben, führen Sie die folgenden Schritte aus:  
  
1.  Laden Sie zunächst ein Verwaltungszertifikat für Ihr Windows Azure-Abonnement herunter. Klicken Sie auf **Herunterladen** , um die Anmeldeseite zu öffnen.  
  
2.  Melden Sie sich bei Microsoft Azure mit Ihrem Microsoft-Konto oder Unternehmenskonto an. Ihr Microsoft- oder Unternehmenskonto hat das Format einer E-Mail-Adresse, z.B. HYPERLINK „mailto:patc@contoso.com“ patc@contoso.com. Weitere Informationen zu Azure-Anmeldeinformationen finden Sie unter [Microsoft-Konto für Organisationen – Häufig gestellte Fragen](http://technet.microsoft.com/jj592903) und [Behandeln von Problemen mit der Anmeldung bei Ihrem Unternehmenskonto](https://support.microsoft.com/kb/2756852).  
  
3.  Stellen Sie als Nächstes eine Verbindung mit dem Abonnement her, indem Sie auf **Verbinden**klicken. Sobald die Verbindung hergestellt ist, werden die Dropdownlisten mit den Microsoft Azure-Parametern, wie **Virtuelles Netzwerk** und **Virtuelles Netzwerk – Subnetz**, aufgefüllt.  
  
4.  Geben Sie die Einstellungen für die Windows Azure-VM an, die das neue sekundäre Replikat hostet:  
  
     Bild  
     Der Name des SQL Server-Images, das für die Windows Azure-VM verwendet werden soll.  
  
     VM-Größe  
     Die Größe der Windows Azure-VM.  
  
     VM-Name  
     Der DNS-Name der Windows Azure-VM.  
  
     VM-Benutzername  
     Der Benutzername des Standardadministrators für die Windows Azure-VM.  
  
     VM-Administratorkennwort (und Kennwortbestätigung)  
     Das Kennwort des Standardadministrators für die Windows Azure-VM.  
  
     Virtuelles Netzwerk  
     Das virtuelle Netzwerk, in das die Windows Azure-VM eingefügt werden soll.  
  
     Virtuelles Netzwerk – Subnetz  
     Das Subnetz des virtuellen Netzwerks, in das die Windows Azure-VM eingefügt werden soll.  
  
     Domäne  
     Die Active Directory (AD)-Domäne, mit der die Windows Azure-VM verknüpft werden soll.  
  
     Domänenbenutzername  
     Der AD-Benutzername, über den die Windows Azure-VM mit der Domäne verknüpft wird.  
  
     Kennwort  
     Das Kennwort, über das die Windows Azure-VM mit der Domäne verknüpft wird.  
  
5.  Klicken Sie auf **OK** , um Ihre Einstellungen zu bestätigen und den Assistenten zum Hinzufügen von Azure-Replikaten zu beenden.  
  
6.  Führen Sie die übrigen Konfigurationsschritte auf der Seite [Replikate angeben](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) wie für jedes neue Replikat aus.  
  
     Sobald Sie den Assistenten für neue Verfügbarkeitsgruppen oder den Assistenten zum Hinzufügen von Replikaten zu Verfügbarkeitsgruppen abgeschlossen haben, führt der Konfigurationsprozess alle notwendigen Vorgänge in Microsoft Azure aus, um den neuen virtuellen Computer zu erstellen, mit der AD-Domäne zu verknüpfen, dem Windows-Cluster hinzuzufügen, hohe Verfügbarkeit mit Always On zu aktivieren und das neue Replikat der Verfügbarkeitsgruppe hinzuzufügen.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Hinzufügen eines sekundären Replikats zu einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Voraussetzungen, Einschränkungen und Empfehlungen für Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Hinzufügen eines sekundären Replikats zu einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  

