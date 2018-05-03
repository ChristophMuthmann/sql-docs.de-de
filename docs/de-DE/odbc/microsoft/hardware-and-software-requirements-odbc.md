---
title: Hardware and Software Requirements (ODBC) | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- hardware requirements [ODBC], desktop database drivers
- software requirements [ODBC], desktop database drivers
- system requirements [ODBC], desktop database drivers
- requirements [ODBC], desktop database drivers
ms.assetid: 6df2e9cd-de10-4629-97bd-32f2782616c7
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45bea6f16f079367caeb36b42370c87e1885c56b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="hardware-and-software-requirements-odbc"></a>Hardware and Software Requirements (ODBC)
In diesem Thema werden die Anforderungen für die Verwendung der ODBC-Datenbanktreiber Desktop aufgelistet.  
  
## <a name="hardware-requirements"></a>Hardwareanforderungen  
 Um die ODBC-Datenbanktreiber Desktop zu verwenden, benötigen Sie Folgendes:  
  
-   Ein IBM-kompatibler Computer.  
  
-   Eine Festplatte mit 6 MB freier Speicherplatz verfügbar.  
  
-   Mindestens 16 MB Arbeitsspeicher (RAM).  
  
## <a name="software-requirements"></a>Softwareanforderungen  
 Um Daten mit einem ODBC-Treiber zuzugreifen, benötigen Sie Folgendes:  
  
-   Der ODBC-Treiber.  
  
-   Die 32-Bit-ODBC-Treiber-Manager, Version 3.51 oder höher (Datei "ODBC32.dll").  
  
-   Microsoft Windows 95 oder höher, Windows NT 4.0 oder Windows 2000.  
  
-   Stapelgröße für eine Anwendung mit Microsoft ODBC-Treiber mindestens 20 KB.  
  
 Bei Verwendung von Microsoft Windows NT 4.0 oder Windows 2000 ist der 32-Bit-Treiber threadsicher, jedoch nur durch die Verwendung von globalen Semaphor, die Zugriff auf den Treiber steuert. Gleichzeitige Verwendung des Treibers ist sehr begrenzt unter Windows NT. Bei allen Zugriffen auf der Jet-ISAM-Ebene werden singlethreadprozess für alle Anwendungen, die mit der Microsoft Jet-Datenbankmodul.  
  
 Wenn mehrere 16-Bit-Anwendungen unter Windows on Windows (WOW) unter Microsoft Windows NT 4.0 ausgeführt wird, müssen die Anwendung in unterschiedlichen Speicherbereichen ausgeführt werden. (Die gleichen Speicherbereich kann nicht verwendet werden, da ODBC nicht mehreren Umgebungen im gleichen Prozess unterstützt.) Wählen Sie zum Ausführen einer Anwendung in einen separaten Speicherbereich Symbol für die Anwendung im Programm-Manager, öffnen die **Datei** Menü, und klicken Sie auf **Eigenschaften**, und klicken Sie dann auf **In separaten Speicher ausführen Speicherplatz**.  
  
 Die Verwendung dieser Treiber von 16-Bit-Anwendungen unter Windows 95 wird nicht unterstützt.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>Treiberspezifische Hardware- und Softwareanforderungen  
  
-   Die MicrosoftAccess und dBASEdrivers erfordert möglicherweise die Änderungen in den Dateien Autoexec.bat oder Config.sys.
