---
title: Abonnementablauf und -deaktivierung | Microsoft Dokumentation
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Distributors [SQL Server replication], distribution retention period
- subscriptions [SQL Server replication], expiration
- publications [SQL Server replication], publication retention periods
- expiration [SQL Server replication]
- retention periods [SQL Server replication]
- publication retention periods
- distribution retention period
- subscriptions [SQL Server replication], deactivation
- deactivating subscriptions
ms.assetid: 4d03f5ab-e721-4f56-aebc-60f6a56c1e07
caps.latest.revision: 45
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 515871c28dbb8f7b3000b02b86a50c61b55d403f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="subscription-expiration-and-deactivation"></a>Abonnementablauf und -deaktivierung
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Abonnements können deaktiviert werden oder ablaufen, wenn sie nicht innerhalb einer angegebenen *Beibehaltungsdauer*synchronisiert werden. Die stattfindende Aktion hängt vom Typ der Replikation und der überschrittenen Beibehaltungsdauer ab.  
  
 Weitere Informationen zum Festlegen von Beibehaltungsdauern finden Sie unter [Festlegen des Ablaufdatums für Abonnements](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md), [Festlegen der Beibehaltungsdauer für die Verteilung bei Transaktionsveröffentlichungen &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/set-distribution-retention-period-for-transactional-publications.md), und [Verleger- und Verteilereigenschaften](../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
## <a name="transactional-replication"></a>Transaktionsreplikation  
 Die Transaktionsreplikation verwendet die maximale Beibehaltungsdauer für die Verteilung (die **@max_distretention**-Parameter von [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)) und die Beibehaltungsdauer für die Veröffentlichung (die **@retention**-Parameter von [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)):  
  
-   Falls ein Abonnement nicht innerhalb der maximalen Beibehaltungsdauer für die Verteilung (standardmäßig 72 Stunden) synchronisiert wird und Änderungen in der Verteilungsdatenbank vorliegen, die noch nicht an den Abonnenten übermittelt wurden, wird das Abonnement vom Auftrag **Verteilungscleanup** , der auf dem Verteiler ausgeführt wird, als deaktiviert gekennzeichnet. Das Abonnement muss erneut initialisiert werden.  
  
-   Falls ein Abonnement nicht innerhalb der Beibehaltungsdauer für die Veröffentlichung (standardmäßig 336 Stunden) synchronisiert wird, läuft das Abonnement ab und wird vom Auftrag **Cleanup abgelaufener Abonnements** gelöscht, der auf dem Verleger ausgeführt wird. Das Abonnement muss neu erstellt und synchronisiert werden.  
  
     Wenn ein Pushabonnement abläuft, wird es vollständig entfernt. Bei Pullabonnements ist dies nicht der Fall. Sie müssen einen Cleanup der Pullabonnements auf dem Abonnenten ausführen. Weitere Informationen finden Sie unter [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
## <a name="merge-replication"></a>Mergereplikation  
 Bei der Mergereplikation wird die Beibehaltungsdauer der Veröffentlichung (die **@retention** und **@retention_period_unit**-Parameter von [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)) verwendet. Wenn ein Abonnement abläuft, muss es erneut initialisiert werden, da Metadaten für das Abonnement entfernt werden. Abonnements, die nicht erneut initialisiert werden, werden vom Auftrag **Cleanup abgelaufener Abonnements** gelöscht, der auf dem Verleger ausgeführt wird. Dieser Auftrag wird standardmäßig einmal pro Tag ausgeführt, und es werden dabei alle Pushabonnements gelöscht, die seit einem Zeitraum, der der doppelten Beibehaltungsdauer der Veröffentlichung entspricht, nicht synchronisiert wurden. Zum Beispiel:  
  
-   Wenn eine Veröffentlichung eine Beibehaltungsdauer von 14 Tagen aufweist, kann ein Abonnement ablaufen, wenn es nicht innerhalb von 14 Tagen synchronisiert wurde.  
  
     Wenn auf dem Verleger [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder eine höhere Version ausgeführt wird und der Agent für das Abonnement aus [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder einer höheren Version stammt, läuft ein Abonnement nur ab, wenn Änderungen an den Daten in der Partition dieses Abonnements vorgenommen wurden. Nehmen wir beispielsweise an, dass ein Abonnent Kundendaten nur für Kunden in Deutschland empfängt. Falls die Beibehaltungsdauer auf 14 Tage festgelegt wurde, läuft das Abonnement nur dann am Tag 14 ab, wenn während der letzten 14 Tage Änderungen an den deutschen Kundendaten vorgenommen wurden.  
  
-   14 bis 27 Tage nach der letzten Synchronisierung kann das Abonnement erneut initialisiert werden.  
  
-   28 Tage nach der letzten Synchronisierung wird das Abonnement vom Auftrag **Cleanup abgelaufener Abonnements** gelöscht. Wenn ein Pushabonnement abläuft, wird es vollständig entfernt. Bei Pullabonnements ist dies nicht der Fall. Sie müssen einen Cleanup der Pullabonnements auf dem Abonnenten ausführen. Weitere Informationen finden Sie unter [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
### <a name="considerations-for-setting-the-publication-retention-period-for-merge-publications"></a>Überlegungen für das Festlegen der Beibehaltungsdauer der Veröffentlichung für Mergeveröffentlichungen  
 Beachten Sie bei der Festlegung der Beibehaltungsdauer für Mergeveröffentlichungen Folgendes:  
  
-   Die Beibehaltungsdauer für Mergeveröffentlichungen weist eine 24-stündige Kulanzfrist auf, um Abonnenten in unterschiedlichen Zeitzonen aufzunehmen. Wenn Sie beispielsweise eine Beibehaltungsdauer von einem Tag festgelegt haben, beträgt die tatsächliche Beibehaltungsdauer 48 Stunden.  
  
-   Der Cleanup der Metadaten für die Mergereplikation hängt von der Beibehaltungsdauer der Veröffentlichung ab:  
  
    -   Die Replikation kann der Cleanup von Metadaten aus den Veröffentlichungs- und Abonnementdatenbanken erst ausführen, wenn das Ablaufdatum erreicht ist. Geben Sie keinen zu hohen Wert für die Beibehaltungsdauer an, da dies zu einer Beeinträchtigung der Replikationsleistung führen kann. Es wird empfohlen, eine niedrigere Einstellung zu verwenden, wenn Sie zuverlässig einschätzen können, dass alle Abonnenten innerhalb dieser Zeitspanne regelmäßig synchronisiert werden.  
  
    -   Es ist möglich anzugeben, dass die Abonnements nie ablaufen (Wert 0 für **@retention**), aber es wird dringend empfohlen, diesen Wert nicht zu verwenden, da kein Cleanup der Metadaten durchgeführt werden darf.  
  
-   Die Beibehaltungsdauer für alle Wiederveröffentlichungen muss auf einen Wert festgelegt werden, der gleich oder niedriger ist als die auf dem ursprünglichen Verleger festgelegte Beibehaltungsdauer. Verwenden Sie zudem dieselben Beibehaltungsdauerwerte für Veröffentlichungen für alle Verleger und ihre alternativen Synchronisierungspartner. Das Verwenden unterschiedlicher Werte kann zu mangelnder Konvergenz der Daten führen. Wenn Sie die Beibehaltungsdauer der Veröffentlichung ändern müssen, sollten Sie den Abonnenten erneut initialisieren, um sicherzustellen, dass die Daten konvergieren.  
  
-   Wenn die Beibehaltungsdauer der Veröffentlichung nach einem Cleanup erhöht wird und für ein Abonnement ein Mergevorgang mit dem Verleger versucht wird (auf dem die Metadaten bereits gelöscht wurden), dann läuft das Abonnement nicht ab, weil die Beibehaltungsdauer erhöht wurde. Allerdings verfügt der Verleger nicht über ausreichende Metadaten zum Herunterladen der Änderungen auf den Abonnenten. Dies führt zu mangelnder Konvergenz der Daten.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erneutes Initialisieren von Abonnements](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Replikations-Agent-Verwaltung](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
