---
title: "Installieren oder Deinstallieren des PowerPivot für SharePoint Add-in (SharePoint 2016) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 34dd07b8-d59d-49ce-bad0-74f40e4db0b8
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1dbd22c1c09de66200cda7300f34666ea453777a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016"></a>Installieren oder Deinstallieren des Power Pivot für SharePoint-Add-In (SharePoint 2016)
  [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] ist eine Sammlung von Anwendungsserverkomponenten und Back-End-Diensten, die [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Datenzugriff in einer [!INCLUDE[SPS2016](../../../includes/sps2016-md.md)] -Farm bereitstellen. Das [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint-Add-In (**spPowerpivot16.msi**) ist ein Installationspaket, mit dem die Anwendungsserverkomponenten installiert werden.  
  
 **Hinweis:** In diesem Thema wird das Installieren der [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]-Lösungsdateien sowie des [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für SharePoint 2016-Konfigurationstools beschrieben. Nach der Installation finden Sie im folgenden Thema Informationen zum Konfigurationstool und zusätzlichen Funktionen: [Konfigurieren von PowerPivot und Bereitstellen von Lösungen &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md).  
  
 Informationen zum Herunterladen von **spPowerPivot16.msi**finden Sie unter [Microsoft® SQL Server® 2016 Power Pivot® für Microsoft SharePoint®](https://www.microsoft.com/download/details.aspx?id=52675).  
  
 **In diesem Thema:**  
  
-   [Hintergrund](#bkmk_background)  
  
-   [Installationsort der Datei „spPowerPivot16.msi“](#bkmk_where_to_install)  
  
-   [Anforderungen und erforderliche Komponenten](#bkmk_prereq)  
  
-   [Installieren von PowerPivot für SharePoint](#bkmk_install)  
  
-   [Bereitstellen der SharePoint-Lösungsdateien mit Power Pivot für SharePoint 2016-Konfigurationstool](#bkmk_deploy_solution)  
  
-   [Deinstallieren oder Reparieren des Add-Ins](#bkmk_remove_addin)  
  

**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2016 
  
##  <a name="bkmk_background"></a> Hintergrund  
  
-   **Anwendungsserver:** [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Funktionen in SharePoint 2016 umfassen die Verwendung von Arbeitsmappen als Datenquelle, die planmäßige Datenaktualisierung und das [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Management-Dashboard.  
  
     [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]ist eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Installer-Paket (**"sppowerpivot16.msi"**), die Analysis Services-Clientbibliotheken bereitstellt und Kopien [!INCLUDE[ssGeminiShort2017](../../../includes/ssgeminishort2017-md.md)] -Installationsdateien auf dem Computer. [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Funktionen in SharePoint werden vom Installationsprogramm nicht bereitgestellt oder konfiguriert. Die folgenden Komponenten sind standardmäßig installiert:  
  
    -   [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]. Diese Komponente enthält PowerShell-Skripts („.ps1“-Dateien), SharePoint-Lösungspakete (.wsp) und das [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] -Konfigurationstool zum Bereitstellen von [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in einer SharePoint 2016-Farm.  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB-Anbieter für Analysis Services (MSOLAP)  
  
    -   ADOMD.NET-Datenanbieter.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Analysis Management Objects.  
  
-   **Back-End-Dienste:** Wenn Sie [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] für Excel verwenden, um Arbeitsmappen mit analytischen Daten zu erstellen, müssen Sie Office Online Server mit einem BI-Server konfigurieren, auf dem [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] im [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Modus ausgeführt wird, um in einer Serverumgebung auf die betreffenden Daten zuzugreifen. Sie können SQL Server-Setup auf einem Computer ausführen, auf dem SharePoint Server 2016 installiert ist, oder auf einem anderen Computer, der keine SharePoint-Software enthält. Zwischen Analysis Services und SharePoint bestehen keine Abhängigkeiten.  
  
     Weitere Informationen zum Installieren, Deinstallieren und Konfigurieren der Back-End-Dienste finden Sie unter:  
  
    -   [Installieren von Analysis Services im PowerPivot-Modus](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
    -   [Deinstallieren von Power Pivot für SharePoint](../../../sql-server/install/uninstall-power-pivot-for-sharepoint.md)  
  
##  <a name="bkmk_where_to_install"></a> Installationsort der Datei „spPowerPivot16.msi“  
 Als bewährte Methode wird empfohlen, **spPowerPivot16.msi** aus Konsistenzgründen auf allen Servern in der SharePoint-Farm zu installieren, einschließlich der Anwendungsserver und Web-Front-End-Server. Das Installationspaket schließt die Analysis Services-Datenanbieter sowie das [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] -Konfigurationstool ein. Sie können die Installation von **spPowerPivot16.msi** anpassen, indem Sie bei der Installation einzelne Komponenten ausschließen.  
  
 **Datenanbieter:** Mehrere SharePoint- und SQL Server-Technologien verwenden die Analysis Services-Datenanbieter, PerformancePoint Services und Power View. Durch die Installation von **spPowerPivot16.msi** auf allen SharePoint-Servern wird sichergestellt, dass der vollständige Satz der Analysis Services-Datenanbieter und [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Konnektivität durchgehend in der Farm verfügbar ist.  
  
> [!NOTE]  
>  Sie müssen die Analysis Services-Datenanbieter mit **spPowerPivot16.msi**auf einem SharePoint 2016-Server installieren. Andere im [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Feature Pack verfügbaren Installationspakete werden nicht unterstützt, da diese Pakete keine SharePoint 2016-Unterstützungsdateien enthalten, die von den Datenanbietern in dieser Umgebung benötigt werden.  
  
 **Konfigurationstool:** Das [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] -Konfigurationstool ist auf nur einem der SharePoint-Server erforderlich. Als bewährte Methode in Multiserverfarmen empfiehlt es sich, das Konfigurationstool auf mindestens zwei Servern zu installieren, damit Sie Zugriff auf das Konfigurationstool haben, wenn einer der beiden Server offline ist.  
  
##  <a name="bkmk_prereq"></a> Anforderungen und erforderliche Komponenten  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SharePoint Server 2016  
  
-   In Übereinstimmung mit den Anforderungen von SharePoint-Produkten und -Technologien ist**spPowerPivot16.msi** nur für 64-Bit ausgelegt.  
  
-   Ein Server im [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Modus. Office Online Server verwendet die SQL Server Analysis Services-Instanz als [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Server. Analysis Services können auf dem lokalen SharePoint-Server oder einem Remotecomputer ausgeführt werden. Es kann nicht auf dem Office Online Server installiert werden.  
  
-   **Berechtigungen:** Zur Installation von [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]muss der aktuelle Benutzer auf dem Computer als Administrator eingeloggt sein und Mitglied der Administratorengruppe der SharePoint-Farm sein.  
  
-   Weitere Informationen zu den [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] -Anforderungen und erforderlichen Komponenten finden Sie unter [Hardware- und Softwareanforderungen für Analysis Services-Server im SharePoint-Modus](http://msdn.microsoft.com/library/fb86ca0a-518c-4c61-ae78-7680c57fae1f).  
  
##  <a name="bkmk_install"></a> Installieren von PowerPivot für SharePoint  
 Das Installationspaket **spPowerpivot16.msi** unterstützt sowohl eine grafische Benutzeroberfläche als auch einen Befehlszeilenmodus. Beide Installationsmethoden setzen voraus, dass die MSI-Datei mit Administratorrechten ausgeführt wird. Nach der Installation finden Sie im folgenden Thema Informationen zu Konfigurationstool und zusätzlichen Funktionen: [Konfigurieren von PowerPivot und Bereitstellen von Lösungen &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md).  
  
### <a name="user-interface-installation"></a>Installation über die Benutzeroberfläche  
 Um [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] über die grafische Benutzeroberfläche zu installieren, führen Sie die folgenden Schritte aus:  
  
1.  Führen Sie **spPowerPivot16.msi**aus.  
  
2.  Wählen Sie auf der Startseite **Weiter** aus.  
  
3.  Lesen und akzeptieren Sie den Lizenzvertrag, und wählen sie **Weiter**aus.  
  
4.  Auf der Seite **Funktionsauswahl** sind alle Funktionen standardmäßig ausgewählt.  
  
5.  Wählen Sie **Weiter**aus.  
  
6.  Wählen Sie **Installieren** aus, um die Installation abzuschließen.  
  
### <a name="command-line-installation"></a>Installation über die Befehlszeile  
 Öffnen Sie zum Installieren über die Befehlszeile eine Eingabeaufforderung mit Administratorberechtigungen, und führen Sie anschließend **spPowerPivot16.msi**aus. Beispiel:  
  
 `Msiexec.exe /i spPowerPivot16.msi`.  
  
 Um ein Installationsprotokoll zu erstellen, verwenden Sie die Standardoptionen für die MsiExec-Protokollierung. Im folgenden Beispiel wird die Protokolldatei Install_Log.txt mit dem v-Schalter für die ausführliche Protokollierung erstellt.  
  
```  
Msiexec.exe /i spPowerPivot16.msi /L v c:\test\Install_Log.txt  
```  
  
### <a name="quiet-command-line-installation-for-scripting"></a>Installation über die Befehlszeile im stillen Modus unter Verwendung eines Skripts  
 Mithilfe der Schalter **/q** oder **/quiet** können Sie eine unbeaufsichtigte Installation ausführen, bei der keine Dialogfelder oder Warnungen angezeigt werden. Die stille Installation ist nützlich, wenn Sie für die Installation des Add-Ins ein Skript schreiben möchten.  
  
> [!IMPORTANT]  
>  Wenn Sie den Schalter **/q** für eine Befehlszeileninstallation im unbeaufsichtigten Modus verwenden, wird der Endbenutzer-Lizenzvertrag nicht angezeigt. Unabhängig von der Installationsmethode unterliegt die Verwendung dieser Software einem Lizenzvertrag, dessen Einhaltung in Ihrer Verantwortung liegt.  
  
 **So führen Sie eine stille Installation aus:**  
  
1.  Öffnen Sie eine Eingabeaufforderung **mit Administratorberechtigungen**.  
  
2.  Führen Sie den folgenden Befehl aus:  
  
    ```  
    Msiexec.exe /i spPowerPivot16.msi /q  
    ```  
  
### <a name="command-line-installation-to-include-specific-components"></a>Installation über die Befehlszeile, um bestimmte Komponenten einzuschließen  
 Das [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] -Konfigurationstool ist nicht auf jedem SharePoint-Server erforderlich, es wird jedoch empfohlen, das Konfigurationstool mindestens auf zwei Servern zu installieren, damit es bei Bedarf verfügbar ist.  
  
 Bei der Installation von „spPowerPivot16.msi“ können Sie anstelle des [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] -Konfigurationstools die Befehlszeilenoptionen verwenden, um bestimmte Komponenten wie die Datenanbieter zu installieren. Die folgende Befehlszeile stellt ein Beispiel für die Installation aller Komponenten mit Ausnahme des Konfigurationstools dar:  
  
```  
Msiexec /i spPowerPivot16.msi AGREETOLICENSE="yes" ADDLOCAL=” SQL_OLAPDM,SQL_ADOMD,SQL_AMO,SQLAS_SP_Common”  
```  
  
|Option|Beschreibung|  
|------------|-----------------|  
|Analysis_Server_SP_addin16|[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] Konfiguration|  
|SQL_OLAPDM|Analysis Services OLE DB Provider für SQL Server 2016|  
|SQL_ADOMD|ADOMD.NET-Anbieter|  
|SQL_AMO|Anbieter für SQL Server 2016 Analysis Management Objects (AMO)|  
|SQLAS_SP16_Common|Allgemeine Analysis Services-Komponenten für SharePoint 2016|  
  
##  <a name="bkmk_deploy_solution"></a> Bereitstellen der SharePoint-Lösungsdateien mit Power Pivot für SharePoint 2016-Konfigurationstool  
 Drei der Dateien, die von spPowerPivot16.msi auf die Festplatte kopiert werden, sind SharePoint-Lösungsdateien. Eine Lösungsdatei bezieht sich auf die Webanwendungsebene, während sich die anderen Dateien auf die Farmebene beziehen. Die Dateien lauten:  
  
-   `PowerPivot16FarmSolution.wsp`  

-   `PowerPivot16WebApplicationSolution.wsp`  
  
 Die Lösungsdateien werden in den folgenden Ordner kopiert:  
  
 `ssInstallPathTools\PowerPivotTools\SPAddinConfiguration\Resources`  
  
 Nach Abschluss der MSI-Installation führen Sie das [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] -Konfigurationstool aus, um die Lösungen in der SharePoint-Farm zu konfigurieren und bereitzustellen.  
  
 **So starten Sie das Konfigurationstool:**  
  
 Geben Sie auf dem Windows-Startbildschirm „power“ ein, und wählen Sie in den Suchergebnissen der Apps **[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] Konfiguration**aus. Beachten Sie, dass die Suchergebnisse u.U. zwei Links enthalten, weil das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup separate [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Konfigurationstools für SharePoint 2013 und SharePoint 2016 installiert. Stellen Sie sicher, dass Sie das [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] -Konfigurationstool starten.  
  
 ![PowerPivot für SharePoint 2016-Konfigurationstool](../../../analysis-services/instances/install-windows/media/powerpivot-for-sharepoint-2016-configuration.png "PowerPivot für SharePoint 2016-Konfigurationstool")  
  
 **Or**  
  
1.  Wechseln Sie zu **Start**, **Alle Programme**.  
  
2.  Wählen Sie [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]aus.  
  
3.  Wählen Sie **Konfigurationstools**aus.  
  
4.  Wählen Sie **[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] Konfiguration**aus.  
  
 Weitere Informationen zum Konfigurationstool finden Sie unter [PowerPivot-Konfigurationstools](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md).  
  
##  <a name="bkmk_remove_addin"></a> Deinstallieren oder Reparieren des Add-Ins  
  
> [!CAUTION]  
>  Bei der Deinstallation von **spPowerPivot16.msi** werden die Datenanbieter und das Konfigurationstool deinstalliert. Nach der Deinstallation der Datenanbieter kann der Server keine Verbindung mehr mit [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]herstellen.  
  
 Sie können [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] mithilfe einer der folgenden Methoden deinstallieren oder reparieren:  
  
1.  **Windows-Systemsteuerung:** Wählen Sie [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]**[!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)]**aus. Wählen Sie entweder **Deinstallieren** oder **Reparieren**aus.  
  
2.  Führen Sie „spPowerPivot16.msi“ aus, und wählen Sie die Option **Entfernen** oder **Reparieren** aus.  
  
 **Befehlszeile:** Öffnen Sie die Eingabeaufforderung mit [!INCLUDE[ssGeminiShort2016](../../../includes/ssgeminishort2016-md.md)] Administratorberechtigungen **, und führen Sie einen der folgenden Befehle aus, um** über die Befehlszeile zu reparieren oder zu deinstallieren:  
  
-   Zum Reparieren führen Sie den folgenden Befehl aus:  
  
    ```  
    msiexec.exe /f spPowerPivot16.msi  
    ```  
  
 oder  
  
-   Zum Deinstallieren führen Sie den folgenden Befehl aus:  
  
    ```  
    msiexec.exe /uninstall spPowerPivot16.msi  
    ```  
  
  

