---
title: "Sicherheitseigenschaften | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "Sicherheit [Analysis Services], Eigenschaften"
  - "SecurityPackageList (Eigenschaft)"
  - "BuiltinAdminsAreServerAdmins (Eigenschaft)"
  - "DisableClientImpersonation (Eigenschaft)"
  - "ErrorMessageMode (Eigenschaft)"
  - "RequiredProtectionLevel (Eigenschaft)"
  - "ServiceAccountIsServerAdmin (Eigenschaft)"
  - "RequireClientAuthentication (Eigenschaft)"
ms.assetid: 2fc7fe10-0cbb-49ac-aa8c-8ec3f7a7705f
caps.latest.revision: 15
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 15
---
# Sicherheitseigenschaften
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] werden die in der folgenden Tabelle aufgeführten Sicherheitseigenschaften des Servers aufgeführt. Weitere Informationen zu zusätzlichen Servereigenschaften und zum Festlegen dieser Eigenschaften finden Sie unter [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Gilt für:** mehrdimensionalen und Tabellenservermodus  
  
## Eigenschaften  
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
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|*0*|Keine, Klartext ist zulässig|  
|*1*|(Standard) Verschlüsselung erforderlich, keine Klartextprotokollierung|  
|*2*|Klartextanforderungen zulässig, aber nur mit Signaturen (schwächer als die Verschlüsselung)|  
  
 **AdministrativeDataProtection\RequiredProtectionLevel**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
## Siehe auch  
 [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Bestimmen des Servermodus einer Analysis Services-Instanz](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  