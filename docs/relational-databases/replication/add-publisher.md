---
title: "Verleger hinzufügen | Microsoft-Dokumentation"
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
f1_keywords: sql13.rep.monitor.addpublisher.f1
helpviewer_keywords: Add Publisher dialog box
ms.assetid: 4b57e298-655f-42c2-82bc-25cdad94a194
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e03e3af1548fa02ab81a310130b326a6f5aa21d5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="add-publisher"></a>Verleger hinzufügen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mithilfe des Dialogfelds **Verleger hinzufügen** können Sie dem linken Bereich des Replikationsmonitors einen oder mehrere Verleger hinzufügen. Nach dem Hinzufügen eines Verlegers werden durch das Auswählen des Verlegers im linken Bereich Informationen zu diesem Verleger im rechten Bereich anzeigt.  
  
## <a name="options"></a>Optionen  
 **Hinzufügen**  
 Klicken Sie auf diese Option, um den Typ des hinzuzufügenden Verlegers auszuwählen. Dadurch wird das Dialogfeld **Verbindung mit Server herstellen** gestartet. Folgende Optionen sind verfügbar:  
  
-   **SQL Server-Verleger hinzufügen...**  
  
     Stellen Sie mithilfe des Dialogfelds **Verbindung mit Server herstellen** eine Verbindung mit dem Verleger her.  
  
-   **Oracle-Verleger hinzufügen...**  
  
     Stellen Sie mithilfe des Dialogfelds [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributor associated with the Oracle Publisher using the **Connect to Server** dialog box.  
  
-   **Geben Sie einen Verteiler an, und fügen Sie seine Verleger hinzu…**  
  
     Stellt mithilfe des Dialogfelds [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verbindung mit Server herstellen **eine Verbindung mit dem** -Verteiler her, der einem oder mehreren Verlegern zugeordnet ist.  
  
 Nach einer erfolgreichen Verbindungsherstellung mit dem Verleger oder Verteiler werden die Namen aller Verleger und ihrer Verteiler in dem Raster im oberen Bereich des Dialogfelds angezeigt.  
  
> [!NOTE]  
>  Verteiler und Verleger werden oft auf derselben Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt, aber der Verteiler kann auch auf einer anderen Instanz ausgeführt werden (diese Konfiguration wird als Remoteverteiler bezeichnet).  
  
 **Entfernen**  
 Wählen Sie einen Verleger in dem Raster im oberen Bereich des Dialogfelds aus, und klicken Sie auf **Entfernen** , um den Verleger aus der Liste der hinzuzufügenden Verleger zu entfernen.  
  
> [!NOTE]  
>  Diese Schaltfläche kann nicht verwendet werden, um einen Verleger zu entfernen, der bereits im Replikationsmonitor angezeigt wird. Klicken Sie zum Entfernen eines Verteilers, der bereits im linken Bereich des Replikationsmonitors angezeigt wird, mit der rechten Maustaste auf den Verleger, und klicken Sie dann auf **Entfernen**.  
  
 **Beim Starten des Replikationsmonitors automatisch Verbindung herstellen**  
 Wählen Sie diese Option aus, damit der Replikationsmonitor automatisch eine Verbindung mit dem Verteiler herstellt und Statusinformationen für den Verleger abruft, der im Raster im oberen Bereich des Dialogfelds ausgewählt ist. Wenn dieses Kontrollkästchen deaktiviert ist, müssen Sie nach dem Starten des Replikationsmonitors manuell eine Verbindung herstellen: Klicken Sie dazu mit der rechten Maustaste auf den Verleger im linken Bereich des Replikationsmonitors, und klicken Sie dann auf **Verbinden**.  
  
 **Status dieses Verlegers und seiner Veröffentlichungen automatisch aktualisieren**  
 Wählen Sie diese Option aus, damit der Replikationsmonitor automatisch den Status für den Verleger aktualisiert, der im Raster im oberen Bereich des Dialogfelds ausgewählt ist. Wenn diese Option ausgewählt ist, ruft der Replikationsmonitor die Statusinformationen für den Verleger und seine Veröffentlichungen über den Verteiler ab. Das Abrufintervall wird durch die Option **Aktualisierungsrate** festgelegt. Weitere Informationen zum Aktualisieren im Replikationsmonitor finden Sie unter [Zwischenspeichern, Aktualisieren und Leistung des Replikationsmonitors](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Aktualisierungsrate**  
 Geben Sie einen Wert (in Sekunden) ein, um anzugeben, wie oft der Replikationsmonitor Statusinformationen über den Verteiler abrufen soll. Geringere Werte führen zu einem häufigeren Abruf, was die Leistung des Verteilers beeinträchtigen kann, wenn eine große Anzahl von Verlegern überwacht wird. Es wird empfohlen, das eigene System zu testen, um einen angemessenen Wert zu bestimmen. Die Einstellung **Aktualisierungsrate** wird ebenfalls verwendet, wenn Sie in einem der Detailfenster des Replikationsmonitors die Option **Automatisch aktualisieren** ausgewählt haben.  
  
 **Diese(n) Verleger in der folgenden Gruppe anzeigen**  
 Wählen Sie eine Verlegergruppe aus der Liste aus. Der Verleger wird unter dieser Gruppe im linken Bereich angezeigt. Gruppen stellen eine Möglichkeit zum Organisieren von Verlegern dar und haben keinen Einfluss auf die Funktion der Replikation. Wenn keine Gruppen definiert wurden oder Sie eine neue Gruppe erstellen möchten, dann klicken Sie auf **Neue Gruppe**.  
  
 **Neue Gruppe**  
 Klicken Sie auf diese Option, um eine neue Verlegergruppe zu erstellen. Eine Verlegergruppe stellt eine einfache Möglichkeit dar, um die Verleger innerhalb des Replikationsmonitors zu organisieren. Gruppen haben keinen Einfluss auf die Replikation der Daten oder die Beziehungen zwischen den Servern in der Replikationstopologie.  
  
## <a name="see-also"></a>Siehe auch  
 [Starten des Replikationsmonitors](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
