---
title: CLR Integration Code Access Security | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- UNSAFE assemblies
- permissions [CLR integration]
- common language runtime [SQL Server], security
- SAFE assemblies
- code access security [CLR integration]
- EXTERNAL_ACCESS assemblies
ms.assetid: 2111cfe0-d5e0-43b1-93c3-e994ac0e9729
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b93a1955adb6f38eebd8de86599e1861a80ff75b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="clr-integration-code-access-security"></a>CLR-Integration und Codezugriffssicherheit
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Die common Language Runtime (CLR) unterstützt ein Sicherheitsmodell der Codezugriffssicherheit für verwalteten Code. In diesem Modell werden Assemblys Berechtigungen auf Grundlage der Identität des Codes gewährt. Weitere Informationen finden Sie im Abschnitt "Codezugriffsicherheit" im .NET Framework Software Development Kit.  
  
 Die Sicherheitsrichtlinie, die die Berechtigungen für Assemblys bestimmt, wird an drei verschiedenen Stellen definiert:  
  
-   Computerrichtlinie: Diese Richtlinie gilt für den gesamten verwalteten Code auf dem Computer, auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] installiert ist.  
  
-   Benutzerrichtlinie: Diese Richtlinie ist für verwalteten Code gültig, der von einem Prozess gehostet wird. Für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gilt die Benutzerrichtlinie für das Windows-Konto, unter dem der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Dienst ausgeführt wird.  
  
-   Hostrichtlinie: Diese Richtlinie wird vom Host der CLR (in diesem Fall [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) eingerichtet, die für den verwalteten Code gültig ist, der auf diesem Host ausgeführt wird.  
  
 Der von der CLR unterstützte Codezugriffs-Sicherheitsmechanismus basiert auf der Annahme, dass die Laufzeit sowohl vollständig vertrauenswürdigen als auch teilweise vertrauenswürdigen Code hosten kann. Die durch die CLR-Codezugriffssicherheit geschützten Ressourcen sind üblicherweise von verwalteten Anwendungsprogrammierschnittstellen umgeben, die die entsprechende Berechtigung vor dem Zugriff auf die Ressource erfordern. Die Anforderung der Berechtigung ist nur dann erfüllt, wenn alle aufrufenden Prozesse (auf Assemblyebene) in der Aufrufliste über die entsprechende Ressourcenberechtigung verfügen.  
  
 Die Menge der Codezugriffsberechtigungen, die verwaltetem Code gewährt werden, wenn dieser innerhalb von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ausgeführt wird, ist die Schnittmenge der Berechtigungen, die auf den drei oben genannten Richtlinienebenen erteilt werden. Auch wenn [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] einer in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] geladenen Assembly einen Berechtigungssatz gewährt, kann der schließlich für Benutzercode gewährte Berechtigungssatz durch die Richtlinien auf Computer- und Benutzerebenen weiter eingeschränkt sein.  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>Berechtigungssätze auf SQL Server Host-Richtlinienebene  
 Die Menge der Codezugriffsberechtigungen, die Assemblys von der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Hostrichtlinienebene gewährt wird, wird von dem Berechtigungssatz bestimmt, der beim Erstellen der Assembly angegeben wurde. Es existieren drei Berechtigungssätze: **sichere**, **EXTERNAL_ACCESS** und **UNSAFE** (angegeben mit der **PERMISSION_SET** -Option von [ Erstellen Sie die ASSEMBLY &#40; Transact-SQL &#41; ](../../../t-sql/statements/create-assembly-transact-sql.md)).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] liefert eine Hostebene Sicherheitsrichtlinie auf Hostebene CLR beim hosten. Diese Richtlinie ist eine zusätzliche Richtlinienebene unterhalb der zwei Richtlinienebenen dar, die immer gültig sind. Die Richtlinie wird für jede Anwendungsdomäne festgelegt, die von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]erstellt wird. Sie ist nicht für die Standardanwendungsdomäne bestimmt, die gültig ist, wenn [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] eine Instanz der CLR erstellt.  
  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Richtlinie auf Hostebene ist eine Kombination der festen Richtlinie von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] für Systemassemblys und der benutzerdefinierten Richtlinie für Benutzerassemblys.  
  
 Die feste Richtlinie für CLR-Assemblys und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Systemassemblys verleiht ihnen volle Vertrauenswürdigkeit.  
  
 Der benutzerdefinierte Teil der Hostrichtlinie von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] basiert darauf, dass der Assemblybesitzer einen von drei Berechtigungsbuckets für jede Assembly angibt. Weitere Informationen über die unten aufgeführten Sicherheitsberechtigungen finden Sie unter .NET Framework SDK.  
  
### <a name="safe"></a>SAFE  
 Nur interne Berechnungen und lokaler Datenzugriff sind zulässig. **Sichere** ist der restriktivste Berechtigungssatz. Code, der ausgeführt wird, von einer Assembly mit **sichere** Berechtigungen können nicht auf externe Systemressourcen wie Dateien, das Netzwerk, Umgebungsvariablen oder die Registrierung zugreifen.  
  
 **Sichere** Assemblys verfügen über folgende Berechtigungen und Werte:  
  
|Berechtigung|Wert(e)/Beschreibung|  
|----------------|-----------------------------|  
|**SecurityPermission**|**Ausführung:** über die Berechtigung zum Ausführen von verwaltetem Code.|  
|**SqlClientPermission**|**Kontextverbindung = "true"**, **kontextverbindung = Yes**: nur die kontextverbindung verwendet werden kann und die Verbindungszeichenfolge nur Sie den Wert geben kann "kontextverbindung =" true "" oder "Context Connection = Yes".<br /><br /> **AllowBlankPassword = "false":** leere Kennwörter sind nicht zulässig.|  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS-Assemblys über die gleichen Berechtigungen wie **sichere** Assemblys, mit der zusätzlichen Fähigkeit, auf externe Systemressourcen wie Dateien, Netzwerke, Umgebungsvariablen und die Registrierung zuzugreifen.  
  
 **EXTERNAL_ACCESS** Assemblys verfügen außerdem über folgende Berechtigungen und Werte:  
  
|Berechtigung|Wert(e)/Beschreibung|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|**Unbeschränkte:** verteilte Transaktionen sind zulässig.|  
|**DNSPermission**|**Unbeschränkte:** Berechtigungen zum Anfordern von Informationen von DNS-Servern.|  
|**EnvironmentPermission**|**Unbeschränkte:** vollständigen Zugriff auf System- und Benutzerumgebungsvariablen ist zulässig.|  
|**EventLogPermission**|**Verwalten Sie** die folgenden Aktionen sind zulässig: Erstellen einer Ereignisquelle, lesen vorhandener Protokolle, Löschen von Ereignisquellen oder Protokollen, reagieren auf Einträge, Löschen eines Ereignisprotokolls, Überwachen von Ereignissen und Zugreifen auf eine Auflistung sämtlicher Ereignisprotokolle.|  
|**FileIOPermission**|**Unbeschränkte:** vollen Zugriff auf Dateien und Ordner zulässig ist.|  
|**KeyContainerPermission**|**Unbeschränkte:** vollständigen Zugriff auf Schlüsselcontainer ist zulässig.|  
|**NetworkInformationPermission**|**Zugriff:** Ping ist zulässig.|  
|**RegistryPermission**|Lässt Leseberechtigungen für **HKEY_CLASSES_ROOT**, **HKEY_LOCAL_MACHINE**, **HKEY_CURRENT_USER**, **HKEY_CURRENT_CONFIG**, und  **HKEY_USERS.**|  
|**SecurityPermission**|**Assertion:** Fähigkeit zu bestätigen, dass alle Aufrufer dieses Codes über die erforderliche Berechtigung für den Vorgang verfügen.<br /><br /> **ControlPrincipal:** können Sie das principal-Objekt zu ändern.<br /><br /> **Ausführung:** über die Berechtigung zum Ausführen von verwaltetem Code.<br /><br /> **SerializationFormatter:** Möglichkeit zum Bereitstellen von Serialisierungsdiensten.|  
|**SmtpPermission**|**Zugriff:** ausgehende Verbindungen mit SMTP-Host, Port 25 sind zulässig.|  
|**SocketPermission**|**Eine Verbindung herstellen:** ausgehende Verbindungen (alle Ports, alle Protokolle) auf einer Transportadresse werden zugelassen.|  
|**SqlClientPermission**|**Unbeschränkte:** vollständigen Zugriff auf die Datenquelle ist zulässig.|  
|**StorePermission**|**Unbeschränkte:** vollen Zugriff auf x. 509-Zertifikat speichert zulässig ist.|  
|**WebPermission**|**Eine Verbindung herstellen:** ausgehende Verbindungen an Webressourcen werden zugelassen.|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE ermöglicht Assemblys den uneingeschränkten Zugriff auf Ressourcen sowohl innerhalb als auch außerhalb [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Code ausführen, die innerhalb einer **UNSAFE** Assembly kann auch nicht verwalteten Code aufrufen.  
  
 **Unsichere** Assemblys erhalten **FullTrust**.  
  
> [!IMPORTANT]  
>  **Sichere** ist die empfohlene berechtigungseinstellung für Assemblys, die berechnungs- und Verwaltungsaufgaben ausführen, ohne den Zugriff auf Ressourcen außerhalb [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **EXTERNAL_ACCESS** wird empfohlen, Assemblys, die Zugriff auf Ressourcen außerhalb [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **EXTERNAL_ACCESS** Assemblys standardmäßig ausgeführt wird, als die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienstkonto. Es ist möglich, dass **EXTERNAL_ACCESS** Code explizit Windows-Authentifizierung-Sicherheitskontext des Aufrufers annehmen. Aufgrund der standardmäßigen Ausführung als die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Dienstkonto und die Berechtigung zum Ausführen von **EXTERNAL_ACCESS** sollte nur vertrauenswürdigen Logins, führen Sie als Dienstkonto zugewiesen werden. Im Hinblick auf Sicherheit **EXTERNAL_ACCESS** und **UNSAFE** Assemblys identisch sind. Allerdings **EXTERNAL_ACCESS** Assemblys bieten Stabilität mehr an Zuverlässigkeit und, die nicht Bestandteil **UNSAFE** Assemblys. Angeben von **UNSAFE** ermöglicht es Code in der Assembly, die nicht zulässige Vorgänge ausführen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Prozessbereich und potenzielle Gefährdung der Stabilität und Skalierbarkeit von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Weitere Informationen zum Erstellen von CLR-Assemblys in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], finden Sie unter [Verwalten von CLR-Integrationsassemblys](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md).  
  
## <a name="accessing-external-resources"></a>Zugreifen auf externe Ressourcen  
 Wenn Sie einen benutzerdefinierten Typ (UDT), gespeicherte Prozedur oder andere Arten von Konstruktassembly mit registriert ist die **sichere** Berechtigungssatz und verwalteten Code ausführt, in das Konstrukt kann nicht auf externe Ressourcen zuzugreifen. Jedoch wenn entweder die **EXTERNAL_ACCESS** oder **UNSAFE** Berechtigungssätze angegeben wurden, und verwalteter Code auf externe Ressourcen zuzugreifen versucht [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] wendet die folgenden Regeln:  
  
|Wenn|Then|  
|--------|----------|  
|Der Ausführungskontext entspricht einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmeldung.|Versuche, auf externe Ressourcen zuzugreifen, werden verweigert, und eine Sicherheitsausnahme wird ausgelöst.|  
|Der Ausführungskontext entspricht einer Windows-Anmeldung, und der Ausführungskontext ist der ursprüngliche Aufrufer.|Der Zugriff auf die externe Ressource erfolgt im Sicherheitskontext des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Dienstkontos.|  
|Bei dem Aufrufer handelt es sich nicht um den ursprünglichen Aufrufer.|Der Zugriff wird verweigert, und eine Sicherheitsausnahme wird ausgelöst.|  
|Der Ausführungskontext entspricht einer Windows-Anmeldung und der Ausführungskontext ist der ursprüngliche Aufrufer des Aufrufers wurde angenommen wurde.|Für den Zugriff wird anstelle des Dienstkontos der Sicherheitskontext des Aufrufers verwendet.|  
  
## <a name="permission-set-summary"></a>Zusammenfassung des Berechtigungssatzes  
 Das folgende Diagramm fasst die Einschränkungen und Berechtigungen für die **sichere**, **EXTERNAL_ACCESS**, und **UNSAFE** Berechtigungssätze.  
  
|||||  
|-|-|-|-|  
||**SAFE**|**EXTERNAL_ACCESS**|**UNSAFE**|  
|**Codezugriffsberechtigungen**|Nur ausführen|Ausführen + Zugriff auf externe Ressourcen|Uneingeschränkt (einschließlich P/Invoke)|  
|**Einschränkungen des Programmiermodells**|ja|Ja|Keine Einschränkungen|  
|**Überprüfbarkeit erforderlich**|ja|ja|nein|  
|**Lokaler Datenzugriff**|ja|ja|ja|  
|**Möglichkeit zum Aufrufen von systemeigenen Codes**|nein|Nein|Ja|  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheit der CLR-Integration](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Hostschutzattribute und Programmierung der CLR-Integration](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [CLR-Integration Einschränkungen des Programmiermodells](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Gehostete CLR-Umgebung](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
