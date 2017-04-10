---
title: "Sicherheits&#252;bersicht (Integration Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SSIS-Pakete, Sicherheit"
  - "Integration Services, Sicherheit"
  - "Sicherheit [Integration Services], Informationen zur Sicherheit"
  - "Kennwörter [Integration Services]"
  - "Pakete [Integration Services], Sicherheit"
  - "SQL Server Integration Services, Sicherheit"
  - "SSIS, Sicherheit"
  - "Integration Services-Pakete, Sicherheit"
  - "SQL Server Integration Services-Pakete, Sicherheit"
ms.assetid: 01aa0b88-d477-4581-9a3b-2efc3de2b133
caps.latest.revision: 73
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 73
---
# Sicherheits&#252;bersicht (Integration Services)
  Sicherheit in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] besteht aus mehreren Ebenen, die eine umfangreiche und flexible Sicherheitsumgebung bereitstellen. Diese Sicherheitsebenen umfassen die Verwendung digitaler Signaturen, Paketeigenschaften, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankrollen und Betriebssystemberechtigungen. Die meisten dieser Sicherheitsfunktionen können den Kategorien Identität und Zugriffssteuerung zugeordnet werden.  
  
## Identitätsfunktionen  
 Sie können das folgende Ziel erreichen, indem Sie Identitätsfunktionen in den Paketen implementieren:  
  
 **Stellen Sie sicher, dass Sie nur Pakete von vertrauenswürdigen Quellen öffnen und ausführen**.  
  
 Um sicherzustellen, dass Sie nur Pakete von vertrauenswürdigen Quellen öffnen und ausführen, müssen Sie zunächst die Quelle der Pakete identifizieren. Sie können die Quelle identifizieren, indem Sie Pakete mit Zertifikaten signieren. Beim Öffnen oder Ausführen der Pakete können Sie dann mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] prüfen, ob die digitalen Signaturen vorhanden und gültig sind. Weitere Informationen finden Sie unter [Identifizieren der Quelle von Paketen mit digitalen Signaturen](../../integration-services/packages/identify-the-source-of-packages-with-digital-signatures.md).  
  
## Zugriffssteuerungsfunktionen  
 Sie können das folgende Ziel erreichen, indem Sie Identitätsfunktionen in den Paketen implementieren:  
  
 **Stellen Sie sicher, dass Pakete nur von autorisierten Benutzern geöffnet und ausgeführt werden**.  
  
 Um sicherzustellen, dass Pakete nur von autorisierten Benutzern geöffnet und ausgeführt werden, müssen Sie den Zugriff auf die folgenden Informationen steuern:  
  
-   Inhalte von Paketen, insbesondere vertrauliche Daten  
  
-   Pakete und Paketkonfigurationen, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gespeichert werden  
  
-   Pakete und zugehörige Dateien, wie Konfigurationen, Protokolle und Prüfpunktdateien, die im Dateisystem gespeichert werden  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst und Informationen über Pakete, die der Dienst in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]anzeigt  
  
### Steuern des Zugriffs auf den Inhalt von Paketen  
 Zum Einschränken des Zugriffs auf den Inhalt eines Pakets können Sie Pakete verschlüsseln, indem Sie die ProtectionLevel-Eigenschaft des jeweiligen Pakets entsprechend festlegen. Sie können diese Eigenschaft auf die für das Paket benötigte Schutzebene festlegen. In einer Teamentwicklungsumgebung kann ein Paket beispielsweise mithilfe eines Kennworts verschlüsselt werden, das nur den Teammitgliedern bekannt ist, die an dem Paket arbeiten.  
  
 Wenn Sie die ProtectionLevel-Eigenschaft eines Pakets festlegen, erkennt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] automatisch vertrauliche Eigenschaften und verarbeitet diese entsprechend der angegebenen Paketschutzebene. Ein Beispiel: Sie legen die ProtectionLevel-Eigenschaft eines Pakets auf eine Ebene fest, bei der vertrauliche Informationen mithilfe eines Kennworts verschlüsselt werden. Für dieses Paket verschlüsselt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] automatisch die Werte aller vertraulichen Eigenschaften und zeigt entsprechende Daten nur an, wenn das korrekte Kennwort eingegeben wird.  
  
 In der Regel identifiziert [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Eigenschaften als vertraulich, wenn diese Eigenschaften Informationen wie ein Kennwort oder eine Verbindungszeichenfolge enthalten oder wenn diese Eigenschaften Variablen oder vom Task generierten XML-Knoten entsprechen. Ob [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eine Eigenschaft als vertraulich einstuft oder nicht, hängt davon ab, ob der Entwickler der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponente, etwa ein Verbindungs-Manager oder Task, die Eigenschaft als vertraulich gekennzeichnet hat. Benutzer können Eigenschaften weder der Liste der als vertraulich eingestuften Eigenschaften hinzufügen noch können sie sie aus dieser Liste entfernen. Wenn Sie benutzerdefinierte Tasks, Verbindungs-Manager oder Datenflusskomponenten erstellen, können Sie angeben, welche Eigenschaften [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] als vertraulich behandeln soll.  
  
 Weitere Informationen finden Sie unter [Access Control for Sensitive Data in Packages](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md).  
  
### Steuern des Zugriffs auf Pakete  
 Sie können [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakete in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in der msdb-Datenbank oder als XML-Dateien mit der Dateinamenerweiterung .dtsx im Dateisystem speichern. Weitere Informationen finden Sie unter [Speichern von Paketen](../../integration-services/save-packages.md).  
  
#### Speichern von Paketen in der msdb-Datenbank  
 Das Speichern der Pakete in der msdb-Datenbank trägt zur Sicherheit auf der Server-, Datenbank- und Tabellenebene bei. In der msdb-Datenbank werden [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakete in der Tabelle „sysssispackages“ gespeichert. Da die Pakete in der sysssispackages- und der sysdtspackages-Tabelle der msdb-Datenbank gespeichert werden, werden die Pakete beim Sichern der msdb-Datenbank ebenfalls automatisch gesichert.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Pakete, die in der msdb-Datenbank gespeichert sind, können auch durch Anwenden der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Rollen auf Datenbankebene geschützt werden. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] bietet auf Datenbankebene die drei festen Rollen „db_ssisadmin“, „db_ssisltduser“ und „db_ssisoperator“ zum Steuern des Paketzugriffs. Den einzelnen Paketen kann eine Lese- und eine Schreibrolle zugewiesen werden. Sie können auch benutzerdefinierte Rollen auf Datenbankebene definieren, die in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen verwendet werden. Rollen können nur für Pakete implementiert werden, die in der msdb-Datenbank in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeichert werden. Weitere Informationen finden Sie unter [Integration Services-Rollen &#40;SSIS-Dienst&#41;](../../integration-services/service/integration-services-roles-ssis-service.md).  
  
#### Speichern von Paketen im Dateisystem  
 Wenn Sie Pakete statt in der msdb-Datenbank im Dateisystem speichern, müssen Sie die Paketdateien und Ordner, die Paketdateien enthalten, sichern.  
  
### Steuern des Zugriffs auf Dateien, die von Paketen verwendet werden  
 Pakete, die für die Verwendung von Konfigurationen, Prüfpunkten und der Protokollierung konfiguriert wurden, generieren Informationen, die außerhalb des Pakets gespeichert werden. Diese Informationen können vertraulich sein und sollten geschützt werden. Prüfpunktdateien können nur auf dem Dateisystem gespeichert werden, Konfigurationen und Protokolle können im Dateisystem oder in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanktabellen gespeichert werden. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeicherte Konfigurationen und Protokolle sind durch die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherheit geschützt. Für die im Dateisystem geschriebenen Informationen sind jedoch zusätzliche Sicherheitsmaßnahmen erforderlich.  
  
 Weitere Informationen finden Sie unter [Zugriff auf Dateien, die von Paketen verwendet werden](../../integration-services/security/access-to-files-used-by-packages.md).  
  
#### Sicheres Speichern von Paketkonfigurationen  
 Die Paketkonfigurationen können in einer Tabelle in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank oder im Dateisystem gespeichert werden.  
  
 Konfigurationen können in jeder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank, nicht nur der msdb-Datenbank, gespeichert werden. So sind Sie in der Lage anzugeben, welche Datenbank als Repository von Paketkonfigurationen dient. Sie können auch den Namen der Tabelle angeben, die die Konfigurationen enthält. Die Tabelle mit der richtigen Struktur wird von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] automatisch erstellt. Das Speichern der Konfigurationen in eine Tabelle ermöglicht Sicherheit auf der Server-, Datenbank- und Tabellenebene. Außerdem werden Konfigurationen, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeichert sind, automatisch beim Sichern der Datenbank gesichert.  
  
 Wenn Sie Konfigurationen statt in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]im Dateisystem speichern, müssen Sie die Ordner, die die Paketkonfigurationsdateien enthalten, sichern.  
  
 Weitere Informationen zu Konfigurationen finden Sie unter [Package Configurations](../../integration-services/packages/package-configurations.md).  
  
### Steuern des Zugriffs auf den Integration Services-Dienst  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] wird der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst zum Auflisten der gespeicherten Pakete verwendet. Damit nicht autorisierte Benutzer keine Informationen über Pakete anzeigen können, die auf lokalen und Remotecomputern gespeichert sind, und auf diese Weise Zugriff auf private Daten erhalten, müssen Sie den Zugriff auf Computer, auf denen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ausgeführt wird, einschränken.  
  
 Weitere Informationen finden Sie unter [Zugriff auf den Integration Services-Dienst](../../integration-services/security/access-to-the-integration-services-service.md).  
  
## Verwandte Aufgaben  
 Die folgende Liste enthält Links zu Themen, in denen die Ausführung bestimmter sicherheitsrelevanter Tasks beschrieben wird.  
  
-   [Erstellen einer benutzerdefinierten Rolle](../../integration-services/service/create-a-user-defined-role.md)  
  
-   [Zuweisen einer Lese- und Schreibrolle zu einem Paket](../../integration-services/service/assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [Implementieren einer Signaturrichtlinie durch Festlegen eines Registrierungswerts](../../integration-services/packages/implement-a-signing-policy-by-setting-a-registry-value.md)  
  
-   [Signieren eines Pakets mit einem digitalen Zertifikat](../../integration-services/packages/sign-a-package-by-using-a-digital-certificate.md)  
  
-   [Festlegen oder Ändern der Schutzebene von Paketen](../../integration-services/packages/set-or-change-the-protection-level-of-packages.md)  
  
## Siehe auch  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  