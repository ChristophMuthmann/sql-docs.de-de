---
title: Installationskomponenten | Microsoft Docs
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
- installing ODBC components [ODBC], setup program
- ODBC [ODBC], component installation
ms.assetid: 9de15ca0-fe6a-4634-8709-a928d3c9cc73
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: eb01be821c1d3fd1d08c7a21b605354836d78a54
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="installation-components"></a>Installationskomponenten
> [!NOTE]  
>  Ab Windows XP und Windows Server 2003, ist ODBC in der Windows-Betriebssystem enthalten. Sie sollten nur explizit ODBC in früheren Versionen von Windows installieren.  
  
 Der Installationsvorgang gestartet, wenn der Benutzer das Setupprogramm ausführt. Das Setup-Programm funktioniert in Verbindung mit der *Installer DLL* und ein *Treiber-Setup-DLL* für jeden Treiber. Das Setup-Programm und das Installationsprogramm DLL verwenden Sie die Argumente in der **SQLInstallDriverEx** und **SQLInstallTranslatorEx** Funktionen, um zu bestimmen, welche Dateien kopieren oder Löschen für jede Komponente. Die folgende Abbildung zeigt die Beziehung zwischen diesen Installationskomponenten.  
  
 ![Beziehung zwischen Installationskomponenten](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]  
>  Die Odbc.inf-Datei, die in ODBC 2. verwendet wurde. *x* beschreiben Sie die Dateien, die benötigt werden. jede ODBC Komponente nicht in ODBC 3. verwendet*.x*. Treiber, die ODBC 3. liefern*.x* Komponenten müssen nicht zur Erstellung einer Odbc.inf-Datei. Das Entfernen der **SQLInstallDriver** und **SQLInstallODBC**, und die Veraltung von **SQLInstallTranslator**, Odbc.inf unnötige gerendert wurden. Der Treiberinformationen, mit der in den Abschnitten Driver-Schlüsselwort Odbc.inf werden, jetzt finden Sie in der *LpszDriver* Argument in **SQLInstallDriverEx**. Das Konvertierungsprogramm Informationen, die in [ODBC-Konvertierungsprogramm] verwendet und Konvertierer Spezifikation Abschnitte der Odbc.inf jetzt finden Sie unter der *LpszTranslator* Argument **SQLInstallTranslatorEx**. Diese Änderungen ermöglichen dem ODBC-Installer über Plattformen hinweg besser portierbar sein.  
  
 Weitere Informationen zu diesen Komponenten finden Sie unter den folgenden Themen am Ende dieses Abschnitts.  
  
-   [Setupprogramm](../../../odbc/reference/install/setup-program.md)  
  
-   [Installationsprogramm-DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [Setup-DLL für Treiber](../../../odbc/reference/install/driver-setup-dll.md)
