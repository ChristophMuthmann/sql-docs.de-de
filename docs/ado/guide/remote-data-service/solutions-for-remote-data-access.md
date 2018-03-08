---
title: "Lösungen für Remotedatenzugriff | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS [ADO]
ms.assetid: d311cc67-7db7-4c43-9590-d465564695e4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2377f7a33f8426d7081806980618c432a56bba42
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="solutions-for-remote-data-access"></a>Lösungen für Remotedatenzugriff
## <a name="the-issue"></a>Das Problem  
 ADO kann die Anwendung direkt Zugriff auf und Ändern von Datenquellen (mitunter als ein 2-Ebenen-System). Beispielsweise ist die Verbindung mit der Datenquelle, die Ihre Daten enthält, ist, die eine direkte Verbindung in einem zweistufigen System.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Möglicherweise möchten jedoch indirekt über einen Mittler z. B. Microsoft® Internet Information Services (IIS) den Zugriff auf Datenquellen. Diese Anordnung wird manchmal eine dreistufige System bezeichnet. IIS ist ein Client/Server-System, das eine effiziente Möglichkeit für eine lokale oder Client-Anwendung zum Aufrufen eines Programms Remote- oder Server, über das Internet oder Intranet bereitstellt. Die Server-Anwendung erhält Zugriff auf die Datenquelle und optional die erfassten Daten verarbeitet.  
  
 Die Intranet-Webseite enthält beispielsweise eine Anwendung in Microsoft® Visual Basic Scripting Edition (VBScript), der an IIS eine Verbindung herstellt. IIS wiederum eine Verbindung mit der tatsächlichen Datenquelle her, ruft die Daten ab, verarbeitet diese in irgendeiner Form und klicken Sie dann die verarbeitete Daten an die Anwendung zurückgegeben.  
  
 In diesem Beispiel verbunden die Anwendung nie direkt mit der Datenquelle. IIS wurde. Und IIS Zugriff auf die Daten mithilfe von ADO.  
  
> [!NOTE]
>  Die Client/Server-Anwendung muss nicht auf das Internet oder Intranet basieren (d. h. Web-based) – Es könnte darin bestehen, ausschließlich der kompilierte Programme auf einem lokalen Netzwerk. Allerdings ist der Normalfall eine webbasierte Anwendung.  
  
 Da einige visuelle Kontrolle, z. B. ein Raster, Kontrollkästchen oder Liste, die die zurückgegebene Informationen verwenden kann, muss die zurückgegebene Informationen problemlos von einem visual-Steuerelement verwendet werden.  
  
 Sie möchten eine einfache und effiziente Anwendung Programmierung-Schnittstelle, die unterstützt drei Ebenen Systeme und gibt Informationen als einfach als wäre es abgerufen wurde auf einem System zwei Ebenen. Remote Data Service (RDS) ist diese Schnittstelle.  
  
## <a name="the-solution"></a>Die Lösung  
 RDS definiert ein Programmiermodell – die Abfolge von Aktivitäten, die zum Zugriff auf und Aktualisieren einer Datenquelle erforderlich sind – für den Zugriff auf Daten über einen Mittler, beispielsweise Internet Information Services (IIS). Das Programmiermodell werden zusammengefasst, die gesamte Funktionalität von RDS.  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegende RDS-Programmiermodell](../../../ado/guide/remote-data-service/basic-rds-programming-model.md)   
 [RDS-Szenario](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS-Lernprogramm](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Verwendung und Sicherheit von RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


