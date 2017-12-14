---
title: Gespeicherte Prozeduren (Integration Services-Katalog) | Microsoft-Dokumentation
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: stored procedures [Integration Services]
ms.assetid: a6ccd884-108f-4fb6-95ad-00b9cb65d5d6
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 60fbd38303bcdb8b07d6831d6ab3fd473a8890c6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="stored-procedures-integration-services-catalog"></a>Gespeicherte Prozeduren (Integration Services-Katalog)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In diesem Abschnitt werden die gespeicherten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozeduren beschrieben, die zum Verwalten von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekten, die in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellt wurden, verfügbar sind.  
  
 Rufen Sie die gespeicherten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Prozeduren auf, um im **SSISDB**-Katalog gespeicherte Objekte hinzuzufügen, zu entfernen, zu ändern oder auszuführen.  
  
 Der Standardname des Katalogs ist „SSISDB“. Die Objekte, die im Katalog gespeichert werden, umfassen Projekte, Pakete, Parameter, Umgebungen und Verwendungsverläufe.  
  
 Sie können die Datenbanksichten und gespeicherten Prozeduren direkt verwenden oder benutzerdefinierten Code schreiben, mit dem die verwaltete API aufgerufen wird. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] und die verwaltete API führen zur Ausführung vieler Tasks eine Abfrage der Sichten durch und rufen gespeicherte Prozeduren auf, die in diesem Abschnitt beschrieben werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
 Fügt der Ausgabe einer Komponente in einem Paketdatenfluss eine Datenabzweigung hinzu.  
  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
 Fügt einem bestimmten Datenflusspfad in einem Paketdatenfluss eine Datenabzweigung hinzu.  
  
 [catalog.check_schema_version](../../integration-services/system-stored-procedures/catalog-check-schema-version.md)  
 Bestimmt, ob das SSISDB-Katalogschema und die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Binärdateien (ISServerExec- und SQLCLR-Assembly) kompatibel sind.  
  
 [catalog.clear_object_parameter_value &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md)  
 Löscht den Wert eines Parameters für ein vorhandenes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekt oder -Paket, das auf dem Server gespeichert wird.  
  
 [catalog.configure_catalog &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)  
 Konfiguriert den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog durch das Festlegen einer Katalogeigenschaft auf einen angegebenen Wert.  
  
 [catalog.create_environment &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database.md)  
 Erstellt eine Umgebung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.create_environment_reference &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database.md)  
 Erstellt einen Umgebungsverweis für ein Projekt im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.create_environment_variable &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database.md)  
 Erstellt eine Umgebungsvariable im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.create_execution &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)  
 Erstellt eine Instanz der Ausführung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.create_execution_dump](../../integration-services/system-stored-procedures/catalog-create-execution-dump.md)  
 Hält ein aktuell ausgeführtes Paket an und erzeugt eine Dumpdatei.  
  
 [catalog.create_folder &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database.md)  
 Erstellt einen Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.delete_environment &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database.md)  
 Löscht eine Umgebung aus einem Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.delete_environment_reference &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database.md)  
 Löscht einen Umgebungsverweis aus einem Projekt im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.delete_environment_variable &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database.md)  
 Löscht eine Umgebungsvariable aus einer Umgebung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.delete_folder &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database.md)  
 Löscht einen Ordner aus dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.delete_project &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database.md)  
 Löscht ein vorhandenes Projekt aus einem Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.deny_permission &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database.md)  
 Verweigert eine Berechtigung für ein sicherungsfähiges Objekt im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.deploy_project &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)  
 Stellt ein Projekt in einem Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog bereit oder aktualisiert ein vorhandenes Projekt, das zuvor bereitgestellt wurde.  
  
 [catalog.get_parameter_values &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md)  
 Ermittelt die Standardparameterwerte und ruft diese aus einem Projekt und den entsprechenden Paketen im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog ab.  
  
 [catalog.get_project &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md)  
 Ruft die Eigenschaften eines vorhandenen Projekts im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog ab.  
  
 [catalog.grant_permission &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)  
 Gewährt eine Berechtigung für ein sicherungsfähiges Objekt im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.move_environment &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database.md)  
 Verschiebt eine Umgebung von einem Ordner in einen anderen Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.move_project &#40;&#40;SSISDB Database&#41;](../Topic/catalog.move_project%20\(\(SSISDB%20Database\).md)  
 Verschiebt ein Projekt von einem Ordner in einen anderen Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.remove_data_tap](../../integration-services/system-stored-procedures/catalog-remove-data-tap.md)  
 Entfernt eine Datenabzweigung aus einer Komponentenausgabe, die aktuell ausgeführt wird.  
  
 [catalog.rename_environment &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database.md)  
 Benennt eine Umgebung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog um.  
  
 [catalog.rename_folder &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database.md)  
 Benennt einen Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog um.  
  
 [catalog.restore_project &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)  
 Stellt die frühere Version eines Projekts im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog wieder her.  
  
 [catalog.revoke_permission &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database.md)  
 Widerruft eine Berechtigung für ein sicherungsfähiges Objekt im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.set_environment_property &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database.md)  
 Legt die Eigenschaft einer Umgebung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest.  
  
 [catalog.set_environment_reference_type &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database.md)  
 Legt den Verweistyp und den Umgebungsnamen fest, die einem vorhandenen Umgebungsverweis für ein Projekt im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog zugeordnet sind.  
  
 [catalog.set_environment_variable_property &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database.md)  
 Legt die Eigenschaft einer Umgebungsvariablen im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest.  
  
 [catalog.set_environment_variable_protection &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database.md)  
 Legt das Vertraulichkeitsbit einer Umgebungsvariable im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest.  
  
 [catalog.set_environment_variable_value &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database.md)  
 Legt den Wert einer Umgebungsvariablen im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest.  
  
 [catalog.set_execution_parameter_value &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 Legt den Wert eines Parameters für eine Instanz der Ausführung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest.  
  
 [catalog.set_execution_property_override_value](../../integration-services/system-stored-procedures/catalog-set-execution-property-override-value.md)  
 Legt den Wert einer Eigenschaft für eine Instanz der Ausführung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest.  
  
 [catalog.set_folder_description &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database.md)  
 Legt die Beschreibung eines Ordners im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest.  
  
 [catalog.set_object_parameter_value &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md)  
 Legt den Wert eines Parameters im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest. Ordnet einer Umgebungsvariablen den Wert zu oder weist einen Literalwert zu, der standardmäßig verwendet wird, wenn keine anderen Werte zugewiesen werden.  
  
 [catalog.start_execution &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)  
 Startet eine Instanz der Ausführung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.startup](../../integration-services/system-stored-procedures/catalog-startup.md)  
 Führt eine Wartung des Status von Vorgängen für den SSISDB-Katalog aus.  
  
 [catalog.stop_operation &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md)  
 Beendet eine Überprüfung oder eine Ausführungsinstanz im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.validate_package &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database.md)  
 Überprüft asynchron ein Paket im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.validate_project &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database.md)  
 Überprüft asynchron ein Projekt im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
[catalog.add_execution_worker &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)   
Fügt einen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out-Worker einer Instanz der Ausführung in Scale Out hinzu.

[catalog.enable_worker_agent &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)   
Aktivieren Sie einen Scale Out-Worker für einen Scale Out-Master, der mit diesem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog arbeitet.

[catalog.disable_worker_agent &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)   
Deaktivieren Sie einen Scale Out-Worker für einen Scale Out-Master, der mit diesem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog arbeitet.


