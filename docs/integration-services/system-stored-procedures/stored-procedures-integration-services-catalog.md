---
title: Gespeicherte Prozeduren (Integration Services-Katalog) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- stored procedures [Integration Services]
ms.assetid: a6ccd884-108f-4fb6-95ad-00b9cb65d5d6
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 21715bf65f3a85669dfe823511ddb9b6c2dd4d57
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="stored-procedures-integration-services-catalog"></a>Gespeicherte Prozeduren (Integration Services-Katalog)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In diesem Abschnitt wird beschrieben, die [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherten Systemprozeduren, die zum Verwalten von verfügbaren [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Projekte, die mit einer Instanz von bereitgestellt wurden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Rufen Sie die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gespeicherte Prozeduren zum Hinzufügen, entfernen, ändern, oder führen Sie die Objekte, die im rowsetcache der **SSISDB** Katalog.  
  
 Der Standardname des Katalogs ist SSISDB. Die Objekte, die im Katalog gespeichert werden, umfassen Projekte, Pakete, Parameter, Umgebungen und Verwendungsverläufe.  
  
 Sie können die Datenbanksichten und gespeicherten Prozeduren direkt verwenden oder benutzerdefinierten Code schreiben, mit dem die verwaltete API aufgerufen wird. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]und die verwaltete API die Sichten Abfragen und rufen Sie die gespeicherten Prozeduren, die beschrieben werden, in diesem Abschnitt können Sie viele Aufgaben ausführen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
 Fügt der Ausgabe einer Komponente in einem Paketdatenfluss eine Datenabzweigung hinzu.  
  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
 Fügt einem bestimmten Datenflusspfad in einem Paketdatenfluss eine Datenabzweigung hinzu.  
  
 [catalog.check_schema_version](../../integration-services/system-stored-procedures/catalog-check-schema-version.md)  
 Bestimmt, ob die SSISDB-Katalogschema und die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Binärdateien (isserverexec-Assembly und SQLCLR-Assembly) kompatibel sind.  
  
 [Catalog. clear_object_parameter_value &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md)  
 Löscht den Wert eines Parameters für eine vorhandene [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Projekt oder Paket, das auf dem Server gespeichert ist.  
  
 [Catalog. configure_catalog &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)  
 Konfiguriert den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog durch das Festlegen einer Katalogeigenschaft auf einen angegebenen Wert.  
  
 [catalog.create_environment &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database.md)  
 Erstellt eine Umgebung, in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.create_environment_reference &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database.md)  
 Erstellt einen umgebungsverweis für ein Projekt in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.create_environment_variable &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database.md)  
 Erstellen Sie eine Umgebungsvariable in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [Catalog. create_execution &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)  
 Erstellt eine Instanz der Ausführung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.create_execution_dump](../../integration-services/system-stored-procedures/catalog-create-execution-dump.md)  
 Hält ein aktuell ausgeführtes Paket an und erzeugt eine Dumpdatei.  
  
 [catalog.create_folder &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database.md)  
 Erstellt einen Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.delete_environment &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database.md)  
 Löscht eine Umgebung aus einem Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.delete_environment_reference &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database.md)  
 Löscht einen umgebungsverweis aus einem Projekt in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.delete_environment_variable &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database.md)  
 Löscht eine Umgebungsvariable aus einer Umgebung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.delete_folder &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database.md)  
 Löscht einen Ordner aus der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.delete_project &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database.md)  
 Löscht ein vorhandenes Projekt aus einem Ordner in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [Catalog. deny_permission &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database.md)  
 Verweigert eine Berechtigung für ein sicherungsfähiges Objekt im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.deploy_project &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)  
 Stellt ein Projekt in einem Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog bereit oder aktualisiert ein vorhandenes Projekt, das zuvor bereitgestellt wurde.  
  
 [Catalog. get_parameter_values &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md)  
 Löst aus, und ruft die Standardparameterwerte aus einem Projekt und den entsprechenden Paketen im ab der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.get_project &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md)  
 Ruft die Eigenschaften eines vorhandenen Projekts im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog ab.  
  
 [Catalog. grant_permission &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)  
 Gewährt eine Berechtigung für ein sicherungsfähiges Objekt in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.move_environment &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database.md)  
 Verschiebt eine Umgebung aus einem Ordner in einen anderen innerhalb der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.move_project &#40;&#40;SSISDB Database&#41;](../Topic/catalog.move_project%20\(\(SSISDB%20Database\).md)  
 Verschiebt ein Projekt aus einem Ordner in einen anderen innerhalb der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.remove_data_tap](../../integration-services/system-stored-procedures/catalog-remove-data-tap.md)  
 Entfernt eine Datenabzweigung aus einer Komponentenausgabe, die aktuell ausgeführt wird.  
  
 [catalog.rename_environment &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database.md)  
 Benennt eine Umgebung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog um.  
  
 [catalog.rename_folder &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database.md)  
 Benennt einen Ordner in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.restore_project &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)  
 Stellt ein Projekt in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog in einer früheren Version.  
  
 [Catalog. revoke_permission &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database.md)  
 Widerruft eine Berechtigung für ein sicherungsfähiges Objekt in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.set_environment_property &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database.md)  
 Legt die Eigenschaft einer Umgebung in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.set_environment_reference_type &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database.md)  
 Legt den Verweistyp fest und den Umgebungsnamen verknüpft sind mit einem vorhandenen umgebungsverweis für ein Projekt in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.set_environment_variable_property &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database.md)  
 Legt die Eigenschaft einer Umgebungsvariablen in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [Catalog. set_environment_variable_protection &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database.md)  
 Legt das vertraulichkeitsbit einer Umgebungsvariablen in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.set_environment_variable_value &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database.md)  
 Legt den Wert einer Umgebungsvariablen im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest.  
  
 [catalog.set_execution_parameter_value &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 Legt den Wert eines Parameters für eine Instanz der Ausführung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest.  
  
 [catalog.set_execution_property_override_value](../../integration-services/system-stored-procedures/catalog-set-execution-property-override-value.md)  
 Legt den Wert einer Eigenschaft für eine Instanz der Ausführung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest.  
  
 [catalog.set_folder_description &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database.md)  
 Legt die Beschreibung eines Ordners im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest.  
  
 [Catalog. set_object_parameter_value &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md)  
 Legt den Wert eines Parameters im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog fest. Ordnet einer Umgebungsvariablen den Wert zu oder weist einen Literalwert zu, der standardmäßig verwendet wird, wenn keine anderen Werte zugewiesen werden.  
  
 [Catalog. start_execution &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)  
 Startet eine Instanz der Ausführung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [catalog.startup](../../integration-services/system-stored-procedures/catalog-startup.md)  
 Führt eine Wartung des Status von Vorgängen für den SSISDB-Katalog aus.  
  
 [Catalog. stop_operation &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md)  
 Beendet eine Überprüfung oder Instanz der Ausführung in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [Catalog. validate_package &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database.md)  
 Überprüft asynchron ein Paket im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog.  
  
 [Catalog. validate_project &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database.md)  
 Überprüft asynchron ein Projekt in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
[Catalog.add_execution_worker &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)   
Fügt eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker mit einer Instanz der Ausführung im horizontal skalieren.

[Catalog.enable_worker_agent &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)   
Aktivieren Sie eine Skalierung Out Worker für Scale Out Master arbeiten mit diesem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.

[Catalog.disable_worker_agent &#40; SSISDB-Datenbank &#41;](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)   
Deaktivieren Sie eine Skala Out Worker für Skalierung Out Master arbeiten mit diesem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.



