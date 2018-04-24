---
title: Erstellen von Skripts für die Replikation | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- scripts [SQL Server replication], replication objects
- merge replication scripting [SQL Server replication]
- replication [SQL Server], scripting
- snapshot replication [SQL Server], scripting
- scripts [SQL Server replication]
- transactional replication, scripting
ms.assetid: e50fac44-54c0-470c-a4ea-9c111fa4322b
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4a2795e0bd6ffb1277dbb8e13f0d92616f34b577
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="scripting-replication"></a>Erstellen von Skripts für die Replikation
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Für die Replikationskomponenten in einer Topologie sollten im Rahmen des Plans zur Wiederherstellung im Notfall Skripts erstellt werden; diese können dann auch zur Automatisierung sich wiederholender Tasks verwendet werden. Skripts enthalten die gespeicherten Transact-SQL-Systemprozeduren, die zum Implementieren der Replikationskomponenten im Skript, wie z. B. der Veröffentlichungen oder Abonnements, benötigt werden. Skripts können nach dem Erstellen einer Komponente nicht mithilfe eines Assistenten (z. B. dem Assistenten für neue Veröffentlichung) oder in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] erstellt werden. Sie können das Skript mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder **sqlcmd**anzeigen, ändern oder ausführen. Skripts können mit Sicherungsdateien gespeichert und dann verwendet werden, wenn eine Replikationstopologie erneut konfiguriert werden muss.  
  
 Wenn die Eigenschaften einer Komponente geändert werden, muss das Skript für diese Komponente neu erstellt werden. Wenn Sie bei einer Transaktionsreplikation benutzerdefinierte gespeicherte Prozeduren verwenden, sollte zusammen mit den Skripts eine Kopie aller dieser Prozeduren gespeichert werden. Nach Änderungen an der Prozedur sollte die Kopie dann aktualisiert werden (zu Prozedurupdates kommt es in der Regel nach Schemaänderungen oder wenn sich die Anwendungsanforderungen ändern). Weitere Informationen zu benutzerdefinierten Prozeduren finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 Bei Mergeveröffentlichungen, die parametrisierte Filter verwenden, enthalten Veröffentlichungsskripts die Aufrufe von gespeicherten Prozeduren zum Erstellen von Datenpartitionen. Die Skripts stellen einen Verweis für die erstellten Partitionen bereit und ermöglichen das erneute Erstellen von Partitionen, falls dies erforderlich wird.  
  
## <a name="example-of-automating-a-task-with-scripts"></a>Beispiel für das Automatisieren einer Aufgabe durch Skripts  
 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]implementiert die Mergereplikation, um Daten an die Außendienstmitarbeiter zu verteilen. Ein Vertriebsmitarbeiter lädt mithilfe von Pullabonnements alle Informationen zu den Kunden in seinem Vertriebsgebiet herunter. Im Offlinebetrieb kann er die Daten aktualisieren und neue Kunden und Bestellungen eingeben. Da [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] über mehr als 50 Vertriebsmitarbeiter in verschiedenen Gebieten verfügt, wäre das Erstellen der verschiedenen Abonnements auf den einzelnen Abonnenten mit dem Assistenten für neue Abonnements recht zeitaufwendig. Stattdessen kann der Replikationsadministrator die folgenden Schritte ausführen:  
  
1.  Einrichten der notwendigen Mergeveröffentlichungen mit Partitionen nach Vertriebsmitarbeiter oder Vertriebsgebiet  
  
2.  Erstellen eines Pullabonnements für einen Abonnenten  
  
3.  Generieren eines Skripts auf der Grundlage dieses Pullabonnements  
  
4.  Ändern des Skripts durch Ändern von Werten, wie z. B. des Namens des Abonnenten  
  
5.  Ausführen des Skripts auf mehreren Abonnenten zum Generieren der erforderlichen Pullabonnements  
  
## <a name="script-replication-objects"></a>Skriptreplikationsobjekte  
 Das Erstellen von Skripts für Replikationsobjekte ist über die Replikations-Assistenten bzw. den Ordner **Replikation** in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]möglich. Wenn Sie die Skripterstellung über die Assistenten vornehmen, können Sie entweder Objekte erstellen und Skripts für sie erstellen oder nur Skripts für sie erstellen.  
  
> [!IMPORTANT]  
>  Bei der Erstellung von Skripts für Kennwörter wird stets NULL angegeben. Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Sie Anmeldeinformationen in einer Skriptdatei speichern, müssen Sie die Datei schützen, um unberechtigtem Zugriff vorzubeugen.  
  
 Weitere Informationen zum Verwenden der Replikations-Assistenten finden Sie hier:  
  
-   [Konfigurieren der Veröffentlichung und der Verteilung](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
-   [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Erstellen eines Pushabonnements](../../relational-databases/replication/create-a-push-subscription.md)  
  
-   [Erstellen eines Pullabonnements](../../relational-databases/replication/create-a-pull-subscription.md)  
  
#### <a name="to-script-an-object-from-a-replication-wizard"></a>So erstellen Sie ein Skript für ein Objekt vom Replikations-Assistenten aus  
  
1.  Aktivieren Sie auf der Seite **Aktionen des Assistenten** das entsprechende Kontrollkästchen für den Assistenten:  
  
    -   **Skriptdatei mit Schritten zur Veröffentlichungserstellung generieren**  
  
    -   **Skriptdatei mit Schritten zur Abonnentenerstellung generieren**  
  
    -   **Skriptdatei mit Schritten zur Verteilungskonfiguration generieren**  
  
2.  Geben Sie Optionen auf der Seite **Skriptdatei** an.  
  
3.  Schließen Sie den Assistenten ab.  
  
#### <a name="to-script-an-object-from-management-studio"></a>So erstellen Sie ein Skript für ein Objekt von Management Studio aus  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verteiler, Verleger oder Abonnenten her, und erweitern Sie dann den Serverknoten.  
  
2.  Erweitern Sie den Ordner **Replikation** , und erweitern Sie dann den Ordner **Lokale Veröffentlichungen** oder **Lokale Abonnements** .  
  
3.  Klicken Sie mit der rechten Maustaste auf eine Veröffentlichung oder ein Abonnement, und klicken Sie dann auf **Skripts generieren**.  
  
4.  Geben Sie Optionen im Dialogfeld **SQL-Skript generieren - \<ReplicationObject>** an.  
  
5.  Klicken Sie auf **Skript in Datei schreiben**.  
  
6.  Geben Sie im Dialogfeld **Speicherort der Skriptdatei** einen Dateinamen ein, und klicken Sie dann auf **Speichern**. Daraufhin wird eine Statusmeldung eingeblendet.  
  
7.  Klicken Sie auf **OK**und dann auf **Schließen**.  
  
#### <a name="to-script-multiple-objects-from-management-studio"></a>So erstellen Sie ein Skript für mehrere Objekte vom Management Studio aus  
  
1.  Stellen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]eine Verbindung mit dem Verteiler, Verleger oder Abonnenten her, und erweitern Sie dann den Serverknoten.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Replikation** , und klicken Sie dann auf **Skripts generieren**.  
  
3.  Geben Sie Optionen im Dialogfeld **SQL-Skript generieren** an.  
  
4.  Klicken Sie auf **Skript in Datei schreiben**.  
  
5.  Geben Sie im Dialogfeld **Speicherort der Skriptdatei** einen Dateinamen ein, und klicken Sie dann auf **Speichern**. Daraufhin wird eine Statusmeldung eingeblendet.  
  
6.  Klicken Sie auf **OK** und dann auf **Schließen**.  
  
  
