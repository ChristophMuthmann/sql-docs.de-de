---
title: "Registrieren von Geschäftsobjekten auf dem Client für die Verwendung mit DCOM | Microsoft Docs"
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
helpviewer_keywords: business objects in RDS [ADO]
ms.assetid: 75a21910-607f-463a-ae18-a17130dafb7e
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3828dcd05256914b4d640ecf4e0a318d80b08e08
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="registering-business-objects-on-the-client-for-use-with-dcom"></a>Registrieren von Geschäftsobjekten auf dem Client für die Verwendung mit DCOM
Benutzerdefinierte Geschäftsobjekte müssen sicherstellen, dass die Clientseite ihren Programmnamen (ProgId) eine ID (CLSID) zugeordnet werden können, die über DCOM verwendet werden kann. Aus diesem Grund muss die ProgID des DCOM-Objekte werden in der Registrierung die clientseitige und ordnen Sie die Klassen-ID des serverseitigen Business-Objekts. Für die anderen unterstützten Protokolle (HTTP, HTTPS und in-Process) ist dies nicht erforderlich.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Wenn Sie ein serverseitiges Geschäftsobjekt aufgerufen MyBObj mit einer bestimmten Klasse-ID, z. B. "{00112233-4455-6677-8899-00AABBCCDDEE}" zur Verfügung stellen Sie z. B. sicher, dass der Client-Side-Registrierung die folgenden Einträge hinzugefügt werden:  
  
```  
[HKEY_CLASSES_ROOT]  
\MyBObj\Clsid\(Default) "{00112233-4455-6677-8899-00AABBCCDDEE}"  
```


