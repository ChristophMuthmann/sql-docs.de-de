---
title: "Hinzufügen und Entfernen von Verlegern vom Replikationsmonitor aus | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Replication Monitor, adding and removing Publishers
ms.assetid: fa36c4b4-bfa5-494e-92e3-07a02d7332c3
caps.latest.revision: "38"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 730ea279e71fc0d4ce02790beeba0d8dbc8bfb34
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="add-and-remove-publishers-from-replication-monitor"></a>Hinzufügen und Entfernen von Verlegern vom Replikationsmonitor aus
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Der Server, von dem aus Sie den Replikationsmonitor starten, wird, sofern es sich um einen Verleger handelt, automatisch dem Replikationsmonitor hinzugefügt. Weitere Verleger können im Dialogfeld **Verleger hinzufügen** hinzugefügt werden. Alle hinzugefügten Verleger werden als Gruppe im linken Bereich des Replikationsmonitors angezeigt. Die Gruppe **Meine Verleger** ist standardmäßig enthalten, Sie können aber zum Verwalten einer oder mehrerer Replikationstopologien auch neue Gruppen erstellen. Informationen zum Starten des Replikationsmonitors finden Sie unter [Starten des Replikationsmonitors](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### <a name="to-add-a-sql-server-publisher"></a>So fügen Sie einen SQL Server-Verleger hinzu  
  
1.  Klicken Sie mit der rechten Maustaste auf den Knoten **Replikationsmonitor** oder auf einen Verlegergruppenknoten im linken Bereich, und klicken Sie dann auf **Verleger hinzufügen**.  
  
2.  Klicken Sie im Dialogfeld **Verleger hinzufügen** auf **Hinzufügen**, und klicken Sie dann auf **SQL Server-Verleger hinzufügen**.  
  
3.  Geben Sie im Dialogfeld **Verbindung mit Server herstellen** einen Namen für den Verleger ein, und wählen Sie dann den Authentifizierungstyp aus. Wenn Sie **SQL Server-Authentifizierung**auswählen, geben Sie einen Anmeldenamen und ein Kennwort ein. Die von Ihnen angegebenen Anmeldeinformationen werden vom Replikationsmonitor für künftige Verbindungen mit diesem Server gespeichert. Das angegebene Windows-Konto bzw. der angegebene SQL Server-Anmeldename muss Mitglied der festen **sysadmin** -Serverrolle bzw. Mitglied der festen **replmonitor** -Datenbankrolle in der Verteilungsdatenbank sein.  
  
4.  Klicken Sie auf **Verbinden**. Wenn der Verleger einen Remoteverteiler verwendet, werden Sie im Dialogfeld **Verbindung mit Server herstellen** aufgefordert, eine Verbindung mit dem Verteiler herzustellen. Die von Ihnen angegebenen Anmeldeinformationen werden vom Replikationsmonitor für künftige Verbindungen mit diesem Server gespeichert. Das angegebene Windows-Konto bzw. der angegebene SQL Server-Anmeldename muss Mitglied der festen **sysadmin** -Serverrolle bzw. Mitglied der festen **replmonitor** -Datenbankrolle in der Verteilungsdatenbank sein.  
  
5.  In der Tabelle **Überwachung der folgenden Verleger starten** werden die Namen des Verlegers und des Verteilers angezeigt.  
  
6.  Wenn Sie Aktualisierungs- und Verbindungsoptionen für einen Verleger angeben möchten, wählen Sie in der Tabelle den entsprechenden Verleger aus, und ändern Sie die Optionen nach Bedarf. Weitere Informationen zu Aktualisierungsoptionen finden Sie unter [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
7.  Wählen Sie die Gruppe aus, in der der Verleger im Replikationsmonitor angezeigt werden soll. Wenn Sie eine neue Gruppe erstellen möchten, klicken Sie auf **Neue Gruppe**, und geben Sie einen Gruppennamen ein. Wählen Sie in der Liste **Diese(n) Verleger in der folgenden Gruppe anzeigen** die Gruppe aus.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-add-an-oracle-publisher"></a>So fügen Sie einen Oracle-Verleger hinzu  
  
1.  Klicken Sie mit der rechten Maustaste auf den Knoten **Replikationsmonitor** oder auf einen Verlegergruppenknoten im linken Bereich, und klicken Sie dann auf **Verleger hinzufügen**.  
  
2.  Klicken Sie im Dialogfeld **Verleger hinzufügen** auf **Hinzufügen**, und klicken Sie dann auf **Oracle-Verleger hinzufügen**.  
  
3.  Geben Sie im Dialogfeld **Verbindung mit Server herstellen** den Namen des [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verteilers ein, der dem Oracle-Verleger zugeordnet ist, und wählen Sie dann den Authentifizierungstyp aus. Wenn Sie **SQL Server-Authentifizierung**auswählen, geben Sie einen Anmeldenamen und ein Kennwort ein. Die von Ihnen angegebenen Anmeldeinformationen werden vom Replikationsmonitor für künftige Verbindungen mit diesem Server gespeichert. Das angegebene Windows-Konto bzw. der angegebene SQL Server-Anmeldename muss Mitglied der festen **sysadmin** -Serverrolle bzw. Mitglied der festen **replmonitor** -Datenbankrolle in der Verteilungsdatenbank sein.  
  
4.  Klicken Sie auf **Verbinden**.  
  
5.  In der Tabelle **Überwachung der folgenden Verleger starten** werden die Namen des Verlegers und des Verteilers angezeigt.  
  
6.  Wenn Sie Aktualisierungs- und Verbindungsoptionen für einen Verleger angeben möchten, wählen Sie in der Tabelle den entsprechenden Verleger aus, und ändern Sie die Optionen nach Bedarf. Weitere Informationen zu Aktualisierungsoptionen finden Sie unter [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
7.  Wählen Sie die Gruppe aus, in der der Verleger im Replikationsmonitor angezeigt werden soll. Wenn Sie eine neue Gruppe erstellen möchten, klicken Sie auf **Neue Gruppe**, und geben Sie einen Gruppennamen ein. Wählen Sie in der Liste **Diese(n) Verleger in der folgenden Gruppe anzeigen** die Gruppe aus.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-add-one-or-more-publishers-that-use-the-same-distributor"></a>So fügen Sie einen oder mehrere Verleger hinzu, die denselben Verteiler verwenden  
  
1.  Klicken Sie mit der rechten Maustaste auf den Knoten **Replikationsmonitor** oder auf einen Verlegergruppenknoten im linken Bereich, und klicken Sie dann auf **Verleger hinzufügen**.  
  
2.  Klicken Sie im Dialogfeld **Verleger hinzufügen** auf **Hinzufügen**, und klicken Sie dann auf **Geben Sie einen Verteiler an, und fügen Sie seine Verleger hinzu**.  
  
3.  Geben Sie im Dialogfeld **Verbindung mit Server herstellen** den Namen des Verlegers ein, und wählen Sie dann den Authentifizierungstyp aus. Wenn Sie **SQL Server-Authentifizierung**auswählen, geben Sie einen Anmeldenamen und ein Kennwort ein. Die von Ihnen angegebenen Anmeldeinformationen werden vom Replikationsmonitor für künftige Verbindungen mit diesem Server gespeichert. Das angegebene Windows-Konto bzw. der angegebene SQL Server-Anmeldename muss Mitglied der festen **sysadmin** -Serverrolle bzw. Mitglied der festen **replmonitor** -Datenbankrolle in der Verteilungsdatenbank sein.  
  
4.  Klicken Sie auf **Verbinden**.  
  
5.  In der Tabelle **Überwachung der folgenden Verleger starten** werden die Namen des Verteilers und der einzelnen Verleger angezeigt. Verleger, die dem Replikationsmonitor bereits hinzugefügt wurden, werden in der Tabelle nicht angezeigt.  
  
6.  Wenn Sie Aktualisierungs- und Verbindungsoptionen für einen Verleger angeben möchten, wählen Sie in der Tabelle den entsprechenden Verleger aus, und ändern Sie die Optionen nach Bedarf. Weitere Informationen zu Aktualisierungsoptionen finden Sie unter [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
7.  Wählen Sie die Gruppe aus, in der die Verleger im Replikationsmonitor angezeigt werden sollen. Wenn Sie eine neue Gruppe erstellen möchten, klicken Sie auf **Neue Gruppe**, und geben Sie einen Gruppennamen ein. Wählen Sie in der Liste **Diese(n) Verleger in der folgenden Gruppe anzeigen** die Gruppe aus.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-modify-settings-for-the-publisher-and-publisher-groups"></a>So ändern Sie die Einstellungen für den Verleger und die Verlegergruppen  
  
1.  Klicken Sie mit der rechten Maustaste im linken Bereich auf einen Verleger, und klicken Sie dann auf **Verlegereinstellungen**.  
  
2.  Nehmen Sie im Dialogfeld **Verlegereinstellungen** die gewünschten Änderungen vor:  
  
    -   Wenn Sie die Anmeldinformationen ändern möchten, die der Replikationsmonitor zum Herstellen einer Verbindung mit einem Server verwendet, klicken Sie auf **Verlegerverbindung** oder **Verteilerverbindung**, und geben Sie dann im Dialogfeld **Verbindung mit Server herstellen** die neuen Anmeldeinformationen ein.  
  
    -   Wenn Sie einen Verleger aus einer Gruppe in eine andere Gruppe verschieben möchten, wählen Sie in der Tabelle **Überwachung der folgenden Verleger starten** den betreffenden Verleger aus, und wählen Sie dann in der Liste **Diese(n) Verleger in der folgenden Gruppe anzeigen** die neue Gruppe aus.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-remove-a-publisher-from-replication-monitor"></a>So entfernen Sie einen Verleger aus dem Replikationsmonitor  
  
1.  Klicken Sie mit der rechten Maustaste auf den betreffenden Verleger im linken Bereich.  
  
2.  Klicken Sie auf **Entfernen**.  
  
### <a name="to-add-a-publisher-group-to-replication-monitor"></a>So fügen Sie dem Replikationsmonitor eine Verlegergruppe hinzu  
  
1.  Verlegergruppen können nur beim Hinzufügen eines Verlegers oder beim Ändern der Einstellungen für einen Verleger erstellt werden. Weitere Informationen dazu finden Sie in den Vorgehensweisethemen zum Hinzufügen eines Verlegers.  
  
### <a name="to-remove-a-publisher-group-from-replication-monitor"></a>So entfernen Sie eine Verlegergruppe aus dem Replikationsmonitor  
  
1.  Verschieben Sie alle in der betreffenden Gruppe vorhandenen Verleger in eine andere Gruppe, oder entfernen Sie diese Verleger aus dem Replikationsmonitor. Weitere Informationen finden Sie in den Anweisungen weiter oben in diesem Thema.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Verlegergruppe, und klicken Sie dann auf **Entfernen**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verteilung konfigurieren](../../../relational-databases/replication/configure-distribution.md)   
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
