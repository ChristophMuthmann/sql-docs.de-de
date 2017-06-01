---
title: "Erweiterte Konflikterkennung und -lösung bei der Mergereplikation | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], about conflict resolution
- default conflict resolver
- column-level conflict tracking
- row-level conflict tracking
- viewing merge replication conflicts
- resolving merge replication conflicts
- logical record-level conflict tracking [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 063d3d9c-ccb5-4fab-9d0c-c675997428b4
caps.latest.revision: 46
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: be8f8a4e1df903cc70191dc582ce2aef19e7e7aa
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="advanced-merge-replication---conflict-detection-and-resolution"></a>Erweiterte Konflikterkennung und -lösung bei der Mergereplikation
  Wenn zwischen einem Verleger und einem Abonnenten eine Verbindung besteht und die Synchronisierung vorgenommen wird, werden jegliche Konflikte vom Merge-Agent erkannt. Wenn Konflikte erkannt werden, verwendet der Merge-Agent einen Konfliktlöser (der angegeben wird, wenn ein Artikel einer Veröffentlichung hinzugefügt wird), um festzustellen, welche Daten akzeptiert und an andere Sites weitergegeben werden.  
  
> [!NOTE]  
>  Obwohl ein Abonnent mit dem Verleger synchronisiert wird, treten Konflikte normalerweise zwischen den Updates auf, die bei verschiedenen Abonnenten erfolgen, und nicht bei Updates, die bei einem Abonnenten und bei dem Verleger ausgeführt werden.  
  
 Das Verhalten der Konflikterkennung und -lösung ist von folgenden in diesem Thema beschriebenen Optionen abhängig:  
  
-   Angabe der Nachverfolgung auf Spaltenebene, auf Zeilenebene oder auf der Ebene des logischen Datensatzes.  
  
-   Angabe der standardmäßigen prioritätsbasierten Mechanismen zur Konfliktlösung oder Angabe eines Artikelkonfliktlösers. Als Artikelkonfliktlöser kommen infrage:  
  
    -   Ein in verwaltetem Code geschriebener *Geschäftslogikhandler*  
  
    -   Ein COM-basierter *benutzerdefinierter Konfliktlöser*  
  
    -   Ein von [!INCLUDE[msCoName](../../../includes/msconame-md.md)]bereitgestellter COM-basierter Konfliktlöser  
  
     Wenn der standardmäßige Mechanismus zur Konfliktlösung verwendet wird, wird das Verhalten durch den verwendeten Abonnementtyp, Client oder Server, näher bestimmt.  
  
## <a name="conflict-detection"></a>Konflikterkennung  
 Ob eine Datenänderung als Konflikt in Betracht kommt oder nicht ist vom Typ der für den Artikel festgelegten Konfliktnachverfolgung abhängig:  
  
-   Wenn Sie die Konfliktnachverfolgung auf Spaltenebene auswählen, wird eine Änderung als Konflikt eingestuft, wenn die Änderungen in derselben Spalte und derselben Zeile auf mehreren Replikationsknoten vorgenommen wurden.  
  
-   Wenn Sie die Nachverfolgung auf Zeilenebene auswählen, wird ein Konflikt verursacht, wenn Änderungen in beliebigen Spalten derselben Zeilen auf mehreren Replikationsknoten vorgenommen wurden (die betroffenen Spalten in den entsprechenden Zeilen müssen identisch sein).  
  
-   Wenn Sie die Nachverfolgung auf der Ebene des logischen Datensatzes auswählen, wird ein Konflikt verursacht, wenn Änderungen in beliebigen Zeilen desselben logischen Datensatzes auf mehreren Replikationsknoten vorgenommen wurden (die betroffenen Spalten in den entsprechenden Zeilen müssen identisch sein).  
  
 Weitere Informationen finden Sie unter [Ermitteln und Lösen von Konflikten in logischen Datensätzen](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md).  
  
 Informationen zum Eingeben der Konfliktnachverfolgungs- und -lösungsebene für einen Artikel finden Sie unter [Geben Sie den Konflikt nachverfolgen und-lösungsebene für Mergeveröffentlichungen](../../../relational-databases/replication/publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md).  
  
## <a name="conflict-resolution"></a>Konfliktlösung  
 Wenn ein Konflikt erkannt wird, startet der Merge-Agent den ausgewählten Konfliktlöser und verwendet diesen zur Bestimmung des Konfliktgewinners. Die Gewinnerzeile wird auf dem Verleger und auf dem Abonnenten angewendet, und die Daten der verlierenden Zeile werden in eine Konflikttabelle geschrieben. Konflikte werden direkt nach dem Ausführen des Konfliktlösers gelöst, es sei denn, Sie haben angegeben, dass Konflikte interaktiv gelöst werden sollen.  
  
### <a name="resolver-types"></a>Konfliktlösertypen  
 Bei der Mergereplikation erfolgt die Konfliktlösung auf Artikelebene. Bei Veröffentlichungen, die sich aus mehreren Artikeln zusammensetzen, ist die Verwendung unterschiedlicher Konfliktlöser für verschiedene Artikel oder desselben Konfliktlösers für einen Artikel, mehrere Artikel oder alle Artikel möglich, die zu einer Veröffentlichung gehören.  
  
 Wenn Sie den prioritätsbasierten Standardkonfliktlöser verwenden möchten, müssen Sie die Resolver-Eigenschaft eines Artikels nicht festlegen. Wenn ein Artikelkonfliktlöser anstatt des Standardkonfliktlösers verwendet werden soll, müssen Sie die Resolver-Eigenschaft für den jeweiligen Artikel festlegen, indem Sie einen verfügbaren Konfliktlöser auf dem Verleger auswählen. Spezielle Informationen, die an den Konfliktlöser weitergegeben werden müssen, können auch in der Eigenschaft für die Konfliktlöserinformationen angegeben werden.  
  
 Für die Mergereplikation stehen vier Arten von Konfliktlösern zur Verfügung:  
  
-   Der prioritätsbasierte Standardkonfliktlöser  
  
     Der standardmäßige Konfliktlösungsmechanismus weist unterschiedliche Verhaltensweisen auf, je nachdem, ob es sich beim Abonnement um ein Client- oder ein Serverabonnement handelt. Sie können einzelnen Abonnenten, auf denen Serverabonnements verwendet werden, Priority-Werte zuweisen. Änderungen, die auf dem Knoten mit dem höchsten Priority-Wert vorgenommen werden, gewinnen alle Konflikte. Bei Clientabonnements gewinnt die Änderung den Konflikt, die zuerst auf den Verleger geschrieben wurde.  
  
     Nach der Erstellung eines Abonnements kann der zugehörige Abonnementtyp nicht mehr geändert werden.  
  
-   Ein Geschäftslogikhandler  
  
     Im Geschäftslogikhandler können Sie eine Assembly in verwaltetem Code schreiben, die während des Mergesynchronisierungsvorgangs aufgerufen wird. Die Assembly enthält eine Geschäftslogik, die während der Synchronisierung auf Konflikte und mehrere andere Bedingungen reagieren kann. Weitere Informationen finden Sie unter [Ausführen von Geschäftslogik während der Mergesynchronisierung](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
-   Ein COM-basierter benutzerdefinierter Konfliktlöser  
  
     Die Mergereplikation stellt eine API bereit, mit der Konfliktlöser als COM-Objekte in Programmiersprachen, z. B. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vcprvc](../../../includes/vcprvc-md.md)] oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)], geschrieben werden können. Weitere Informationen finden Sie unter [COM-basierte benutzerdefinierte Konfliktlöser](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md).  
  
-   Ein von [!INCLUDE[msCoName](../../../includes/msconame-md.md)]bereitgestellter COM-basierter Konfliktlöser  
  
     [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] enthält mehrere COM-basierte Konfliktlöser. Weitere Informationen finden Sie unter [Microsoft COM-basierte Konfliktlöser](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
 Informationen zum Auswählen des geeigneten Konfliktlösertyps finden Sie unter [Auswählen von Resolvern](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-choose-a-resolver.md).  
  
> [!NOTE]  
>  Einige Artikelkonfliktlöser wurden geschrieben, um nur Konflikte für bestimmte Operationen zu verarbeiten. So verarbeitet ein Konfliktlöser beispielsweise Updates, nicht jedoch Einfüge- oder Löschvorgänge. Der prioritätsbasierte Standardkonfliktlöser verarbeitet alle Konflikte, die nicht vom Artikelkonfliktlöser bearbeitet werden.  
  
 Information zum Angeben eines Mergeabonnementtyps und einer Konfliktlösungspriorität finden Sie im entsprechenden Artikel.  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Specify a Merge Subscription Type and Conflict Resolution Priority &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md)  
  
-   Replikations- [!INCLUDE[tsql](../../../includes/tsql-md.md)] - und Replication Management Objects-Programmierung (RMO): [Erstellen eines Pullabonnements](../../../relational-databases/replication/create-a-pull-subscription.md) und [Erstellen eines Pushabonnements](../../../relational-databases/replication/create-a-push-subscription.md)  
  
### <a name="interactive-resolver"></a>Interaktiver Konfliktlöser  
 Die Replikation stellt eine Benutzeroberfläche für den interaktiven Konfliktlöser bereit, die in Verbindung mit dem prioritätsbasierten Standardkonfliktlöser oder mit einem Artikelkonfliktlöser verwendet werden kann. Bei der Ausführung einer bedarfsgesteuerten Synchronisierung mit der Synchronisierungsverwaltung von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows zeigt der interaktive Konfliktlöser Konfliktdaten in Laufzeit an und bietet Ihnen die Möglichkeit, die Art der Konfliktlösung auszuwählen. Weitere Informationen zum Aktivieren der interaktiven Konfliktlösung und zum Starten des interaktiven Konfliktlösers finden Sie unter [Interaktive Konfliktlösung](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
## <a name="viewing-conflicts"></a>Anzeigen von Konflikten  
 Die einfachste Möglichkeit zum Anzeigen von Konflikten ist die Verwendung des Replikationskonflikt-Viewers, der in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] verfügbar ist ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bietet ebenfalls gespeicherte Prozeduren, mit denen die Konflikttabellen abgefragt werden können). Der Konflikt-Viewer und die interaktive Konfliktlöser sind ähnliche Tools, im interaktiven Konfliktlöser können Sie jedoch bei der Synchronisierung Konflikte lösen, während der Konflikt-Viewer für die Anzeige von Konflikten nach der Konfliktlösung bestimmt ist. Wenn die Konfliktmetadaten weiterhin in den Systemtabellen verfügbar sind (Konfliktmetadaten werden standardmäßig 14 Tage lang beibehalten), können Sie die Ergebnisse der Konfliktlösung überschreiben. Wenn jedoch regelmäßig ein direktes Eingreifen erforderlich ist, sollten Sie die Verwendung des interaktiven Konfliktlösers in Betracht ziehen.  
  
> [!NOTE]  
>  Konflikte, die logische Datensätze einschließen, werden im Konflikt-Viewer nicht angezeigt. Mit den gespeicherten Replikationsprozeduren können Informationen zu diesen Konflikten angezeigt werden. Weitere Informationen finden Sie unter [Anzeigen von Konfliktinformationen zu Mergeveröffentlichungen &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md).  
  
 Im Konflikt-Viewer werden Informationen aus drei Systemtabellen angezeigt:  
  
-   Die Replikation erstellt eine Konflikttabelle für jede Tabelle in einem Mergeartikel, deren Name das folgende Format aufweist: **MSmerge_conflict_\<PublicationName>_\<ArticleName>**.  
  
     Konflikttabellen weisen dieselbe Struktur auf wie die Tabellen, auf denen sie basieren. Eine Zeile in einer dieser Tabellen besteht aus der verlierenden Version einer Konfliktzeile (die gewinnende Version der Zeile befindet sich in der eigentlichen Benutzertabelle).  
  
-   Die **MSmerge_conflict_info** -Tabelle enthält Informationen zu allen Konflikten, einschließlich des Konflikttyps.  
  
-   Die **sysmergearticles** -Tabelle identifiziert die Benutzertabellen mit Konflikttabellen und stellt Informationen zu den Konflikttabellen bereit.  
  
 Standardmäßig werden Konfliktinformationen an den folgenden Orten gespeichert:  
  
-   Auf dem Verleger und Abonnenten, wenn die Veröffentlichung mindestens einen Kompatibilitätsgrad von 90RTM aufweist.  
  
-   Auf dem Verleger, wenn die Veröffentlichung einen geringeren Kompatibilitätsgrad als 80RTM aufweist.  
  
-   Auf dem Verleger, wenn auf den Abonnenten [!INCLUDE[ssEW](../../../includes/ssew-md.md)]ausgeführt wird. Konfliktdaten dürfen nicht auf Abonnenten mit [!INCLUDE[ssEW](../../../includes/ssew-md.md)] gespeichert werden.  
  
 **So zeigen Sie Konflikte an**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [View and Resolve Data Conflicts for Merge Publications &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   Replikation [!INCLUDE[tsql](../../../includes/tsql-md.md)] Programmierung: [Anzeigen von Konfliktinformationen zu Mergeveröffentlichungen &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Synchronisieren von Daten](../../../relational-databases/replication/synchronize-data.md)  
  
  
