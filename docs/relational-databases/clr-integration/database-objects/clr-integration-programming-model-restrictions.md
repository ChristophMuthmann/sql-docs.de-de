---
title: "CLR-Integration Beschränkungen des Programmiermodells | Microsoft Docs"
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
- common language runtime [SQL Server], programming model restrictions
- assemblies [CLR integration], CREATE ASSEMBLY checks
- programming model restrictions [CLR integration]
- assemblies [CLR integration], runtime checks
ms.assetid: 2446afc2-9d21-42d3-9847-7733d3074de9
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d282b317a5ea31fe8170a847f5b425bcd1af4fd
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="clr-integration-programming-model-restrictions"></a>Beschränkungen des Programmiermodells für die CLR-Integration
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Wenn Sie eine verwaltete gespeicherte Prozedur oder ein anderes verwaltetes Datenbankobjekt erstellen, es gibt bestimmte Prüfungen durch Code [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , die berücksichtigt werden müssen. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]überprüft auf die Assembly mit verwaltetem Code, wenn sie zuerst in der Datenbank registriert wird mithilfe der **CREATE ASSEMBLY** -Anweisung sowie auch zur Laufzeit. Der verwaltete Code wird außerdem zur Laufzeit überprüft, da in einer Assembly Codepfade vorhanden sein können, die zur Laufzeit eigentlich nicht erreicht werden.  Dadurch wird Flexibilität für die Registrierung von Assemblys von Drittanbietern geschaffen, sodass eine Assembly nicht blockiert wird, wenn ein "Unsafe"-Code vorliegt, der in einer Clientumgebung ausgeführt werden soll, jedoch nie in der gehosteten CLR ausgeführt wird. Die Anforderungen an, die der verwaltete Code erfüllen muss, hängen davon ab, ob die Assembly, als registriert ist **sichere**, **EXTERNAL_ACCESS**, oder **UNSAFE**, **SAFE** ist die strengste Anforderung und Werte sind unten aufgeführt.  
  
 Neben den Einschränkungen, die für verwaltete Codeassemblys gelten, werden außerdem Sicherheitsberechtigungen für Code erteilt. Die CLR (Common Language Runtime) unterstützt ein Sicherheitsmodell, das als Codezugriffssicherheit für verwalteten Code bezeichnet wird. In diesem Modell werden Assemblys Berechtigungen auf Grundlage der Identität des Codes gewährt. **Sichere**, **EXTERNAL_ACCESS**, und **UNSAFE** Assemblys verfügen über andere CAS-Berechtigungen. Weitere Informationen finden Sie unter [CLR Integration Code Access Security](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
## <a name="create-assembly-checks"></a>CREATE ASSEMBLY-Überprüfungen  
 Wenn die **CREATE ASSEMBLY** -Anweisung ausgeführt wird, werden die folgenden Überprüfungen für jede Sicherheitsebene ausgeführt.  Wenn eine fehl Überprüfung, **CREATE ASSEMBLY** mit einer Fehlermeldung fehl.  
  
### <a name="global-any-security-level"></a>Global (eine beliebige Sicherheitsebene)  
 Alle Assemblys, auf die verwiesen wird, müssen ein oder mehrere der folgenden Kriterien erfüllen:  
  
-   Die Assembly ist bereits in der Datenbank registriert.  
  
-   Die Assembly ist eine der unterstützten Assemblys. Weitere Informationen finden Sie unter [unterstützt .NET Framework-Bibliotheken](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
-   Verwenden Sie **CREATE ASSEMBLY FROM ***\<Speicherort >,* und alle referenzierten Assemblys und deren Abhängigkeiten stehen im  *\<Speicherort >*.  
  
-   Verwenden Sie **CREATE ASSEMBLY FROM ***\<Bytes... >,* und alle Verweise, durch Leerzeichen angegeben werden getrennte Bytes.  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 Alle **EXTERNAL_ACCESS** Assemblys müssen die folgenden Kriterien erfüllen:  
  
-   Statische Felder werden nicht verwendet, um Informationen zu speichern. Schreibgeschützte statische Felder sind zulässig.  
  
-   Der PEVerify-Test wird bestanden. Das PEVerify-Tool (peverify.exe), das überprüft, ob der MSIL-Code und die zugeordneten Metadaten den Anforderungen an die Typsicherheit entsprechen, wird mit .NET Framework SDK zur Verfügung gestellt.  
  
-   Synchronisierung, z. B. mit der **SynchronizationAttribute** Klasse, wird nicht verwendet.  
  
-   Finalizer-Methoden werden nicht verwendet.  
  
 Die folgenden benutzerdefinierten Attribute sind nicht zulässig **EXTERNAL_ACCESS** Assemblys:  
  
-   System.ContextStaticAttribute  
  
-   System.MTAThreadAttribute  
  
-   System.Runtime.CompilerServices.MethodImplAttribute  
  
-   System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
  
-   System.Runtime.Remoting.Contexts.ContextAttribute  
  
-   System.Runtime.Remoting.Contexts.SynchronizationAttribute  
  
-   System.Runtime.InteropServices.DllImportAttribute  
  
-   System.Security.Permissions.CodeAccessSecurityAttribute  
  
-   System.Security.SuppressUnmanagedCodeSecurityAttribute  
  
-   System.Security.UnverifiableCodeAttribute  
  
-   System.STAThreadAttribute  
  
-   System.ThreadStaticAttribute  
  
### <a name="safe"></a>SAFE  
  
-   Alle **EXTERNAL_ACCESS** assemblybedingungen werden überprüft.  
  
## <a name="runtime-checks"></a>Laufzeitüberprüfungen  
 Zur Laufzeit wird die Codeassembly auf die folgenden Bedingungen überprüft. Wird eine dieser Bedingungen erkannt, darf der verwaltete Code nicht ausgeführt werden und es wird eine Ausnahme ausgelöst.  
  
### <a name="unsafe"></a>UNSAFE  
 Laden einer Assembly – entweder explizit durch Aufrufen der **System.Reflection.Assembly.Load()** Methode aus einem Bytearray oder implizit durch die Verwendung von **"Reflection.Emit"** Namespace – ist nicht zulässig.  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 Alle **UNSAFE** Bedingungen werden überprüft.  
  
 Alle Typen und Methoden, die mit den folgenden Hostschutzattributwerten in der unterstützten Assemblyliste als Anmerkungen versehen sind, sind nicht zulässig.  
  
-   SelfAffectingProcessMgmt  
  
-   SelfAffectingThreading  
  
-   Synchronization  
  
-   SharedState  
  
-   ExternalProcessMgmt  
  
-   ExternalThreading  
  
-   SecurityInfrastructure  
  
-   MayLeakOnAbort  
  
-   UI  
  
 Weitere Informationen über Hostschutzattribute und eine Liste der unzulässigen Typen und Member in den unterstützten Assemblys finden Sie unter [Hostschutzattribute und Programmieren von CLR-Integration](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md).  
  
### <a name="safe"></a>SAFE  
 Alle **EXTERNAL_ACCESS** Bedingungen werden überprüft.  
  
## <a name="see-also"></a>Siehe auch  
 [Unterstützte .NET Framework-Bibliotheken](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)   
 [CLR Integration Code Access Security](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Hostschutzattribute und Programmierung der CLR-Integration](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Erstellen einer Assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
