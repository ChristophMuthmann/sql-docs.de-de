---
title: "Registrieren ein benutzerdefiniertes Geschäftsobjekt | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- custom business object in RDS [ADO]
- registering custom business objects in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: e9032ad8-d14c-42e3-ba13-cb5f00084a79
caps.latest.revision: "19"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c121ddf9e271f4dfb67490d77a719267cfa11a3b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="registering-a-custom-business-object"></a>Registrieren ein benutzerdefiniertes Geschäftsobjekt
Um ein benutzerdefiniertes Geschäftsobjekt (.dll oder .exe) erfolgreich über den Webserver zu starten, muss das Geschäftsobjekt ProgID in der Registrierung eingegeben werden, wie in diesem Verfahren beschrieben. Dieses Feature von RDS schützt die Sicherheit Ihres Webservers, indem nur zulässige ausführbare Dateien ausgeführt.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
> [!NOTE]
>  Für MDAC 2.0 und höher und Windows DAC, die Business-Standardobjekt [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), ist nicht standardmäßig während der Installation von MDAC/Windows DAC registriert. Jedoch wenn **RDSServer.DataFactory** registriert wurde, als für die Ausführung auf dem Computer vor der Installation sicher, wird der Registrierungseintrag für die neue Installation beibehalten.  
  
### <a name="to-register-a-custom-business-object"></a>So registrieren Sie ein benutzerdefiniertes Geschäftsobjekt:  
  
1.  Klicken Sie auf **starten** , und klicken Sie dann auf **ausführen**.  
  
2.  Typ **RegEdit** , und klicken Sie auf **OK**.  
  
3.  Navigieren Sie im Registrierungs-Editor zu den **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch** Registrierungsschlüssel.  
  
4.  Wählen Sie die **ADCLaunch** Schlüssel, und klicken Sie dann im die **bearbeiten**Sie im Menü **neu** , und klicken Sie auf **Schlüssel**.  
  
5.  Geben Sie die ProgID des benutzerdefinierten Geschäftsobjekts, und klicken Sie auf **EINGABETASTE**. Lassen Sie die **Wert** Eintrag leer.


