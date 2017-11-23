---
title: "Registrierungseinträge für Datenquellen | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC]
- data sources [ODBC], registry entries
- registry entries for data sources [ODBC], about registry entries
- data sources [ODBC], configuring
- registry entries for data sources [ODBC]
ms.assetid: 78aaa3d3-d081-4550-80e3-720c910d5996
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 96e3a3e03e0a3b8f995323c81f6052bf41d16dbd
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="registry-entries-for-data-sources"></a>Registrierungseinträge für Datenquellen
> [!NOTE]  
>  Ab Windows XP und Windows Server 2003, ist ODBC in der Windows-Betriebssystem enthalten. Sie sollten nur explizit ODBC in früheren Versionen von Windows installieren.  
  
 Das Installationsprogramm DLL verwaltet in der Registrierung Informationen über jede Datenquelle. In Microsoft Windows NT/Windows 2000 und Microsoft Windows 95-und Windows 98 werden diese Informationen im Unterschlüssel unter einem der folgenden zwei Schlüssel in der Registrierung gespeichert:  
  
 HKEY_LOCAL_MACHINE  
  
 SOFTWARE  
  
 ODBC  
  
 ODBC.ini  
  
 HKEY_CURRENT_USER  
  
 SOFTWARE  
  
 ODBC  
  
 ODBC.ini  
  
 Hängt von der Schlüssel verwendet wird, ob die Datenquelle ist eine *Systemdatenquelle,* steht für alle Benutzer oder eine *Benutzerdatenquelle,* steht nur für den aktuellen Benutzer. Systemdatenquellen sind in der HKEY_LOCAL_MACHINE-Struktur, und Benutzerdatenquellen in der HKEY_CURRENT_USER-Struktur gespeichert sind. System-Datenquellen und Benutzerdatenquellen sind in jeder anderen Hinsicht identisch.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Unterschlüssel für ODBC-Datenquellen](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [Unterschlüssel für Datenquellenspezifikationen](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [Standardunterschlüssel](../../../odbc/reference/install/default-subkey.md)  
  
-   [ODBC-Unterschlüssel](../../../odbc/reference/install/odbc-subkey.md)
