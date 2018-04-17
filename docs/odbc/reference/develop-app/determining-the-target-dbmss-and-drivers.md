---
title: Ermitteln der Ziel-DBMS und die Treiber | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- target DBMSs and drivers in interoperability [ODBC]
- interoperability [ODBC], target dbmss and drivers
ms.assetid: 23bee0f6-e12a-4598-b34e-df11a8086829
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 904383158c521cad2e29889020d35bf2374ad517
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="determining-the-target-dbmss-and-drivers"></a>Ermitteln der Ziel-DBMS und Treiber
Ist die nächste Frage zu berücksichtigen, was sind das Ziel-DBMS für die Anwendung, und welche Treiber zur Verfügung stehen unterstützen, die diese DBMS? Da allgemeine Anwendungen häufig sehr interoperabel sein, ist die Frage des Ziel-DBMS-Systeme am besten geeignete benutzerdefinierte und vertikale Anwendungen. Allerdings gilt die Frage der Zieltreiber für alle Anwendungen, denn Treiber Geschwindigkeit, Qualität, Unterstützung von Funktionen und Verfügbarkeit variieren. Auch wenn Treiber sind mit der Anwendung verteilt werden, müssen die Kosten und die Verfügbarkeit von lizenzierungsplänen berücksichtigt werden.  
  
 Für viele benutzerdefinierte Anwendungen, die Ziel-DBMS offensichtlich sind: sie befinden sich vorhandene DBMS-Systeme, die die Anwendung mit folgenden Zielen konzipiert ist zugreifen. DBMS-Systeme auf die Migration in der Zukunft ist geplant, die ebenfalls berücksichtigt werden sollte. Die wichtigste Frage für diese Anwendungen ist jedoch der bzw. die Treiber für die Verwendung mit ihnen. Für andere benutzerdefinierten Anwendungen – diejenigen, bei denen nicht entwickelt wurden, um eine vorhandene DBMS zugreifen – das Ziel-DBMS basierend auf funktionsunterstützung, Unterstützung für gleichzeitige Benutzer Verfügbarkeit von Gerätetreibern und Erschwinglichkeit ausgewählt werden kann.  
  
 Für vertikale Anwendungen auf Grundlage der zielintegritätsdienst DBMS in der Regel ausgewählt werden Feature-Unterstützung, die Verfügbarkeit von Gerätetreibern und Zugang zum Markt. Beispielsweise muss eine vertikale Anwendung, die speziell für kleine Unternehmen DBMS abzielen, die kostengünstige Entwicklung von diese Unternehmen sind; eine vertikale Anwendung entworfen, wie häufig ein Add-on zu vorhandenen DBMS abzielen muss verwendeten DBMS.  
  
 Die Unterschiede zwischen Desktop und Server-Datenbanken sollte berücksichtigt werden, bei der Auswahl von Ziel-DBMS. Desktopdatenbanken wie z. B. Paradox, dBASE und Btrieve sind weniger leistungsfähig als Server-Datenbanken. Da sie in der Regel über weniger leistungsstarke SQL-Module, die in den meisten dateibasierten Treibern gefunden zugegriffen werden, sie häufig fehlender volle transaktionsunterstützung, weniger gleichzeitiger Benutzer zu unterstützen, und haben SQL beschränkt. Allerdings günstig sind und eine große Installationsbasis haben.  
  
 Wie Oracle, DB2 und SQL Server-Datenbanken unterstützen die vollständige Transaktion, unterstützen viele gleichzeitige Benutzer und umfangreiche SQL haben. Sie sind viel teurer und eine kleinere Basis installierte haben. Andererseits, tendenziell Software Preise höher etwas versetzen eines kleineren potenziellen Marktes.  
  
 Daher kann Ziel-DBMS-Systeme manchmal basierend auf die von der Anwendung und die Zielgruppe für die Anwendung erforderlichen Funktionen ausgewählt werden. Beispielsweise kann ein bestellungseingabesystem für große Unternehmen nicht Desktopdatenbanken abzielen, da diese keine transaktionsunterstützung für die entsprechende. Ein ähnliches System, die speziell für kleine Unternehmen möglicherweise die meisten Serverdatenbanken auf Basis der Kosten ausschließen. Und Entwickler generischen Anwendungen sowohl als Ziel können jedoch zu vermeiden, verwenden die erweiterten Funktionen in Server-Datenbanken.
