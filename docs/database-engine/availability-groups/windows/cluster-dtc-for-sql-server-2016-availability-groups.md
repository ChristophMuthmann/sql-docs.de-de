---
title: "Cluster-DTC für SQL Server 2016-Verfügbarkeitsgruppen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/30/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a47c5005-20e3-4880-945c-9f78d311af7a
caps.latest.revision: "3"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b912f3496847bc915e62b616638a39d51218574d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="cluster-dtc-for-sql-server-2016-availability-groups"></a>Cluster-DTC für SQL Server 2016-Verfügbarkeitsgruppen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema werden die Anforderungen und Schritte zum Gruppieren des Microsoft DTC-Diensts (Distributed Transaction Coordinator) für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] beschrieben. Weitere Informationen zu verteilten Transaktionen und [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] finden Sie unter [Datenbankübergreifende Transaktionen und verteilte Transaktionen für Always On-Verfügbarkeitsgruppen oder Datenbankspiegelung (SQL Server)](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).

 ## <a name="checklist-preliminary-requirements"></a>Prüfliste: Vorbereitende Anforderungen
||Task|Verweis|  
|------|-----------------|----------|  
|![Kontrollkästchen](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Stellen Sie sicher, dass alle Knoten, Dienste und die Verfügbarkeitsgruppe ordnungsgemäß konfiguriert wurden.|[Voraussetzungen, Einschränkungen und Empfehlungen für Always On-Verfügbarkeitsgruppen (SQL Server)](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)|
|![Kontrollkästchen](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Stellen Sie sicher, dass die Anforderungen des Verfügbarkeitsgruppen-DTCs erfüllt wurden.|[Datenbankübergreifende Transaktionen und verteilte Transaktionen für Always On-Verfügbarkeitsgruppen oder Datenbankspiegelung (SQL Server)](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)

## <a name="checklist-clustered-dtc-resource-dependencies"></a>Prüfliste: Ressourcenabhängigkeiten für gruppierte DTCs
||Task|Verweis|  
|------|-----------------|----------|  
|![Kontrollkästchen](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Ein Laufwerk mit freigegebenem Speicher.|[Konfigurieren Sie das Laufwerk mit freigegebenem Speicher](https://msdn.microsoft.com/library/cc982358(v=bts.10).aspx). Erwägen Sie die Verwendung des Laufwerkbuchstabens **M**.|
|![Kontrollkästchen](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Eine eindeutige DTC-Netzwerknamenressource.  Der Name wird als Clustercomputerobjekt in Active Directory registriert.<br /><br />Stellen Sie sicher, dass eine der folgenden Aussagen zutrifft:<br /><br />• Der Benutzer, der die DTC-Netzwerknamenressource erstellt, verfügt über die Berechtigung zum Erstellen von Computerobjekten für die Organisationseinheit oder den Container, in dem die DTC-Netzwerknamenressource gespeichert wird.<br /><br />• Verfügt der Benutzer nicht über die Berechtigung zum Erstellen von Computerobjekten, bitten Sie einen Domänenadministrator, vorab ein Clustercomputerobjekt für die DTC-Netzwerknamenressource bereitzustellen.|[Vorabbereitstellung von Clustercomputerobjekten in Active Directory Domain Services](https://technet.microsoft.com/library/dn466519(v=ws.11).aspx)|
|![Kontrollkästchen](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Eine gültige verfügbare, statische IP-Adresse und die entsprechende Subnetzmaske für die IP-Adresse.||

## <a name="cluster-the-dtc-resource"></a>Gruppieren der DTC-Ressource
Nachdem Sie Ihre Verfügbarkeitsgruppenressource erstellt haben, erstellen Sie eine gruppierte DTC-Ressource, und fügen Sie sie der Verfügbarkeitsgruppe hinzu.  Ein Beispielskript finden Sie unter [Erstellen eines gruppierten DTCs für eine Always On-Verfügbarkeitsgruppe](../../../database-engine/availability-groups/windows/create-clustered-dtc-for-an-always-on-availability-group.md).


## <a name="checklist-post-clustered-dtc-resource-configurations"></a>Prüfliste: Bereitstellen von gruppierten DTC-Ressourcenkonfigurationen
||Task|Verweis|  
|------|-----------------|----------|  
|![Kontrollkästchen](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Aktivieren Sie den sicheren Netzwerkzugriff für die gruppierte DTC-Ressource.|[Sicheres Aktivieren des Netzwerkzugriffs für MS DTC](https://technet.microsoft.com/library/cc753620(v=ws.10).aspx)|
|![Kontrollkästchen](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Beenden und deaktivieren Sie den lokalen DTC-Dienst.|[Konfigurieren des Startvorgangs für einen Dienst](https://technet.microsoft.com/library/cc755249(v=ws.11).aspx)|
|![Kontrollkästchen](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Durchlaufen Sie den SQL Server-Dienst für jede Instanz in der Verfügbarkeitsgruppe.  Führen Sie bei Bedarf einen Failover für die Verfügbarkeitsgruppe aus.|[Ausführen eines geplanten manuellen Failovers einer Verfügbarkeitsgruppe (SQL Server)](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)<br /><br />[Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agent oder des SQL Server-Browsers](../../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)|

- Wenn es sich bei dem Betriebssystem um Windows Server 2012 R2 handelt, benötigen Sie unbedingt [KB 3030373](http://support.microsoft.com/kb/3090973) .

- Bereiten Sie die Server gemäß der Prüflisten unter [Voraussetzungen, Einschränkungen und Empfehlungen für Always On-Verfügbarkeitsgruppen](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md) für Verfügbarkeitsgruppen vor.

- Konfigurieren Sie die Serverinstanzen für [**Always On-Verfügbarkeitsgruppen**](../../../database-engine/availability-groups/windows/configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md).

### <a name="resources"></a>RESSOURCEN


[Weitere Informationen zum Testen von DTC für Verfügbarkeitsgruppen:](https://blogs.technet.microsoft.com/dataplatform/2016/01/25/sql-server-2016-dtc-support-in-availability-groups/)

[Überwachen der Katalogsichten von Always On-Verfügbarkeitsgruppen](monitor-availability-groups-transact-sql.md)

[Schritt-für-Schritt-Anleitung zum Erstellen von Verfügbarkeitsgruppen](create-an-availability-group-transact-sql.md)


[SQL Server 2016 DTC-Unterstützung in Verfügbarkeitsgruppen](http://blogs.technet.microsoft.com/dataplatform/2016/01/25/sql-server-2016-dtc-support-in-availability-groups/) 

[Externer Link: Konfigurieren von DTC für eine Clusterinstanz von SQL Server mit Windows Server 2008 R2](http://sqlha.com/2013/03/12/how-to-properly-configure-dtc-for-clustered-instances-of-sql-server-with-windows-server-2008-r2/)
