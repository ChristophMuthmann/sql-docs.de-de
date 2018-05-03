---
title: Ausführen von Geschäftsobjekten in Komponentendienste | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9c82380ce591f9554a59b2cb3f816cdf9f1585b3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="running-business-objects-in-component-services"></a>Ausführen von Geschäftsobjekten in Komponentendienste
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Geschäftsobjekte können es sich um ausführbare Dateien (.exe) oder Dynamic Link Libraries (DLL) sein. Die Konfiguration, die Sie verwenden, um das Geschäftsobjekt ausgeführt wird, hängt davon ab, gibt an, ob das Objekt eine .dll oder .exe-Datei ist:  
  
-   Geschäftsobjekten als .exe-Dateien erstellt, können über DCOM aufgerufen werden. Wenn diese Geschäftsobjekte über Internet Information Services (IIS) verwendet werden, unterliegen sie zusätzliche Marshalling von Daten, die Clientleistung verlangsamt werden.  
  
-   Geschäftsobjekte erstellt, da die DLL-Dateien, die über IIS verwendet werden können und daher auch über HTTP. Sie können auch über DCOM nur über Component Services oder Microsoft Transaction Server, verwendet werden, bei Verwendung von Windows NT. Geschäftsobjekt DLLs müssen auf dem IIS-Servercomputer für den Zugriff über IIS registriert werden. Informationen zum Konfigurieren einer DLL zur Ausführung auf DCOM finden Sie im Abschnitt [Aktivieren einer DLL für die Ausführung auf DCOM](../../../ado/guide/remote-data-service/enabling-a-dll-to-run-on-dcom.md).  
  
> [!NOTE]
>  Wenn Geschäftsobjekten auf der mittleren Ebene werden als implementiert Component Services-Komponenten mit **GetObjectContext**, **SetComplete**, und **SetAbort**, das Unternehmen Objekte können Komponentendienste (oder MTS, bei Verwendung von Windows NT) Kontextobjekte Zustand über mehrere Clientaufrufe hinweg beibehalten. Dieses Szenario ist bei DCOM, die in der Regel zwischen vertrauenswürdigen Clients und Servern in einem Intranet implementiert wird. In diesem Fall die [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) Objekt und [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) Methode auf der Clientseite werden durch die Transaktion Context-Objekt ersetzt und **CreateInstance** Methode, die bereitgestellt werden, indem Sie die **ITransactionContext** Schnittstelle und von Komponentendienste implementiert.  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


