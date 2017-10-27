---
title: "Registrierungseinträge für ODBC-Komponenten | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC]
- installing ODBC components [ODBC], registry entries
- registry entries for components [ODBC]
- subkeys [ODBC], for components
- registry entries for components [ODBC], about registry entries
ms.assetid: c90aa8a4-6ece-48de-901c-17d23739a9ff
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d28365bb906cdaec6027a5549d5bdedebfee7a00
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="registry-entries-for-odbc-components"></a>Registrierungseinträge für ODBC-Komponenten
> [!NOTE]  
>  Ab Windows XP und Windows Server 2003, ist ODBC in der Windows-Betriebssystem enthalten. Sie sollten nur explizit ODBC in früheren Versionen von Windows installieren.  
  
 Das Installationsprogramm DLL verwaltet die Informationen in der Registrierung zu allen installierten ODBC-Komponenten. Auf Computern unter Microsoft Windows NT und Microsoft Windows 95-und Windows 98 werden diese Informationen im Unterschlüssel unter dem folgenden Schlüssel in der Registrierung gespeichert:  
  
 HKEY_LOCAL_MACHINE  
  
 SOFTWARE  
  
 ODBC  
  
 "Odbcinst.ini"  
  
 Da "Odbcinst.ini" einen Unterschlüssel der HKEY_LOCAL_MACHINE-Struktur ist, sind die Informationen zu ODBC-Komponenten für alle Benutzer des Computers verfügbar.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Unterschlüssel für ODBC-Kernkomponenten](../../../odbc/reference/install/odbc-core-subkey.md)  
  
-   [Unterschlüssel für ODBC-Treiber](../../../odbc/reference/install/odbc-drivers-subkey.md)  
  
-   [Unterschlüssel für Treiberspezifikationen](../../../odbc/reference/install/driver-specification-subkeys.md)  
  
-   [Unterschlüssel für Standardtreiber](../../../odbc/reference/install/default-driver-subkey.md)  
  
-   [Unterschlüssel für ODBC-Konvertierungsprogramme](../../../odbc/reference/install/odbc-translators-subkey.md)  
  
-   [Unterschlüssel für Konvertierungsprogrammspezifikationen](../../../odbc/reference/install/translator-specification-subkeys.md)

