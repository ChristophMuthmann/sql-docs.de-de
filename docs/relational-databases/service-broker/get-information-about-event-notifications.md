---
title: Abrufen von Informationen zu Ereignisbenachrichtigungen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: service-broker
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event notifications [SQL Server], metadata
- status information [SQL Server], event notifications
- metadata [SQL Server], event notifications
ms.assetid: 8bc10867-66d6-4f57-ac32-a6c29f3327cd
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3e8a2f7837c7f18293afe66c168b5d52c8b03da9
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="get-information-about-event-notifications"></a>Abrufen von Informationen zu Ereignisbenachrichtigungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Zum Abfragen von Metadaten zu Ereignisbenachrichtigungen stehen die folgenden Katalogsichten zur Verfügung.  
  
 **So rufen Sie Informationen zu Ereignisbenachrichtigungen auf der Nichtserverebene ab**  
  
-   [sys.event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  Um in **sys.event_notifications** Metadaten zu Ereignisbenachrichtigungen anzeigen zu können, die auf der Datenbankebene erstellt wurden, müssen folgende Voraussetzungen erfüllt sein: Sie müssen über CONTROL-, ALTER-, TAKE OWNERSHIP- oder VIEW DEFINITION-Berechtigungen für die Datenbank verfügen, Sie müssen der Besitzer der Ereignisbenachrichtigung sein oder über die ALTER ANY DATABASE EVENT NOTIFICATION-Berechtigung verfügen. Für Ereignisbenachrichtigungen, die für eine bestimmte Warteschlange erstellt wurden, müssen mindestens die folgenden Voraussetzungen erfüllt sein: Sie müssen über CONTROL-, ALTER-, TAKE OWNERSHIP- oder VIEW DEFINITION-Berechtigungen für das Objekt verfügen, Sie müssen der Besitzer der Ereignisbenachrichtigung sein oder über die ALTER ANY DATABASE EVENT NOTIFICATION-Berechtigung verfügen.  
  
 **So rufen Sie Informationen zu Ereignisbenachrichtigungen auf der Serverebene ab**  
  
-   [sys.server_event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  Zum Anzeigen von Metadaten über Ereignisbenachrichtigungen in **sys.server_event_notifications**müssen mindestens die folgenden Voraussetzungen erfüllt sein: Sie müssen über die CONTROL- oder VIEW ANY DEFINITION-Berechtigung für den Server verfügen, Sie müssen der Anmeldename oder Besitzer der Ereignisbenachrichtigung sein, oder Sie müssen über die ALTER ANY EVENT NOTIFICATION-Berechtigung verfügen.  
  
 **So rufen Sie Informationen zu sämtlichen Ereignissen ab, die zur Auslösung von Ereignisbenachrichtigungen führen können**  
  
-   [sys.event_notification_event_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notification-event-types-transact-sql.md)  
  
> [!NOTE]  
>  Diese Katalogsicht gibt keine Ereignisgruppen zurück.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ereignisbenachrichtigungen](../../relational-databases/service-broker/event-notifications.md)  
  
  
