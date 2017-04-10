---
title: "Identifizieren der Quelle von Paketen mit digitalen Signaturen | Microsoft Docs"
ms.custom: ""
ms.date: "08/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Signieren von Paketen [Integration Services]"
  - "Zertifikate [Integration Services]"
  - "Pakete [Integration Services], Sicherheit"
  - "Sicherheit [Integration Services], Zertifikate"
  - "Signaturrichtlinien [Integration Services]"
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
caps.latest.revision: 46
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 46
---
# Identifizieren der Quelle von Paketen mit digitalen Signaturen
  Ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paket kann mit einem digitalen Zertifikat signiert werden, um seine Quelle zu identifizieren. Nachdem das Paket mit einem digitalen Zertifikat signiert wurde, können Sie die digitale Signatur vor dem Laden des Pakets mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] überprüfen. Damit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] die Signatur prüft, legen Sie eine Option entweder in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] oder im **dtexec**-Hilfsprogramm (dtexec.exe) fest, oder geben Sie einen optionalen Registrierungswert an.  
  
## Signieren eines Pakets mit einem digitalen Zertifikat  
 Bevor Sie ein Paket mit einem digitalen Zertifikat signieren können, müssen Sie zunächst ein Zertifikat abrufen oder erstellen. Sobald Sie das Zertifikat vorliegen haben, können Sie es zum Signieren des Pakets verwenden. Weitere Informationen zum Abrufen eines Zertifikats und zum Signieren eines Pakets mit diesem Zertifikat finden Sie unter [Signieren eines Pakets mit einem digitalen Zertifikat](../../integration-services/packages/sign-a-package-by-using-a-digital-certificate.md).  
  
## Festlegen einer Option zum Überprüfen der Paketsignatur  
 Sowohl [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] als auch das **dtexec**-Hilfsprogramm bieten eine Option, mit der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] für die Überprüfung der digitalen Signatur eines signierten Pakets konfiguriert wird. Ob Sie [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] oder das **dtexec**-Hilfsprogramm verwenden, hängt davon ab, ob Sie alle Pakete oder nur bestimmte Pakete überprüfen möchten:  
  
-   Wählen Sie die Option **Digitale Signatur beim Laden eines Pakets überprüfen** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] aus, um die digitale Signatur aller Pakete vor dem Laden der Pakete zum Entwurfszeitpunkt zu überprüfen. Diese Option ist eine globale Einstellung für alle Pakete in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].
  
-   Zum Überprüfen der digitalen Signatur eines einzelnen Pakets legen Sie die Option **/VerifyS[igned]** fest, wenn Sie das Paket mit dem **dtexec**-Hilfsprogramm ausführen. Weitere Informationen finden Sie unter [dtexec Utility](../../integration-services/packages/dtexec-utility.md).  
  
## Festlegen eines Registrierungswerts zum Überprüfen der Paketsignatur  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] unterstützt außerdem den optionalen Registrierungswert **BlockedSignatureStates**, mit dem Sie die Richtlinie einer Organisation zum Laden von signierten und nicht signierten Paketen verwalten können. Der Registrierungswert kann das Laden von Paketen verhindern, wenn die Pakete nicht signiert sind, oder ungültige oder nicht vertrauenswürdige Signaturen enthalten. Weitere Informationen zum Festlegen des Registrierungswerts finden Sie unter [Implementieren einer Signaturrichtlinie durch Festlegen eines Registrierungswerts](../../integration-services/packages/implement-a-signing-policy-by-setting-a-registry-value.md).  
  
> **HINWEIS**: Der optionale Registrierungswert **BlockedSignatureStates** kann eine Einstellung angeben, die restriktiver ist als die Option für die digitale Signatur, die in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] oder in der **dtexec**-Befehlszeile festgelegt wurde. In dieser Situation überschreibt die restriktivere Registrierungseinstellung die andere Einstellung.  
  
## Siehe auch  
 [Integration Services-Pakete &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md)   
 [Sicherheitsübersicht &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)  
  
  