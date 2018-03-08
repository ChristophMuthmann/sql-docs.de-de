---
title: Testen der Berechtigungen eines Benutzers (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 83a03b85-ea7f-4b4a-b19b-f7eca534ffae
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5c84a7d6c678f7bf98d62ed63e78b6922243c7e
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2018
---
# <a name="test-a-user39s-permissions-master-data-services"></a>Testen der Berechtigungen eines Benutzers (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie einen Testbenutzer erstellen und sich bei der Webanwendung anmelden, um Berechtigungen zu testen. Wenn ein Benutzer versucht, auf die [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -URL zuzugreifen, werden die Anmeldeinformationen des Benutzers authentifiziert. In Internet Explorer wird über Sicherheitseinstellungen gesteuert, ob dies automatisch stattfindet oder ob der Benutzer einen Benutzernamen und ein Kennwort eingeben muss. Um diese Einstellungen zu ändern, führen Sie die folgenden Schritte aus:  
  
### <a name="to-test-a-users-security"></a>So testen Sie die Sicherheitseinstellungen für einen Benutzer  
  
1.  Klicken Sie in Internet Explorer 7 und höher auf **Extras**, **Internetoptionen**und dann auf die Registerkarte **Sicherheit** .  
  
2.  Klicken Sie auf **Lokales Intranet** und dann auf die Schaltfläche **Stufe anpassen** .  
  
3.  Wählen Sie im Abschnitt **Benutzerauthentifizierung** die Option **Nach Benutzername und Kennwort fragen**aus.  
  
4.  Das nächste Mal, wenn Sie das Browserfenster öffnen, werden Sie zur Eingabe eines Benutzernamens und Kennworts aufgefordert.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Sicherheit &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  
