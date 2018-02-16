---
title: "Erstellen einer Datenquelle (SSAS – mehrdimensional) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.sqlserverstudio.impersonationinfo.f1
- sql13.asvs.connectionmanager.f1
- sql13.asvs.datasourcedesigner.f1
helpviewer_keywords:
- impersonation [Analysis Services]
- data sources [Analysis Services], creating
- security [Analysis Services], data source connections
ms.assetid: 9fab8298-10dc-45a9-9a91-0c8e6d947468
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 213bc7a17344f42cd10258962f91711a5ee3acba
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="create-a-data-source-ssas-multidimensional"></a>Erstellen einer Datenquelle (SSAS – mehrdimensional)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
In einem mehrdimensionalen Modell von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt ein Datenquellenobjekt eine Verbindung zu der Datenquelle dar, von der Sie Daten verarbeiten (oder importieren). Ein mehrdimensionales Modell muss mindestens ein Datenquellenobjekt enthalten, Sie können jedoch weitere hinzufügen, um Daten aus mehreren Data Warehouses zu kombinieren. Erstellen Sie anhand der Anweisungen in diesem Thema ein Datenquellenobjekt für Ihr Modell. Weitere Informationen zum Festlegen von Eigenschaften für dieses Objekt finden Sie unter [Festlegen von Datenquelleneigenschaften &#40;SSAS – mehrdimensional&#41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md).  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Auswählen eines Datenanbieters](#bkmk_provider)  
  
 [Festlegen von Anmeldeinformationen und Identitätswechseloptionen](#bkmk_impersonation)  
  
 [Anzeigen oder Bearbeiten von Verbindungseigenschaften](#bkmk_ConnectionString)  
  
 [Erstellen einer Datenquelle mit dem Datenquellen-Assistent](#bkmk_steps)  
  
 [Erstellen einer Datenquelle mit einer vorhandenen Verbindung](#bkmk_connection)  
  
 [Hinzufügen mehrerer Datenquellen zu einem Modell](#bkmk_multipleDS)  
  
##  <a name="bkmk_provider"></a> Auswählen eines Datenanbieters  
 Die Verbindung können Sie mit einem verwaltetem [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework- oder einem systemeigenem OLE DB-Anbieter herstellen. Als Datenanbieter wird für SQL Server-Datenquellen SQL Server Native Client empfohlen, da dieser meist eine bessere Leistung bietet.  
  
 Bei Oracle- und anderen Datenquellen von Drittanbietern überprüfen Sie, ob der Drittanbieter einen systemeigenen OLE DB-Anbieter bereitstellt, mit dem Sie es als Erstes probieren. Bei Fehlern versuchen Sie es mit einem anderen .NET-Anbieter oder systemeigenen OLE DB-Anbieter, der im Verbindungs-Manager aufgeführt wird. Stellen Sie sicher, dass jeder von Ihnen verwendete Datenanbieter auf allen Computern installiert ist, die zum Entwickeln und Ausführen der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Lösung verwendet werden.  
  
##  <a name="bkmk_impersonation"></a> Festlegen von Anmeldeinformationen und Identitätswechseloptionen  
 Eine Datenquellenverbindung kann manchmal die Windows-Authentifizierung oder einen vom Datenbank-Managementsystem bereitgestellten Authentifizierungsdienst verwenden, z. B. die SQL Server-Authentifizierung beim Herstellen einer Verbindung mit SQL Azure-Datenbanken. Das angegebene Konto muss über Anmeldeinformationen für den Remotedatenbankserver und Leseberechtigungen für die externe Datenbank verfügen.  
  
### <a name="windows-authentication"></a>Windows-Authentifizierung  
 Verbindungen mit Verwendung der Windows-Authentifizierung werden auf der Registerkarte **Identitätswechselinformationen** des Datenquellen-Designers angegeben. Auf dieser Registerkarte wählen Sie die Identitätswechseloption aus, die das Konto angibt, unter dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ausgeführt wird, wenn Sie eine Verbindung mit der externen Datenquelle herstellen. Nicht alle Optionen können in allen Szenarien verwendet werden. Weitere Informationen zu diesen Optionen und ihrer Verwendung finden Sie unter [Festlegen von Identitätswechseloptionen &#40;SSAS – mehrdimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md).  
  
### <a name="database-authentication"></a>Datenbankauthentifizierung  
 Als Alternative zur Windows-Authentifizierung können Sie auch eine Verbindung angeben, für die ein vom Datenbankmanagementsystem bereitgestellter Authentifizierungsdienst verwendet wird. In manchen Fällen muss die Datenbankauthentifizierung verwendet werden. Zu den Szenarien, in denen die Datenbankauthentifizierung verwendet werden muss, gehören die Verwendung der SQL Server-Authentifizierung zum Verbinden mit einer Windows Azure SQL-Datenbank und der Zugriff auf eine relationale Datenquelle unter einem anderen Betriebssystem oder in einer nicht vertrauenswürdigen Domäne.  
  
 Bei einer Datenquelle mit Verwendung der Datenbankauthentifizierung werden in der Verbindungszeichenfolge der Benutzername und das Kennwort einer Datenbankanmeldung angegeben. Wenn Sie beim Einrichten der Datenquellenverbindung im Verbindungs-Manager im [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Modell einen Benutzernamen und ein Kennwort eingeben, werden der Verbindungszeichenfolge Anmeldeinformationen hinzugefügt. Geben Sie unbedingt eine Benutzeridentität an, die über Leseberechtigungen für die Daten verfügt.  
  
 Beim Abrufen von Daten formuliert die Clientbibliothek, von der die Verbindung hergestellt wird, eine Verbindungsanforderung, in deren Verbindungszeichenfolge die Anmeldeinformationen enthalten sind. Die auf der Registerkarte "Identitätswechselinformationen" angegebenen Anmeldeinformationsoptionen für die Windows-Authentifizierung werden nicht für die Verbindung verwendet, können jedoch für andere Vorgänge verwendet werden, z. B. für den Zugriff auf Ressourcen auf dem lokalen Computer. Weitere Informationen finden Sie unter [Festlegen von Identitätswechseloptionen &#40;SSAS – mehrdimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md).  
  
 Wenn Sie das Datenquellenobjekt im Modell gespeichert haben, werden die Verbindungszeichenfolge und das Kennwort verschlüsselt.  Aus Sicherheitsgründen werden beim späteren Anzeigen in Tools, Skript oder Code alle sichtbaren Spuren des Kennworts aus der Verbindungszeichenfolge entfernt.  
  
> [!NOTE]  
>  Standardmäßig werden in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] Kennwörter nicht mit der Verbindungszeichenfolge gespeichert. Wenn das Kennwort nicht gespeichert wird, werden Sie von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zur Eingabe des Kennworts aufgefordert, sobald es benötigt wird. Wenn Sie sich für die Speicherung des Kennworts entscheiden, wird es in verschlüsselter Form in der Datenverbindungszeichenfolge gespeichert. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verschlüsselt Kennwortinformationen für Datenquellen mithilfe des Verschlüsselungsschlüssels der Datenbank, die die Datenquelle enthält. Werden verschlüsselte Verbindungsinformationen verwendet, müssen Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager verwenden, um das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dienstkonto oder das zugehörige Kennwort zu ändern; andernfalls können die verschlüsselten Informationen nicht wiederhergestellt werden. Weitere Informationen finden Sie unter [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).  
  
### <a name="defining-impersonation-information-for-data-mining-objects"></a>Definieren von Identitätswechselinformationen für Data Mining-Objekte  
 Data Mining-Abfragen können im Kontext des [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dienstkontos ausgeführt werden. Es ist jedoch auch möglich, sie im Kontext des Benutzers, der die Abfrage gesendet hat, oder im Kontext eines angegebenen Benutzers auszuführen. Der Kontext, in dem eine Abfrage ausgeführt wird, kann sich auf das Ergebnis der Abfrage auswirken. Bei Data Mining-Vorgängen des Typs **OPENQUERY** kann es sich anbieten, die Data Mining-Abfrage nicht im Kontext des Dienstkontos, sondern im Kontext des aktuellen Benutzers oder im Kontext eines angegebenen Benutzers (unabhängig vom Benutzer, der die Abfrage ausführt) auszuführen. Hierdurch ist es möglich, die Abfrage mit eingeschränkten Sicherheitsanmeldeinformationen auszuführen. Wenn [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die Identität des aktuellen Benutzers oder eines angegebenen Benutzers annehmen soll, müssen Sie entweder die Option **Bestimmten Benutzernamen und bestimmtes Kennwort** oder **Anmeldeinformationen des aktuellen Benutzers** auswählen.  
  
##  <a name="bkmk_steps"></a> Erstellen einer Datenquelle mit dem Datenquellen-Assistent  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt, oder stellen Sie eine Verbindung mit der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank her, in dem bzw. der Sie die Datenquelle definieren möchten.  
  
2.  Klicken Sie im **Projektmappen-Explorer**mit der rechten Maustaste auf den Ordner **Datenquellen** , und klicken Sie anschließend auf **Neue Datenquelle** , um den **Datenquellen-Assistenten**zu starten.  
  
3.  Klicken Sie auf der Seite **Wählen Sie aus, wie die Verbindung definiert werden soll** auf **Eine Datenquelle basierend auf einer vorhandenen oder neuen Verbindung erstellen** , und klicken Sie dann auf **Neu** , um den **Verbindungs-Manager**zu öffnen.  
  
     Neue Verbindungen werden im Verbindungs-Manager erstellt. Wählen Sie im Verbindungs-Manager einen Anbieter aus, und geben Sie dann die von diesem Anbieter verwendeten Verbindungszeichenfolgeneigenschaften an, um eine Verbindung mit den zugrunde liegenden Daten herzustellen. Welche Informationen hier genau erforderlich sind, hängt vom ausgewählten Anbieter ab. Im Allgemeinen gehören hierzu ein Server oder eine Dienstinstanz, Angaben zur Anmeldung am Server oder an der Dienstinstanz, ein Datenbank- oder Dateiname sowie andere anbieterspezifische Einstellungen. Im weiteren Verlauf dieser Prozedur wird eine SQL Server-Datenbankverbindung angenommen.  
  
4.  Wählen Sie den [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework- oder den systemeigenen OLE DB-Anbieter aus, der für die Verbindung verwendet werden soll.  
  
     Der Standardanbieter für eine neue Verbindung ist der Native OLE DB\\[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Native Client-Anbieter. Dieser Anbieter wird dazu verwendet, mit OLE DB eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankmodulinstanz herzustellen. Für Verbindungen zu einer relationalen SQL Server-Datenbank ist die Verwendung von Native OLE DB\SQL Server Native Client 11.0 oftmals schneller als die Verwendung von alternativen Anbietern.  
  
     Sie können einen anderen Anbieter auswählen, um auf andere Datenquellen zuzugreifen. Eine Liste der von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]unterstützten Anbieter und relationalen Datenbanken finden Sie unter [Unterstützte Datenquellen &#40;SSAS – Mehrdimensional&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md).  
  
5.  Geben Sie die für den ausgewählten Anbieter angeforderten Informationen ein, um eine Verbindung mit der zugrunde liegenden Datenquelle herzustellen. Wenn Sie den Anbieter **Native OLE DB\SQL Server Native Client** ausgewählt haben, geben Sie die folgenden Informationen ein:  
  
    1.  **Servername** ist der Netzwerkname der Datenbankmodulinstanz. Er kann als IP-Adresse, NETBIOS-Name des Computers oder als vollqualifizierter Domänenname angegeben werden. Wenn der Server als benannte Instanz installiert ist, müssen Sie den Instanznamen beinhalten (z. B. \<Computername >\\< Instancename\>).  
  
    2.  **Am Server anmelden** gibt an, wie die Verbindung authentifiziert wird. **Windows-Authentifizierung verwenden** verwendet die Windows-Authentifizierung. Mit**SQL Server-Authentifizierung verwenden** wird eine Datenbank-Benutzeranmeldung für eine Windows Azure SQL-Datenbank- oder SQL Server-Instanz angegeben, die eine Authentifizierung im gemischten Modus unterstützt.  
  
        > [!IMPORTANT]  
        >  Der Verbindungs-Manager umfasst das Kontrollkästchen **Kennwort speichern** für Verbindungen, die die SQL Server-Authentifizierung verwenden. Obwohl das Kontrollkästchen immer sichtbar ist, wird es nicht immer verwendet.  
        >   
        >  Zu den Bedingungen, unter denen Analysis Services dieses Kontrollkästchen nicht verwendet, gehört das Aktualisieren oder Verarbeiten der relationalen SQL Server-Daten, die in der aktiven Analysis Services-Datenbank verwendet wird. Unabhängig davon, ob Sie das Kontrollkästchen **Kennwort speichern**deaktivieren oder aktivieren, verschlüsselt Analysis Services stets das Kennwort und speichert es. Das Kennwort wird verschlüsselt und sowohl in ABF-Dateien (*.abf) als auch Datendateien gespeichert. Dieses Verhalten ist darauf zurückzuführen, dass Analysis Services keinen sitzungsbasierten Kennwortspeicher auf dem Server unterstützt.  
        >   
        >  Dieses Verhalten gilt nur für Datenbanken, die a) auf einer Analysis Services-Serverinstanz vorhanden sind und b) die SQL Server-Authentifizierung verwenden, um relationale Daten zu aktualisieren oder zu verarbeiten. Es gilt nicht für Datenquellenverbindungen, die Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] einrichten und die nur für die Dauer einer Sitzung verwendet werden. Obwohl ein bereits gespeichertes Kennwort nicht entfernt werden kann, können Sie jedoch andere Anmeldeinformationen oder die Windows-Authentifizierung verwenden, um die Benutzerinformationen zu überschreiben, die derzeit in der Datenbank gespeichert sind.  
  
    3.  **Datenbanknamen eingeben oder auswählen** oder **Datenbankdatei anfügen** wird verwendet, um die Datenbank anzugeben.  
  
    4.  Klicken Sie auf der linken Seite des Dialogfelds auf **Alle** , um weitere Einstellungen für diese Verbindung, einschließlich aller Standardeinstellungen für diesen Anbieter, anzuzeigen.  
  
    5.  Nehmen Sie für die Umgebung geeignete Änderungen an den Einstellungen vor, und klicken Sie dann auf **OK**.  
  
         Die neue Verbindung wird im Bereich **Datenverbindung** der Seite **Wählen Sie aus, wie die Verbindung definiert werden soll** des Datenquellen-Assistenten angezeigt.  
  
6.  Klicken Sie auf **Weiter**.  
  
7.  Geben Sie unter **Identitätswechselinformationen**die Windows-Anmeldeinformationen oder die Benutzeridentität an, die Analysis Services beim Herstellen einer Verbindung mit der externen Datenquelle verwendet. Wenn Sie die Datenbankauthentifizierung verwenden, werden diese Einstellungen für Verbindungszwecke ignoriert.  
  
     Richtlinien zum Auswählen einer Identitätswechseloption ändern sich in Abhängigkeit davon, wie Sie die Datenquelle verwenden. Bei Verarbeitungstasks muss der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dienst im Sicherheitskontext seines Dienstkontos oder eines angegebenen Benutzerkontos ausgeführt werden, wenn eine Verbindung mit einer Datenquelle hergestellt wird.  
  
    -   Verwenden Sie**Bestimmter Windows-Benutzername und bestimmtes Kennwort** , um einen eindeutigen Satz von Anmeldeinformationen mit den niedrigsten Privilegien anzugeben.  
  
    -   Verwenden Sie die Option**Dienstkonto verwenden** , um die Daten mit der Dienstidentität zu verarbeiten.  
  
     Das angegebene Konto muss über Leseberechtigungen für die Datenquelle verfügen.  
  
8.  Klicken Sie auf **Weiter**.  Geben Sie unter **Assistenten abschließen**einen Datenquellennamen ein, oder verwenden Sie den Standardnamen. Der Standardname entspricht dem Namen der in der Verbindung angegebenen Datenbank. Im Bereich **Vorschau** wird die Verbindungszeichenfolge für die neue Datenquelle angezeigt.  
  
9. Klicken Sie auf **Fertig stellen**.  Die neue Datenquelle wird im Projektmappen-Explorer im Ordner **Datenquellen** angezeigt.  
  
##  <a name="bkmk_connection"></a> Erstellen einer Datenquelle mit einer vorhandenen Verbindung  
 Wenn Sie ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt verwenden, kann die Datenquelle basierend auf einer vorhandenen Datenquelle in der Projektmappe oder basierend auf einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt erstellt werden. Der Datenquellen-Assistent bietet mehrere Optionen zum Erstellen des Datenquellenobjekts, darunter die Verwendung einer vorhandenen Verbindung in demselben Projekt.  
  
-   Das Erstellen einer  Datenquelle basierend auf einer vorhandenen Datenquelle in der Projektmappe ermöglicht es Ihnen, eine Datenquelle zu erstellen, die mit der bestehenden Datenquelle synchronisiert ist. Wenn ein Build des Projekts, das diese neue Datenquelle enthält, erstellt wird, werden die Datenquelleneinstellungen der zugrunde liegenden Datenquelle verwendet.  
  
-   Das Erstellen einer Datenquelle basierend auf einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt ermöglicht es Ihnen, im aktuellen Projekt auf ein anderes [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt der Projektmappe zu verweisen. Die neue Datenquelle verwendet den MSOLAP.3-Anbieter, wobei die **Data Source** - und **Initial Catalog** -Eigenschaften aus den **TargetServer** - und **TargetDatabase** -Eigenschaften des ausgewählten Projekts abgerufen werden. Diese Funktion ist bei Projektmappen hilfreich, bei denen mehrere [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekte zur Verwaltung von Remotepartitionen verwendet werden, da für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Quell- und Zieldatenbanken wechselseitig abgeglichene Datenquellen zur Unterstützung von Speicher- und Verarbeitungsvorgängen auf der Remotepartition erforderlich sind.  
  
 Wenn Sie auf ein Datenquellenobjekt verweisen, können Sie dieses Objekt nur in dem Objekt oder Projekt bearbeiten, auf das verwiesen wurde. Es ist nicht möglich, die Verbindungsinformationen in dem Datenquellenobjekt zu bearbeiten, das den Verweis enthält. Änderungen an den Verbindungsinformationen in dem Objekt oder Projekt, auf das verwiesen wird, werden in der neuen Datenquelle angezeigt, wenn sie erstellt wird. Die Informationen zur Verbindungszeichenfolge, die in der Datenquellendatei (.ds) des Projekts vorkommen, werden synchronisiert, sobald Sie das Projekt erstellen oder den Verweis im Datenquellen-Designer entfernen.  
  
##  <a name="bkmk_ConnectionString"></a> Anzeigen oder Bearbeiten von Verbindungseigenschaften  
 Die Verbindungszeichenfolge wird auf Grundlage der Eigenschaften formuliert, die Sie im Datenquellen-Designer oder im Datenquellen-Assistenten auswählen. Die Verbindungszeichenfolge und weitere Eigenschaften können Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]anzeigen.  
  
 **So bearbeiten Sie die Verbindungszeichenfolge**  
  
1.  Doppelklicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]im Projektmappen-Explorer auf ein Datenquellenobjekt.  
  
2.  Klicken Sie auf **Bearbeiten**und dann im linken Navigationsbereich auf **Alles** .  
  
3.  Das Eigenschaftenraster wird angezeigt; es enthält verfügbare Eigenschaften des Datenanbieters, den Sie verwenden. Weitere Informationen zu diesen Eigenschaften finden Sie in der Produktdokumentation des Anbieters.  Informationen zum systemeigenen SQL Server-Client finden Sie unter [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Wenn die Projektmappe über mehrere Datenquellenobjekte verfügt und Sie die Verbindungszeichenfolge zentral verwalten möchten, können Sie die aktuelle Datenquelle so konfigurieren, dass sie auf das andere Datenquellenobjekt verweist.  
  
 Ein *Datenquellenverweis* ist eine Zuordnung zu einem anderen Projekt bzw. einer anderen Datenquelle von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in derselben Projektmappe. Verweise stellen eine Möglichkeit zur Synchronisierung von Datenquellen zwischen Objekten in einer Projektmappe dar. Die Verbindungszeichenfolgeninformationen werden synchronisiert, sobald Sie das Projekt erstellen. Um die Verbindungszeichenfolge für eine Datenquelle zu ändern, die auf ein anderes Objekt verweist, müssen Sie die Verbindungszeichenfolge des Objekts ändern, auf das verwiesen wird.  
  
 Sie können den Verweis entfernen, indem Sie das Kontrollkästchen deaktivieren. Dadurch wird die Synchronisierung zwischen den Objekten beendet, und Sie können die Verbindungszeichenfolge in der Datenquelle ändern.  
  
##  <a name="bkmk_multipleDS"></a> Hinzufügen mehrerer Datenquellen zu einem Modell  
 Sie können mehrere Datenquellenobjekte erstellen, um Verbindungen mit zusätzlichen Datenquellen zu unterstützen. Jede Datenquelle muss Spalten aufweisen, die zur Erstellung von Beziehungen verwendet werden können.  
  
> [!NOTE]  
>  Wenn mehrere Datenquellen definiert sind und von mehreren Quellen über eine einzelne Abfrage Daten abgefragt werden, beispielsweise für eine Schneeflockendimension, muss eine Datenquelle definiert werden, die Remoteabfragen mithilfe von **OpenRowset**unterstützt. In der Regel ist dies eine Microsoft SQL Server-Datenquelle.  
  
 Für die Verwendung mehrerer Datenquellen gelten die folgenden Anforderungen:  
  
-   Legen Sie eine Datenquelle als primäre Datenquelle fest. Die primäre Datenquelle ist diejenige, die zum Erstellen einer Datenquellensicht verwendet wurde.  
  
-   Eine primäre Datenquelle muss die **OpenRowset** -Funktion unterstützen.  Weitere Informationen zu dieser Funktion in SQL Server finden Sie unter <xref:Microsoft.SqlServer.TransactSql.ScriptDom.TSqlTokenType.OpenRowSet>.  
  
 Gehen Sie folgendermaßen vor, um Daten von mehreren Datenquellen zu kombinieren:  
  
1.  Erstellen Sie die Datenquellen im Modell.  
  
2.  Erstellen Sie mithilfe einer relationalen SQL Server-Datenbank als Datenquelle eine Datenquellensicht. Dies ist die primäre Datenquelle.  
  
3.  Klicken Sie unter Verwendung der soeben erstellten Datenquellensicht im Datenquellensicht-Designer mit der rechten Maustaste auf eine beliebige Stelle im Arbeitsbereich, und wählen Sie **Tabellen hinzufügen/entfernen**aus.  
  
4.  Wählen Sie die zweite Datenquelle aus, und wählen Sie dann die Tabellen aus, die Sie hinzufügen möchten.  
  
5.  Suchen Sie die hinzugefügte Tabelle, und wählen Sie sie aus. Klicken Sie mit der rechten Maustaste auf die Tabelle, und wählen Sie **Neue Beziehung**aus. Wählen Sie die Quell- und Zielspalten aus, die übereinstimmende Daten enthalten.  
  
## <a name="see-also"></a>Siehe auch  
 [Unterstützte Datenquellen &#40;SSAS – Mehrdimensional&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)   
 [Datenquellsichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
