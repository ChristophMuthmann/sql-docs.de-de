---
title: "Festlegen von Verschlüsselungsoptionen auf Zielservern | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, encryption
- target servers [SQL Server], encryption
- multiserver environments [SQL Server], setting encryption options on target servers
ms.assetid: 1a9fd539-e166-4ea8-9f21-ac400ca74dee
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a7a7204e78c23ef6a4c5309f0c8f45d756f740fb
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="set-encryption-options-on-target-servers"></a>Festlegen von Verschlüsselungsoptionen auf Zielservern
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Wenn Sie für die verschlüsselte SSL-Kommunikation (Secure Sockets Layer) zwischen Masterservern und einigen oder allen Zielservern kein Zertifikat verwenden können, aber den Kanal zwischen diesen verschlüsseln möchten, müssen Sie auf dem Zielserver die erforderliche Sicherheitsstufe konfigurieren.  
  
Zum Konfigurieren der für einen bestimmten Kommunikationskanal zwischen einem Master- und einem Zielserver erforderlichen geeigneten Sicherheitsstufe legen Sie den Registrierungsunterschlüssel **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\**\<*instance_name*>**\SQLServerAgent\MsxEncryptChannelOptions(REG_DWORD)** für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent auf dem Zielserver auf einen der folgenden Werte fest. Der Wert von \<*Instanz_Name*> ist **MSSQL.***n*. Beispiel: **MSSQL.1** oder **MSSQL.3**.  
  
|value|Description|  
|---------|---------------|  
|**0**|Deaktiviert die Verschlüsselung zwischen diesem Zielserver und dem Masterserver. Wählen Sie diese Option nur aus, wenn der Kanal zwischen Zielserver und Masterserver auf andere Weise gesichert ist.|  
|**1**|Aktiviert nur die Verschlüsselung zwischen diesem Zielserver und dem Masterserver, eine Zertifikatüberprüfung ist jedoch nicht erforderlich.|  
|**2**|Aktiviert die vollständige SSL-Verschlüsselung und Zertifikatüberprüfung zwischen diesem Zielserver und dem Masterserver. Dies ist die Standardeinstellung. Es wird empfohlen, diesen Wert nicht zu ändern, es sei denn, dafür liegen spezifische Gründe vor.|  
  
Wenn **1** oder **2** angegeben wird, muss SSL sowohl auf dem Master- als auch auf dem Zielserver aktiviert sein. Wenn **2** angegeben wird, muss außerdem auf dem Masterserver ein ordnungsgemäß signiertes Zertifikat vorhanden sein.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry_md.md)]  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Vorgehensweise: Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul (SQL Server-Konfigurations-Manager).](http://msdn.microsoft.com/en-us/e1e55519-97ec-4404-81ef-881da3b42006)  
  
