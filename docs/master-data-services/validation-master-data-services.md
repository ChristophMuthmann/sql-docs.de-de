---
title: Überprüfung (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 98eb49e7-b190-4a21-8316-08c07cde14ed
caps.latest.revision: 12
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 51f80ad82de3996cb602ddb348110f4083e1607a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="validation-master-data-services"></a>Überprüfung (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]werden Daten überprüft, um deren Genauigkeit sicherzustellen. Ein Teil der Überprüfung erfolgt automatisch und ein Teil basiert auf Geschäftsregeln, die von Administratoren erstellt werden.  
  
## <a name="when-data-validation-occurs"></a>Durchführen von Überprüfungen  
 Die Überprüfung tritt zu unterschiedlichen Zeiten auf und wird in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Webanwendung unterschiedlich angezeigt.  
  
|Überprüfungstyp|Standards bestimmt durch|Zeitpunkt des Auftretens|Angezeigt in der MasterData Manager-Webbenutzeroberfläche als|Angezeigt im Add-In für Excel als|Werden Daten im MDS-Repository gespeichert?|  
|---------------------|-----------------------------|--------------------|---------------------------------------------------|-------------------------------------------|------------------------------------------|  
|Überprüfung anhand Geschäftsregeln|MDS-Administrator|Automatisch beim Hinzufügen oder Bearbeiten von Daten.<br /><br /> Manuell, wenn ein Benutzer Geschäftsregeln anwendet.<br /><br /> Manuell, wenn ein Administrator im Funktionsbereich **Versionsverwaltung** der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung eine Version anhand von Geschäftsregeln überprüft.|Überprüfungsfehler|ValidationStatus|ja|  
|Datentyp und Inhaltsüberprüfung|MDS-Administrator beim Erstellen von Modellobjekten (z. B. Länge oder Datentyp eines Attributs)|Automatisch beim Hinzufügen oder Bearbeiten von Daten|Eingabefehler|InputStatus|nein|  
|Datentyp und Inhaltsüberprüfung|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] oder [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|Automatisch beim Hinzufügen oder Bearbeiten von Daten|Eingabefehler|InputStatus|nein|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Erstellen Sie Geschäftsregeln zum Überprüfen von Daten, und veröffentlichen Sie sie.|[Erstellen und Veröffentlichen einer Geschäftsregel &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|Überprüfen Sie eine Version der Daten anhand von Geschäftsregeln. Nur Administratoren.|[Überprüfen einer Version anhand von Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)|  
|Überprüfen Sie bestimmte Teilmengen der Daten anhand von Geschäftsregeln. Alle Benutzer mit Zugriffsberechtigung auf den Funktionsbereich **Explorer** .|[Überprüfen von bestimmten Elementen auf Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)|  
|Überprüfen Sie bestimmte Teilmengen der Daten anhand von Geschäftsregeln. Alle Benutzer mit der Zugriffsberechtigung auf den Funktionsbereich **Explorer** und die mit [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]arbeiten.|[Anwenden von Geschäftsregeln &#40;MDS-Add-In für Excel&#41;](../master-data-services/microsoft-excel-add-in/apply-business-rules-mds-add-in-for-excel.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
