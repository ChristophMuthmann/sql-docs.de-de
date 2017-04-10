---
title: "Ver&#246;ffentlichungseigenschaften, FTP-Momentaufnahme und Internet | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.internetsynchronization.f1"
ms.assetid: 8e0198c3-5e4e-418c-9920-78ccbbfc1323
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Ver&#246;ffentlichungseigenschaften, FTP-Momentaufnahme und Internet
  Auf dieser Seite haben Sie folgende Möglichkeiten:  
  
-   Legen Sie Eigenschaften für die Übermittlung der Momentaufnahme mittels FTP (File Transfer Protocol) fest. Weitere Informationen finden Sie unter [Momentaufnahmen über FTP übertragen](../../relational-databases/replication/transfer-snapshots-through-ftp.md). Sie müssen einen FTP-Server einrichten, um FTP für die Momentaufnahmeübermittlung verwenden zu können. Weitere Informationen finden Sie in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Dokumentation.  
  
    > [!NOTE]  
    >  Bei jeder Änderung an den FTP-Einstellungen muss eine neue Momentaufnahme erstellt werden.  
  
-   Festlegen von Eigenschaften zur Websynchronisierung für Mergereplikationen unter [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen. Dies ermöglicht die Synchronisierung von Abonnements über HTTPS (Secure Hypertext Transfer Protocol). Für die Verwendung der Websynchronisierung müssen Sie einen [!INCLUDE[msCoName](../../includes/msconame-md.md)] IIS-Server (Internetinformationsdienste) konfigurieren. Weitere Informationen finden Sie unter [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
## Optionen  
 **Auf Momentaufnahmedateien über FTP zugreifen**  
 Wählen Sie **ermöglichen Abonnenten das Herunterladen von momentaufnahmedateien über FTP (File Transfer Protocol) von**, und geben Sie **FTP-Servernamen**, **Portnummer**, **Pfad des FTP-Stammordners**, **Anmeldung**, und **Kennwort**, um die Abonnenten über FTP zur Übermittlung von Momentaufnahmen zu ermöglichen.  
  
 Mithilfe dieser Option können Abonnenten selbst entscheiden, ob sie Momentaufnahmedateien über FTP abrufen möchten. Wenn diese Option ausgewählt ist, kann der Abonnent im Assistenten für neue Abonnements Momentaufnahmedateien standardmäßig über FTP abrufen. Sie können diese Einstellung im Dialogfeld **Abonnementeigenschaften** ändern. Wenn Sie Abonnenten die Möglichkeit einräumen, über FTP auf die Momentaufnahmedateien zuzugreifen, geben Sie auf der Seite **Momentaufnahme** des Dialogfelds **Veröffentlichungseigenschaften** den FTP-Ordner als Speicherort für Momentaufnahmedateien an. Diese Einstellung hat zur Folge, dass der Momentaufnahme-Agent die Dateien im FTP-Ordner automatisch aktualisiert, sobald eine neuer Momentaufnahme generiert wird. Wenn als Speicherort nicht der FTP-Ordner festgelegt ist, müssen Sie die Dateien beim Generieren neuer Momentaufnahmen manuell aktualisieren. Weitere Informationen finden Sie unter [liefern eine Momentaufnahme über FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
 **Websynchronisierung**  
 Nur für Mergereplikationen zulässig. Wählen Sie die Option **Abonnenten das Synchronisieren durch Herstellen einer Verbindung mit einem Webserver ermöglichen**aus, und geben Sie eine Webserveradresse an, damit Mergeabonnenten die Websynchronisierung verwenden können. Der Webserver muss Secure Sockets Layer (SSL) verwenden, und die Webadresse muss vollqualifiziert sein (z. B. https://server.domain.com/synchronize). Weitere Informationen finden Sie unter [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).  
  
## Siehe auch  
 [Erstellen einer Veröffentlichung](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Anzeigen und Ändern der Eigenschaften von Pullabonnements](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Anzeigen und Ändern der Eigenschaften von Pushabonnements](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Erstellen und Anwenden der Anfangsmomentaufnahme](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  