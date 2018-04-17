---
title: Verwenden 32-Bit-Anwendungen mit 32-Bit-Treibern | Microsoft Docs
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
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
ms.assetid: 0cdd5788-5642-4280-8d53-b4ec461aafa1
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 008f948580057fdaa6e59802fd6fa8395140b735
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>Verwenden 32-Bit-Anwendungen mit 32-Bit-Treiber
Sie können die 32-Bit-Anwendungen mit 32-Bit-Treiber ausführen. Verwenden die 32-Bit-Anwendungen und die 32-Bit-Treiber der Win32®-API.  
  
## <a name="architecture"></a>Aufbau  
 Die folgende Abbildung zeigt, wie die 32-Bit-Anwendungen mit 32-Bit-Treiber kommunizieren. Die Anwendung ruft die 32-Bit-Treiber-Managers, die ihrerseits 32-Bit-Treiber.  
  
 ![Wie 32&#45;Bit-apps kommunizieren mit 32&#45;bit-Treiber](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  Verwenden Sie die 32-Bit-Installationsprogramm thunking DLL nicht auf Windows NT/Windows2000 aus. Obwohl es auf den gleichen Namen wie das Installationsprogramm für 32-Bit-DLL hat, ist es eine andere DLL.  
  
## <a name="administration"></a>Verwaltung  
 Sie können Datenquellen für 32-Bit-Treibern mithilfe von ODBC-Datenquellen-Administrator verwalten. Um den ODBC-Administrator auf Computern unter Windows 2000 zu öffnen, öffnen Sie die Windows-Systemsteuerung, doppelklicken Sie auf **Verwaltung**, und doppelklicken Sie dann auf **Datenquellen (ODBC)**. Auf Computern unter früheren Versionen von Microsoft Windows lautet das Symbol " **32-Bit-ODBC-** oder einfach **ODBC**.  
  
## <a name="components"></a>Components  
 Die ODBC-Komponente enthält die folgenden Dateien für die Ausführung von 32-Bit-Anwendungen mit 32-Bit-Treiber. Diese Komponenten sind im Verzeichnis \Redist.  
  
|Dateiname|Description|  
|---------------|-----------------|  
|Datei "ODBC32.dll"|32-Bit-Treiber-Manager|  
|ODBCCP32.dll|32-Bit-Installationsprogramm DLL|  
|Odbcad32.exe|32-Bit-ODBC-Administratorprogramm|  
|Odbcinst.hlp|Installer-Hilfedatei|  
|Msvcrt40.dll|C-Laufzeitbibliothek|
