---
title: Legacypaketbereitstellung (SSIS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: packages
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.packageconfigurationorganizer.f1
- sql13.dts.configwizard.finishdtsconfiguration.f1
- sql13.dts.configwizard.selectobjects.f1
- sql13.dts.configwizard.selecconfigtype.f1
- sql13.dts.configwizard.welcome.f1
- sql13.dts.deploymentwizard.welcome.f1
- sql13.dts.deploymentwizard.confirminstallation.f1
- sql13.dts.deploymentwizard.deploydtspackages.f1
- sql13.dts.deploymentwizard.finish.f1
- sql13.dts.deploymentwizard.configurepackages.f1
- sql13.dts.deploymentwizard.selectinstfolder.f1
- sql13.dts.deploymentwizard.packagevalidation.f1
- sql13.dts.deploymentwizard.specifytargetsqlserver.f1
helpviewer_keywords:
- Integration Services packages, deploying
- deploying packages [Integration Services]
- SQL Server Integration Services packages, deploying
- deploying packages [Integration Services], about deploying packages
- packages [Integration Services], deploying
- SSIS packages, deploying
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
caps.latest.revision: "46"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 486fa573b955848828bff349f364543e6a1e23f7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="legacy-package-deployment-ssis"></a>Legacy-Paketbereitstellung (SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthält Tools und Assistenten, mit denen Sie problemlos Pakete vom Entwicklungscomputer auf dem Produktionsserver oder anderen Computern bereitstellen können.  
  
 Das Paketbereitstellungsverfahren gliedert sich in vier Schritte:  
  
1.  Der erste Schritt ist optional und umfasst das Erstellen von Paketkonfigurationen, die Eigenschaften von Paketelementen zur Laufzeit aktualisieren. Diese Konfigurationen werden beim Bereitstellen der Pakete automatisch mit eingeschlossen.  
  
2.  Im zweiten Schritt wird das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt erstellt, um damit ein Paketbereitstellungshilfsprogramm zu erstellen. Das Bereitstellungshilfsprogramm für das Projekt enthält die Pakete, die Sie bereitstellen möchten.  
  
3.  Im dritten Schritt wird der Bereitstellungsordner, den Sie beim Erstellen des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekts erstellt haben, auf den Zielcomputer kopiert.  
  
4.  Im vierten Schritt wird auf dem Zielcomputer der Paketinstallations-Assistent ausgeführt, um damit die Pakete auf dem Dateisystem oder einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu installieren.  

## <a name="package-configurations"></a>Paketkonfigurationen
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt Paketkonfigurationen bereit, die Sie zum Aktualisieren der Werte von Eigenschaften zur Laufzeit verwenden können.  
  
> **HINWEIS:** Konfigurationen sind für das Paketbereitstellungsmodell verfügbar. Parameter werden für das Projektbereitstellungsmodell anstelle von Konfigurationen verwendet. Mithilfe des Projektbereitstellungsmodells können Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekte auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitstellen. Weitere Informationen zu Bereitstellungsmodellen finden Sie unter [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).   
  
 Eine Konfiguration ist ein Eigenschaft/Wert-Paar, das zu einem fertigen Paket hinzugefügt werden kann. Normalerweise erstellen Sie ein Paket, legen bei der Paketentwicklung die Eigenschaften der Paketobjekte fest und fügen die Konfiguration dem Paket hinzu. Bei der Ausführung ruft das Paket die neuen Werte für die Eigenschaften aus der Konfiguration ab. Sie können mithilfe einer Konfiguration beispielsweise die Verbindungszeichenfolge eines Verbindungs-Managers ändern oder den Wert einer Variablen aktualisieren.  
  
 Paketkonfigurationen bieten die folgenden Vorteile:  
  
-   Konfigurationen erleichtern das Verschieben von Paketen aus einer Entwicklungsumgebung in eine Produktionsumgebung. Mit einer Konfiguration können Sie z. B. den Pfad einer Quelldatei aktualisieren oder den Namen einer Datenbank oder eines Servers ändern.  
  
-   Konfigurationen sind nützlich, wenn Sie Pakete für viele unterschiedliche Server bereitstellen. Eine Variable in der Konfiguration für jedes bereitgestellte Paket kann beispielsweise verschiedene Speicherplatzwerte enthalten, und wenn der verfügbare Speicherplatz nicht dem Wert entspricht, kann das Paket nicht ausgeführt werden.  
  
-   Konfigurationen machen Pakete flexibler. So kann z. B. eine Konfiguration den Wert einer Variablen aktualisieren, die in einem Eigenschaftsausdruck verwendet wird.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] unterstützt verschiedene unterschiedliche Methoden zum Speichern von Paketkonfigurationen, z.B. als XML-Dateien, als Tabellen in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank und als Umgebungs- und Paketvariablen.  
  
 Jede Konfiguration besteht aus einem Paar aus Eigenschaft und Wert. Die XML-Konfigurationsdatei und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurationstypen können mehrere Konfigurationen enthalten.  
  
 Die Konfigurationen werden einbezogen, wenn Sie ein Paketbereitstellungshilfsprogramm zum Installieren von Paketen erstellen. Wenn Sie die Pakete installieren, können die Konfigurationen im Rahmen eines Schritts bei der Paketinstallation aktualisiert werden.  
  
### <a name="understanding-how-package-configurations-are-applied-at-run-time"></a>Grundlegendes zur Anwendung von Paketkonfigurationen zur Laufzeit  
 Wenn Sie das Befehlszeilen-Hilfsprogramm **dtexec.exe** verwenden, um ein bereitgestelltes Paket auszuführen, wendet das Hilfsprogramm Paketkonfigurationen zweimal an. Das Hilfsprogramm wendet Konfigurationen sowohl vor als auch nach dem Anwenden der Optionen an, die Sie in der Befehlszeile angegeben haben.  
  
 Während das Hilfsprogramm das Paket lädt und ausführt, treten Ereignisse in der folgenden Reihenfolge auf:  
  
1.  Das Hilfsprogramm **dtexec** lädt das Paket.  
  
2.  Das Hilfsprogramm wendet die Konfigurationen, die zur Entwurfszeit im Paket angegeben wurden, in der Reihenfolge an, die im Paket festgelegt ist. (Die einzige Ausnahme ist hierbei die Variablenkonfiguration für übergeordnete Pakete. Das Hilfsprogramm wendet diese Konfigurationen nur einmal später im Prozess an.)  
  
3.  Das Hilfsprogramm wendet dann alle Optionen an, die Sie in der Befehlszeile angegeben haben.  
  
4.  Anschließend lädt das Hilfsprogramm die Konfigurationen neu, die zur Entwurfszeit im Paket angegeben wurden. Dabei wird die Reihenfolge verwendet, die im Paket festgelegt ist. (Die Ausnahme von dieser Regel ist wiederum die Variablenkonfiguration für übergeordnete Pakete.) Das Hilfsprogramm verwendet alle angegebenen Befehlszeilenoptionen, um die Konfigurationen neu zu laden. Es kann also sein, dass andere Werte von einem anderen Speicherort erneut geladen werden.  
  
5.  Das Hilfsprogramm wendet die Variablenkonfiguration für übergeordnete Pakete an.  
  
6.  Das Hilfsprogramm führt das Paket aus.  
  
 Die Art und Weise, wie das Hilfsprogramm **dtexec** Konfigurationen anwendet, wirkt sich auf die folgenden Befehlszeilenoptionen aus:  
  
-   Sie können zur Laufzeit die Option **/Connection** oder **/Set** verwenden, um Paketkonfigurationen von einem anderen Speicherort als dem zur Entwurfszeit angegebenen Speicherort zu laden.  
  
-   Sie können die Option **/ConfigFile** verwenden, um zur Laufzeit zusätzliche Konfigurationen zu laden, die Sie zur Entwurfszeit nicht angegeben haben.  
  
 Für diese Befehlszeilenoptionen gelten jedoch einige Einschränkungen:  
  
-   Sie können die Option **/Set** oder **/Connection** nicht verwenden, um einzelne Werte zu überschreiben, die auch von einer Konfiguration festgelegt werden.  
  
-   Sie können die Option **/ConfigFile** nicht verwenden, um Konfigurationen zu laden, die die zur Entwurfszeit angegebenen Konfigurationen ersetzen.  
  
 Weitere Informationen zu diesen Optionen und zum Unterschied des Verhaltens dieser Optionen für [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] und frühere Versionen finden Sie unter [Verhaltensänderungen von Integration Services-Features in SQL Server 2016](http://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794).  
  
### <a name="package-configuration-types"></a>Paketkonfigurationstypen  
 Die folgende Tabelle beschreibt die verschiedenen Paketkonfigurationstypen.  
  
|Typ|Description|  
|----------|-----------------|  
|XML-Konfigurationsdatei|Eine XML-Datei enthält die Konfigurationen. Die XML-Datei kann mehrere Konfigurationen enthalten.|  
|Umgebungsvariable|Eine Umgebungsvariable enthält die Konfiguration.|  
|Registrierungseintrag|Ein Registrierungseintrag enthält die Konfiguration.|  
|Variable für das übergeordnete Paket|Eine Variable im Paket enthält die Konfiguration. Dieser Konfigurationstyp wird normalerweise zum Aktualisieren von Eigenschaften in untergeordneten Paketen verwendet.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] table|Eine Tabelle in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank enthält die Konfiguration. Die Tabelle kann mehrere Konfigurationen enthalten.|  
  
#### <a name="xml-configuration-files"></a>XML-Konfigurationsdateien  
 Wenn Sie den Konfigurationstyp **XML-Konfigurationsdatei** auswählen, können Sie eine neue Konfigurationsdatei erstellen, eine vorhandene Datei erneut verwenden und neue Konfigurationen hinzufügen oder eine vorhandene Datei erneut verwenden und dabei den bisherigen Dateiinhalt überschreiben.  
  
 Eine XML-Konfigurationsdatei besteht aus zwei Abschnitten:  
  
-   Einer Überschrift, die Informationen zur Konfigurationsdatei enthält. Dieses Element enthält Attribute wie z. B. der Erstellungszeitpunkt der Datei und den Namen der Person, von der die Datei erstellt wurde.  
  
-   Konfigurationselemente können Informationen zu jeder Konfiguration enthalten. Dieses Element enthält Attribute wie z. B. den Eigenschaftspfad und den konfigurierten Wert einer Eigenschaft.  
  
 Das folgende XML-Codebeispiel veranschaulicht die Syntax von XML-Konfigurationsdateien. Das Beispiel zeigt eine Konfiguration für die Value-Eigenschaft der ganzzahligen Variable `MyVar`.  
  
```xml
\<?xml version="1.0"?>  
<DTSConfiguration>  
   <DTSConfigurationHeading>  
      <DTSConfigurationFileInfo  
          GeneratedBy="DomainName\UserName"  
          GeneratedFromPackageName="Package"  
          GeneratedFromPackageID="{2AF06766-817A-4E28-9878-0DE37A150648}"  
          GeneratedDate="2/01/2005 5:58:09 PM"/>  
   </DTSConfigurationHeading>  
   <Configuration ConfiguredType="Property" Path="\Package.Variables[User::MyVar].Value" ValueType="Int32">  
      <ConfiguredValue>0</ConfiguredValue>  
   </Configuration>  
</DTSConfiguration>  
  
```  
  
#### <a name="registry-entry"></a>Registrierungseintrag  
 Wenn Sie zum Speichern einer Konfiguration einen Registrierungseintrag verwenden möchten, können Sie entweder einen vorhandenen Schlüssel verwenden oder einen neuen Schlüssel in HKEY_CURRENT_USER erstellen. Der verwendete Registrierungsschlüssel muss einen Wert mit dem Namen **Value**aufweisen. Bei diesem Wert kann es sich um einen Wert vom Typ DWORD oder um eine Zeichenfolge handeln.  
  
 Wenn Sie den Konfigurationstyp **Registrierungseintrag** auswählen, geben Sie den Namen des Registrierungsschlüssels im Eingabefeld Registrierung ein. Das Format lautet: \<Registrierungsschlüssel>. Wenn Sie einen Registrierungsschlüssel verwenden möchten, der nicht im Stamm von HKEY_CURRENT_USER enthalten ist, verwenden Sie das Format \<Registrierungsschlüssel\Registrierungsschlüssel\\...>, um den Schlüssel zu identifizieren. Wenn Sie beispielsweise den Schlüssel MyPackage verwenden, der sich in SSISPackages befindet, geben Sie **SSISPackages\MyPackage**ein.  
  
#### <a name="sql-server"></a>SQL Server  
 Wenn Sie den Konfigurationstyp **SQL Server** auswählen, geben Sie die Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank an, in der die Konfigurationen gespeichert werden sollen. Sie können die Konfigurationen in einer vorhandenen Tabelle speichern oder eine neue Tabelle in der angegebenen Datenbank erstellen.  
  
 Die folgende SQL-Anweisung zeigt die standardmäßige CREATE TABLE-Anweisung, die der Paketkonfigurations-Assistent bereitstellt.  
  
```sql
CREATE TABLE [dbo].[SSIS Configurations]  
(  
ConfigurationFilter NVARCHAR(255) NOT NULL,  
ConfiguredValue NVARCHAR(255) NULL,  
PackagePath NVARCHAR(255) NOT NULL,  
ConfiguredValueType NVARCHAR(20) NOT NULL  
)  
  
```  
  
 Der Name, den Sie für die Konfiguration bereitstellen, ist der Wert, der in der **ConfigurationFilter** -Spalte gespeichert wird.  
  
### <a name="direct-and-indirect-configurations"></a>Direkte und indirekte Konfigurationen  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ermöglicht direkte und indirekte Konfigurationen. Wenn Sie Konfigurationen direkt angeben, erstellt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eine direkte Verknüpfung zwischen dem Konfigurationselement und der Paketobjekteigenschaft. Direkte Konfigurationen sind die bessere Wahl, wenn sich der Speicherort der Quelle nicht ändert. Wenn Sie z. B. sicher sind, dass alle Bereitstellungen im Paket denselben Dateipfad verwenden, können Sie eine XML-Konfigurationsdatei angeben.  
  
 Indirekte Konfigurationen verwenden Umgebungsvariablen. Statt die Konfigurationseinstellung direkt anzugeben, zeigt die Konfiguration auf eine Umgebungsvariable, die ihrerseits den Konfigurationswert enthält. Das Verwenden indirekter Konfigurationen ist die bessere Wahl, wenn sich der Speicherort der Konfiguration für jede Bereitstellung eines Pakets ändern kann.  

## <a name="create-package-configurations"></a>Erstellen von Paketkonfigurationen
  Erstellen Sie im Dialogfeld **Paketkonfigurationsplaner** und im Paketkonfigurations-Assistenten entsprechende Paketkonfigurationen. Um auf diese Tools zuzugreifen, klicken Sie in **im Menü** SSIS **auf** Paketkonfigurationen [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
  
 **HINWEISE:**
>Sie können auch durch Klicken auf die Schaltfläche mit den Auslassungspunkten neben der Eigenschaft **Konfiguration** auf den **Paketkonfigurationsplaner** zugreifen. Die Eigenschaft Konfiguration wird im Eigenschaftenfenster für das Paket angezeigt.  
  
>Konfigurationen sind für das Paketbereitstellungsmodell verfügbar. Parameter werden für das Projektbereitstellungsmodell anstelle von Konfigurationen verwendet. Mithilfe des Projektbereitstellungsmodells können Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekte auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitstellen. Weitere Informationen zu Bereitstellungsmodellen finden Sie unter [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).    
  
>Im Dialogfeld **Paketkonfigurationsplaner** können Sie Pakete zum Verwenden von Konfigurationen aktivieren, Konfigurationen hinzufügen und löschen sowie die bevorzugte Reihenfolge festlegen, in der die Konfigurationen geladen werden sollten. 
 
>Wenn Paketkonfigurationen in der bevorzugten Reihenfolge geladen werden, werden die Konfigurationen in der Reihenfolge geladen, in der sie im Dialogfeld **Paketkonfigurationsplaner** angezeigt werden, wobei mit der Konfiguration am Anfang der Liste begonnen wird. Zur Laufzeit werden Paketkonfigurationen möglicherweise aber nicht in der bevorzugten Reihenfolge geladen. Beispielsweise werden übergeordnete Paketkonfigurationen nach Konfigurierungen anderer Typen geladen.  
  
>Wenn mehrere Konfigurationen dieselbe Objekteigenschaft festlegen, wird der zuletzt geladene Wert zur Laufzeit verwendet.  
  
 Im Dialogfeld **Paketkonfigurationsplaner** führen Sie den Paketkonfigurations-Assistenten aus, der Sie durch die Schritte zum Erstellen einer Konfiguration führt. Um den Paketkonfigurations-Assistenten auszuführen, fügen Sie im Dialogfeld **Paketkonfigurationsplaner** eine neue Konfiguration hinzu, oder bearbeiten Sie eine vorhandene Konfiguration. Auf den Seiten des Assistenten wählen Sie den Konfigurationstyp aus. Sie legen fest, ob Sie direkt auf die Konfiguration zugreifen oder Umgebungsvariablen verwenden möchten, und Sie wählen die in der Konfiguration zu speichernden Eigenschaften aus.  
  
 Im folgenden Beispiel werden die Zieleigenschaften einer Variablen und eines Pakets gezeigt, so wie sie auf der Seite Assistenten abschließen des Paketkonfigurations-Assistenten angezeigt werden:  
  
 \Package.Variables[User::TodaysDate].Properties[RaiseChangedEvent]  
  
 \Package.Properties[MaximumErrorCount]  
  
 \Package.Properties[LoggingMode]  
  
 \Package.Properties[LocaleID]  
  
 \Package\My SQL Task.Variables[User::varTableName].Properties[Value]  
  
 In diesem Beispiel werden diese Eigenschaften von der Konfiguration aktualisiert:  
  
-   Die RaiseChangedEvent-Eigenschaft der benutzerdefinierten Variablen `TodaysDate`.  
  
-   Die Eigenschaften MaximumErrorCount, LoggingMode und LocaleID des Pakets.  
  
-   Die Value-Eigenschaft der benutzerdefinierten Variablen `varTableName`im Bereich des Tasks My SQL Task.  
  
 "\Package" stellt den Stamm dar, und Punkte (.) trennen die Objekte, die den Pfad für die von der Konfiguration aktualisierten Eigenschaft definieren. Die Namen von Variablen und Eigenschaften werden in eckigen Klammern eingeschlossen. Der Begriff Package wird immer in der Konfiguration verwendet, unabhängig vom Paketnamen. Für alle anderen Objekte im Pfad werden jedoch die benutzerdefinierten Namen verwendet.  
  
 Nachdem der Assistent beendet ist, wird die neue Konfiguration der Konfigurationsliste im Dialogfeld **Paketkonfigurationsplaner** hinzugefügt.  
  
> **HINWEIS:** Auf der letzten Seite des Paketkonfigurations-Assistenten, der Seite Assistenten abschließen, werden die Zieleigenschaften der Konfiguration aufgelistet. Wenn Sie beim Ausführen von Paketen mithilfe des Eingabeaufforderungs-Hilfsprogramms **dtexec** die Eigenschaften aktualisieren möchten, können Sie die Zeichenfolgen, die die Eigenschaftspfade darstellen, generieren. Führen Sie hierzu den Paketkonfigurations-Assistenten aus, kopieren Sie dann die Zeichenfolgen, und fügen Sie diese im Eingabeaufforderungsfenster für die Verwendung mit der festgelegten Option von **dtexec**ein.  
  
 In der folgenden Tabelle werden die Spalten der Konfigurationsliste im Dialogfeld **Paketkonfigurationsplaner** beschrieben.  
  
|Column|Description|  
|------------|-----------------|  
|**Konfigurationsname**|De Name der Konfiguration.|  
|**Konfigurationstyp**|Der Konfigurationstyp.|  
|**Konfigurationszeichenfolge**|Der Speicherort der Konfiguration. Beim Speicherort kann es sich um einen Pfad, eine Umgebungsvariable, einen Registrierungsschlüssel, den Namen einer Variablen eines übergeordneten Pakets oder eine Tabelle in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank handeln.|  
|**Zielobjekt**|Der Name des Objekts mit einer Eigenschaft, die eine Konfiguration besitzt. Wenn es sich bei der Konfiguration um eine XML-Konfigurationsdatei handelt, ist die Spalte leer, da die Konfiguration mehrere Objekte aktualisieren kann.|  
|**Zieleigenschaft**|Der Name der Eigenschaft. Wenn die Konfiguration in eine XML-Konfigurationsdatei oder in eine SQL Server-Tabelle schreibt, ist die Spalte leer, da die Konfiguration mehrere Objekte aktualisieren kann.|  
  
### <a name="to-create-a-package-configuration"></a>So erstellen Sie eine Paketkonfiguration  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer auf die Registerkarte **Ablaufsteuerung**, **Datenfluss**, **Ereignishandler**oder **Paket-Explorer** .  
  
4.  Klicken Sie im Menü **SSIS** auf **Paketkonfigurationen**.  
  
5.  Wählen Sie im Dialogfeld **Paketkonfigurationsplaner** die Option **Paketkonfigurationen aktivieren**aus, und klicken Sie dann auf **Hinzufügen**.  
  
6.  Klicken Sie auf der Willkommensseite des Paketkonfigurationsassistenten auf **Weiter**.  
  
7.  Geben Sie auf der Seite "Konfigurationstyp auswählen" den Konfigurationstyp an, und legen Sie dann die für den Konfigurationstyp relevanten Eigenschaften fest. Weitere Informationen finden Sie unter [Package Configuration Wizard UI Reference](../../integration-services/packages/package-configuration-wizard-ui-reference.md).  
  
8.  Wählen Sie auf der Seite zum Auswählen der zu exportierenden Eigenschaften die Eigenschaften von Paketobjekten aus, die in der Konfiguration enthalten sein sollen. Wenn der Konfigurationstyp nur eine Eigenschaft unterstützt, lautet die Überschrift dieser Assistentenseite Zieleigenschaft auswählen. Weitere Informationen finden Sie unter [Package Configuration Wizard UI Reference](../../integration-services/packages/package-configuration-wizard-ui-reference.md).  
  
    > **HINWEIS:** Nur die Konfigurationstypen **XML-Konfigurationsdatei** und **SQL Server** unterstützen die Berücksichtigung von mehreren Eigenschaften in einer Konfiguration.  
  
9. Geben Sie auf der Seite "Assistenten abschließen" den Namen der Konfiguration ein, und klicken Sie dann auf **Fertig stellen**.  
  
10. Zeigen Sie die Konfiguration im Dialogfeld **Paketkonfigurationsplaner** an.  
  
11. Klicken Sie auf **Schließen**.  

## <a name="package-configurations-organizer"></a>Paketkonfigurationsplaner
  Mithilfe des Dialogfelds **Paketkonfigurationsplaner** können Sie Paketkonfigurationen aktivieren, eine Liste der Konfigurationen für das aktuelle Paket anzeigen und die bevorzugte Reihenfolge angeben, in der die Konfigurationen geladen werden sollten.  
  
> **HINWEIS:** Konfigurationen sind für das Paketbereitstellungsmodell verfügbar. Parameter werden für das Projektbereitstellungsmodell anstelle von Konfigurationen verwendet. Mithilfe des Projektbereitstellungsmodells können Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekte auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitstellen. Weitere Informationen zu Bereitstellungsmodellen finden Sie unter [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).    
  
 Wenn mehrere Konfigurationen dieselbe Eigenschaft aktualisieren, ersetzen Werte aus Konfigurationen weiter unten in der Konfigurationsliste die Werte aus Konfigurationen weiter oben in der Liste. Der letzte in die Eigenschaft geladene Wert ist der Wert, der verwendet wird, wenn das Paket ausgeführt wird. Auch muss die indirekte Konfiguration, die auf den Speicherort der direkten Konfiguration verweist, weiter oben in der Liste stehen, wenn das Paket eine Kombination aus direkter Konfiguration, z. B. XML-Konfigurationsdatei, und indirekter Konfiguration, z. B. Umgebungsvariable, verwendet.  
  
> **HINWEIS:** Wenn Paketkonfigurationen in der bevorzugten Reihenfolge geladen werden, werden die Konfigurationen in der Reihenfolge geladen, in der sie im Dialogfeld **Paketkonfigurationsplaner** angezeigt werden, wobei mit der Konfiguration am Anfang der Liste begonnen wird. Zur Laufzeit werden Paketkonfigurationen möglicherweise aber nicht in der bevorzugten Reihenfolge geladen. Beispielsweise werden übergeordnete Paketkonfigurationen nach Konfigurationen anderer Typen geladen.  
  
 Paketkonfigurationen aktualisieren die Werte der Eigenschaften von Paketobjekten zur Laufzeit. Beim Laden eines Pakets werden die beim Entwickeln des Pakets festgelegten Werte durch die Werte der Konfigurationen ersetzt. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] unterstützt unterschiedliche Konfigurationstypen. Beispielsweise können Sie eine XML-Datei mit mehreren möglichen Konfigurationen oder eine Umgebungsvariable mit einer einzigen enthaltenen Konfiguration verwenden. Weitere Informationen finden Sie unter [Package Configurations](../../integration-services/packages/package-configurations.md).  
  
### <a name="options"></a>enthalten  
 **Paketkonfigurationen aktivieren**  
 Wählen Sie diese Option aus, um mit dem Paket Konfigurationen zu verwenden.  
  
 **Konfigurationsname**  
 Zeigt den Namen der Konfiguration an.  
  
 **Konfigurationstyp**  
 Zeigt den Typ des Speicherorts von Konfigurationen an.  
  
 **Konfigurationszeichenfolge**  
 Zeigt den Speicherort der Konfigurationswerte an. Der Speicherort kann der Pfad einer Datei, der Name einer Umgebungsvariablen, der Name einer Variablen für das übergeordnete Paket, ein Registrierungsschlüssel oder der Name einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle sein.  
  
 **Zielobjekt**  
 Zeigt den Namen des Objekts an, das von der Konfiguration aktualisiert wird. Wenn es sich bei der Konfiguration um eine XML-Konfigurationsdatei oder eine SQL Server-Tabelle handelt, ist die Spalte leer, da die Konfiguration mehrere Objekte enthalten kann.  
  
 **Zieleigenschaft**  
 Zeigt den Namen der durch die Konfiguration geänderten Eigenschaft an. Diese Spalte ist leer, wenn der Konfigurationstyp mehrere Konfigurationen unterstützt.  
  
 **Hinzufügen**  
 Fügt mithilfe des Paketkonfigurationsassistenten eine Konfiguration hinzu.  
  
 **Bearbeiten**  
 Bearbeitet eine vorhandene Konfiguration, indem der Paketkonfigurationsassistent erneut ausgeführt wird.  
  
 **Entfernen**  
 Wählen Sie eine Konfiguration aus, und klicken Sie auf **Entfernen**.  
  
 **Pfeile**  
 Wählen Sie eine Konfiguration aus, und verschieben Sie sie mithilfe der Pfeile in der Liste nach oben oder nach unten. Konfigurationen werden in der Reihenfolge geladen, in der sie in der Liste angezeigt werden.  

## <a name="package-configuration-wizard-ui-reference"></a>Referenz zur Benutzeroberfläche des Paketkonfigurations-Assistenten
  Der **Paketkonfigurations-Assistent** unterstützt Sie dabei, Konfigurationen zu erstellen, durch die die Eigenschaften eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakets und seiner Objekte zur Laufzeit aktualisiert werden. Dieser Assistent wird ausgeführt, wenn Sie im Dialogfeld **Paketkonfigurationsplaner** eine neue Konfiguration hinzufügen oder eine vorhandene Konfiguration ändern. Um das Dialogfeld **Paketkonfigurationsplaner** zu öffnen, wählen Sie in **im Menü** SSIS **die Option** Paketkonfigurationen [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aus. Weitere Informationen finden Sie unter [Erstellen von Paketkonfigurationen](../../integration-services/packages/create-package-configurations.md).  
  
> **HINWEIS:** Konfigurationen sind für das Paketbereitstellungsmodell verfügbar. Parameter werden für das Projektbereitstellungsmodell anstelle von Konfigurationen verwendet. Mithilfe des Projektbereitstellungsmodells können Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekte auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitstellen. Weitere Informationen zu Bereitstellungsmodellen finden Sie unter [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).  
  
 In den folgenden Abschnitten werden Seiten des Assistenten beschrieben.  
  
### <a name="welcome-to-the-package-configuration-wizard-page"></a>Willkommensseite des Paketkonfigurationsassistenten  
 Mithilfe des **SSIS-Konfigurations-Assistenten** können Sie Konfigurationen erstellen, durch die die Eigenschaften eines Paketes und seiner Objekte zur Laufzeit aktualisiert werden.  
  
#### <a name="options"></a>enthalten  
 **Diese Seite nicht wieder anzeigen**  
 Die Willkommensseite beim nächsten Öffnen des Assistenten auslassen.  
  
 **Weiter**  
 Mit dieser Option können Sie zur nächsten Seite des Assistenten wechseln.  
  
### <a name="select-configuration-type-page"></a>Seite "Konfigurationstyp" auswählen  
 Auf der Seite **Konfigurationstyp auswählen** können Sie die Art der Konfiguration angeben, die erstellt werden soll.  
  
 Weitere Informationen dazu, welchen Konfigurationstyp Sie verwenden sollten, finden Sie unter [Package Configurations](../../integration-services/packages/package-configurations.md).  
  
#### <a name="static-options"></a>Statische Optionen  
 **Konfigurationstyp**  
 Wählen Sie mithilfe folgender Optionen den Typ der Quelle aus, in der die Konfiguration gespeichert werden soll:  
  
|Wert|Description|  
|-----------|-----------------|  
|**XML-Konfigurationsdatei**|Speichert die Konfiguration als XML-Datei. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen im Abschnitt **Konfigurationstyp**angezeigt.|  
|**Umgebungsvariable**|Speichert die Konfiguration in einer der Umgebungsvariablen. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen im Abschnitt **Konfigurationstyp**angezeigt.|  
|**Registrierungseintrag**|Speichert die Konfiguration in der Registrierung. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen im Abschnitt **Konfigurationstyp**angezeigt.|  
|**Variable für das übergeordnete Paket**|Speichert die Konfiguration als Variable in dem Paket, das den Task enthält.  Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen im Abschnitt **Konfigurationstyp**angezeigt.|  
|**SQL Server**|Speichert die Konfiguration in einer Tabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen im Abschnitt **Konfigurationstyp**angezeigt.|  
  
 **Weiter**  
 Zeigt die nächste Seite in der Sequenz des Assistenten an.  
  
#### <a name="dynamic-options"></a>Dynamische Optionen  
  
##### <a name="configuration-type-option--xml-configuration-file"></a>Konfigurationstypoption = XML-Konfigurationsdatei  
 **Konfigurationseinstellungen direkt angeben**  
 Verwenden Sie diese Option, um die Einstellungen direkt anzugeben.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Konfigurationsdateiname**|Geben Sie den Pfad der Konfigurationsdatei ein, die der Assistent generiert.|  
|**Durchsuchen**|Im Dialogfeld **Speicherort der Konfigurationsdatei auswählen** können Sie den Pfad für die Konfigurationsdatei angeben, die der Assistent generiert. Wenn die Datei nicht vorhanden ist, wird sie durch den Assistenten erstellt.|  
  
 **Konfigurationsspeicherort ist in einer Umgebungsvariablen gespeichert**  
 Verwenden Sie diese Option, um die Umgebungsvariable anzugeben, in der die Konfiguration gespeichert werden soll.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Umgebungsvariable**|Wählen Sie eine Umgebungsvariable aus der Liste aus.|  
  
##### <a name="configuration-type-option--environment-variable"></a>Konfigurationstypoption = Umgebungsvariable  
 **Umgebungsvariable**  
 Wählen Sie die Umgebungsvariable aus, die die Konfigurationsinformationen enthält.  
  
##### <a name="configuration-type-option--registry-entry"></a>Konfigurationstypoption = Registrierungseintrag  
 **Konfigurationseinstellungen direkt angeben**  
 Verwenden Sie diese Option, um die Einstellungen direkt anzugeben.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Registrierungseintrag**|Geben Sie den Registrierungsschlüssel ein, der die Konfigurationsinformationen enthält. Das Format lautet: \<Registrierungsschlüssel>.<br /><br /> Der Registrierungsschlüssel muss bereits in HKEY_CURRENT_USER vorhanden sein und einen Wert mit dem Namen "Value" aufweisen. Bei diesem Wert kann es sich um einen Wert vom Typ DWORD oder um eine Zeichenfolge handeln.<br /><br /> Wenn Sie einen Registrierungsschlüssel verwenden möchten, der nicht im Stamm von HKEY_CURRENT_USER gespeichert ist, verwenden Sie das Format \<Registrierungsschlüssel\Registrierungsschlüssel\\...>, um den Schlüssel zu identifizieren.|  
  
 **Konfigurationsspeicherort ist in einer Umgebungsvariablen gespeichert**  
 Verwenden Sie diese Option, um die Umgebungsvariable anzugeben, in der die Konfiguration gespeichert werden soll.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Umgebungsvariable**|Wählen Sie eine Umgebungsvariable aus der Liste aus.|  
  
##### <a name="configuration-type-option--parent-package-variable"></a>Konfigurationstypoption = Variable für das übergeordnete Paket  
 **Konfigurationseinstellungen direkt angeben**  
 Verwenden Sie diese Option, um die Einstellungen direkt anzugeben.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Übergeordnete Variable**|Geben Sie die Variable im übergeordneten Paket an, die die Konfigurationsinformationen enthält.|  
  
 **Konfigurationsspeicherort ist in einer Umgebungsvariablen gespeichert**  
 Verwenden Sie diese Option, um die Umgebungsvariable anzugeben, in der die Konfiguration gespeichert wird.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Umgebungsvariable**|Wählen Sie eine Umgebungsvariable aus der Liste aus.|  
  
##### <a name="configuration-type-options--sql-server"></a>Konfigurationstypoptionen = SQL Server  
 **Konfigurationseinstellungen direkt angeben**  
 Verwenden Sie diese Option, um die Einstellungen direkt anzugeben.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Verbindung**|Wählen Sie eine Verbindung aus der Liste aus, oder klicken Sie auf **Neu** , um eine neue Verbindung herzustellen.|  
|**Konfigurationstabelle**|Wählen Sie eine vorhandene Tabelle aus, oder klicken Sie auf **Neu** , um eine SQL-Anweisung zu schreiben, die eine neue Tabelle erstellt.|  
|**Konfigurationsfilter**|Wählen Sie einen vorhandenen Konfigurationsnamen aus, oder geben Sie einen neuen Namen ein.<br /><br /> Viele SQL Server-Konfigurationen können in derselben Tabelle gespeichert werden, und jede Konfiguration kann mehrere Konfigurationselemente enthalten.<br /><br /> Dieser benutzerdefinierte Wert wird in der Tabelle gespeichert, um Konfigurationselemente zu identifizieren, die zu einer bestimmten Konfiguration gehören.|  
  
 **Konfigurationsspeicherort ist in einer Umgebungsvariablen gespeichert**  
 Verwenden Sie diese Option, um die Umgebungsvariable anzugeben, in der die Konfiguration gespeichert ist.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Umgebungsvariable**|Wählen Sie eine Umgebungsvariable aus der Liste aus.|  
  
### <a name="select-objects-to-export-page"></a>Seite "Eigenschaften für den Exportvorgang auswählen"  
 Verwenden Sie die Seite **Zieleigenschaft auswählen** oder die Seite Eigenschaften für den Exportvorgang auswählen, um die in der Konfiguration enthaltenen Objekteigenschaften anzugeben. Mehrere Eigenschaften können nur ausgewählt werden, wenn Sie als Konfigurationstyp XML auswählen.  
  
#### <a name="options"></a>enthalten  
 **Objekte**  
 Erweitern Sie die Pakethierarchie, und wählen Sie die zu exportierenden Eigenschaften aus.  
  
 **Eigenschaftsattribute**  
 Zeigen Sie die Attribute einer Eigenschaft an.  
  
 **Weiter**  
 Mit dieser Option können Sie zur nächsten Seite des Assistenten wechseln.  
  
### <a name="completing-the-wizard-page"></a>Seite "Assistenten abschließen"  
 Mithilfe der Seite **Assistenten abschließen** können Sie einen Namen für die Konfiguration und die Einstellungen der Sicht angeben, die der Assistent zum Erstellen der Konfiguration verwendet. Nach dem Abschließen des Assistenten wird der **Paketkonfigurationsplaner** angezeigt, in dem alle Konfigurationen für das Paket aufgeführt werden.  
  
#### <a name="options"></a>enthalten  
 **Konfigurationsname**  
 Geben Sie den Namen der Konfiguration ein.  
  
 **Vorschau**  
 Zeigen Sie die Einstellungen an, die vom Assistenten zum Erstellen der Konfiguration verwendet werden.  
  
 **Fertig stellen**  
 Erstellen Sie die Konfiguration, und beenden Sie den **Paketkonfigurations-Assistenten**.  

## <a name="child"></a> Verwenden der Werte von Variablen und Parametern in einem untergeordneten Paket
  In diesem Verfahren wird das Erstellen einer Paketkonfiguration beschrieben, die den Konfigurationstyp der übergeordneten Variablen verwendet. Durch diesen Konfigurationstyp kann ein untergeordnetes Paket, das von einem übergeordneten Paket ausgeführt wird, auf eine Variable im übergeordneten Element zugreifen.  
  
> [!NOTE]  
>  Sie können auch Werte an ein untergeordnetes Paket übergeben, indem Sie den Task Paket ausführen konfigurieren, um untergeordneten Paketparametern Variablen oder Parameter für übergeordnete Pakete bzw. Projektparameter zuzuordnen. Weitere Informationen finden Sie unter [Execute Package Task](../../integration-services/control-flow/execute-package-task.md).  
  
 Dabei ist das Erstellen der Variablen im übergeordneten Paket vor dem Erstellen der Paketkonfiguration im untergeordneten Paket nicht erforderlich. Sie können dem übergeordneten Paket jederzeit die Variable hinzufügen. Allerdings müssen Sie in der Paketkonfiguration den genauen Namen der übergeordneten Variablen verwenden. Bevor Sie jedoch eine übergeordnete Variablenkonfiguration erstellen können, muss im untergeordneten Paket bereits eine Variable vorhanden sein, die von der Konfiguration aktualisiert werden kann. Weitere Informationen zum Hinzufügen und Konfigurieren von Variablen finden Sie unter [Hinzufügen, Löschen, Ändern des Bereichs von benutzerdefinierten Variablen in einem Paket](http://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e).  
  
 Der Gültigkeitsbereich der Variablen im übergeordneten Paket, das in einer übergeordneten Variablenkonfiguration verwendet wird, kann auf den Task Paket ausführen, auf den Container, in dem der Task enthalten ist, oder auf das Paket festgelegt werden. Wenn in einem Paket mehrere gleichnamige Variablen vorhanden sind, wird die Variable verwendet, die im Gültigkeitsbereich des Tasks Paket ausführen am nächsten liegt. Der Gültigkeitsbereich, der am nächsten am Task Paket ausführen liegt, ist der Task selbst.  
  
### <a name="to-add-a-variable-to-a-parent-package"></a>So fügen Sie einem übergeordneten Paket eine Variable hinzu  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem Paket, dem Sie eine Variable hinzufügen möchten, um diese an ein untergeordnetes Paket zu übergeben.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Gehen Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zum Definieren des Gültigkeitsbereichs der Variablen wie folgt vor:  
  
    -   Um den Gültigkeitsbereich des Pakets festzulegen, klicken Sie an eine beliebige Stelle auf der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** .  
  
    -   Klicken Sie auf den Container, um den Gültigkeitsbereich des übergeordneten Containers des Tasks "Paket ausführen" festzulegen.  
  
    -   Klicken Sie auf den Task, um den Bereich auf den Task "Paket ausführen" festzulegen.  
  
4.  Fügen Sie eine Variable hinzu, und konfigurieren Sie diese.  
  
    > [!NOTE]  
    >  Wählen Sie einen Datentyp aus, der mit den in der Variablen gespeicherten Daten kompatibel ist.  
  
5.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
### <a name="to-add-a-variable-to-a-child-package"></a>So fügen Sie einem untergeordneten Paket eine Variable hinzu  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem Paket, dem Sie eine übergeordnete Variablenkonfiguration hinzufügen möchten.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer an eine beliebige Stelle auf der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** , um den Gültigkeitsbereich des Pakets festzulegen.  
  
4.  Fügen Sie eine Variable hinzu, und konfigurieren Sie diese.  
  
    > [!NOTE]  
    >  Wählen Sie einen Datentyp aus, der mit den in der Variablen gespeicherten Daten kompatibel ist.  
  
5.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  

## <a name="create-a-deployment-utility"></a>Erstellen eines Bereitstellungs-Hilfsprogramms
  Der erste Schritt beim Bereitstellen von Paketen besteht im Erstellen eines Bereitstellungshilfsprogramms für ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt. Das Bereitstellungshilfsprogramm ist ein Ordner, der die Dateien enthält, die Sie zum Bereitstellen der in einem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt enthaltenen Pakete auf einem anderen Server benötigen. Das Bereitstellungshilfsprogramm wird auf dem Computer erstellt, auf dem das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt gespeichert ist.  
  
 Sie erstellen ein Paketbereitstellungshilfsprogramm für ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt, indem Sie zuerst den Erstellungsprozess konfigurieren, mit dem ein Bereitstellungshilfsprogramm erstellt wird, und anschließend das Projekt erstellen. Wenn Sie das Projekt erstellen, werden alle Pakete und Paketkonfigurationen aus dem Projekt automatisch einbezogen. Wenn Sie zusammen mit dem Projekt zusätzliche Dateien – wie z. B. eine Readme-Datei – bereitstellen möchten, müssen Sie die Dateien in den **Miscellaneous** -Ordner des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekts kopieren. Beim Erstellen des Projekts werden diese Dateien dann automatisch einbezogen.  
  
 Sie können jede Projektbereitstellung unterschiedlich konfigurieren. Bevor Sie das Projekt erstellen und das Paketbereitstellungshilfsprogramm erstellen, können Sie die Eigenschaften des Bereitstellungshilfsprogramms festlegen, um die Bereitstellung der im Projekt enthaltenen Pakete anzupassen. So können Sie z. B. angeben, ob die Paketkonfigurationen aktualisiert werden können, wenn das Projekt bereitgestellt wird. Zum Zugreifen auf die Eigenschaften eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekts klicken Sie mit der rechten Maustaste auf das Projekt, und klicken Sie anschließend auf **Eigenschaften**.  
  
 In der folgenden Tabelle sind die Eigenschaften des Bereitstellungshilfsprogramms aufgeführt.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|AllowConfigurationChange|Ein Wert, der angibt, ob Konfigurationen während der Bereitstellung aktualisiert werden können.|  
|CreateDeploymentUtility|Ein Wert, der angibt, ob beim Erstellen des Projekts ein Paketbereitstellungshilfsprogramm erstellt wird. Diese Eigenschaft muss auf **True** festgelegt sein, um ein Bereitstellungshilfsprogramm zu erstellen.|  
|DeploymentOutputPath|Der Speicherort des Bereitstellungshilfsprogramms, relativ zur Position des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekts.|  
  
 Wenn Sie ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekt erstellen, wird eine Manifestdatei mit dem Namen „\<Projektname>.SSISDeploymentManifest.xml“ erstellt und zusammen mit Kopien der Projektpakete und Paketabhängigkeiten in den „bin\Deployment“-Ordner des Projekts oder den Speicherort kopiert, der in der DeploymentOutputPath-Eigenschaft angegeben ist. Diese Manifestdatei enthält eine Auflistung der Pakete, der Paketkonfigurationen und aller sonstigen Dateien, die im Projekt enthalten sind.  
  
 Der Inhalt des Bereitstellungsordners wird bei jedem Erstellen des Projekts aktualisiert. Das bedeutet, dass alle in diesem Ordner gespeicherten Dateien, die durch den Erstellungsprozess nicht erneut in den Ordner kopiert werden, gelöscht werden. Beispielsweise werden die in den Bereitstellungsordnern gespeicherten Paketkonfigurationsdateien gelöscht.  
  
### <a name="to-create-a-package-deployment-utility"></a>So erstellen Sie ein Paketbereitstellungshilfsprogramm  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]die Projektmappe, die das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt enthält, für das ein Paketbereitstellungshilfsprogramm erstellt werden soll.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Projekt, und klicken Sie anschließend auf **Eigenschaften**.  
  
3.  Klicken Sie im Dialogfeld **\<Projektname>-Eigenschaftenseiten** auf **Bereitstellungshilfsprogramm**.  
  
4.  Wenn die Paketkonfigurationen beim Bereitstellen der Pakete aktualisiert werden sollen, legen Sie **AllowConfigurationChanges** auf **True**fest.  
  
5.  Legen Sie **CreateDeploymentUtility** auf **True**fest.  
  
6.  Aktualisieren Sie bei Bedarf den Speicherort des Bereitstellungshilfsprogramms, in dem Sie die **DeploymentOutputPath** -Eigenschaft ändern.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt, und klicken Sie anschließend auf **Erstellen**.  
  
9. Im **Ausgabe** -Fenster können Sie den Erstellungsprozess verfolgen, in dem auch Fehler bei der Erstellung angezeigt werden.  

## <a name="deploy-packages-by-using-the-deployment-utility"></a>Bereitstellen von Paketen mithilfe des Bereitstellungshilfsprogramms
  Wenn Sie ein Bereitstellungshilfsprogramm erstellt haben, um Pakete aus einem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt auf einem anderen Computer zu installieren als dem Computer, auf dem das Bereitstellungshilfsprogramm erstellt wurde, müssen Sie zuerst den Bereitstellungsordner auf den Zielcomputer kopieren.  
  
 Der Pfad des Bereitstellungsordners wird in der DeploymentOutputPath-Eigenschaft des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekts angegeben, für das Sie das Bereitstellungshilfsprogramm erstellt haben. Der Standardpfad ist bin\Deployment, relativ zum [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt. Weitere Informationen finden Sie unter [Create a Deployment Utility](../../integration-services/packages/create-a-deployment-utility.md).  
  
 Sie können zum Installieren der Pakete den Paketinstallations-Assistenten verwenden. Doppelklicken Sie zum Starten des Assistenten auf die Datei des Bereitstellungshilfsprogramms, nachdem Sie den Bereitstellungsordner auf den Server kopiert haben. Die Datei hat den Namen „\<Projektname>.SSISDeploymentManifest“ und befindet sich im Bereitstellungsordner des Zielcomputers.  
  
> [!NOTE]  
>  Abhängig von der Version des Pakets, das Sie bereitstellen, könnte ein Fehler auftreten, wenn Sie verschiedene Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parallel installiert haben. Dieser Fehler kann auftreten, da die Dateinamenerweiterung ".SSISDeploymentManifest" für alle Versionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]identisch ist. Durch Doppelklicken auf die Datei wird das Installationsprogramm („dtsinstall.exe“) für die zuletzt installierte Version von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]aufgerufen, die möglicherweise nicht der Version der Datei des Bereitstellungs-Hilfsprogramms entspricht. Um dieses Problem zu umgehen, führen Sie die richtige Version von "dtsinstall.exe" in der Befehlszeile aus, und stellen Sie den Pfad der Datei des BereitstellungsHilfsprogramms bereit.  
  
 Der Paketinstallations-Assistent führt Sie schrittweise durch das Installieren der Pakete im Dateisystem oder in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Es gibt folgende Möglichkeiten, um die Installation zu konfigurieren:  
  
-   Auswählen des Speichertyps und des Speicherorts zum Installieren der Pakete.  
  
-   Auswählen des Speicherorts zum Installieren von Paketabhängigkeiten.  
  
-   Überprüfen der Pakete nach dem Installieren der Pakete auf dem Zielserver.  
  
 Die dateibasierten Abhängigkeiten für Pakete werden immer im Dateisystem installiert. Wenn Sie ein Paket im Dateisystem installieren, werden die Abhängigkeiten im selben Ordner installiert, den Sie für das Paket angeben. Wenn Sie ein Paket in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installieren, können Sie den Ordner angeben, in dem die dateibasierten Abhängigkeiten gespeichert werden sollen.  
  
 Wenn das Paket Konfigurationen enthält, die zum Verwenden auf dem Zielcomputer geändert werden sollen, können Sie die Werte der Eigenschaften mit diesem Assistenten aktualisieren.  
  
 Außer der Installation von Paketen mit dem Paketinstallations-Assistenten können Sie Pakete mit dem Eingabeaufforderungs-Hilfsprogramm **dtutil** kopieren und verschieben. Weitere Informationen finden Sie unter [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
### <a name="to-deploy-packages-to-an-instance-of-sql-server"></a>So stellen Sie Pakete in einer Instanz von SQL Server bereit  
  
1.  Öffnen Sie den Bereitstellungsordner auf dem Zielcomputer.  
  
2.  Doppelklicken Sie auf die Manifestdatei „\<Projektname>.SSISDeploymentManifest“, um den Paketinstallations-Assistenten zu starten.  
  
3.  Wählen Sie auf der Seite **SSIS-Pakete bereitstellen** die Option **Bereitstellung in SQL Server** .  
  
4.  Wählen Sie optional **Pakete nach der Installation überprüfen** , wenn Sie die Pakete nach der Installation auf dem Zielserver überprüfen lassen möchten.  
  
5.  Geben Sie auf der Seite **Zielserver mit SQL Server angeben** die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, in der die Pakete installiert werden sollen, und wählen Sie einen Authentifizierungsmodus aus. Wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung auswählen, müssen Sie einen Benutzernamen und ein Kennwort bereitstellen.  
  
6.  Geben Sie auf der Seite **Installationsordner auswählen** den Dateisystemordner für die zu installierenden Paketabhängigkeiten an.  
  
7.  Wenn das Paket Konfigurationen enthält, können Sie diese bearbeiten, indem Sie die Werte der **Wert** -Liste auf der Seite Pakete konfigurieren aktualisieren.  
  
8.  Wenn Sie ausgewählt haben, dass Pakete nach der Installation überprüft werden sollen, zeigen Sie nun die Überprüfungsergebnisse der bereitgestellten Pakete an.  

## <a name="redeployment-of-packages"></a>Erneutes Bereitstellen von Paketen
  Nachdem ein Projekt bereitgestellt wurde, kann es erforderlich werden, die Paketfunktionalität zu aktualisieren oder zu erweitern und anschließend das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt, das die aktualisierten Pakete enthält, erneut bereitzustellen. Im Zusammenhang mit dem erneuten Bereitstellen von Paketen sollten Sie die zum Bereitstellungshilfsprogramm gehörenden Konfigurationseigenschaften überprüfen. Beispielsweise können Sie festlegen, dass nach dem erneuten Bereitstellen des Pakets keine Konfigurationsänderungen zulässig sein sollen.  
  
### <a name="process-for-redeployment"></a>Prozess für die erneute Bereitstellung  
 Nachdem Sie die Pakete aktualisiert haben, erstellen Sie das Projekt neu. Kopieren Sie dann den Bereitstellungsordner zum Zielcomputer, und führen Sie dann den Paketinstallations-Assistenten erneut aus.  
  
 Wenn Sie nur wenige Pakete aus dem Projekt aktualisieren, muss eventuell nicht das gesamte Projekt erneut bereitgestellt werden. Um nur wenige Pakete bereitzustellen, können Sie ein neues [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt erstellen, diesem neuen Projekt die aktualisierten Pakete hinzufügen und dann das Projekt erstellen und bereitstellen. Die Paketkonfigurationen werden automatisch zusammen mit dem Paket kopiert, wenn Sie das Paket einem anderen Projekt hinzufügen.  

## <a name="package-installation-wizard-ui-reference"></a>Referenz zur Benutzeroberfläche des Paketinstallations-Assistenten
  Mit dem **Paketinstallations-Assistenten** können Sie ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt einschließlich der enthaltenen Pakete, verschiedenen Dateien und Paketabhängigkeiten bereitstellen.  
  
 Bevor Sie Pakete bereitstellen, können Sie Konfigurationen erstellen und diese dann mit den Paketen bereitstellen. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendet Konfigurationen, um Eigenschaften von Paketen und Paketobjekten zur Laufzeit dynamisch zu aktualisieren. Beispielsweise kann die Verbindungszeichenfolge einer OLE DB-Verbindung zur Laufzeit dynamisch festgelegt werden, indem Sie eine Konfiguration erstellen, die der Eigenschaft, die die Verbindungszeichenfolge enthält, einen Wert zuordnet.  
  
 Der Paketinstallations-Assistent kann erst ausgeführt werden, nachdem Sie ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt und ein Bereitstellungshilfsprogramm erstellt haben. Weitere Informationen finden Sie unter [Deploy Packages by Using the Deployment Utility](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md).  
  
 In den folgenden Abschnitten werden Seiten des Assistenten beschrieben.  
  
### <a name="welcome-to-the-package-installation-wizard-page"></a>Willkommen auf der Seite des Paketinstallations-Assistenten.  
 Mit dem **Paketinstallations-Assistenten** können Sie ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt bereitstellen, für das Sie ein Paketbereitstellungshilfsprogramm erstellt haben.  
  
 **Diese Anfangsseite nicht mehr anzeigen**  
 Wählen Sie diese Option aus, um die Startseite bei der nächsten Ausführung des Assistenten auszulassen.  
  
 **Weiter**  
 Mit dieser Option können Sie zur nächsten Seite des Assistenten wechseln.  
  
 **Fertig stellen**  
 Springen Sie zur Seite <ui>Fertigstellen des Assistenten</ui>. Verwenden Sie diese Option, wenn Sie die Assistentenseiten noch einmal mithilfe der Zurück-Option durchgegangen sind, um die ausgewählten Optionen zu überprüfen, und jetzt mit der Auswahl zufrieden sind.  
  
### <a name="configure-packages-page"></a>Seite "Pakete konfigurieren"  
 Mithilfe der Seite **Pakete konfigurieren** können Sie Paketkonfigurationen bearbeiten.  
  
#### <a name="options"></a>enthalten  
 **Konfigurationsdatei**  
 Bearbeiten Sie die Inhalte einer Konfigurationsdatei, indem Sie die Datei aus der Liste auswählen.  
  
 **Related Topics:** [Create Package Configurations](../../integration-services/packages/create-package-configurations.md)  
  
 **Pfad**  
 Zeigen Sie den Pfad der zu konfigurierenden Eigenschaft an.  
  
 **Typ**  
 Zeigen Sie den Datentyp der Eigenschaft an.  
  
 **Wert**  
 Geben Sie den Wert der Konfiguration an.  
  
 **Weiter**  
 Mit dieser Option können Sie zur nächsten Seite des Assistenten wechseln.  
  
 **Fertig stellen**  
 Springen Sie zur Seite <ui>Fertigstellen des Assistenten</ui>. Verwenden Sie diese Option, wenn Sie die Assistentenseiten noch einmal mithilfe der Zurück-Option durchgegangen sind, um die ausgewählten Optionen zu überprüfen, und jetzt mit der Auswahl zufrieden sind.  
  
### <a name="confirm-installation-page"></a>Seite "Installation bestätigen"  
 Mithilfe der Seite **Installation bestätigen** können Sie die Installation von Paketen starten und den Status sowie die Informationen anzeigen, die der Assistent zum Installieren von Dateien aus dem angegebenen Projekt verwendet.  
  
 **Weiter**  
 Installiert die Pakete und die dazugehörigen Abhängigkeiten und wechselt nach Abschluss der Installation zur nächsten Seite des Assistenten.  
  
 **Status**  
 Zeigt den Fortschritt der Paketinstallation an.  
  
 **Fertig stellen**  
 Wechseln Sie zur Seite <ui>Fertigstellen des Assistenten</ui>. Verwenden Sie diese Option, wenn Sie die Assistentenseiten noch einmal mithilfe der Zurück-Option durchgegangen sind, um die ausgewählten Optionen zu überprüfen, und jetzt mit der Auswahl zufrieden sind.  
  
### <a name="deploy-ssis-packages-page"></a>Seit "SSIS-Paket bereitstellen"  
 Mithilfe der Seite **SSIS-Pakete bereitstellen** können Sie angeben, an welcher Stelle [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete und ihre Abhängigkeiten installiert werden sollen.  
  
#### <a name="options"></a>enthalten  
 **Bereitstellung im Dateisystem**  
 Stellen Sie Pakete und Abhängigkeiten in einem bestimmten Ordner im Dateisystem bereit.  
  
 **Bereitstellung in SQL Server**  
 Stellen Sie Pakete und Abhängigkeiten in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]bereit. Verwenden Sie diese Option, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Pakete zwischen Servern freigibt. Bestehende Paketabhängigkeiten werden im angegebenen Ordner im Dateisystem installiert.  
  
 **Pakete nach der Installation überprüfen**  
 Geben Sie an, ob Pakete nach der Installation überprüft werden sollen.  
  
 **Weiter**  
 Mit dieser Option können Sie zur nächsten Seite des Assistenten wechseln.  
  
 **Fertig stellen**  
 Springen Sie zur Seite <ui>Fertigstellen des Assistenten</ui>. Verwenden Sie diese Option, wenn Sie die Assistentenseiten noch einmal mithilfe der Zurück-Option durchgegangen sind, um die ausgewählten Optionen zu überprüfen, und jetzt mit der Auswahl zufrieden sind.  
  
### <a name="packages-validation-page"></a>Seite "Paketüberprüfung"  
 Auf der Seite **Paketüberprüfung** können Sie den Fortschritt und die Ergebnisse der Paketüberprüfung anzeigen.  
  
 **Weiter**  
 Mit dieser Option können Sie zur nächsten Seite des Assistenten wechseln.  
  
### <a name="select-installation-folder-page"></a>Seite "Installationsordner auswählen"  
 Mithilfe der Seite **Installationsordner auswählen** können Sie den Dateisystemordner angeben, in dem die Pakete und deren Abhängigkeiten installiert werden sollen.  
  
#### <a name="options"></a>enthalten  
 **Ordner**  
 Geben Sie den Pfad und den Ordner an, in den das Paket und seine Abhängigkeiten kopiert werden sollen.  
  
 **Durchsuchen**  
 Suchen Sie den Zielordner im Dialogfeld **Ordner suchen** .  
  
 **Weiter**  
 Mit dieser Option können Sie zur nächsten Seite des Assistenten wechseln.  
  
 **Fertig stellen**  
 Springen Sie zur Seite <ui>Fertigstellen des Assistenten</ui>. Verwenden Sie diese Option, wenn Sie die Assistentenseiten noch einmal mithilfe der Zurück-Option durchgegangen sind, um die ausgewählten Optionen zu überprüfen, und jetzt mit der Auswahl zufrieden sind.  
  
### <a name="specify-target-sql-server-page"></a>Seite "Zielserver mit SQL Server angeben"  
 Auf der Seite **Zielserver mit SQL Server angeben** können Sie Optionen zur Bereitstellung des Pakets für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz angeben.  
  
#### <a name="options"></a>enthalten  
 **Servername**  
 Geben Sie den Namen des Servers an, auf dem die Pakete bereitgestellt werden sollen.  
  
 **Windows-Authentifizierung verwenden**  
 Geben Sie an, ob für die Anmeldung beim Server die Windows-Authentifizierung verwendet werden soll. Im Sinne einer größeren Sicherheit wird die Windows-Authentifizierung empfohlen.  
  
 **SQL Server-Authentifizierung verwenden**  
 Geben Sie an, ob vom Paket für die Anmeldung beim Server die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwendet werden soll. Wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwenden, müssen Sie einen Benutzernamen und ein Kennwort angeben.  
  
 **Benutzername**  
 Geben Sie einen Benutzernamen an.  
  
 **Kennwort**  
 Geben Sie ein Kennwort an.  
  
 **Paketpfad**  
 Geben Sie den Namen des logischen Ordners an, oder geben Sie / für den Standardordner ein.  
  
 Klicken Sie zum Auswählen des Ordners im Dialogfeld **SSIS-Paket** auf die Schaltfläche zum Durchsuchen (...). Allerdings bietet das Dialogfeld keine Möglichkeit, den Standardordner auszuwählen. Wenn Sie den Standardordner verwenden möchten, müssen Sie im Textfeld / eingeben.  
  
> [!NOTE]  
>  Wenn Sie keinen gültigen Paketpfad eingeben, wird die folgende Fehlermeldung angezeigt: "Mindestens ein Argument ist ungültig."  
  
 **Serverspeicher für die Verschlüsselung verwenden**  
 Wählen Sie diese Option aus, um die Pakete mithilfe von Sicherheitsfunktionen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] zu sichern.  
  
 **Weiter**  
 Mit dieser Option können Sie zur nächsten Seite des Assistenten wechseln.  
  
 **Fertig stellen**  
 Springen Sie zur Seite <ui>Fertigstellen des Assistenten</ui>. Verwenden Sie diese Option, wenn Sie die Assistentenseiten noch einmal mithilfe der Zurück-Option durchgegangen sind, um die ausgewählten Optionen zu überprüfen, und jetzt mit der Auswahl zufrieden sind.  
  
### <a name="finish-the-package-installation-page"></a>Seite "Fertigstellen des Assistenten"  
 Auf der Seite **Fertigstellen des Assistenten** können Sie eine Übersicht über die Ergebnisse der Paketinstallation anzeigen. Die Seite enthält verschiedene Detailinformationen, z. B. den Namen des bereitgestellten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekts, die Namen der installierten Pakete, die Konfigurationsdateien und den Installationsspeicherort.  
  
 **Fertig stellen**  
 Durch Klicken auf **Fertig stellen**beenden Sie den Assistenten.  

