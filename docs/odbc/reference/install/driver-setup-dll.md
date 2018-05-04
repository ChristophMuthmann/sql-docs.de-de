---
title: Setup-DLL für Treiber | Microsoft Docs
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
- installing ODBC components [ODBC], driver setup DLL
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: 49bab021-81fa-402e-b7a4-a5214f1fadc4
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58d236da053585b4aced435697100e0f6c87379c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="driver-setup-dll"></a>Treiber-Setup-DLL
> [!NOTE]  
>  Ab Windows XP und Windows Server 2003, ist ODBC in der Windows-Betriebssystem enthalten. Sie sollten nur explizit ODBC in früheren Versionen von Windows installieren.  
  
 Der Setup-Treiber-DLL enthält die **ConfigDriver** und **ConfigDSN** Funktionen. **ConfigDriver** treiberspezifische installationstasks wie das Eingeben von treiberspezifische Informationen in der Registrierung führt. **ConfigDSN** verwaltet treiberspezifische Informationen zu den Datenquellen in der Registrierung. Eine vollständige Beschreibung dieser Funktionen, finden Sie unter [Setup DLL-API-Referenz](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 **ConfigDSN** Ruft die folgenden Funktionen in der Installer DLL Datenquelleninformationen in der Registrierung zu verwalten:  
  
-   **SQLWriteDSNToIni**. Fügen Sie eine Datenquelle hinzu.  
  
-   **SQLRemoveDSNFromIni**. Löschen einer Datenquelle an.  
  
-   **SQLWritePrivateProfileString**. Schreiben Sie einen treiberspezifische Wert unter einem Data Source-Spezifikation Unterschlüssel.  
  
-   **SQLGetPrivateProfileString**. Gelesen Sie einen treiberspezifische-Wert aus dem Data Source-Spezifikation Unterschlüssel.  
  
-   **SQLGetTranslator**. Fordert den Benutzer für einen Übersetzer Namen und eine Option. Diese Funktion ruft **ConfigTranslator** in das Konvertierungsprogramm setup-DLL.  
  
 Der Setup-Treiber wird vom Treiber Entwickler DLL geschrieben. Kann es Teil der Treiber-DLL oder eine separate DLL.
