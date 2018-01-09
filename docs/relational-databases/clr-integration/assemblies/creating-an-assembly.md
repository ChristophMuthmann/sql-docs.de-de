---
title: Erstellen einer Assembly | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- creating assemblies
- UNSAFE assemblies
- CREATE ASSEMBLY statement
- SAFE assemblies
- EXTERNAL_ACCESS assemblies
- assemblies [CLR integration], creating
ms.assetid: a2bc503d-b6b2-4963-8beb-c11c323f18e0
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 249bd52e59dfb91ca4d4a24efb3cd824fb329864
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="creating-an-assembly"></a>Erstellen von Assemblys
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Verwaltete Datenbankobjekte, z. B. gespeicherte Prozeduren oder Trigger, werden kompiliert und dann in so genannten Assemblys bereitgestellt. Verwaltete DLL-Assemblys müssen registriert werden, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bevor die von die Assembly bereitgestellte Funktion verwendet werden kann. So registrieren Sie eine Assembly in eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datenbank, verwenden Sie die CREATE ASSEMBLY-Anweisung. In diesem Thema wird erläutert, wie Sie eine Assembly mithilfe der CREATE ASSEMBLY-Anweisung in einer Datenbank registrieren und wie Sie die Sicherheitseinstellungen für die Assembly festlegen.  
  
## <a name="the-create-assembly-statement"></a>Die CREATE ASSEMBLY-Anweisung  
 Die CREATE ASSEMBLY-Anweisung dient zum Erstellen einer Assembly in einer Datenbank. Beispiel:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 Die FROM-Klausel legt den Pfadnamen der zu erstellenden Assembly fest. Bei diesem Pfad kann es sich entweder um einen UNC-Pfad (Universal Naming Convention) oder einen physischen Dateipfad handeln, der sich lokal auf dem Rechner befindet.  
  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ist es nicht zulässig, verschiedene Versionen einer Assembly mit demselben Namen, derselben Kultur und demselben öffentlichen Schlüssel zu registrieren.  
  
 Es ist möglich, Assemblys zu erstellen, die auf andere Assemblys verweisen. Beim Erstellen einer Assemblys in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] erstellt außerdem die Assemblys, auf die Assembly auf Stammebene verweist auf, wenn die referenzierten Assemblys nicht bereits in der Datenbank erstellt werden.  
  
 Datenbankbenutzer oder Benutzerrollen erhalten Berechtigungen zum Erstellen von Assemblys in einer Datenbank, deren Besitzer sie dann sind. Um Assemblys zu erstellen, benötigt der Datenbankbenutzer oder die Rolle die CREATE ASSEMBLY-Berechtigung.  
  
 Eine Assembly kann nur unter folgenden Voraussetzungen erfolgreich auf andere Assemblys verweisen:  
  
-   Die Assembly, die aufgerufen wird oder auf die verwiesen wird, gehört dem gleichen Benutzer oder der Rolle.  
  
-   Die Assembly, die aufgerufen wird oder auf die verwiesen wird, wurde in derselben Datenbank erstellt.  
  
## <a name="specifying-security-when-creating-assemblies"></a>Festlegen der Sicherheit beim Erstellen von Assemblys  
 Beim Erstellen einer Assembly in eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datenbank können angeben, eine der drei verschiedenen Sicherheitsstufen, die in dem der Code ausgeführt: **sichere**, **EXTERNAL_ACCESS**, oder **UNSAFE** . Beim Ausführen der **CREATE ASSEMBLY** -Anweisung werden bestimmte Überprüfungen für die Code-Assembly durchgeführt, aufgrund derer die Assembly möglicherweise nicht beim Server registriert werden kann. Weitere Informationen finden Sie unter dem Beispiel für den Identitätswechsel auf [CodePlex](http://msftengprodsamples.codeplex.com/).  
  
 **SAFE** ist der Standardberechtigungssatz und funktioniert für die meisten Szenarien. Um eine bestimmte Sicherheitsstufe anzugeben, ändern Sie die Syntax der CREATE ASSEMBLY-Anweisung wie folgt:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 Sie können eine Assembly mit eingestellter **SAFE** -Berechtigung auch erstellen, indem Sie einfach die dritte Zeile des oben angegeben Codes auslassen:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 Wird der Code in einer Assembly mit eingestellter **SAFE** -Berechtigung ausgeführt, können Berechnungen und Datenzugriffe im Server ausschließlich über den prozessinternen verwalteten Anbieter erfolgen.  
  
### <a name="creating-externalaccess-and-unsafe-assemblies"></a>Erstellen von EXTERNAL_ACCESS- und UNSAFE-Assemblys  
 **EXTERNAL_ACCESS** wird für Szenarien verwendet, in denen der Code auf Ressourcen außerhalb des Servers zugreift, z. B. Datei-, Netzwerk-, Registrierungs- und Umgebungsvariablen. Immer wenn der Server auf eine externe Ressource zugreift, verwendet er den Sicherheitskontext des Benutzers, der den verwalteten Code aufruft.  
  
 **Unsichere** wird für diese Situationen, in denen eine Assembly ist nicht überprüfbar sicher oder erfordert zusätzlichen Zugriff auf, Ressourcen, wie z. B. beschränkt die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Win32-API.  
  
 Zum Erstellen einer **EXTERNAL_ACCESS** oder **UNSAFE** Assembly im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], eine der beiden folgenden Bedingungen muss erfüllt sein:  
  
1.  Die Assembly wurde mit einem starken Namen oder Authenticode mit Zertifikat signiert. Diese starken Namen (oder Zertifikat) wird erstellt, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] als asymmetrischen Schlüssel (oder Zertifikat), und verfügt über einen entsprechenden Anmeldenamen mit **EXTERNAL ACCESS ASSEMBLY** -Berechtigung (für Assemblys mit externem Zugriff) oder  **UNSAFE-ASSEMBLY** -Berechtigung (für unsichere Assemblys).  
  
2.  Der Datenbankbesitzer (DBO) hat **EXTERNAL ACCESS ASSEMBLY** (für **EXTERNAL ACCESS** Assemblys) oder **UNSAFE ASSEMBLY** (für **UNSAFE** Berechtigung Assemblys), und die Datenbank hat die [TRUSTWORTHY-Datenbankeigenschaft](../../../relational-databases/security/trustworthy-database-property.md) festgelegt **ON**.  
  
 Die beiden oben aufgeführten Bedingungen werden auch zur Assemblyladezeit (dazu gehört auch die Ausführung) überprüft. Mindestens eine der Bedingungen muss erfüllt sein, um die Assembly zu laden.  
  
 Es wird empfohlen, die die [TRUSTWORTHY-Datenbankeigenschaft](../../../relational-databases/security/trustworthy-database-property.md) für eine Datenbank nicht festgelegt werden **ON** nur zum Ausführen der common Language Runtime (CLR)-Codes im Server-Prozess. Stattdessen empfiehlt es sich, dass ein asymmetrischer Schlüssel aus der Assemblydatei in der Masterdatenbank erstellt wird. Anschließend muss eine Anmeldung für diesen asymmetrischen Schlüssel erstellt werden, und die Anmeldung muss eine **EXTERNAL ACCESS ASSEMBLY** - oder **UNSAFE ASSEMBLY** -Berechtigung erhalten.  
  
 Die folgenden [!INCLUDE[tsql](../../../includes/tsql-md.md)] Anweisungen führen Sie die Schritte, die erforderlich sind, erstellen Sie einen asymmetrischen Schlüssel, der diesem Schlüssel eine Anmeldung zuzuweisen und erteilen Sie dann **EXTERNAL_ACCESS** -Berechtigung. Führen Sie die folgende [!INCLUDE[tsql](../../../includes/tsql-md.md)] Anweisungen vor dem Ausführen der CREATE ASSEMBLY-Anweisung.  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll'     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey     
GRANT EXTERNAL ACCESS ASSEMBLY TO SQLCLRTestLogin;   
GO   
```  
  
> [!NOTE]  
>  Sie müssen eine neue Anmeldung erstellen, die dem asymmetrischen Schlüssel zugeordnet wird. Diese Anmeldung dient nur zum Erteilen von Berechtigungen. Sie muss weder einem Benutzer zugeordnet noch innerhalb der Anwendung verwendet werden.  
  
 Um eine **EXTERNAL ACCESS** -Assembly zu erstellen, muss der Ersteller die **EXTERNAL ACCESS** -Berechtigung haben. Diese wird beim Erstellen der Assembly angegeben:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 Die folgenden [!INCLUDE[tsql](../../../includes/tsql-md.md)] Anweisungen führen Sie die Schritte, die erforderlich sind, erstellen Sie einen asymmetrischen Schlüssel, der diesem Schlüssel eine Anmeldung zuzuweisen und erteilen Sie dann **UNSAFE** -Berechtigung. Führen Sie die folgende [!INCLUDE[tsql](../../../includes/tsql-md.md)] Anweisungen vor dem Ausführen der CREATE ASSEMBLY-Anweisung.  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 Um festzulegen, dass eine Assembly mit **UNSAFE** -Berechtigung geladen wird, geben Sie die **UNSAFE** -Berechtigung beim Laden der Assembly auf den Server an:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 Weitere Informationen zu den Berechtigungen für jede der Einstellungen finden Sie unter [CLR Integration Security](../../../relational-databases/clr-integration/security/clr-integration-security.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von CLR-Integrationsassemblys](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [Ändern einer Assembly](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)   
 [Durch Löschen einer Assembly](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [CLR Integration Code Access Security](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [TRUSTWORTHY-Datenbankeigenschaft](../../../relational-databases/security/trustworthy-database-property.md)   
 [Zulassen von teilweise vertrauenswürdigen Aufrufern](http://msdn.microsoft.com/library/20b0248f-36da-4fc3-97d2-3789fcf6e084)  
  
  
