---
title: Installieren von Integration Services | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Integration Services, installing
- SSIS, installing
- installing Integration Services, about installing Integration Services
- SQL Server Integration Services, installing
- Setup [Integration Services], about installing Integration Services
- installing Integration Services
- Setup [Integration Services]
ms.assetid: bd20fd3a-414b-4581-959d-ebba4ddf5a55
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 8233e11171d5adc7656fd2b2ce75c86fca2c07fa
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="install-integration-services"></a>Installieren von Integration Services
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt ein einzelnes Setupprogramm bereit, mit dem eine oder alle Komponenten installiert werden können, einschließlich [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Während des Setups können Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mit oder ohne andere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten auf einem einzelnen Computer installieren.    
    
 Dieses Thema behandelt wichtige Überlegungen, die Sie beachten sollten, bevor Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]installieren. Informationen zu diesem Thema helfen Ihnen bei der Bewertung der Installationsoptionen, sodass Sie die Werte auswählen können, die zu einer erfolgreichen Installation führen.    
    
## <a name="preparing-to-install-integration-services"></a>Vorbereiten der Installation von Integration Services    
 Überprüfen Sie vor der Installation von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]folgende Voraussetzungen:    
    
-   [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)    
    
-   [Überprüfen der Parameter für die Systemkonfigurationsprüfung](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)    
    
-   [Überlegungen zur Sicherheit bei SQL Server-Installationen](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)    
    
## <a name="selecting-an-integration-services-configuration"></a>Auswählen der Konfiguration von Integration Services    
 Sie können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in folgenden Konfigurationen installieren:    
    
-   Sie können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf einem Computer installieren, auf dem sich keine früheren Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]befinden.    
    
-   Sie können [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] parallel zu einer bestehenden Instanz von [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] oder [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]installieren    
    
     Wenn Sie einen Computer, auf dem bereits eine dieser früheren Versionen von [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] installiert ist, auf [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] aktualisieren, wird [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] parallel zur früheren Version installiert.    
    
     Weitere Informationen zum Upgrade von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]finden Sie unter [Upgrade von Integration Services](../../integration-services/install-windows/upgrade-integration-services.md). Informationen zur Abwärtskompatibilität mit früheren Versionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]finden Sie unter [Integration Services – Abwärtskompatibilität](../../integration-services/integration-services-backward-compatibility.md).    
    
## <a name="installing-integration-services"></a>Installieren von Integration Services    
 Nachdem Sie die Installationsanforderungen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] überprüft und sichergestellt haben, dass der Computer diese erfüllt, können Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]installieren.    
    
> [!NOTE]    
>  In vorherigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hatten alle Benutzer in der Gruppe Benutzer standardmäßig Zugriff auf den Dienst [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , wenn Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installiert haben. Wenn Sie [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]installieren, haben Benutzer keinen Zugriff auf den Dienst [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Der Dienst ist standardmäßig sicher. Nach der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Administrator das DCOM-Konfigurationstool (Dcomcnfg.exe) ausführen, um bestimmten Benutzern Zugriff auf **SQL Server Integration Services 13.0**zu gewähren.    
>     
>  Anweisungen zum Gewähren von Berechtigungen finden Sie unter [Integration Services-Dienst &#40;SSIS-Dienst&#41;](../../integration-services/service/integration-services-service-ssis-service.md).    
    
 Wenn Sie bei der Installation von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]einen Setup-Assistenten verwenden, müssen Sie die Komponenten und Optionen auf mehreren Seiten angeben. In der folgenden Tabelle werden nur die Seiten im Setup-Assistenten aufgeführt, in denen sich die von Ihnen ausgewählten Optionen auf die Installation von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]auswirken:    
    
|Seite|Empfehlungen|    
|----------|---------------------|    
|**Funktionsauswahl**|Wählen Sie **Integration Services** aus, um den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst zu installieren und Pakete außerhalb der Entwurfsumgebung auszuführen.<br /><br /> Um eine vollständige Installation von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]mit den Tools und der Dokumentation für die Entwicklung und Verwaltung von Paketen auszuführen, wählen Sie sowohl **Integration Services** als auch die folgenden **freigegebenen Funktionen**aus:<br /><br /> -<br />                    **SQL Server Data Tools** , um die Tools zum Entwerfen von Paketen zu installieren.<br /><br /> -<br />                    **Verwaltungstools – Vollständig** , um [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zum Verwalten von Paketen zu installieren.<br /><br /> -<br />                    **Clienttools SDK** , um verwaltete Assemblys für die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Programmierung zu installieren.<br /><br /> Viele Data Warehousing-Lösungen erfordern außerdem die Installation weiterer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten wie z.B. das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> **Installation auf einem 64-Bit-Computer** Wenn Sie **Integration Services** auf einem 64-Bit-Computer auswählen, werden nur die 64-Bit-Versionen der Runtime und der Tools installiert. Wenn Sie Pakete im 32-Bit-Modus ausführen müssen, müssen Sie eine zusätzliche Option auswählen, um die 32-Bit-Version der Laufzeit und der Tools zu installieren:<br /><br /> - Wenn auf dem 64-Bit-Computer ein x86-Betriebssystem ausgeführt wird, wählen Sie **SQL Server Data Tools** oder **Verwaltungstools – Vollständig**aus.<br /><br /> - Wenn auf dem 64-Bit-Computer ein [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] -Betriebssystem ausgeführt wird, wählen Sie **Verwaltungstools – Vollständig**aus.<br /><br /> **Installieren auf einem dedizierten Server für ETL** Wenn Sie einen dedizierten Server für ETL-Prozesse (Extrahieren, Transformieren, Laden) verwenden möchten, empfiehlt es sich, beim Installieren von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] eine lokale Instanz des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]s zu installieren. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] speichert Pakete üblicherweise in einer Instanz des [!INCLUDE[ssDE](../../includes/ssde-md.md)] s und verwendet den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent zum Planen dieser Pakete. Wenn der ETL-Server keine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]aufweist, müssen Sie Pakete von einem Server planen oder ausführen, der eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]aufweist. Dies bedeutet, dass die Pakete nicht auf dem ETL-Server ausgeführt werden, sondern stattdessen auf dem Server, auf dem sie gestartet wurden. Als Ergebnis werden die Ressourcen des dedizierten ETL-Servers nicht wie gewünscht verwendet. Darüber hinaus werden die Ressourcen anderer Server möglicherweise durch die ausgeführten ETL-Prozesse belastet.<br /><br /> <br /><br /> Hinweis: Einige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten, die Sie auf der Seite **Funktionsauswahl** des Setup-Assistenten zur Installation auswählen können, installieren eine Teilmenge der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponenten. Diese Komponenten sind für bestimmte Tasks hilfreich, aber die Funktionalität von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ist begrenzt. Beispielsweise werden mit der Option **Database Engine Services** die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponenten installiert, die für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten erforderlich sind. Die Option **SQL Server Data Tools** installiert die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponenten, die für den Entwurf eines Pakets erforderlich sind. Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst wird jedoch nicht installiert, und Sie können keine Pakete außerhalb von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]ausführen. Um eine vollständige Installation von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]sicherzustellen, müssen Sie auf der Seite **Funktionsauswahl** die **Integration Services** auswählen.|    
|**Instanzkonfiguration**|Optionen, die Sie auf der Seite **Instanzkonfiguration** ausgewählt haben, wirken sich nicht auf [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] oder den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst aus.<br /><br /> Es kann nur eine Instanz des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts auf einem Computer installiert werden. Sie stellen mithilfe des Computernamens eine Verbindung zu dem Dienst her.<br /><br /> Standardmäßig wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst für die Verwaltung von Paketen konfiguriert, die in der **msdb** -Datenbank in der Instanz des Datenbankmoduls gespeichert sind, das zur selben Zeit wie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]installiert wird. Wenn eine Instanz des Datenbankmoduls nicht zur selben Zeit installiert wird wie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst für die Verwaltung von Paketen konfiguriert, die in der **msdb** -Datenbank der lokalen Standardinstanz des [!INCLUDE[ssDE](../../includes/ssde-md.md)]s gespeichert sind. Um Pakete zu verwalten, die in einer benannten Instanz, einer Remoteinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]oder in mehreren Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)]gespeichert sind, müssen Sie die Konfigurationsdatei ändern. Weitere Informationen zum Ändern dieser Konfigurationsdatei finden Sie unter [Integration Services-Dienst &#40;SSIS-Dienst&#41;](../../integration-services/service/integration-services-service-ssis-service.md).|    
|**Serverkonfiguration**|Überprüfen Sie die Einstellungen für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst auf der Registerkarte **Dienstkonten** der Seite **Serverkonfiguration** .<br /><br /> Wenn Windows 7 oder Windows Server 2008 R2 installiert ist, wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst für die Ausführung unter dem virtuellen Konto NT Services\MsDtsServer130 registriert, und der **Starttyp** ist **Automatisch**.  Sie müssen kein Kennwort für das virtuelle Konto eingeben. Wenn Microsoft Vista oder Windows Server 2008 installiert ist, wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst für die Ausführung unter dem integrierten Netzwerkdienstkonto registriert, und der **Starttyp** ist **Automatisch**. Sie müssen kein Kennwort für das integrierte Netzwerkdienstkonto eingeben.|    
    
 Bei einer Neuinstallation wird [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] standardmäßig so konfiguriert, dass Ereignisse im Zusammenhang mit der Ausführung von Paketen im Anwendungsereignisprotokoll nicht protokolliert werden. Mit dieser Einstellung wird verhindert, dass zu viele Ereignisprotokolleinträge erstellt werden, wenn Sie die Datensammler-Funktion von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]verwenden. Zu den nicht protokollierten Ereignissen gehören EventID 12288 "Paket wurde gestartet" und EventID 12289 "Paket wurde erfolgreich beendet". Wenn Sie diese Ereignisse im Anwendungsereignisprotokoll protokollieren möchten, öffnen Sie die Registrierung zum Bearbeiten. Suchen Sie anschließend in der Registrierung den Knoten "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS", und ändern Sie den Wert DWORD der Einstellung LogPackageExecutionToEventLog von 0 auf 1.    
    
## <a name="understanding-the-integration-services-service"></a>Grundlegendes zu den Integration Services    
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installiert den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst.    
    
 Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst wird installiert, wenn Sie auf der Seite **Funktionsauswahl** die Option **Integration Services** ausgewählt haben. Wenn Sie die Standardeinstellungen auf der Seite **Serverkonfiguration** übernehmen, wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst aktiviert, und der **Starttyp** ist **Automatisch**.    
    
 Es kann nur eine einzige Instanz des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienstes auf einem Computer installiert werden. Der Dienst ist nicht spezifisch für eine bestimmte Instanz des Datenbankmoduls. Sie stellen eine Verbindung mit dem Dienst mit dem Namen des Computers her, auf dem der Dienst ausgeführt wird.    
    
## <a name="installing-integration-services-on-64-bit-computers"></a>Installieren von Integration Services auf 64-Bit-Computern    
    
### <a name="integration-services-features-installed-on-64-bit-computers"></a>Auf 64-Bit-Computern installierte Integration Services-Funktionen    
 Das Setup installiert basierend auf den von Ihnen gewählten Setupoptionen verschiedene [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Funktionen:    
    
-   Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installieren und dabei [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] zur Installation auswählen, installiert das Setup alle verfügbaren 64-Bit-Funktionen und -Tools von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .    
    
-   Wenn Sie die Entwurfszeitfunktionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] benötigen, müssen Sie auch [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]installieren.    
    
-   Wenn Sie 32-Bit-Versionen der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Runtime und -Tools benötigen, um bestimmte Pakete im 32-Bit-Modus auszuführen, müssen Sie auch [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]installieren.    
    
 64-Bit-Funktionen werden im Verzeichnis **Programme** installiert, 32-Bit-Funktionen werden getrennt davon im Verzeichnis **Programme (x86)** installiert. (Dieses Verhalten ist nicht spezifisch für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] oder für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].)    
    
> [!IMPORTANT]    
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], die 32-Bit-Entwicklungsumgebung für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakete, wird auf Computern mit dem [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]-64-Bit-Betriebssystem nicht unterstützt und auf [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]-Servern nicht installiert.    
    
  
