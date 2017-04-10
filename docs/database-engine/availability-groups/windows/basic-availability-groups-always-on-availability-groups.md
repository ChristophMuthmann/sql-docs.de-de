---
title: "Basis-Verf&#252;gbarkeitsgruppen (AlwaysOn-Verf&#252;gbarkeitsgruppen) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 285adbc7-ac9b-40f6-b4a9-3f1591d3b632
caps.latest.revision: 9
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 9
---
# Basis-Verf&#252;gbarkeitsgruppen (AlwaysOn-Verf&#252;gbarkeitsgruppen)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  AlwaysOn-Basis-Verfügbarkeitsgruppen bieten eine Lösung mit hoher Verfügbarkeit für SQL Server 2016 Standard Edition. Eine Basis-Verfügbarkeitsgruppe unterstützt eine Failoverumgebung für eine einzelne Datenbank. Sie wird mit Enterprise Edition erstellt und verwaltet, ähnlich wie traditionelle (erweiterte) [AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md). Die Unterschiede und Einschränkungen zwischen und für Basis-Verfügbarkeitsgruppen werden in diesem Dokument zusammengefasst.  
  
## Funktionen  
 AlwaysOn-Basis-Verfügbarkeitsgruppen ersetzen das veraltete Feature „Datenbankspiegelung“ und bieten ein ähnliches Level an Featureunterstützung. Basis-Verfügbarkeitsgruppen ermöglichen einer primären Datenbank, ein einzelnes Replikat beizubehalten. Dieses Replikat kann entweder den synchronen Commit-Modus oder den asynchronen Commit-Modus verwenden. Weitere Informationen zu Verfügbarkeitsmodi finden Sie unter [Verfügbarkeitsmodi &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md). Das sekundäre Replikat bleibt inaktiv, es sei denn, es muss ein Failover durchgeführt werden. Dieses Failover kehrt die primären und sekundären Rollenzuweisungen, und verursacht damit, dass das sekundäre Replikat zur primären aktiven Datenbank wird. Weitere Informationen zum Failover finden Sie unter [Failover und Failovermodi &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md). Basis-Verfügbarkeitsgruppen können in einer Hybridumgebung arbeiten, die die lokale und die Microsoft Azure-Umgebung umfasst.  
  
## Einschränkungen  
 Basis-Verfügbarkeitsgruppen verwenden eine Teilmenge der Funktionen verglichen mit erweiterten Verfügbarkeitsgruppen auf SQL Server 2016 Enterprise Edition. Basis-Verfügbarkeitsgruppen beinhalten die folgenden Einschränkungen:  
  
-   Beschränkung auf zwei Replikate (primäres und sekundäres)  
  
-   Kein Lesezugriff auf das sekundäre Replikat.  
  
-   Keine Sicherung auf das sekundäre Replikat.  
  
-   Keine Unterstützung für Replikate, die auf Servern gehostet werden, die eine Version von SQL Server vor SQL Server 2016 Community Technology Preview 3 (CTP3) ausführen.  
  
-   Keine Unterstützung für das Hinzufügen oder Entfernen eines Replikats an oder von einer vorhandenen Basis-Verfügbarkeitsgruppe.  
  
-   Unterstützung für eine Verfügbarkeitsdatenbank.  
  
-   Basis-Verfügbarkeitsgruppen können nicht zu erweiterten Verfügbarkeitsgruppen upgegradet werden. Die Gruppe muss gelöscht und erneut einer Gruppe hinzugefügt werden, die nur Server enthält, die SQL Server 2016 Enterprise Edition ausführen.  
  
-   Basis-Verfügbarkeitsgruppen werden nur für Standard Editions-Server unterstützt.  
  
## Konfiguration  
 Eine Basis-AlwaysOn-Verfügbarkeitsgruppe kann auf zwei beliebigen SQL Server 2016 Standard Edition-Servern erstellt werden. Wenn Sie eine Basis-Verfügbarkeitsgruppe erstellen, müssen Sie beide Replikate während der Erstellung angeben.  
  
 Verwenden Sie den Transact-SQL-Befehl **CREATE AVAILABILITY GROUP** um eine Basis-Verfügbarkeitsgruppe zu erstellen, und geben Sie die Option **WITH BASIC** an, (der Standard ist **ADVANCED**). Weitere Informationen finden Sie unter [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md). Zu diesem Zeitpunkt besteht keine Benutzeroberflächenunterstützung für die Erstellung von Basis-Verfügbarkeitsgruppen in SQL Server Management Studio.  
  
> [!NOTE]  
>  Die Einschränkungen von Basis-Verfügbarkeitsgruppen gelten für den Befehl **CREATE AVAILABILITY GROUP** wenn **WITH BASIC** angegeben ist. Beispielsweise erhalten Sie einen Fehler, wenn Sie versuchen, eine Basis-Verfügbarkeitsgruppe zu erstellen, die Lesezugriff zulässt. Andere Einschränkungen gelten in der gleichen Weise. Weitere Informationen finden Sie im Abschnitt „Einschränkungen“ dieses Themas.  
  
## Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  