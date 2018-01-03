---
title: SSIS Paketupgrade-Assistent (F1-Hilfe) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- sql13.is.upgradewizard.ssisupgradewizard.f1
- sql13.is.upgradewizard.selectsourcelocation.f1
- sql13.is.upgradewizard.selectdestinationlocation.f1
- sql13.is.upgradewizard.selectpackagemgtoptions.f1
- sql13.is.upgradewizard.selectpackages.f1
- sql13.is.upgradewizard.completewizard.f1
- sql13.is.upgradewizard.upgradingpackage.f1
ms.assetid: 7fe886ff-1ea5-48d5-9d20-d5da36dd1cd7
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 59869c0fdcb73fc30ee9bc763e8665f05f71df90
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="ssis-package-upgrade-wizard-f1-help"></a>SSIS Paketupgrade-Assistent (F1-Hilfe)
  Verwenden Sie den SSIS-Paketupgrade-Assistenten, um ein Upgrade für die mit früheren Versionen erstellten [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Pakete auf das für die aktuelle Version von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]verwendete Paketformat durchzuführen.  
  
 **So führen Sie den SSIS Paketupgrade-Assistenten aus**  
  
-   [Aktualisieren von Integration Services-Paketen mit dem SSIS-Paketupgrade-Assistenten](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  

## <a name="ssis-upgrade-wizard"></a>SSIS-Paketupgrade-Assistent
  
### <a name="options"></a>Tastatur  
 **Diese Seite nicht mehr anzeigen.**  
 Lassen Sie die Willkommensseite beim nächsten Öffnen des Assistenten aus.  
 
## <a name="select-source-location-page"></a>Seite „Quellspeicherort auswählen“
 Mithilfe der Seite **Quellspeicherort auswählen** geben Sie die Quelle an, aus der Pakete aktualisiert werden sollen.  
  
> [!NOTE]  
>  Diese Seite ist nur verfügbar, wenn Sie den [!INCLUDE[ssIS](../includes/ssis-md.md)] -Paketupgrade-Assistenten in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] oder an der Eingabeaufforderung ausführen.  
  
### <a name="static-options"></a>Statische Optionen  
 **Paketquelle**  
 Wählen Sie den Speicherort aus, der die zu aktualisierenden Pakete enthält. Für diese Option sind die in der folgenden Tabelle aufgeführten Werte verfügbar.  
  
|value|Description|  
|-----------|-----------------|  
|**Dateisystem**|Gibt an, dass sich die zu aktualisierenden Pakete in einem Ordner auf dem lokalen Computer befinden.<br /><br /> Die ursprünglichen Pakete müssen im Dateisystem gespeichert sein, damit der Assistent die ursprünglichen Pakete vor deren Upgrade sichern kann. Weitere Informationen finden Sie in den Vorgehensweisen zu diesem Thema.|  
|**SSIS-Paketspeicher**|Gibt an, dass sich die zu aktualisierenden Pakete im Paketspeicher befinden. Der Paketspeicher besteht aus dem Satz von Dateisystemordnern, die vom [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Dienst verwaltet werden. Weitere Informationen finden Sie unter [Paketverwaltung &#40;SSIS-Dienst&#41;](../integration-services/service/package-management-ssis-service.md).<br /><br /> Bei Auswahl dieses Werts werden die entsprechenden dynamischen Optionen **Paketquelle** angezeigt.|  
|**Microsoft SQL Server**|Gibt an, dass die zu aktualisierenden Pakete aus einer vorhandenen Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]stammen.<br /><br /> Bei Auswahl dieses Werts werden die entsprechenden dynamischen Optionen **Paketquelle** angezeigt.|  
  
 **Ordner**  
 Geben Sie den Namen eines Ordners ein, in dem die zu aktualisierenden Pakete enthalten sind, oder klicken Sie auf **Durchsuchen** , und suchen Sie den Ordner.  
  
 **Durchsuchen**  
 Suchen Sie nach dem Ordner, der die zu aktualisierenden Pakete enthält.  
  
### <a name="package-source-dynamic-options"></a>Dynamische Paketquellenoptionen  
  
#### <a name="package-source--ssis-package-store"></a>Paketquelle = SSIS-Paketspeicher  
 **Server**  
 Geben Sie den Namen des Servers ein, auf dem die zu aktualisierenden Pakete gespeichert sind, oder wählen Sie diesen Server aus der Liste aus.  
  
#### <a name="package-source--microsoft-sql-server"></a>Paketquelle = Microsoft SQL Server  
 **Server**  
 Geben Sie den Namen des Servers ein, auf dem die zu aktualisierenden Pakete gespeichert sind, oder wählen Sie diesen Server aus der Liste aus.  
  
 **Windows-Authentifizierung verwenden**  
 Wählen Sie diese Option aus, um für die Herstellung einer Verbindung mit dem Server die Windows-Authentifizierung zu verwenden.  
  
 **SQL Server-Authentifizierung verwenden**  
 Wählen Sie diese Option aus, um für die Herstellung einer Verbindung mit dem Server die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung zu verwenden. Wenn Sie die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung verwenden, müssen Sie einen Benutzernamen und ein Kennwort angeben.  
  
 **User name**  
 Geben Sie den Benutzernamen ein, den die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung verwendet, um eine Verbindung mit dem Server herzustellen.  
  
 **Kennwort**  
 Geben Sie das Kennwort ein, das die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung verwendet, um eine Verbindung mit dem Server herzustellen.  
 
## <a name="select-destination-location-page"></a>Seite „Zielspeicherort auswählen“
 Auf der Seite **Zielspeicherort auswählen** können Sie das Ziel angeben, an dem die aktualisierten Pakete gespeichert werden sollen.  
  
> [!NOTE]  
>  Diese Seite ist nur verfügbar, wenn Sie den [!INCLUDE[ssIS](../includes/ssis-md.md)] -Paketupgrade-Assistenten in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] oder an der Eingabeaufforderung ausführen.  
 
### <a name="static-options"></a>Statische Optionen  
 **An Quellspeicherort speichern**  
 Speichert die aktualisierten Pakete an demselben Speicherort, der auf der Seite **Quellspeicherort auswählen** des Assistenten festgelegt wurde.  
  
 Wenn die ursprünglichen Pakete im Dateisystem gespeichert sind und der Assistent diese Pakete sichern soll, wählen Sie die Option **An Quellspeicherort speichern** aus. Weitere Informationen finden Sie unter [Aktualisieren von Integration Services-Paketen mit dem SSIS Paketupgrade-Assistenten](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md).  
  
 **Neuen Zielspeicherort auswählen**  
 Speichert die aktualisierten Pakete an dem Zielspeicherort, der auf dieser Seite angegeben ist.  
  
 **Paketquelle**  
 Gibt an, wo die Upgradepakete gespeichert werden sollen. Für diese Option sind die in der folgenden Tabelle aufgeführten Werte verfügbar.  
  
|value|Description|  
|-----------|-----------------|  
|**Dateisystem**|Gibt an, dass die aktualisierten Pakete in einem Ordner auf dem lokalen Computer gespeichert werden sollen.|  
|**SSIS-Paketspeicher**|Gibt an, dass die aktualisierten Pakete im Integration Services-Paketspeicher gespeichert werden sollen. Der Paketspeicher besteht aus dem Satz von Dateisystemordnern, die vom Integration Services-Dienst verwaltet werden. Weitere Informationen finden Sie unter [Paketverwaltung &#40;SSIS-Dienst&#41;](../integration-services/service/package-management-ssis-service.md).<br /><br /> Bei Auswahl dieses Werts werden die entsprechenden dynamischen Optionen **Paketquelle** angezeigt.|  
|**Microsoft SQL Server**|Gibt an, dass die aktualisierten Pakete in einer vorhandenen Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]gespeichert werden sollen.<br /><br /> Bei Auswahl dieses Werts werden die entsprechenden dynamischen Optionen **Paketquelle** angezeigt.|  
  
 **Ordner**  
 Geben Sie den Namen eines Ordners ein, in dem die aktualisierten Pakete gespeichert werden, oder klicken Sie auf **Durchsuchen** , und suchen Sie den Ordner.  
  
 **Durchsuchen**  
 Suchen Sie nach dem Ordner, in dem die aktualisierten Pakete gespeichert werden sollen.  
  
### <a name="package-source-dynamic-options"></a>Dynamische Paketquellenoptionen  
  
#### <a name="package-source--ssis-package-store"></a>Paketquelle = SSIS-Paketspeicher  
 **Server**  
 Geben Sie den Namen des Servers ein, auf dem die Upgradepakete gespeichert werden sollen, oder wählen Sie einen Server aus der Liste aus.  
  
#### <a name="package-source--microsoft-sql-server"></a>Paketquelle = Microsoft SQL Server  
 **Server**  
 Geben Sie den Namen des Servers ein, auf dem die Upgradepakete gespeichert werden sollen, oder wählen Sie diesen Server aus der Liste aus.  
  
 **Windows-Authentifizierung verwenden**  
 Wählen Sie diese Option aus, um für die Herstellung einer Verbindung mit dem Server die Windows-Authentifizierung zu verwenden.  
  
 **SQL Server-Authentifizierung verwenden**  
 Wählen Sie diese Option aus, um für die Herstellung einer Verbindung mit dem Server die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung zu verwenden. Wenn Sie die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung verwenden, müssen Sie einen Benutzernamen und ein Kennwort angeben.  
  
 **User name**  
 Geben Sie den Benutzernamen ein, der bei der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung verwendet werden soll, um eine Verbindung mit dem Server herzustellen.  
  
 **Kennwort**  
 Geben Sie das Kennwort ein, das bei der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung verwendet werden soll, um eine Verbindung mit dem Server herzustellen.  
 
## <a name="select-package-management-options-page"></a>Seite „Paketverwaltungsoptionen auswählen“
  Verwenden Sie die Seite **Paketverwaltungsoptionen auswählen** , um Optionen für Paketupgrades anzugeben.  
  
 **So führen Sie den SSIS Paketupgrade-Assistenten aus**  
  
-   [Aktualisieren von Integration Services-Paketen mit dem SSIS-Paketupgrade-Assistenten](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
### <a name="options"></a>Tastatur  
 **Verbindungszeichenfolgen zum Verwenden neuer Anbieternamen aktualisieren**  
 Aktualisieren Sie die Verbindungszeichenfolgen, um für die aktuelle Version von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]die Namen für die folgenden Anbieter zu verwenden:  
  
-   OLE DB-Anbieter für [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 Der [!INCLUDE[ssIS](../includes/ssis-md.md)] -Paketupgrade-Assistent aktualisiert nur Verbindungszeichenfolgen, die in Verbindungs-Managern gespeichert sind. Der Assistent aktualisiert keine Verbindungszeichenfolgen, die dynamisch mithilfe der [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Ausdruckssprache oder mithilfe von Code in einem Skripttask erstellt wurden.  
  
 **Upgradepakete überprüfen**  
 Überprüfen Sie die Upgradepakete, und speichern Sie nur die Upgradepakete, die die Überprüfung bestehen.  
  
 Wenn Sie diese Option nicht aktivieren, überprüft der Assistent keine Upgradepakete. Deshalb speichert der Assistent alle Upgradepakete, unabhängig davon, ob die Pakete gültig sind oder nicht. Der Assistent speichert Upgradepakete unter dem Ziel, das auf der Seite **Zielspeicherort auswählen** des Assistenten angegeben ist.  
  
 Die Überprüfung verlängert die Dauer des Upgradevorgangs. Es wird empfohlen, diese Option für große Pakete, die voraussichtlich erfolgreich aktualisiert werden, nicht zu aktivieren.  
  
 **Neue Paket-IDs erstellen**  
 Erstellen Sie neue Paket-IDs für die Upgradepakete.  
  
 **Upgradeprozess bei fehlerhaftem Paketupgrade fortsetzen**  
 Legen Sie fest, dass der [!INCLUDE[ssIS](../includes/ssis-md.md)] -Paketupgrade-Assistent mit dem Upgrade der restlichen Pakete fortfährt, wenn ein Paket nicht aktualisiert werden kann.  
  
 **Paketnamenskonflikte**  
 Geben Sie an, wie der Assistent Pakete behandeln soll, die denselben Namen haben. Für diese Option sind die in der folgenden Tabelle aufgeführten Werte verfügbar.  
  
 **Vorhandene Paketdateien überschreiben**  
 Ersetzt das vorhandene Paket durch das Upgradepaket desselben Namens.  
  
 **Zum Aktualisieren von Paketnamen numerische Suffixe hinzufügen**  
 Fügt dem Namen des Upgradepakets ein numerisches Suffix hinzu.  
  
 **Kein Upgrade für Pakete durchführen**  
 Unterbricht das Upgrade der Pakete und zeigt einen Fehler an, wenn Sie den Assistenten abschließen.  
  
 Diese Optionen sind nicht verfügbar, wenn Sie die Option **An Quellspeicherort speichern** auf der Seite **Zielspeicherort auswählen** des Assistenten auswählen.  
  
 **Konfigurationen ignorieren**  
 Lädt keine Paketkonfigurationen während des Paketupgrades. Durch Auswahl dieser Option wird weniger Zeit für das Paketupgrade benötigt.  
  
 **Originalpakete sichern**  
 Lassen Sie den Assistenten die Originalpakete in einem **SSISBackupFolder** -Ordner sichern. Der Assistent erstellt den **SSISBackupFolder** -Ordner als Unterordner des Ordners, der die Originalpakete und die Upgradepakete enthält.  
  
> [!NOTE]  
>  Diese Option ist nur verfügbar, wenn Sie festlegen, dass die Originalpakete und die Upgradepakete im Dateisystem und im selben Ordner gespeichert werden.  

## <a name="select-packages-page"></a>Seite „Pakete auswählen“
  Verwenden Sie die Seite **Pakete auswählen** , um die Pakete für das Upgrade auszuwählen. Auf dieser Seite werden die Pakete aufgelistet, die am auf der Seite **Quellspeicherort auswählen** des Assistenten ausgewählten Speicherort gespeichert sind.  
  
### <a name="options"></a>Tastatur  
 **Vorhandener Paketname**  
 Wählen Sie ein oder mehrere Pakete für das Upgrade aus.  
  
 **Upgradepaketname**  
 Geben Sie den Namen des Zielpakets an, oder verwenden Sie den Standardnamen, den der Assistent bereitstellt.  
  
> [!NOTE]  
>  Sie können den Zielpaketnamen auch noch ändern, nachdem Sie das Paket aktualisiert haben. Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] oder [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]das aktualisierte Paket, und ändern Sie den Paketnamen.  
  
 **Kennwort**  
 Geben Sie das Kennwort an, das zur Entschlüsselung der ausgewählten Upgradepakete verwendet wird.  
  
 **Auf Auswahl anwenden**  
 Wenden Sie das festgelegte Kennwort an, um die ausgewählten Upgradepakete zu entschlüsseln.  
 
## <a name="complete-the-wizard-page"></a>Seite „Assistenten abschließen“
  Verwenden Sie die Seite **Assistenten abschließen** , um die Paketupgradeoptionen zu überprüfen und zu bestätigen, die Sie ausgewählt haben. Dies ist die letzte Seite des Assistenten, auf der Sie zurückgehen und die Optionen für diese Sitzung des Assistenten ändern können.  
  
### <a name="options"></a>Tastatur  
 **Zusammenfassungsoptionen**  
 Überprüfen Sie die Upgradeoptionen, die Sie im Assistenten ausgewählt haben. Um Optionen zu ändern, klicken Sie auf **Zurück** , um zu den vorherigen Assistentenseiten zurückzukehren.
 
## <a name="upgrading-the-packages-page"></a>Seite „Pakete werden aktualisiert“
  Verwenden Sie die Seite **Pakete werden aktualisiert** , um den Status der Paketaktualisierung anzuzeigen und um den Aktualisierungsprozess unterbrechen. Der [!INCLUDE[ssIS](../includes/ssis-md.md)] Paketaktualisierungs-Assistent aktualisiert die ausgewählten Pakete nacheinander.  
  
### <a name="options"></a>Tastatur  
 **Bereich „Meldung“**  
 Zeigt während der Aktualisierung Statusmeldungen und Zusammenfassungsinformationen an.  
  
 **Aktion**  
 Zeigen Sie die Aktionen in der Aktualisierung an.  
  
 **Status**  
 Zeigen Sie das Ergebnis der einzelnen Aktionen an.  
  
 **MessageBox**  
 Zeigen Sie die Fehlermeldungen an, die die einzelnen Aktionen generieren.  
  
 **Beenden**  
 Beenden Sie die Paketaktualisierung.  
  
 **Bericht**  
 Wählen Sie aus, wie Sie mit dem Bericht, der die Ergebnisse der Paketaktualisierung enthält, verfahren möchten:  
  
-   Den Bericht online anzeigen  
  
-   Den Bericht in einer Datei speichern  
  
-   Den Bericht in die Zwischenablage speichern.  
  
-   Den Bericht als E-Mail-Nachricht versenden.  

## <a name="view-upgraded-packages"></a>Anzeigen von Paketen mit durchgeführtem Upgrade
### <a name="view-upgraded-packages-that-were-saved-to-a-sql-server-database-or-to-the-package-store"></a>Anzeigen von Paketen mit durchgeführtem Upgrade, die in einer SQL Server-Datenbank oder dem Paketspeicher gespeichert wurden
  
Stellen Sie in [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]im Objekt-Explorer eine Verbindung mit der lokalen Instanz von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]her, und erweitern Sie dann den Knoten **Gespeicherte Pakete** , um die aktualisierten Pakete anzuzeigen.  
  
### <a name="view-upgraded-packages-that-were-upgraded-from-sql-server-data-tools"></a>Anzeigen von Paketen mit in SQL Server Data Tools durchgeführtem Upgrade  
  
Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]im Projektmappen-Explorer das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt, und erweitern Sie dann den Knoten **SSIS-Pakete** , um die aktualisierten Pakete anzuzeigen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Aktualisieren von Integration Services-Paketen](../integration-services/install-windows/upgrade-integration-services-packages.md)  
  
  
