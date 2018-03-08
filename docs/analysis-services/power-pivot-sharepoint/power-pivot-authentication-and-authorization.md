---
title: Power Pivot-Authentifizierung und Autorisierung | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 48230cc0-4037-4f99-8360-dadf4bc169bd
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 691bf8b3fd2e26a3f906c88fbc8ceb840b636f6c
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="power-pivot-authentication-and-authorization"></a>Power Pivot-Authentifizierung und -Autorisierung
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Bereitstellung, die innerhalb einer SharePoint 2010-Farm ausgeführt wird, verwendet das von den SharePoint-Servern bereitgestellte Authentifizierungssubsystem und Autorisierungsmodell. Die SharePoint-Sicherheitsinfrastruktur erstreckt sich auch auf [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Inhalte und -Vorgänge, da sämtliche [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-bezogenen Inhalte in SharePoint-Inhaltsdatenbanken gespeichert und alle [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-bezogenen Vorgänge von freigegebenen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Diensten in der Farm ausgeführt werden. Benutzer, die eine Arbeitsmappe mit [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten anfordern, werden mit einer SharePoint-Benutzeridentität authentifiziert, die auf deren Windows-Benutzeridentität basiert. Anzeigeberechtigungen für die Arbeitsmappe bestimmen, ob die Anforderung gewährt oder verweigert wird.  
  
 Da die Integration mit Excel Services für Self-Service-Datenanalysen erforderlich ist, sollten Ihnen zum Sichern eines [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Servers auch die Sicherheitsfunktionen von Excel Services vertraut sein. Wenn ein Benutzer eine PivotTable abfragt, die über eine Datenverbindung zu [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten verfügt, leiten die Excel Services eine Datenverbindungsanforderung zum Laden der Daten an einen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Server in der Farm weiter. Aufgrund der Interaktion zwischen den Servern sollten Sie wissen, wie Sie Sicherheitseinstellungen für beide Server konfigurieren.  
  
 Klicken Sie auf die folgenden Links, um bestimmte Abschnitte in diesem Thema zu lesen:  
  
 [Windows-Authentifizierung unter Verwendung der Anmeldungsanforderung im klassischen Modus](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md#bkmk_auth)  
  
 [Power Pivot-Vorgänge, die eine Benutzerautorisierung erfordern](#UserConnections)  
  
 [SharePoint-Berechtigungen für Power Pivot-Datenzugriff](#Permissions)  
  
 [Excel Services – Sicherheitsüberlegungen für Power Pivot-Arbeitsmappen](#excel)  
  
##  <a name="bkmk_auth"></a> Windows-Authentifizierung unter Verwendung der Anmeldungsanforderung im klassischen Modus  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint unterstützt eine eingeschränkte Anzahl der Authentifizierungsoptionen, die in SharePoint verfügbar sind. Von den verfügbaren Authentifizierungsoptionen wird nur die Windows-Authentifizierung für eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Bereitstellung unterstützt. Außerdem muss die Webanwendung, über die die Anmeldung erfolgt, für den klassischen Modus konfiguriert sein.  
  
 Die Windows-Authentifizierung ist erforderlich, weil das Analysis Services-Datenmodul in einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Bereitstellung nur die Windows-Authentifizierung unterstützt. Excel Services stellt über den MSOLAP OLE DB-Anbieter Verbindungen mit Analysis Services her. Dabei wird die Identität eines Windows-Benutzers verwendet, der über NTLM oder das Kerberos-Protokoll authentifiziert wurde.  
  
 Durch die zweite Anforderung, dass für die Webanwendung die Authentifizierung im klassischen Modus verwendet werden soll, wird sichergestellt, dass der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Webdienst funktioniert. Der Webdienst ist eine Komponente, die auf einem Web-Front-End ausgeführt wird und die HTTP-Umleitung an einen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Server in der Farm vornimmt. Während der Webdienst bei der Dienst-zu-Dienst-Kommunikation als eine Ansprüche unterstützende Anwendung fungiert, trifft dies für Datenverbindungsanforderungen, die an einen freigegebenen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienst in der Farm umgeleitet werden, nicht zu. Anforderungen zum Laden von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten werden nur für authentifizierte Verbindungen unterstützt, die unter Verwendung einer Windows-Identität von IIS gesendet werden. Die Anmeldung im klassischen Modus in der Webanwendung ermöglicht eine erfolgreiche Verbindung vom [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Webdienst zu freigegebenen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Diensten in der Farm.  
  
 Obwohl die Anmeldung im klassischen Modus für das allgemeinere Datenzugriffsszenario (in dem [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten aus derselben bereitstellenden Excel-Arbeitsmappe extrahiert werden) nicht erforderlich ist, verwenden Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint nicht mit SharePoint-Webanwendungen, die zur Verwendung anderer Authentifizierungsanbieter konfiguriert sind. Dies führt zu einem Verbindungsfehler, wenn Benutzer eine Verbindung mit [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen als externe Datenquelle herstellen möchten.  
  
 Ohne klassische Modusanmeldung sind die folgenden Anforderungstypen, die vom [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Webdienst behandelt werden, fehlerhaft:  
  
-   Jede Anforderung für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten, die von außerhalb der Farm stammt (z.B. Erstellen eines Berichts im Berichts-Designer oder Berichts-Generator, wo die Datenquelle eine SharePoint-URL für eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe ist)  
  
-   Farminterne Anforderungen von einer Clientanwendung oder einem Bericht, die bzw. der die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe als externe Datenquelle verwendet (z.B. Erstellen einer Arbeitsmappe in der Excel-Desktopanwendung, wobei als Datenquelle eine zweite veröffentlichte Excel-Arbeitsmappe mit [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten verwendet wird)  
  
### <a name="how-to-check-the-authentication-provider-for-your-application"></a>So überprüfen Sie den Authentifizierungsanbieter für eine Anwendung  
 Aktivieren Sie bei der Erstellung einer neuen Webanwendung auf der Seite „Neue Webanwendung erstellen“ die Option **Klassischer Authentifizierungsmodus** .  
  
 Für vorhandene Webanwendungen befolgen Sie die folgenden Anweisungen, um sicherzustellen, dass die Webanwendung für die Verwendung der Windows-Authentifizierung konfiguriert sind.  
  
1.  Klicken Sie in der Zentraladministration unter Anwendungsverwaltung auf **Webanwendungen verwalten**.  
  
2.  Wählen Sie die Webanwendung aus.  
  
3.  Klicken Sie auf **Authentifizierungsanbieter**.  
  
4.  Überprüfen Sie, ob es einen Anbieter für jede Zone gibt und die Standardzone auf Windows festgelegt ist.  
  
##  <a name="UserConnections"></a> Power Pivot-Vorgänge, die eine Benutzerautorisierung erfordern  
 Die SharePoint-Autorisierung wird ausschließlich für alle Zugriffsebenen für die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Abfrage- und -Datenverarbeitung verwendet.  
  
 Das rollenbasierte Analysis Services-Autorisierungsmodell wird nicht unterstützt. Für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten steht keine rollenbasierte Autorisierung auf Zellen-, Zeilen- oder Tabellenebene zur Verfügung. Sie können nicht verschiedene Teile der Arbeitsmappe sichern, um ausgewählten Benutzern Zugriff auf vertrauliche Daten in der Datenquelle zu gewähren oder zu verweigern. Eingebettete [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten sind für Benutzer mit Anzeigeberechtigungen für die Excel-Arbeitsmappe in einer SharePoint-Bibliothek uneingeschränkt verfügbar.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint nimmt in den folgenden Fällen die Identität eines SharePoint-Benutzers an:  
  
-   Abfragen an PivotTables oder PivotCharts, die über Datenverbindungen mit einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbank verfügen. Dabei stellt eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung im Namen eines Benutzers Verbindungen mit einer bestimmten freigegebenen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstinstanz her, die die Daten verarbeitet.  
  
-   Das Laden von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten aus dem Zwischenspeicher oder einer Bibliothek, wenn die Daten andernfalls nicht verfügbar sind. Wenn eine Datenverbindungsanforderung für eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenquelle ausgegeben wird, die noch nicht in das System geladen wurde, nimmt die [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] -Instanz die Identität eines SharePoint-Benutzers an, um die Datenquelle aus einer Inhaltsbibliothek abzurufen und in den Arbeitsspeicher zu laden.  
  
-   Datenaktualisierungsvorgänge, bei denen eine aktualisierte Kopie der Datenquelle in der Arbeitsmappe in einer Inhaltsbibliothek gespeichert wird. In diesem Fall wird ein aktuelles Protokoll für den Vorgang unter Verwendung des Benutzernamens und des Kennworts ausgeführt, der/das aus einer Zielanwendung in Secure Store Service abgerufen wird. Die Anmeldeinformationen können das Konto der unbeaufsichtigten [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenaktualisierung oder die Anmeldeinformationen sein, die zusammen mit dem Datenaktualisierungszeitplan bei seiner Erstellung gespeichert wurden. Weitere Informationen finden Sie unter [Konfigurieren gespeicherter Anmeldeinformationen für die Power Pivot-Datenaktualisierung (Power Pivot für SharePoint)](http://msdn.microsoft.com/en-us/987eff0f-bcfe-4bbd-81e0-9aca993a2a75) und [Konfigurieren des Power Pivot-Kontos für die unbeaufsichtigte Datenaktualisierung (Power Pivot für SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493).  
  
##  <a name="Permissions"></a> SharePoint-Berechtigungen für Power Pivot-Datenzugriff  
 Die Veröffentlichung, Verwaltung und Sicherung einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe wird nur durch die SharePoint-Integration unterstützt. SharePoint-Server bieten Authentifizierungs- und Autorisierungssubsysteme an, die den berechtigten Zugang zu Daten sicherstellen. Szenarios für die sichere Bereitstellung einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe außerhalb einer SharePoint-Farm werden nicht unterstützt.  
  
 Der Benutzerzugriff auf [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten ist auf dem Server schreibgeschützt und erfordert mindestens Anzeigeberechtigungen. Über Teilnahmeberechtigungen wird das Hinzufügen und Bearbeiten der Datei erlaubt. Änderungen an [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten erfordern, dass Sie die Arbeitsmappe in eine Excel-Desktopanwendung herunterladen, in der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für Excel installiert ist. Über die Teilnahmeberechtigungen für die Datei wird ermittelt, ob der Benutzer berechtigt ist, die Datei lokal herunterzuladen und Änderungen in SharePoint zurückzuspeichern.  
  
 Dies bedeutet, dass der effektive Berechtigungssatz für den Benutzerzugriff auf [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten durch die Berechtigungsstufen Mitwirken und Anzeigen definiert wird. Andere Berechtigungsstufen können insofern verwendet werden, dass sie die gleichen Berechtigungen wie Mitwirken und Nur anzeigen beinhalten. (Beispiel: Da Lesen die Berechtigung Nur anzeigen einschließt, verfügt ein Benutzer, dem Lesen zugewiesen wird, über die gleiche Zugriffsebene wie ein Nur anzeigen.)  
  
 In der folgenden Tabelle werden die Berechtigungsebenen zusammengefasst, die den Zugriff auf [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten- und -Servervorgänge bestimmen:  
  
|Berechtigungsstufe|Lässt diese Tasks zu|  
|----------------------|------------------------|  
|Farm- oder Dienstadministrator|Installieren, Aktivieren und Konfigurieren von Diensten und Anwendungen<br /><br /> Verwenden des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Verwaltungsdashboards und Anzeigen von Administratorberichten.|  
|Vollzugriff|Aktivieren der Integration von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Features auf Websitesammlungsebene.<br /><br /> Erstellen einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Katalogbibliothek.<br /><br /> Erstellen einer Datenfeedbibliothek|  
|Mitwirken|Hinzufügen, Bearbeiten, Löschen und Herunterladen von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen.<br /><br /> Konfigurieren der Datenaktualisierung<br /><br /> Erstellen neuer Arbeitsmappen und Berichte auf Grundlage von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen auf einer SharePoint-Website.<br /><br /> Erstellen von Datendienstdokumenten in einer Datenfeedbibliothek|  
|Lesen|Zugriff auf [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen als externe Datenquelle, wobei die Arbeitsmappen-URL explizit in einem Verbindungsdialogfeld eingegeben wird (z.B. im Datenverbindungs-Assistenten von Microsoft Excel).|  
|Nur anzeigen|Anzeigen von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen<br /><br /> Anzeigen des Datenaktualisierungsverlaufs<br /><br /> Herstellen einer Verbindung mit einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe auf einer SharePoint-Website, um die Daten auf andere Weise erneut zu nutzen<br /><br /> Laden Sie eine Momentaufnahme der Arbeitsmappe herunter. Die Momentaufnahme ist eine statische Kopie der Daten, ohne Slicer, Filter, Formeln oder Datenverbindungen. Der Inhalt der Momentaufnahme entspricht den Zellenwerten im Browserfenster.|  
  
##  <a name="excel"></a> Excel Services – Sicherheitsüberlegungen für Power Pivot-Arbeitsmappen  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Die serverseitige Verarbeitung von Abfragen ist eng mit Excel Services verbunden. Die Produktintegration beginnt auf Dokumentebene, auf der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen als Excel-Arbeitsmappendateien (.xlsx) angesehen werden, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten enthalten oder darauf verweisen. Es gibt keine separate Dateierweiterung für eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe.  
  
 Wenn eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe auf einer SharePoint-Website geöffnet wird, liest Excel Services die eingebettete [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenverbindungszeichenfolge und leitet die Anforderung an den lokalen OLE DB-Anbieter für SQL Server Analysis Services weiter. Der Anbieter übergibt die Verbindungsinformationen daraufhin an einen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Server in der Farm. Damit die Anforderungen ungehindert zwischen den zwei Servern ausgetauscht werden können, muss Excel Services so konfiguriert werden, dass die für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint erforderlichen Einstellungen verwendet werden.  
  
 In Excel Services werden sicherheitsbezogene Konfigurationseinstellungen für Speicherorte, Datenanbieter und Datenverbindungsbibliotheken angegeben, die als vertrauenswürdig eingestuft wurden. In der folgenden Tabelle werden die Einstellungen beschrieben, die den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenzugriff aktivieren oder verbessern. Wenn eine Einstellung hier nicht aufgeführt wird, hat sie keine Auswirkungen auf [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Serververbindungen. Schritt-für-Schritt-Anweisungen zum Angeben dieser Einstellungen finden Sie im Abschnitt „Aktivieren von Excel Services“ unter [Anfängliche Konfiguration (Power Pivot für SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146).  
  
> [!NOTE]  
>  Die meisten sicherheitsbezogenen Einstellungen gelten für vertrauenswürdige Speicherorte. Wenn Sie die Standardwerte beibehalten oder andere Werte für verschiedene Websites verwenden möchten, können Sie einen zusätzlichen vertrauenswürdigen Speicherort für Websites mit [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten erstellen und dann die folgenden Einstellungen nur für diese Websites konfigurieren. Weitere Informationen finden Sie unter [Erstellen eines vertrauenswürdigen Speicherorts für Power Pivot-Websites in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
|Bereich|Einstellung|Description|  
|----------|-------------|-----------------|  
|Webanwendung|Windows-Authentifizierungsanbieter|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] konvertiert ein von Excel Services abgerufenes Anspruchstoken in eine Windows-Benutzeridentität. Jede Webanwendung, die Excel Services als Ressource verwendet, muss für die Verwendung des Anbieters der Windows-Authentifizierung konfiguriert sein.|  
|Vertrauenswürdiger Speicherort|Speicherorttyp|Für diesen Wert muss **Microsoft SharePoint Foundation**festgelegt werden. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Server rufen eine Kopie der XLSX-Datei ab und laden sie auf einen Analysis Services-Server in der Farm hoch. Der Server kann nur XLSX-Dateien aus einer Inhaltsbibliothek abrufen.|  
||Externe Daten zulassen|Für diesen Wert muss **Vertrauenswürdige Datenverbindungsbibliotheken und eingebettete Verbindungen**festgelegt werden. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Datenverbindungen sind in die Arbeitsmappe eingebettet. Wenn Sie keine eingebetteten Verbindungen zulassen, können Benutzer den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Cache anzeigen, aber eine Interaktion mit [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten kann nicht stattfinden.|  
||Beim Aktualisieren warnen|Dieser Wert sollte deaktiviert werden, wenn Sie Arbeitsmappen und Berichte mithilfe des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Katalogs speichern. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Der Katalog umfasst eine Dokumentvorschaufunktion, die am besten funktioniert, wenn Beim Öffnen aktualisieren und Beim Aktualisieren warnen deaktiviert sind.|  
|Vertrauenswürdige Datenanbieter|MSOLAP.4<br /><br /> MSOLAP.5|MSOLAP.4 ist standardmäßig eingeschlossen, aber der Zugriff auf [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten erfordert, dass der MSOLAP.4-Anbieter der SQL Server 2008 R2-Version entspricht.<br /><br /> MSOLAP.5 wird mit der [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Version von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint installiert.<br /><br /> Entfernen Sie diese Anbieter nicht aus der Liste vertrauenswürdiger Datenanbieter. In einigen Fällen kann es erforderlich sein, zusätzliche Kopien dieses Anbieters auf weiteren SharePoint-Servern in der Farm zu installieren. Weitere Informationen finden Sie unter [Installieren des OLE DB-Anbieters für Analysis Services auf SharePoint-Servern](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859).|  
|Vertrauenswürdige Datenverbindungsbibliotheken|Optional.|Sie können Office Data Connection-Dateien (ODC) in [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen verwenden. Wenn Sie Verbindungsinformationen mithilfe von ODC-Dateien für lokale [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen bereitstellen, können Sie der Bibliothek die gleichen ODC-Dateien hinzufügen.|  
|Benutzerdefinierte Funktionsassembly|Nicht verfügbar.|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint ignoriert benutzerdefinierte Funktionsassemblys, die Sie für Excel Services erstellen und bereitstellen. Wenn Sie benutzerdefinierte Assemblys für ein bestimmtes Verhalten benötigen, beachten Sie, dass die von Ihnen erstellten benutzerdefinierten Funktionen bei der Verarbeitung von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Abfragen nicht verwendet werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von Power Pivot-Dienstkonten](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [Konfigurieren des PowerPivot für die unbeaufsichtigte Datenaktualisierung Konto (PowerPivot für SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)   
 [Erstellen eines vertrauenswürdigen Speicherorts für PowerPivot-Websites in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)   
 [PowerPivot-Sicherheitsarchitektur](http://go.microsoft.com/fwlink/?linkID=220970)  
  
  
