---
title: Konfigurieren von Warnungen zur Benachrichtigung von Richtlinienadministratoren bei Richtlinienfehlern | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, configure alerts
ms.assetid: e8e60159-d5b0-49d5-91f3-af8e9cb994c1
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 44565d371ca75d4d707274b90d52794473f63a72
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="configure-alerts-to-notify-policy-administrators-of-policy-failures"></a>Konfigurieren von Warnungen zur Benachrichtigung von Richtlinienadministratoren bei Richtlinienfehlern
  Wenn Richtlinien der richtlinienbasierten Verwaltung in einem der drei automatisierten Auswertungsmodi ausgeführt werden, wird bei einem Richtlinienverstoß eine Meldung im Ereignisprotokoll aufgezeichnet. Wenn Sie bei Aufzeichnung einer solchen Meldung im Ereignisprotokoll benachrichtigt werden möchten, können Sie eine Warnung erstellen, die die Meldung erkennt und eine Aktion ausführt. Die Warnung sollte die Meldungen wie in der folgenden Tabelle gezeigt erkennen.  
  
|Ausführungsmodus|Meldungsnummer|  
|--------------------|--------------------|  
|Bei Änderung - Verhindern<br /><br /> (wenn automatisch)|34050|  
|Bei Änderung - Verhindern<br /><br /> (wenn bedarfsgesteuert)|34051|  
|Nach Zeitplan|34052|  
|Bei Änderung|34053|  
  
 Wie Sie eine Warnung einrichten können, um auf Fehlermeldungen der richtlinienbasierten Verwaltung zu reagieren, wird in den folgenden Themen erläutert:  
  
-   [Erstellen eines Operators](http://msdn.microsoft.com/library/1359d790-5905-4927-a208-e7155e7768a2)  
  
-   [Erstellen einer Warnung mithilfe einer Fehlernummer](http://msdn.microsoft.com/library/03dd7fac-5073-4f86-babd-37e45a86023c)  
  
-   [Zuweisen von Warnungen zu einem Operator](http://msdn.microsoft.com/library/aa818155-6fa2-4565-a09f-5c7e31c89754)  
  
## <a name="permissions"></a>Berechtigungen  
 Bei Bedarf ausgewertete Richtlinien werden im Sicherheitskontext des Benutzers ausgeführt. Um in das Fehlerprotokoll schreiben zu können, muss der Benutzer über die ALTER TRACE-Berechtigung verfügen oder Mitglied der festen Serverrolle sysadmin sein. Bei Auswertung einer Richtlinie durch einen Benutzer mit niedrigeren Berechtigungen werden eventuell erkannte Fehler nicht in das Ereignisprotokoll geschrieben und lösen keine Warnung aus.  
  
 Die automatisierten Ausführungsmodi werden als Mitglied der Rolle sysadmin ausgeführt. Dies ermöglicht es, dass eventuell erkannte Fehler für die Richtlinie in das Fehlerprotokoll geschrieben werden und eine Warnung auslösen.  
  
## <a name="additional-considerations-about-alerts"></a>Weitere Überlegungen zu Warnungen  
 Beachten Sie die folgenden weiteren Überlegungen zu Warnungen:  
  
-   Warnungen werden nur für Richtlinien ausgelöst, die aktiviert sind. Da **bedarfsgesteuerte** Richtlinien nicht aktiviert werden können, werden Warnungen nicht für Richtlinien ausgelöst, die bedarfsgesteuert ausgeführt werden.  
  
-   Wenn die Aktion, die Sie ausführen möchten, das Senden einer E-Mail umfasst, müssen Sie ein E-Mail-Konto konfigurieren. Es empfiehlt sich die Verwendung von Datenbank-E-Mail. Weitere Informationen zum Einrichten von Datenbank-E-Mail finden Sie unter [Erstellen eines Kontos für Datenbank-E-Mail](../../relational-databases/database-mail/create-a-database-mail-account.md).  
  
  
