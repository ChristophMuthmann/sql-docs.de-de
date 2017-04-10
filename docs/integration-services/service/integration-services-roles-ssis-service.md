---
title: "Integration Services-Rollen (SSIS-Dienst) | Microsoft Docs"
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
  - "Sicherheit [Integration Services], Rollen"
  - "db_ssisoperator (Rolle)"
  - "db_ssisadmin (Rolle)"
  - "Feste Datenbankrollen [Integration Services]"
  - "Pakete [Integration Services], Sicherheit"
  - "Rollen [Integration Services]"
  - "db_ssisltduser (Rolle)"
ms.assetid: 9702e90c-fada-4978-a473-1b1423017d80
caps.latest.revision: 50
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# Integration Services-Rollen (SSIS-Dienst)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt bestimmte feste Rollen auf Datenbankebene für den sicheren Zugriff auf Pakete bereit, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeichert sind. Die verfügbaren Rollen unterscheiden sich abhängig davon, ob Sie Pakete in der SSIS-Katalogdatenbank (SSISDB) oder in der msdb-Datenbank speichern.  
  
## Rollen in der SSIS-Katalogdatenbank (SSISDB)  
 Die SSIS-Katalogdatenbank (SSISDB) bietet die folgenden festen Rollen auf Datenbankebene für den sicheren Zugriff auf Pakete und Informationen zu Paketen.  
  
-   **ssis_admin**. Diese Rolle bietet vollen administrativen Zugriff auf die SSIS-Katalogdatenbank.  
  
-   **ssis_logreader**: Diese Rolle bietet Berechtigungen für den Zugriff auf alle Ansichten, die mit operativen SSISDB-Protokollen verbunden sind.  
  
     Die Liste der Ansichten enthält: [catalog].[projects], [catalog].[packages], [catalog].[operations], [catalog].[extended_operation_info], [catalog].[operation_messages], [catalog].[event_messages], [catalog].[execution_data_statistics], [catalog].[execution_component_phases], [catalog].[execution_data_taps], [catalog].[event_message_context], [catalog].[executions], [catalog].[executables], [catalog].[executable_statistics], [catalog].[validations], [catalog].[execution_parameter_values] und [catalog].[execution_property_override_values].  
  
## Rollen in der msdb-Datenbank  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] bietet auf Datenbankebene die drei festen Rollen **db_ssisadmin**, **db_ssisltduser**, und **db_ssisoperator** zum Steuern des Paketzugriffs. Diese werden in der **msdb**-Datenbank gespeichert. Rollen weisen Sie mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zu. Die Rollenzuweisungen werden in der **msdb**-Datenbank gespeichert.  
  
### Lese- und Schreibaktionen  
 In der folgenden Tabelle werden die Lese- und Schreibaktionen von Windows und der festen Rollen auf Datenbankebene in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] beschrieben.  
  
|Rolle|Leseaktion|Schreibaktion|  
|----------|-----------------|------------------|  
|**db_ssisadmin**<br /><br /> oder<br /><br /> **sysadmin**|Eigene Pakete aufzählen.<br /><br /> Alle Pakete aufzählen.<br /><br /> Eigene Pakete anzeigen.<br /><br /> Alle Pakete anzeigen.<br /><br /> Eigene Pakete ausführen.<br /><br /> Alle Pakete ausführen.<br /><br /> Eigene Pakete exportieren.<br /><br /> Alle Pakete exportieren.<br /><br /> Alle Pakete in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent ausführen.|Pakete importieren.<br /><br /> Eigene Pakete löschen.<br /><br /> Alle Pakete löschen.<br /><br /> Eigene Paketrollen ändern.<br /><br /> Alle Paketrollen ändern.<br /><br /> <br /><br /> **\*\*Warnung\*\*** Mitglieder der db_ssisadmin-Rolle und der dc_admin-Rolle können Ihre Berechtigungen möglicherweise auf sysadmin erhöhen. Diese Ausweitung von Berechtigungen ist möglich, da diese Rollen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakete ändern können und [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakete von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe des sysadmin-Sicherheitskontexts des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents ausgeführt werden können. Konfigurieren Sie als Schutz vor dieser Ausweitung von Berechtigungen beim Ausführen von Wartungsplänen, Datensammlungssätzen und anderen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen Aufträge des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents, die Pakete ausführen, für die Verwendung eines Proxykontos mit einschränkten Berechtigungen, oder fügen Sie der db_ssisadmin-Rolle und der dc_admin-Rolle nur sysadmin-Mitglieder hinzu.|  
|**db_ssisltduser**|Eigene Pakete aufzählen.<br /><br /> Alle Pakete aufzählen.<br /><br /> Eigene Pakete anzeigen.<br /><br /> Eigene Pakete ausführen.<br /><br /> Eigene Pakete exportieren.|Pakete importieren.<br /><br /> Eigene Pakete löschen.<br /><br /> Eigene Paketrollen ändern.|  
|**db_ssisoperator**|Alle Pakete aufzählen.<br /><br /> Alle Pakete anzeigen.<br /><br /> Alle Pakete ausführen.<br /><br /> Alle Pakete exportieren.<br /><br /> Alle Pakete in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent ausführen.|InclusionThresholdSetting|  
|**Windows-Administratoren**|Ausführungsdetails zu allen ausgeführten Paketen anzeigen.|Alle derzeit ausgeführten Pakete anhalten.|  
  
### Sysssispackages-Tabelle  
 Die **sysssispackages**-Tabelle in **msdb** enthält die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeicherten Pakete. Weitere Informationen finden Sie unter [sysssispackages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysssispackages-transact-sql.md).  
  
 Die **sysssispackages**-Tabelle enthält Spalten, die Informationen über die Rollen enthalten, die Paketen zugewiesen sind.  
  
-   In der Spalte **readerrole** wird die Rolle angegeben, die über Lesezugriff auf das Paket verfügt.  
  
-   In der Spalte **writerrole** wird die Rolle angegeben, die über Schreibzugriff auf das Paket verfügt.  
  
-   Die **ownersid**-Spalte enthält den eindeutigen Sicherheitsbezeichner des Benutzers, der das Paket erstellte. In dieser Spalte wird der Besitzer des Pakets definiert.  
  
### Berechtigungen  
 Standardmäßig gelten die Berechtigungen der festen Rollen auf Datenbankebene **db_ssisadmin** und **db_ssisoperator** und die eindeutige Sicherheits-ID des Benutzers, der das Paket erstellt hat, für die Leserolle für Pakete, und die Berechtigungen der **db_ssisadmin**-Rolle und die eindeutige Sicherheits-ID des Benutzers, der das Paket erstellt hat, gelten für die Schreibrolle. Ein Benutzer muss Mitglied der Rolle **db_ssisadmin**, **db_ssisltduser** oder **db_ssisoperator** sein, um über Lesezugriff auf das Paket zu verfügen. Ein Benutzer muss Mitglied der **db_ssisadmin**-Rolle sein, um über Schreibzugriff zu verfügen.  
  
### Zugriff auf Pakete  
 Die festen Rollen auf Datenbankebene arbeiten mit benutzerdefinierten Rollen zusammen. Die benutzerdefinierten Rollen sind die Rollen, die Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] erstellen und dann zum Zuweisen von Berechtigungen zu Paketen verwenden. Um auf ein Paket zuzugreifen, muss ein Benutzer Mitglied der benutzerdefinierten Rolle und der entsprechenden festen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Datenbankrolle sein. Wenn die Benutzer z.B. Mitglieder der benutzerdefinierten **AuditUsers**-Rolle sind, die einem Paket zugewiesen ist, müssen sie auch Mitglieder der **db_ssisadmin**-, **db_ssisltduser**- oder **db_ssisoperator**-Rolle sein, um Lesezugriff auf das Paket zu erhalten.  
  
 Wenn Sie Paketen keine benutzerdefinierten Rollen zuweisen, wird der Paketzugriff durch die festen Rollen auf Datenbankebene bestimmt.  
  
 Wenn Sie benutzerdefinierte Rollen verwenden möchten, müssen Sie diese der **msdb**-Datenbank hinzufügen, bevor Sie sie Paketen zuweisen. Neue Datenbankrollen können Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] erstellen.  
  
 Die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Rollen auf Datenbankebene gewähren den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Systemtabellen in der msdb-Datenbank Rechte.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (der MSSQLSERVER-Dienst) muss gestartet werden, bevor Sie eine Verbindung zum Datenbankmodul herstellen und auf die **msdb**-Datenbank zugreifen können.  
  
 Um Rollen Paketen zuzuweisen, müssen Sie die folgenden Tasks ausführen.  
  
-   **Öffnen Sie den Objekt-Explorer und stellen Sie eine Verbindung mit Integration Services her.**  
  
     Bevor Sie Paketen Rollen mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zuweisen können, müssen Sie den Objekt-Explorer in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] öffnen und eine Verbindung mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] herstellen.  
  
     Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst muss gestartet werden, bevor Sie eine Verbindung mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] herstellen können.  
  
-   **Paketen Lese- und Schreibrollen zuweisen**  
  
     Sie können jedem Paket eine Lese- und eine Schreibrolle zuweisen.  
  
## Verwandte Aufgaben  
  
-   [Zuweisen einer Lese- und Schreibrolle zu einem Paket](../../integration-services/service/assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [Erstellen einer benutzerdefinierten Rolle](../../integration-services/service/create-a-user-defined-role.md)  
  
-   [Herstellen einer Verbindung mit Integration Services](../../integration-services/service/connect-to-integration-services.md)  
  
  