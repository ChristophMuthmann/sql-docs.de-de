---
title: Entwerfen von Assemblys | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- designing assemblies [SQL Server]
- assemblies [CLR integration], designing
ms.assetid: 9c07f706-6508-41aa-a4d7-56ce354f9061
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 769c0aa7f6d9593ab3e2360a0e26876f23f16b41
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="assemblies---designing"></a>Assemblys - entwerfen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema werden die folgenden Faktoren beschrieben, die Sie beim Entwerfen von Assemblys berücksichtigen sollten:  
  
-   Verpacken von Assemblys  
  
-   Verwalten der Assemblysicherheit  
  
-   Einschränkungen für Assemblys  
  
## <a name="packaging-assemblies"></a>Verpacken von Assemblys  
 Eine Assembly kann Funktionen für mehrere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Routinen oder -Typen in ihren Klassen und Methoden enthalten. In den meisten Fällen ist es sinnvoll, die Funktionen von Routinen, die verwandte Funktionen ausführen, in der gleichen Assembly zu verpacken, insbesondere, wenn diese Routinen Klassen gemeinsam verwenden, deren Methoden sich gegenseitig aufrufen. Klassen, die Dateneingabe-Verwaltungstasks für CLR-Trigger (Common Language Runtime) und CLR-gespeicherte Prozeduren ausführen, können z. B. in der gleichen Assembly verpackt werden. Dies hängt damit zusammen, dass sich die Methoden für diese Klassen mit größerer Wahrscheinlichkeit gegenseitig aufrufen als die Methoden anderer, weniger verwandter Tasks.  
  
 Sie sollten Folgendes beachten, wenn Sie Code in einer Assembly verpacken:  
  
-   CLR-benutzerdefinierte Typen und Indizes, die von CLR-benutzerdefinierten Funktionen abhängen, können bewirken, dass sich persistente Daten in der Datenbank befinden, die von der Assembly abhängen. Das Bearbeiten des Codes einer Assembly ist in der Regel komplexer, wenn persistente Daten vorhanden sind, die von der Assembly in der Datenbank abhängen. Auf diesem Grund ist es im Allgemeinen besser, Code, von dem die Abhängigkeiten persistenter Daten abhängen (z. B. benutzerdefinierte Typen und Indizes, die benutzerdefinierte Funktionen verwenden), von Code zu trennen, der keine solchen Abhängigkeiten persistenter Daten aufweist. Weitere Informationen finden Sie unter [implementieren Assemblys](../../relational-databases/clr-integration/assemblies-implementing.md) und [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md).  
  
-   Wenn verwalteter Code höhere Berechtigungen verlangt, ist es besser, diesen Code in einer anderen Assembly als den Code zu speichern, für den die höheren Berechtigungen nicht erforderlich sind.  
  
## <a name="managing-assembly-security"></a>Verwalten der Assemblysicherheit  
 Sie können steuern, im welchem Umfang eine Assembly auf Ressourcen zugreifen kann, die durch .NET Code Access Security geschützt ist, wenn diese verwalteten Code ausführt. Sie geben zu diesem Zweck einen von drei Berechtigungssätzen an, wenn Sie eine Assembly erstellen oder ändern: SAFE, EXTERNAL_ACCESS oder UNSAFE.  
  
### <a name="safe"></a>SAFE  
 SAFE ist der Standardberechtigungssatz und die restriktivste Einstellung. Code, der von einer Assembly mit SAFE-Berechtigungen ausgeführt wird, kann nicht auf externe Systemressourcen wie z. B. Dateien, das Netzwerk, Umgebungsvariablen oder die Registrierung zugreifen. SAFE-Code kann auf Daten aus den lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanken zugreifen oder Berechnungen und Geschäftslogik ausführen, für die kein Zugriff auf Ressourcen außerhalb der lokalen Datenbanken erforderlich ist.  
  
 Die meisten Assemblys führen Berechnungs- und Datenverwaltungsaufgaben aus, ohne dass ein Zugriff auf Ressourcen außerhalb von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erforderlich ist. Aus diesem Grund wird empfohlen, SAFE als Berechtigungssatz für die Assembly zu verwenden.  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS ermöglicht Assemblys den Zugriff auf bestimmte externe Systemressourcen wie z. B. Dateien, Netzwerke, Webdienste, Umgebungsvariablen und die Registrierung. Nur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen mit EXTERNAL ACCESS-Berechtigungen können EXTERNAL_ACCESS-Assemblys erstellen.  
  
 SAFE- und EXTERNAL_ACCESS-Assemblys können nur Code enthalten, der überprüfbar typsicher ist. Dies bedeutet, dass diese Assemblys auf Klassen nur über definierte Einstiegspunkte zugreifen können, die für die Typdefinition gültig sind. Daher können sie nicht beliebig auf Speicherpuffer zugreifen, die sich nicht im Besitz des Codes befinden. Außerdem können sie keine Vorgänge durchführen, die nachteilige Auswirkungen auf die Robustheit des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozess besitzen könnten.  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE ermöglicht Assemblys den uneingeschränkten Zugriff auf Ressourcen innerhalb und außerhalb von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Code, der aus einer UNSAFE-Assembly ausgeführt wird, kann nicht verwalteten Code aufrufen.  
  
 Wenn Sie UNSAFE angeben, kann der Code in der Assembly außerdem Vorgänge ausführen, die von der CLR-Überprüfung als typunsicher betrachtet werden. Diese Vorgänge können potenziell auf unkontrollierte Weise auf Speicherpuffer im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozessraum zugreifen. UNSAFE-Assemblys können außerdem potenziell das Sicherheitssystem von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder der CLR unterlaufen. UNSAFE-Berechtigungen sollten nur hochgradig vertrauenswürdigen Assemblys durch erfahrene Entwickler oder Administratoren erteilt werden. Nur Mitglieder der **Sysadmin** -Serverrolle kann UNSAFE-Assemblys erstellen.  
  
## <a name="restrictions-on-assemblies"></a>Einschränkungen für Assemblys  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] belegt verwalteten Code in Assemblys mit einigen Einschränkungen, damit sichergestellt wird, dass diese auf zuverlässige und skalierbare Weise ausgeführt werden können. Dies bedeutet, dass bestimmte Vorgänge, die die Robustheit des Servers beeinträchtigen könnten, in SAFE- und EXTERNAL_ACCESS-Assemblys nicht zulässig sind.  
  
### <a name="disallowed-custom-attributes"></a>Unzulässige benutzerdefinierte Attribute  
 Assemblys dürfen nicht mit den folgenden benutzerdefinierten Attributen mit Anmerkungen versehen werden:  
  
```  
System.ContextStaticAttribute  
System.MTAThreadAttribute  
System.Runtime.CompilerServices.MethodImplAttribute  
System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
System.Runtime.Remoting.Contexts.ContextAttribute  
System.Runtime.Remoting.Contexts.SynchronizationAttribute  
System.Runtime.InteropServices.DllImportAttribute   
System.Security.Permissions.CodeAccessSecurityAttribute  
System.STAThreadAttribute  
System.ThreadStaticAttribute  
```  
  
 Außerdem dürfen SAFE- und EXTERNAL_ACCESS-Assemblys nicht mit den folgenden benutzerdefinierten Attributen mit Anmerkungen versehen werden:  
  
```  
System.Security.SuppressUnmanagedCodeSecurityAttribute  
System.Security.UnverifiableCodeAttribute  
```  
  
### <a name="disallowed-net-framework-apis"></a>Unzulässige .NET Framework-APIs  
 Alle [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -API, die mit einem der unzulässigen kommentiert wird **HostProtectionAttributes** kann nicht aus Safe- und EXTERNAL_ACCESS-Assemblys aufgerufen werden.  
  
```  
eSelfAffectingProcessMgmt  
eSelfAffectingThreading  
eSynchronization  
eSharedState   
eExternalProcessMgmt  
eExternalThreading  
eSecurityInfrastructure  
eMayLeakOnAbort  
eUI  
```  
  
### <a name="supported-net-framework-assemblies"></a>Unterstützte .NET Framework-Assemblys  
 Jede Assembly, auf die durch die benutzerdefinierte Assembly verwiesen wird, muss mithilfe von CREATE ASSEMBLY in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geladen werden. Die folgenden [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Assemblys wurden bereits in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geladen; daher kann durch benutzerdefinierte Assemblys auf sie verwiesen werden, ohne dass CREATE ASSEMBLY verwendet werden muss.  
  
```  
custommarshallers.dll  
Microsoft.visualbasic.dll  
Microsoft.visualc.dll  
mscorlib.dll  
system.data.dll  
System.Data.SqlXml.dll  
system.dll  
system.security.dll  
system.web.services.dll  
system.xml.dll  
System.Transactions  
System.Data.OracleClient  
System.Configuration  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Assemblys & #40; Datenbankmodul & #41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Sicherheit der CLR-Integration](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
