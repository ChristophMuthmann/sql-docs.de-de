---
title: "Festlegen von Identitätswechseloptionen (SSAS – mehrdimensional) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.sqlserverstudio.impersonationinfo.f1
helpviewer_keywords: Impersonation Information dialog box
ms.assetid: 8e127f72-ef23-44ad-81e6-3dd58981770e
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: b448d78a897c6e7c6aa6973b6e61b92ff7a9aade
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="set-impersonation-options-ssas---multidimensional"></a>Festlegen von Identitätswechseloptionen (SSAS – mehrdimensional)
  Wenn Sie ein **data source** -Objekt in einem Analysis Services-Modell erstellen, müssen Sie unter den verschiedenen Einstellungen eine Option für den Identitätswechsel konfigurieren. Diese Option bestimmt, ob Analysis Services die Identität eines bestimmten Windows-Benutzerkontos annimmt, wenn lokale Vorgänge im Zusammenhang mit der Verbindung ausgeführt werden, z. B. das Laden eines OLE DB-Datenanbieters oder das Auflösen von Benutzerprofilinformationen in Umgebungen, die Roamingprofile unterstützen.  
  
 Bei Verbindungen, die Windows-Authentifizierung verwenden, bestimmt die Identitätswechseloption außerdem die Benutzeridentität, unter der Abfragen an die externe Datenquelle ausgeführt werden. Wenn Sie die Identitätswechseloption z.B. auf **contoso\dbuser**festlegen, werden Datenabfragen während der Verarbeitung als **contoso\dbuser** auf dem Datenbankserver ausgeführt.  
  
 In diesem Thema wird erläutert, wie Identitätswechseloptionen beim Konfigurieren eines Datenquellenobjekts im Dialogfeld **Identitätswechselinformationen** festgelegt werden.  
  
## <a name="set-impersonation-options-in-sql-server-data-tools"></a>Festlegen von Identitätswechseloptionen in SQL Server-Datentools  
  
1.  Doppelklicken Sie im Projektmappen-Explorer auf eine Datenquelle, um den Datenquellen-Designer zu öffnen.  
  
2.  Klicken Sie im Datenquellen-Designer auf die Registerkarte **Identitätswechselinformationen** .  
  
3.  Wählen Sie eine der Optionen aus, die in diesem Thema unter [Identitätswechseloptionen](#bkmk_options) beschrieben werden.  
  
## <a name="set-impersonation-options-in-management-studio"></a>Festlegen von Identitätswechseloptionen in Management Studio  
 Öffnen Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]das Dialogfeld **Identitätswechselinformationen** , indem Sie für die folgenden Eigenschaften dieser Dialogfelder auf die Schaltfläche mit den Auslassungspunkten (**...**) klicken:  
  
-   Dialogfeld**Datenbankeigenschaften** , über die Eigenschaft "Identitätswechselinformationen der Datenquelle"  
  
-   Dialogfeld**Datenquelleneigenschaften** , über die Eigenschaft "Identitätswechselinformationen"  
  
-   Dialogfeld**Assemblyeigenschaften** , über die Eigenschaft "Identitätswechselinformationen"  
  
##  <a name="bkmk_options"></a> Identitätswechseloptionen  
 Alle Optionen sind im Dialogfeld verfügbar, aber nicht alle Optionen sind für jedes Szenario geeignet. Bestimmen Sie anhand folgender Informationen die beste Option für das Szenario.  
  
 **Bestimmten Benutzernamen und bestimmtes Kennwort verwenden**  
 Wählen Sie diese Option aus, damit die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Objekt verwenden Sie die Anmeldeinformationen des Windows-Benutzerkontos in folgendem Format angegeben:  *\<Domänenname >*  **\\**   *\<Benutzerkontoname >*.  
  
 Wählen Sie diese Option aus, um eine dedizierte Windows-Benutzeridentität mit den niedrigsten Privilegien zu verwenden, die Sie speziell für Datenzugriffszwecke erstellt haben. Wenn Sie z. B. routinemäßig ein allgemeines Konto zum Abrufen von Daten für Berichte erstellen, können Sie dieses Konto hier angeben.  
  
 Bei mehrdimensionalen Datenbanken werden die angegebenen Anmeldeinformationen für Verarbeitungsvorgänge, ROLAP-Abfragen, Out-of-Line-Bindungen, lokale Cubes, Miningmodelle, Remotepartitionen, verknüpfte Objekte und Synchronisierungen vom Ziel zur Quelle verwendet.  
  
 Bei DMX OPENQUERY-Anweisungen wird diese Option ignoriert, und die Anmeldeinformationen des aktuellen Benutzers werden anstelle des angegebenen Benutzerkontos verwendet.  
  
 **Dienstkonto verwenden**  
 Wählen Sie diese Option aus, damit das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekt die Anmeldeinformationen mit dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dienst verwendet, der das Objekt verwaltet. Diese Option ist die Standardeinstellung. In früheren Versionen war dies die einzige Option, die Sie verwenden konnten. Möglicherweise bevorzugen Sie diese Option, um den Datenzugriff auf Dienstebene anstelle einzelner Benutzerkonten zu überwachen.  
  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]kann das Dienstkonto abhängig vom verwendeten Betriebssystem einem NetworkService oder einem integrierten virtuellen Konto entsprechen, das für eine bestimmte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz erstellt wurde. Wenn Sie das Dienstkonto für eine Verbindung auswählen, die die Windows-Authentifizierung verwendet, denken Sie daran, eine Datenbankanmeldung für dieses Konto zu erstellen und Leseberechtigungen zu gewähren, da diese während der Verarbeitung zum Abrufen von Daten verwendet werden. Weitere Informationen zum Dienstkonto finden Sie unter [Configure Windows Service Accounts and Permissions](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
> [!NOTE]  
>  Wenn Sie die Datenbankauthentifizierung verwenden, sollten Sie die Identitätswechseloption **Dienstkonto verwenden** auswählen, wenn der Dienst unter dem dedizierten virtuellen Konto für Analysis Services ausgeführt wird. Dieses Konto verfügt über Berechtigungen für den Zugriff auf lokale Dateien. Wenn der Dienst als NetworkService ausgeführt wird, empfiehlt es sich, ein Windows-Benutzerkonto mit geringeren Rechten zu verwenden, das über die Berechtigung **Lokal anmelden zulassen** verfügt. Abhängig vom angegebenen Konto müssen Sie möglicherweise auch Dateizugriffsberechtigungen für den Analysis Services-Programmordner gewähren.  
  
 Bei mehrdimensionalen Datenbanken werden die Dienstkonto-Anmeldeinformationen für Verarbeitungsvorgänge, ROLAP-Abfragen, Remotepartitionen, verknüpfte Objekte und Synchronisierungen vom Ziel zur Quelle verwendet.  
  
 Bei DMX-OPENQUERY-Anweisungen, lokalen Cubes und Miningmodellen werden die Anmeldeinformationen des aktuellen Benutzers auch dann verwendet, wenn Sie die Dienstkontooption auswählen. Die Dienstkontooption wird für Out-of-Line-Bindungen nicht unterstützt.  
  
> [!NOTE]  
>  Wenn ein Data Mining-Modell aus einem Cube verarbeitet wird, können Fehler auftreten, sofern das Dienstkonto nicht über Administratorberechtigungen für die Analysis Services-Instanz verfügt. Weitere Informationen finden Sie unter [Minigstruktur: Fehler bei der Verarbeitung, wenn die Datenquelle ein OLAP-Cube ist](http://go.microsoft.com/fwlink/?LinkId=251610).  
  
 **Anmeldeinformationen des aktuellen Benutzers verwenden**  
 Wählen Sie diese Option aus, damit vom [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekt für Out-of-Line-Bindungen, DMX OPENQUERY-Anweisungen, lokale Cubes und Miningmodelle die Sicherheitsanmeldeinformationen des aktuellen Benutzers verwendet werden.  
  
 Mit Ausnahme lokaler Cubes und der Verarbeitung mit Out-of-Line-Bindungen wird diese Option für mehrdimensionale Datenbanken nicht unterstützt.  
  
 **Standard** oder **Erben**  
 Im Dialogfeld wird **Standard** für die Identitätswechseloptionen auf Datenbankebene und **Erben** für Identitätswechseloptionen auf Datenquellenebene verwendet.  
  
 **Datenquellen – Option "Erben"**  
  
 Auf Datenquellenebene wird durch **Erben** angegeben, dass von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die Identitätswechseloption des übergeordneten Objekts verwendet werden muss. In mehrdimensionalen Modellen wird als übergeordnetes Objekt die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank verwendet. Wenn Sie die Option **Erben** auswählen, können Sie die Identitätswechseleinstellungen für diese und andere Datenquellen, die Teil derselben Datenbank sind, zentral verwalten. Um diese Option sinnvoll einzusetzen, wählen Sie einen bestimmten Windows-Benutzernamen und ein Kennwort auf Datenbankebene aus. Ansonsten entspricht die Kombination von **Erben** für die Datenquelle und **Standard** für die Datenbank der Verwendung der Dienstkontooption.  
  
 Um einen Windows-Benutzernamen und ein Kennwort auf Datenbankebene anzugeben, gehen Sie wie folgt vor:  
  
1.  Klicken Sie mit der rechten Maustaste auf [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , und wählen Sie **Eigenschaften**aus.  
  
2.  Geben Sie in **Identitätswechselinformationen der Datenquelle**einen Windows-Benutzernamen und ein Kennwort an.  
  
3.  Klicken Sie mit der rechten Maustaste auf die einzelnen Datenquellen, und zeigen Sie deren Eigenschaften an, um sicherzustellen, dass für jede die Option **Erben** verwendet wird.  
  
 Weitere Informationen zu den Standardeinstellungen auf Datenbankebene finden Sie unter [Festlegen von Eigenschaften für mehrdimensionale Datenbanken &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md).  
  
 **Datenbanken – Option "Standard"**  

 Bei mehrdimensionalen Datenbanken entspricht **Standard** der Verwendung des Dienstkontos und des aktuellen Benutzers für Data Mining-Vorgänge.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer Datenquelle &#40;SSAS – mehrdimensional&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)   
 [Festlegen von Datenquelleneigenschaften &#40;SSAS – mehrdimensional&#41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md)   

  
  
