---
title: Verwenden von 16-Bit-Anwendungen mit 32-Bit-Treibern | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: 68feb3b7-c01a-4f42-8df9-f9c182d89325
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 95ff3ce88daf4a508145c28ea194a97b9cbbbabe
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>Verwenden von 16-Bit-Anwendungen mit 32-Bit-Treiber
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Planen von Anwendungen zu ändern, die dieses Feature verwenden. Verwenden Sie stattdessen die 32-Bit oder 64-Bit-Treiber-Manager.  
  
 Sie können 16-Bit-Anwendungen mit 32-Bit-Treiber auf Ihrem Windows-basierten System ausführen, solange die 32-Bit-Treiber nicht explizit Win32 API-Funktionen aufruft, die Threads erstellen. Die Windows on Windows (WOW)-Subsystem die Anwendungen in 16-Bit-Modus ausgeführt und löst 16-Bit-Aufrufe des Betriebssystems. ODBC thunking DLLs Resolve 16-Bit-Aufruf aus der Anwendung auf 32-Bit-Treiber. Die 16-Bit-Anwendungen verwenden die Windows-API und 32-Bit-Treiber verwendet die Win32-API.  
  
## <a name="architecture"></a>Aufbau  
 Die folgende Abbildung zeigt, wie die 16-Bit-Anwendungen mit 32-Bit-Treiber kommunizieren. Zwischen der 16-Bit-Treiber-Manager und die 32-Bit-Treiber sind generische thunking DLLs, die 16-Bit-ODBC-Aufrufe für 32-Bit-ODBC-Aufrufe zu konvertieren.  
  
 ![Wie 16 &#45; Bit-apps, die Kommunikation mit 32 &#45; bit-Treiber](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  Jedes Mal, wenn eine 16-Bit-Anwendung mit einem 32-Bit-Treiber interagiert, gibt der 32-Bit-Treiber-Manager immer "2.0" als ODBC-Version vom Treiber unterstützt werden.  
  
## <a name="administration"></a>Verwaltung  
 Sie können Datenquellen für 32-Bit-Treibern mithilfe von ODBC-Datenquellen-Administrator verwalten. Um den ODBC-Administrator auf Computern unter Microsoft® Windows® 2000 zu öffnen, öffnen Sie die Windows-Systemsteuerung, doppelklicken Sie auf **Verwaltung**, und doppelklicken Sie dann auf **Datenquellen (ODBC)**. Auf Computern unter früheren Versionen von Microsoft Windows lautet das Symbol " **32-Bit-ODBC-** oder einfach **ODBC**.  
  
 Die folgende Abbildung zeigt, wie eine 16-Bit-Anwendung eine 32-Bit-Treiber-Setup-DLL aufruft. Zwischen den 16-Bit-Installationsprogramm DLL und der 32-Bit-Treiber ist Setup-DLL für eine generische thunking-DLL, die 16-Bit-Installationsprogramm DLL-Aufrufe für 32-Bit-Installationsprogramm DLL Aufrufe konvertiert.  
  
 ![Wie ein 16 &#45; Bit-Anwendung aufruft, eine 32 &#45; -bit-Treiber-Setup-DLL](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 In der Windows on Windows (16-Bit in 32-Bit thunking) eine zusätzliche thunking-DLL, die mit dem Namen Ds32gt.dll konvertiert eine 32-Bit-Installation 16-Bit-Argumentwerte weitergereicht DLL wieder in 16-Bit.  
  
## <a name="components"></a>Components  
 Die ODBC-Komponente, der das MDAC 2.8 SP1-SDK enthält die folgenden Dateien für die Ausführung von 16-Bit-Anwendungen mit 32-Bit-Treiber. Diese Komponenten sind im Verzeichnis \Redist.  
  
|Dateiname|Description|  
|---------------|-----------------|  
|Odbc16gt.dll|16-Bit-ODBC-generischen thunking-DLL|  
|Odbc32gt.dll|32-Bit-ODBC-generischen thunking-DLL|  
|ODBCCP32.dll|32-Bit-Installationsprogramm DLL|  
|Odbcad32.exe|32-Bit-Administratorprogramm|  
|Odbcinst.hlp|Installer-Hilfedatei|  
|Ds16gt.dll|generische thunking DLL 16-Bit-Treiber-setup|  
|CTL3D32.dll|dreidimensionale Fenster 32-Bit-Bibliothek|  
  
 Darüber hinaus die folgenden Dateien zusammen mit der 16-Bit-ODBC-2.10 Treiber-Manager, die nicht Teil des ODBC 3.51 sind, sind erforderlich und sollte mit der 16-Bit-Anwendung installiert werden.  
  
|Dateiname|Description|  
|---------------|-----------------|  
|ODBC|16-Bit-Treiber-Manager|  
|Die Datei ODBCINST.dll|16-Bit-Installationsprogramm DLL|  
|Odbcadm.exe|16-Bit-ODBC-Administratorprogramm|
