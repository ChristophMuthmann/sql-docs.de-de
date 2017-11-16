---
title: Bereitstellen von PowerPivot und Power View - Multi-Tier SharePoint 2016 Farm | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e36a632-0750-4247-92b6-1fe38c7a4ce2
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d7dc4fc8e7b1926359096447183dc17c9c1a1cd8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="deploy-powerpivot-and-power-view---multi-tier-sharepoint-2016-farm"></a>Bereitstellen von PowerPivot und Power View - Multi-Tier SharePoint 2016 Farm
  **Zusammenfassung:** Dieses Whitepaper bietet SharePoint-Administratoren und Architekten detaillierte Anleitungen für die Bereitstellung und Konfiguration einer Microsoft BI Demo-Umgebung in einer SharePoint-Farm mit mehreren Servern auf Grundlage der Preview-Versionen von SharePoint Server 2016, Office Online-Server und des SQL Server 2016 BI-Stack für SharePoint 2016. Nach einer kurzen Einführung wichtiger architektonischer Änderungen und entsprechender Systemabhängigkeiten werden Software-und Konfigurationsanforderungen sowie der empfohlene Bereitstellungspfad für die Aktivierung und Überprüfung der BI-Funktionen in drei Hauptphasen beschrieben. Dieses Whitepaper behandelt auch bekannte Probleme in SharePoint Server 2016 Beta 2, Office Online Server Preview und SQL Server 2016 CTP 3.1 mit entsprechenden Lösungs- bzw. Umgehungsvorschlägen. In den endgültigen Produktversionen sind diese Umgehungen nicht mehr erforderlich. Überprüfen Sie vor der Bereitstellung von RTM-Releases, ob es eine aktuellere Version dieses Whitepapers gibt.  
  
 **Autor:**Kay Unkroth, Jason Haak  
  
 **Technische Bearbeiter:** Adam Saxton, Anne Zorner, Craig Guyer, Frank Weigel, Gregory Appel, Heidi Steen, Kasper de Jonge, Kirk Stark, Klaus Sobel, Mike Plumley, Mike Taghizadeh, Patrick Wheeler, Riccardo Muti, Steve Hord  
  
 **Veröffentlicht:**Januar 2016  
  
 **Gilt für:** SQL Server 2016 CTP3.1, SharePoint 2016 Preview, Office Online Server Preview  
  
 Wenn Sie dieses englischsprachige Whitepaper lesen möchten, laden Sie das Word-Dokument [Deploying SQL Server 2016 PowerPivot and Power View in a Multi-Tier SharePoint 2016 Farm](http://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/Deploying%20SQL%20Server%202016%20PowerPivot%20and%20Power%20View%20in%20a%20Multi-Tier%20SharePoint%202016%20Farm.docx) herunter.  
  
  

