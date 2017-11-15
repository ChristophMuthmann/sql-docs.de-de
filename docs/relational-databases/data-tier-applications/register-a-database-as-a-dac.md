---
title: Registrieren einer Datenbank als eine DAC | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.registerdacwizard.summary.f1
- sql13.swb.registerdacwizard.introduction.f1
- sql13.swb.registerdacwizard.setproperties.f1
- sql13.swb.registerdacwizard.registerdac.f1
helpviewer_keywords:
- wizard [DAC], register
- How to [DAC], register
- register DAC
- data-tier application [SQL Server], register
ms.assetid: 08e52aa6-12f3-41dd-a793-14b99a083fd5
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9b6f99676e0fbb0a8b883593e88eb8a0e9ccf258
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="register-a-database-as-a-dac"></a>Registrieren einer Datenbank als eine DAC
  Verwenden Sie entweder den **Assistenten zum Registrieren von Datenschichtanwendungen** oder ein Windows PowerShell-Skript, um eine Definition für eine Datenschichtanwendung (DAC) zu erstellen, in der die Objekte in einer vorhandenen Datenbank beschrieben werden, und registrieren Sie die DAC-Definition in der **msdb** -Systemdatenbank (**master** in [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]).  
  
-   **Vorbereitungen:**  [Einschränkungen](#LimitationsRestrictions), [Berechtigungen](#Permissions)  
  
-   **So aktualisieren Sie eine DAC mit:**  [dem Assistenten zum Registrieren von Datenebenenanwendungen](#UsingRegisterDACWizard), [PowerShell](#RegisterDACPowerShell)  
  
## <a name="before-you-begin"></a>Vorbereitungen  
 Beim Registrierungsprozess wird eine DAC-Definition erstellt, die die Objekte in der Datenbank definiert. Eine DAC-Instanz setzt sich aus der Kombination von DAC-Definition und Datenbank zusammen. Bei der Registrierung einer Datenbank als DAC in einer verwalteten Instanz des Datenbankmoduls wird die registrierte DAC in das SQL Server-Hilfsprogramm integriert, wenn der Hilfsprogramm-Sammlungssatz das nächste Mal von der Instanz an den Steuerungspunkt für das Hilfsprogramm gesendet wird. Die DAC ist dann unter dem Knoten **Bereitgestellte Datenschichtanwendungen** im [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Utility Explorer** and reported in the **Bereitgestellte Datenschichtanwendungen** details page.  
  
###  <a name="LimitationsRestrictions"></a> Einschränkungen  
 Die DAC-Registrierung kann nur für eine Datenbank in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]oder [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) oder höher ausgeführt werden. Die DAC-Registrierung ist nicht möglich, wenn eine DAC bereits für die Datenbank registriert ist. Wenn die Datenbank durch Bereitstellung einer DAC erstellt wurde, kann der **Assistent zum Registrieren von Datenschichtanwendungen**beispielsweise nicht ausgeführt werden.  
  
 Es kann keine DAC registriert werden, wenn die Datenbank Objekte, die in einer DAC nicht unterstützt werden, oder enthaltene Benutzer enthält. Weitere Informationen zu den in einer DAC unterstützten Objekttypen finden Sie unter [DAC Support For SQL Server Objects and Versions](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md).  
  
###  <a name="Permissions"></a> Berechtigungen  
 Zum Registrieren einer DAC in einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] sind mindestens die ALTER ANY LOGIN-Berechtigung und die VIEW DEFINITION-Berechtigung im Datenbankbereich sowie SELECT-Berechtigungen für **sys.sql_expression_dependencies**und die Mitgliedschaft in der festen Serverrolle **dbcreator** erforderlich. Mitglieder der festen Serverrolle **sysadmin** oder des integrierten SQL Server-Systemadministratorkontos **sa** sind ebenfalls zum Registrieren einer DAC berechtigt. Zum Registrieren einer DAC, die keine Anmeldungen in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] enthält, müssen Sie Mitglied der Rollen **dbmanager** oder **serveradmin** sein. Zum Registrieren einer DAC, die Anmeldungen in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] enthält, müssen Sie Mitglied der Rollen **loginmanager** oder **serveradmin** sein.  
  
##  <a name="UsingRegisterDACWizard"></a> Verwenden des Assistenten zum Registrieren von Datenebenenanwendungen  
 **So registrieren Sie eine DAC mithilfe eines Assistenten**  
  
1.  Erweitern Sie im **Objekt-Explorer**den Knoten für die Instanz, die die Datenbank enthält, die als DAC registriert werden soll.  
  
2.  Erweitern Sie den Knoten **Datenbanken** .  
  
3.  Klicken Sie mit der rechten Maustaste auf die zu registrierende Datenbank, zeigen Sie auf **Tasks**, und wählen Sie dann **Als Datenschichtanwendung registrieren…**aus.  
  
4.  Bearbeiten Sie die Dialogfenster des Assistenten:  
  
    1.  [Seite "Einführung"](#Introduction)  
  
    2.  [Seite "Eigenschaften festlegen"](#Set_properties)  
  
    3.  [Seite "Überprüfung und Zusammenfassung"](#Summary)  
  
    4.  [Seite "DAC registrieren"](#Register)  
  
##  <a name="Introduction"></a> Seite "Einführung"  
 Auf dieser Seite werden die Schritte zum Registrieren einer Datenebenenanwendung beschrieben.  
  
 **Diese Seite nicht mehr anzeigen.** – Aktivieren Sie dieses Kontrollkästchen, damit die Seite in Zukunft nicht mehr angezeigt wird.  
  
 **Weiter >** – Geht zur Seite **Eigenschaften festlegen** über.  
  
 **Abbrechen** – Beendet den Assistenten, ohne eine DAC zu registrieren.  
  
 [Verwenden des Assistenten zum Registrieren von Datenebenenanwendungen](#UsingRegisterDACWizard)  
  
##  <a name="Set_properties"></a> Seite "Eigenschaften festlegen"  
 Verwenden Sie diese Seite, um Eigenschaften auf DAC-Ebene anzugeben, z. B. den Anwendungsnamen und die Version.  
  
 **Anwendungsname** – Eine Zeichenfolge mit dem Namen, der die DAC-Definition identifiziert. Das Feld enthält den Namen der Datenbank.  
  
 **Version** – Ein numerischer Wert, der die Version der DAC identifiziert. Die DAC-Version wird in Visual Studio verwendet, um die Version der DAC zu identifizieren, an der die Entwickler arbeiten. Bei der Bereitstellung einer DAC wird die Version in der **msdb** -Datenbank gespeichert und kann später unter dem Knoten **Datenschichtanwendungen** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]angezeigt werden.  
  
 **Beschreibung** – Optional. Ein Text, der den Zweck der DAC erläutert. Bei der Bereitstellung einer DAC wird die Beschreibung in einer **msdb**-Datenbank gespeichert und kann später unter dem Knoten **Datenschichtanwendungen** in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] angezeigt werden.  
  
 **< Zurück** – Sie kehren zur Seite **Einführung** zurück.  
  
 **Weiter >** – Überprüft, ob eine DAC aus den in der Datenbank enthaltenen Objekten erstellt werden kann, und zeigt die Ergebnisse auf der Seite **Überprüfung und Zusammenfassung** an.  
  
 **Abbrechen** – Beendet den Assistenten, ohne die DAC zu registrieren.  
  
 [Verwenden des Assistenten zum Registrieren von Datenebenenanwendungen](#UsingRegisterDACWizard)  
  
##  <a name="Summary"></a> Seite "Überprüfung und Zusammenfassung"  
 Verwenden Sie diese Seite, um die Aktionen zu überprüfen, die der Assistent beim Registrieren der DAC ausführt. Die Seite durchläuft drei Statusübergänge, während überprüft wird, ob eine DAC aus den in der Datenbank enthaltenen Objekten erstellt werden kann.  
  
 [Verwenden des Assistenten zum Registrieren von Datenebenenanwendungen](#UsingRegisterDACWizard)  
  
### <a name="retrieving-objects"></a>Abrufen von Objekten  
 **Datenbank- und Serverobjekte werden abgerufen.** – Zeigt eine Statusanzeige an, während der Assistent alle erforderlichen Objekte aus der Datenbank und der Instanz des Datenbankmoduls abruft.  
  
 **< Zurück**– Sie kehren zur Seite **Eigenschaften festlegen** zurück, auf der Sie Ihre Einträge ändern.  
  
 **Weiter >** – Registriert die DAC und zeigt die Ergebnisse auf der Seite **DAC registrieren** an.  
  
 **Abbrechen** – Beendet den Assistenten, ohne die DAC zu registrieren.  
  
 [Verwenden des Assistenten zum Registrieren von Datenebenenanwendungen](#UsingRegisterDACWizard)  
  
### <a name="validating-objects"></a>Überprüfen von Objekten  
 **Prüfung**  *SchemaName* **beispielsweise nicht ausgeführt werden.** *ObjectName* **beispielsweise nicht ausgeführt werden.** – Zeigt eine Statusanzeige an, während der Assistent die Abhängigkeiten der abgerufenen Objekten überprüft und sicherstellt, dass sie alle für eine DAC gültig sind. *SchemaName***.***ObjectName* gibt das derzeit überprüfte Objekt an.  
  
 **< Zurück**– Sie kehren zur Seite **Eigenschaften festlegen** zurück, auf der Sie Ihre Einträge ändern.  
  
 **Weiter >** – Registriert die DAC und zeigt die Ergebnisse auf der Seite **DAC registrieren** an.  
  
 **Abbrechen** – Beendet den Assistenten, ohne die DAC zu registrieren.  
  
 [Verwenden des Assistenten zum Registrieren von Datenebenenanwendungen](#UsingRegisterDACWizard)  
  
### <a name="summary"></a>Zusammenfassung  
 **Die folgende Einstellung wird verwendet, um die DAC zu registrieren.** – Zeigt einen Bericht der Eigenschaften und Objekte an, die in der DAC enthalten sind.  
  
 **Bericht speichern** – Klicken Sie auf diese Schaltfläche, um eine Kopie des Überprüfungsberichts in einer HTML-Datei zu speichern. Der Standardordner ist ein Ordner **SQL Server Management Studio\DAC Packages** im Ordner „Dokumente“ unter Ihrem Windows-Konto.  
  
 **< Zurück**– Sie kehren zur Seite **Eigenschaften festlegen** zurück, auf der Sie Ihre Einträge ändern.  
  
 **Weiter >** – Registriert die DAC und zeigt die Ergebnisse auf der Seite **DAC registrieren** an.  
  
 **Abbrechen** – Beendet den Assistenten, ohne die DAC zu registrieren.  
  
 [Verwenden des Assistenten zum Registrieren von Datenebenenanwendungen](#UsingRegisterDACWizard)  
  
##  <a name="Register"></a> Seite "DAC registrieren"  
 Auf dieser Seite wird angegeben, ob der Registrierungsvorgang erfolgreich war oder fehlgeschlagen ist.  
  
 **Die DAC wird registriert** – Gibt an, ob die einzelnen Aktionen zum Registrieren der DAC erfolgreich waren oder ob ein Fehler aufgetreten ist. Überprüfen Sie die Informationen, um zu bestimmen, ob die einzelnen Aktionen erfolgreich waren oder fehlgeschlagen sind. Für alle Aktionen, die fehlerhaft waren, ist in der Spalte **Ergebnis** ein Link enthalten. Klicken Sie auf den Link, um einen Bericht des für diese Aktion aufgetretenen Fehlers anzuzeigen.  
  
 **Bericht speichern** – Klicken Sie auf diese Schaltfläche, um den Registrierungsbericht in einer HTML-Datei zu speichern. In der Datei ist der Status der einzelnen Aktionen aufgeführt, einschließlich aller durch die Aktionen generierten Fehler. Der Standardordner ist ein Ordner **SQL Server Management Studio\DAC Packages** im Ordner „Dokumente“ unter Ihrem Windows-Konto. Der Dateiname hat das Format \<DACPackageName>_RegisterDACReport_yyyymmdd.html, wobei \<*DACPackageName*> dem Namen des bereitgestellten Pakets, *JJJJ* dem aktuellen Jahr, *MM* dem aktuellen Monat und *TT* dem aktuellen Tag entspricht.  
  
 **Fertig stellen** : Beendet den Assistenten.  
  
 [Verwenden des Assistenten zum Registrieren von Datenebenenanwendungen](#UsingRegisterDACWizard)  
  
##  <a name="RegisterDACPowerShell"></a> Registrieren einer DAC mit PowerShell  
 **So registrieren Sie eine DAC mithilfe der Methode „Register()“ in einem PowerShell-Skript**  
  
1.  Erstellen Sie ein SMO-Serverobjekt, und legen Sie es auf die Instanz fest, die die als DAC zu registrierende Datenbank enthält.  
  
2.  Fügen Sie eine Variable hinzu, die den Namen der Datenbank angibt.  
  
3.  Geben Sie die Metadaten für die DAC an, z. B. DAC-Namen, Version und Beschreibung.  
  
4.  Führen Sie die Register-Methode mit den oben angegebenen Informationen aus.  
  
### <a name="example-powershell"></a>Beispiel (PowerShell)  
 Im folgenden Beispiel wird die Datenbank MyDB als DAC registriert.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Specify the database to register as a DAC.  
$dbname = "MyDB"  
  
## Specify the DAC metadata.  
$applicationname = "MyApplication"  
$version = "1.0.0.0"  
$description = "This DAC defines the database used by my application."  
  
## Register the DAC.  
$registerunit = New-Object Microsoft.SqlServer.Management.Dac.DacExtractionUnit($srv, $dbname, $applicationname, $version)  
$registerunit.Description = $description  
$registerunit.Register()  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenebenenanwendungen](../../relational-databases/data-tier-applications/data-tier-applications.md)  
  
  
