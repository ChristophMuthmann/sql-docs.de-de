---
title: Verlauf der Desktop-Datenbanktreiber | Microsoft Docs
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
- Jet-based ODBC drivers [ODBC], history
- ODBC desktop database drivers [ODBC], history
- desktop database drivers [ODBC], history
ms.assetid: b4a2aff8-bde7-4bd5-8580-bc50f27311c8
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f753260ad83582e3b9dfa7f9901af72082a3abe9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="history-of-the-desktop-database-drivers"></a>Verlauf der Desktop-Datenbanktreiber
Die folgende Tabelle zeigt die Desktop-Datenbanktreiber Versionsverlauf.  
  
|Version|Veröffentlichungsdatum|Description|  
|-------------|------------------|-----------------|  
|1,0|August 1993|Verwendet die SIMBA der Abfrageprozessor von PageAhead Software erzeugt. SIMBA empfangen ODBC-Aufrufe und SQL-Anweisungen, verarbeitet diese in Microsoft Jet installierbare ISAM-Aufrufe und anschließend aufgerufen, die Microsoft Jet-ISAM-Dispatch-Ebene, um das Laden und Aufrufen des entsprechenden installierbaren ISAM-Treibers.|  
|2.0|Dezember 1994|Verwendet ODBC-Version 2.0, das ODBC-Funktionalität erheblich erweitert. Die wichtige Änderung der Version 2.0 wurde, dass das Microsoft Jet-Datenbankmodul den Abfrageprozessor SIMBA ersetzt. Mit dem Microsoft Jet-Datenbankmodul integriert in der Microsoft Jet installierbare ISAM-Treiber und der Microsoft Access-Technologie weitaus eng der Desktop-Datenbanktreiber. Deutliche Verbesserungen wurden:<br /><br /> -Systemeigene Unterstützung für scrollfähige Cursor.<br />-Systemeigene Unterstützung für äußere Joins, aktualisiert und heterogene Joins und Transaktionen.<br />-32-Bit-Versionen der Treiber für Microsoft Windows NT.|  
|3.0|Oktober 1995|Unterstützung für Windows 95 und Windows NT-Arbeitsstation oder NT Server 3.51 wird bereitgestellt. Nur 32-Bit-Treiber wurden in dieser Version enthalten; die 16-Bit-Treiber für Windows-Version 3.1 wurden entfernt.|  
|3.5|Oktober 1996|Diese Treiber wurden Doppelbyte-Zeichensatz (DBCS)-aktiviert, wurden für die Verwendung mit Internetanwendungen als in vorherigen Versionen besser geeignet, und nur die Verwendung von Datei-Datenquellennamen (DSNs) unterstützen. Der Microsoft Access-Treiber wurde eine RISC-Version für die Verwendung auf einer Alpha-Plattformen für Windows 95-und Windows 98, Windows NT 3.51 und höher bereitgestellt.|  
|4.0|Spät 1998|Bietet Unterstützung für Microsoft Jet-Datenbankmodul Unicode-Format sowie Kompatibilität mit ANSI-Format von Vorgängerversionen.|  
  
> [!NOTE]  
>  Die Treiber version3.5 wurden ODBC2 portzuweisung entworfen. *x*. Obwohl sie auch mit ODBC 3.0 zu arbeiten, unterstützt sie nicht alle ODBC 3.0-Funktionen. Weitere Informationen über die Funktionsweise von diese Treiber mit ODBC 3.0 finden Sie unter [Abwärtskompatibilität und zur Einhaltung von Standards](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).
