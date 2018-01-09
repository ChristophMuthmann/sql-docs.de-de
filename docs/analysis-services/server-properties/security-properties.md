---
title: Sicherheitseigenschaften | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- security [Analysis Services], properties
- SecurityPackageList property
- BuiltinAdminsAreServerAdmins property
- DisableClientImpersonation property
- ErrorMessageMode property
- RequiredProtectionLevel property
- ServiceAccountIsServerAdmin property
- RequireClientAuthentication property
ms.assetid: 2fc7fe10-0cbb-49ac-aa8c-8ec3f7a7705f
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e99cf48fc3eb863b0a0d1e04fc19e83655ccc47f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="security-properties"></a>Sicherheitseigenschaften
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] unterstützt die Sicherheitseigenschaften des Servers in der folgenden Tabelle aufgeführt. Weitere Informationen zu zusätzlichen Servereigenschaften und zum Festlegen dieser Eigenschaften finden Sie unter [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Gilt für:** mehrdimensionalen und Tabellenservermodus  
  
## <a name="properties"></a>Eigenschaften  
 **RequireClientAuthentication**  
 Eine boolesche Eigenschaft, die anzeigt, ob eine Client-Authentifizierung erforderlich ist.  
  
 Der Standardwert für diese Eigenschaft ist auf True festgelegt, was anzeigt, dass eine Client-Authentifizierung erforderlich ist.  
  
 **SecurityPackageList**  
 Eine Zeichenfolgeneigenschaft, die eine Liste mit durch Trennzeichen getrennten SSPI-Paketen enthält, die vom Server zur Client-Authentifizierung verwendet werden.  
  
 **DisableClientImpersonation**  
 Eine boolesche Eigenschaft, die anzeigt, ob Clientidentitätswechsel (z. B. für gespeicherte Prozeduren) deaktiviert sind.  
  
 Der Standardwert für diese Eigenschaft ist auf False festgelegt, was anzeigt, dass Clientidentitätswechsel aktiviert sind.  
  
 **BuiltinAdminsAreServerAdmins**  
 Eine boolesche Eigenschaft, die anzeigt, ob Mitglieder der Gruppe Administratoren auf dem lokalen Computer Administratoren von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sind.  
  
 **ServiceAccountIsServerAdmin**  
 Eine boolesche Eigenschaft, die anzeigt, ob das Dienstkonto ein Serveradministrator ist.  
  
 Der Standardwert für diese Eigenschaft ist auf True festgelegt, was anzeigt, dass das Dienstkonto ein Serveradministrator ist.  
  
 **ErrorMessageMode**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **DataProtection\RequiredProtectionLevel**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die die erforderliche Schutzebene für alle Clientanforderungen definiert. Diese Eigenschaft hat einen der in der folgenden Tabelle aufgeführten Werte.  
  
|value|Description|  
|-----------|-----------------|  
|*0*|Keine, Klartext ist zulässig|  
|*1*|(Standard) Verschlüsselung erforderlich, keine Klartextprotokollierung|  
|*2*|Klartextanforderungen zulässig, aber nur mit Signaturen (schwächer als die Verschlüsselung)|  
  
 **AdministrativeDataProtection\RequiredProtectionLevel**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Bestimmen des Servermodus einer Analysis Services-Instanz](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
