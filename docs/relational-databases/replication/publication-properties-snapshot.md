---
title: Veröffentlichungseigenschaften, Momentaufnahme | Microsoft-Dokumentation
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
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.snapshotformat.f1
ms.assetid: 8e9133b1-fc37-4a85-8a7c-d5eaf172fbef
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee2cdb54da4e68ba59789245a4e17e83ed98265e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="publication-properties-snapshot"></a>Veröffentlichungseigenschaften, Momentaufnahme
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Mithilfe der Seite **Momentaufnahme** des Dialogfelds **Veröffentlichungseigenschaften** können Sie das Momentaufnahmeformat, den Speicherort des Momentaufnahmeordners und Skripts, die vor und nach der Anwendung der Momentaufnahme ausgeführt werden, festlegen. Der Momentaufnahmeordner muss als Freigabe definiert sein und über ausreichend Berechtigungen verfügen, sodass Agents Dateien im Ordner lesen und schreiben können. Weitere Informationen zum angemessenen Sichern des Ordners finden Sie unter [Sichern des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
> [!NOTE]  
>  Änderungen erfordern eine neue Momentaufnahme für die Veröffentlichung. Weitere Informationen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
## <a name="options"></a>Tastatur  
 **Momentaufnahmeformat**  
 Wählen Sie für das Momentaufnahmeformat den einheitlichen Modus oder den Zeichenmodus aus.  
  
-   Wählen Sie **Systemeigenes Format von SQL Server - alle Abonnenten müssen Server mit SQL Server sein** aus, wenn alle Abonnenten andere Instanzen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind als [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)]. Das systemeigene Momentaufnahmeformat bietet die beste Leistung.  
  
-   Wählen Sie **Zeichen - erforderlich, wenn auf einem Verleger oder Abonnenten SQL Server nicht ausgeführt wird** aus, wenn Abonnenten [!INCLUDE[ssEW](../../includes/ssew-md.md)] ausführen oder es sich um Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abonnenten handelt.  
  
 **Speicherort der Momentaufnahmedateien**  
 Wählen Sie den Speicherort zum Speichern der Momentaufnahmedateien aus. Die Dateien können am Standardspeicherort gespeichert werden; Sie können jedoch auch an einem alternativen Speicherort statt dem oder zusätzlich zum Standardspeicherort gespeichert werden. An einem alternativen Speicherort gespeicherte Dateien können komprimiert werden.  
  
-   Wählen Sie **Dateien im Standardordner speichern** aus, um für den Verleger den Standard-Momentaufnahmeordner zu verwenden. Der Speicherort des Momentaufnahmeordners ist in diesem Dialogfeld schreibgeschützt, da er für den Verleger nur im Dialogfeld **Verteilereigenschaften** geändert werden kann. Weitere Informationen finden Sie unter [Angeben des standardmäßigen Momentaufnahmespeicherorts &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md).  
  
-   Wählen Sie **Dateien im folgenden Ordner speichern** aus, um anstelle des Standardspeicherorts oder zusätzlich dazu einen alternativen Speicherort anzugeben. Geben Sie in das Textfeld einen Pfad ein, oder klicken Sie auf **Durchsuchen** , und navigieren Sie zu einem Speicherort. Wählen Sie **Momentaufnahmedateien in diesem Ordner komprimieren** aus, um die Dateien am alternativen Momentaufnahmespeicherort zu komprimieren. Der alternative Speicherort kann sich auf einem anderen Server, auf einem Netzlaufwerk oder auf Wechselmedien befinden, z. B. auf CD-ROM oder auf einem Wechseldatenträger. Weitere Informationen finden Sie unter [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md) und [Compressed Snapshots](../../relational-databases/replication/compressed-snapshots.md).  
  
 **Weitere Skripts ausführen**  
 Geben Sie Skripts an, die vor oder nach dem Anwenden der Momentaufnahme auf dem Abonnenten ausgeführt werden. Skripts können nicht angegeben werden, wenn für **Momentaufnahmeformat** die Option **Zeichen**festgelegt wurde.  
  
 Skripts sind optional. Sie stellen jedoch eine benutzerfreundliche Möglichkeit dar, Befehle auszuführen und administrative Änderungen auf Abonnenten anzuwenden. Weitere Informationen zum Ausführen von Skripts finden Sie unter [Ausführen von Skripts vor und nach dem Anwenden der Momentaufnahme](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).  
  
-   Geben Sie in das Textfeld **Dieses Skript vor Anwenden der Momentaufnahme ausführen** einen Pfad ein, oder klicken Sie auf **Durchsuchen** , um einen Speicherort für das Skript anzugeben.  
  
-   Geben Sie in das Textfeld **Dieses Skript nach Anwenden der Momntaufnahme ausführen** einen Pfad ein, oder klicken Sie auf **Durchsuchen** , um einen Speicherort für das Skript anzugeben.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Erstellen und Anwenden der Anfangsmomentaufnahme](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
