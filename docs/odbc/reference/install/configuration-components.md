---
title: Konfigurationskomponenten | Microsoft Docs
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
- data sources [ODBC], configuring
ms.assetid: 0b68ff48-12e4-41aa-b9e2-b39ed5023ea7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a9f3796703c2e778f9685714dcae2f541aa2b9a8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configuration-components"></a>Konfigurationskomponenten
> [!NOTE]  
>  Ab Windows XP und Windows Server 2003, ist ODBC in der Windows-Betriebssystem enthalten. Sie sollten nur explizit ODBC in früheren Versionen von Windows installieren.  
  
 Datenquellen werden vom Installationsprogramm DLL konfiguriert DLLs und Translator-Setup-DLLs in Turn Aufrufe Treiber einrichten, wie sie benötigt werden. Das Installationsprogramm DLL ist entweder direkt über die Systemsteuerung aufgerufen oder geladen und aufgerufen werden, von einem anderen Programm, bekannt als die *-Verwaltungsprogramm*. Die folgende Abbildung zeigt die Beziehung zwischen den Konfigurationskomponenten.  
  
 ![Beziehung zwischen Konfigurationskomponenten](../../../odbc/reference/install/media/pr30.gif "pr30")  
  
 Weitere Informationen zu diesen Komponenten finden Sie unter den folgenden Themen am Ende dieses Abschnitts.  
  
-   [Setupprogramm](../../../odbc/reference/install/setup-program.md)  
  
-   [Installationsprogramm-DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [Setup-DLL für Treiber](../../../odbc/reference/install/driver-setup-dll.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Installationskomponenten](../../../odbc/reference/install/installation-components.md)
