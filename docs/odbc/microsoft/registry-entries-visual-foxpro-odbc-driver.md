---
title: "Einträge in der Registrierung (Visual FoxPro-ODBC-Treiber) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- registry keys [ODBC]
- Visual FoxPro ODBC driver [ODBC], registry entries
- keys [ODBC]
- FoxPro ODBC driver [ODBC], registry entries
ms.assetid: 1a63d92d-ca3a-46ae-911f-6788292c801e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 83c2d0752cc8b786a9de84d1a5005a8bc0c5b5f5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>Einträge in der Registrierung (Visual FoxPro-ODBC-Treiber)
Bei der Installation der Visual FoxPro-ODBC-Treiber aktualisiert das Installationsprogramm der Registrierung Ihres Systems, in den Registrierungsschlüssel HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini, um einen neuen Schlüssel namens Microsoft Visual FoxPro-Treiber hinzuzufügen. Unter diesem Schlüssel werden in der folgenden Tabelle beschriebenen Werte hinzugefügt.  
  
|Wertname|Werttyp|Wert|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|Treiber|REG_SZ|Systempfad zur Datei vfpodbc.dll|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|"*.DBF,\*CDX,\*.fpt"|  
|FileUsage|REG_SZ|"1"|  
|Setup|REG_SZ|Systempfad zur Datei vfpodbc.dll|  
|SQLLevel|REG_SZ|"0"|  
  
 Das Installationsprogramm fügt auch die Taste "Visual FoxPro-Dateien", den standardmäßige Visual FoxPro-Treiber für Ihr System HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini Schlüssel darstellt. Unter diesem Schlüssel fügt das Installationsprogramm die Werte in der folgenden Tabelle beschrieben.  
  
|Wertname|Werttyp|Wert|  
|----------------|----------------|-----------|  
|Treiber|REG_SZ|Systempfad zur Datei vfpodbc.dll|  
  
 Bei jedem eine Visual FoxPro-ODBC-Datenquelle die ODBC-Konfiguration hinzufügen wird ein neuer Schlüssel hinzugefügt, die für diesen Namen Datenquelle. Die Werte für die Datenquelle entsprechen Werten, die Sie, in Festlegen der **ODBC Visual FoxPro-Setup** (Dialogfeld), wie in der folgenden Tabelle aufgeführt.  
  
|Wertname (Schlüsselwort)|Werttyp|Wert|  
|----------------------------|----------------|-----------|  
|Sortieren|REG_SQ|Alle unterstützten Sortierreihenfolge|  
|Description|REG_SZ|Benutzerbeschreibung der Datenquelle|  
|Treiber||Systempfad zur Datei vfpodbc.dll|  
|Exclusive||Ja oder Nein|  
|BackgroundFetch||Ja oder Nein|  
|SourceDB|REG_SZ|Pfad zu. Datenbank-Datei|  
|SourceType|REG_SZ|"Datenbank" oder "DBF"|  
  
 Sie sollten diese Informationen nicht direkt zugreifen. Verwaltung der Registrierung durch den ODBC-Administrator behandelt, wenn Sie Daten hinzufügen, ändern oder einer Datenquelle löschen.  
  
 Sie können einige dieser Schlüsselwörter und Werte als Parameter in der [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) ODBC API-Funktion.
