---
title: Verbindungszeichenfolgen-Eigenschaften (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 29a00a41-5b0d-44b2-8a86-1b16fe507768
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: cd41219341488f64487b831ec42c50869552a660
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="connection-string-properties-analysis-services"></a>Verbindungszeichenfolgen-Eigenschaften (Analysis Services)
  In diesem Thema sind Eigenschaften für Verbindungszeichenfolgen dokumentiert, die Sie u. U. in einem der Designer- oder Verwaltungstools festlegen bzw. die in Verbindungszeichenfolgen von Clientanwendungen verwendet werden, die eine Verbindung mit Analysis Services-Daten herstellen und diese abfragen. In diesem Dokument wird daher nur auf einen Teilbereich der verfügbaren Eigenschaften eingegangen. Die vollständige Liste umfasst zahlreiche Server- und Datenbankeigenschaften, mit denen eine Verbindung unabhängig davon, wie die Instanz oder Datenbank auf dem Server konfiguriert ist, an spezifische Anwendungen angepasst werden kann.  
  
 Entwickler, die benutzerdefinierte Verbindungszeichenfolgen im Anwendungscode erstellen, finden in der API-Dokumentation für ADOMD.NET-Clients eine ausführlichere Liste: <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>  
  
 Die in diesem Thema beschriebenen Eigenschaften werden von den Analysis Services-Clientbibliotheken, ADOMD.NET, AMO und dem OLE DB-Anbieter für Analysis Services verwendet. Die meisten Eigenschaften für Verbindungszeichenfolgen können mit allen drei Clientbibliotheken verwendet werden. Auf Ausnahmen wird in der Beschreibung hingewiesen.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Häufig verwendete Verbindungsparameter](#bkmk_common)  
  
 [Authentifizierung und Sicherheit](#bkmk_auth)  
  
 [Spezielle Parameter](#bkmk_special)  
  
 [Für künftige Verwendung vorbehalten](#bkmk_reserved)  
  
 [Exemplarische Verbindungszeichenfolgen](#bkmk_examples)  
  
 [In Analysis Services verwendete Formate für Verbindungszeichenfolgen](#bkmk_supportedstrings)  
  
 [Verschlüsseln von Verbindungszeichenfolgen](#bkmk_encrypt)  
  
> [!NOTE]  
>  Falls Sie versehentlich zweimal dieselbe Eigenschaft festlegen, wird die letzte Eigenschaft in der Verbindungszeichenfolge verwendet.  
  
 Weitere Informationen dazu, wie eine Analysis Services-Verbindung in vorhandenen Microsoft-Anwendungen angegeben wird, finden Sie unter [Herstellen einer Verbindung von Clientanwendungen &#40;Analysis Services&#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md).  
  
##  <a name="bkmk_common"></a> Häufig verwendete Verbindungsparameter  
 In der folgenden Tabelle sind Eigenschaften beschrieben, die am häufigsten beim Erstellen einer Verbindungszeichenfolge verwendet werden.  
  
|Eigenschaft|Description|Beispiel|  
|--------------|-----------------|-------------|  
|**Data Source** oder **DataSource**|Gibt die Serverinstanz an. Diese Eigenschaft ist für alle Verbindungen erforderlich. Gültige Werte sind der Netzwerkname oder die IP-Adresse des Servers, local oder localhost für lokale Verbindungen, eine URL, wenn der Server für den HTTP- oder HTTPS-Zugriff konfiguriert ist, oder der Name einer lokalen Cubedatei (CUB).|`Data source=AW-SRV01` für die Standardinstanz und den Standardport (TCP 2383).<br /><br /> `Data source=AW-SRV01$Finance:8081` für eine benannte Instanz ($Finance) und einen festen Port<br /><br /> `Data source=AW-SRV01.corp.Adventure-Works.com` für einen vollqualifizierten Domänennamen, vorausgesetzt, die Standardinstanz und der Standardport werden verwendet.<br /><br /> `Data source=172.16.254.1` für eine IP-Adresse des Servers unter Umgehung des DNS-Serverlookups. Eignet sich für die Behandlung von Verbindungsproblemen.|  
|**Initial Catalog** oder **Catalog**|Gibt den Namen der Analysis Services-Datenbank an, mit der eine Verbindung hergestellt werden soll. Die Datenbank muss unter Analysis Services bereitgestellt werden, und Sie müssen berechtigt sein, eine Verbindung damit herzustellen. Diese Eigenschaft ist für AMO-Verbindungen optional, für ADOMD.NET jedoch erforderlich.|`Initial catalog=AdventureWorks2016`|  
|**Anbieter**|Gültige Werte sind MSOLAP. \<Version >, wobei \<Version > 4, 5, 6 oder 7 ist.<br /><br /> –   MSOLAP.4 wurde in SQL Server 2008 und erneut in SQL Server 2008 R2 veröffentlicht (der Dateiname lautet „msolap100.dll“ für SQL Server 2008 und 2008 R2)<br />–   MSOLAP.5 wurde in SQL Server 2012 veröffentlicht (der Dateiname ist „msolap110.dll“)<br />–   MSOLAP.6 wurde in SQL Server 2014 veröffentlicht (der Dateiname ist „msolap1200.dll“)<br />–   MSOLAP.7 wurde in SQL Server 2016 veröffentlicht (der Dateiname ist „msolap130.dll“)<br /><br /> Diese Eigenschaft ist optional. Standardmäßig wird die aktuelle Version des OLE DB-Anbieters von den Clientbibliotheken aus der Registrierung gelesen. Sie müssen diese Eigenschaft nur festlegen, wenn Sie eine bestimmte Datenanbieterversion benötigen, beispielsweise um eine Verbindung mit einer SQL Server 2012-Instanz herzustellen.<br /><br /> MSOLAP.4 wurde sowohl mit SQL Server 2008 als auch mit SQL Server 2008 R2 bereitgestellt. Die 2008 R2-Version unterstützt [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen und muss auf SharePoint-Servern manchmal manuell installiert werden. Um zwischen diesen Versionen zu unterscheiden, überprüfen Sie die Buildnummer in den Dateieigenschaften des Anbieters unter Programme\Microsoft Analysis Services\AS OLEDB\10. Klicken Sie mit der rechten Maustaste auf „msolap110.dll“, und wählen Sie **Eigenschaften**. Klicken Sie auf **Details**. Zeigen Sie die Dateiversionsinformationen an. Die Version sollte 10.50. enthalten. \<Buildnumber > für SQL Server 2008 R2. Weitere Informationen finden Sie unter [Installieren des OLE DB-Anbieters für Analysis Services auf SharePoint-Servern](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859) und [Für Analysis Services-Verbindungen verwendete Datenanbieter](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md).|`Provider=MSOLAP.7` wird für Verbindungen verwendet, die die SQL Server 2016-Version des OLE DB-Anbieters für Analysis Services erfordern.|  
|**Cube**|Cubename oder Perspektivenname. Eine Datenbank kann mehrere Cubes und Perspektiven enthalten. Wenn mehrere Ziele möglich sind, schließen Sie den Cube- oder Perspektivennamen in die Verbindungszeichenfolge ein.|`Cube=SalesPerspective` veranschaulicht, dass Sie mithilfe der Cube-Eigenschaft einer Verbindungszeichenfolge entweder den Namen eines Cubes oder den einer Perspektive angeben können.|  
  
##  <a name="bkmk_auth"></a> Authentifizierung und Sicherheit  
 In diesem Abschnitt werden Verbindungszeichenfolgen-Eigenschaften in Zusammenhang mit der Authentifizierung und Verschlüsselung erörtert. Analysis Services nutzt ausschließlich die Windows-Authentifizierung, Sie können jedoch Eigenschaften für die Verbindungszeichenfolge festlegen, um einen bestimmten Benutzernamen und ein zugehöriges Kennwort zu übergeben.  
  
 Die Eigenschaften sind in alphabetischer Reihenfolge aufgeführt.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**EffectiveUserName**|Wird verwendet, wenn auf dem Server die Identität eines Endbenutzers angenommen werden muss. Geben Sie das Konto im Format "Domäne\Benutzer" an. Zur Verwendung dieser Eigenschaft muss der Aufrufer über Administratorberechtigungen in Analysis Services verfügen. Weitere Informationen zur Verwendung dieser Eigenschaft in einer Excel-Arbeitsmappe in SharePoint finden Sie unter [Verwenden von "EffectiveUserName" der Analysis Services in SharePoint Server 2013](http://go.microsoft.com/fwlink/?LinkId=311905). Die Verwendung dieser Eigenschaft mit Reporting Services wird unter [Verwenden von "EffectiveUserName" für den Identitätswechsel in SSAS](http://go.microsoft.com/fwlink/?LinkId=301385)veranschaulicht.<br /><br /> **EffectiveUserName** wird in [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Installation verwendet, um Informationen zur Verwendung zu erfassen. Die Benutzeridentität wird für den Server bereitgestellt, damit Ereignisse oder Fehler in Zusammenhang mit der Benutzeridentität in den Protokolldateien aufgezeichnet werden können. Bei [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]wird sie nicht zu Autorisierungszwecken verwendet.|  
|**Encrypt Password**|Gibt an, ob ein lokales Kennwort zur Verschlüsselung lokaler Cubes verwendet werden soll. Gültige Werte sind True oder False. Der Standardwert ist False.|  
|**Encryption Password**|Das zum Entschlüsseln eines verschlüsselten lokalen Cubes verwendete Kennwort. Der Standardwert ist leer. Dieser Wert muss vom Benutzer explizit festgelegt werden.|  
|**Impersonation Level**|Gibt die Identitätswechselebene an, die der Server beim Annehmen der Identität des Clients verwenden kann. Gültige Werte sind:<br /><br /> -   Anonymous. Der Client ist gegenüber dem Server anonym. Der Serverprozess kann keine Informationen zum Client abrufen und keinen Identitätswechsel für den Client durchführen.<br />-   Identify. Der Serverprozess kann die Clientidentität abrufen. Der Server kann zu Autorisierungszwecken die Clientidentität annehmen, aber nicht als Client auf Systemobjekte zugreifen.<br />-   Impersonate. Dies ist der Standardwert. Die Clientidentität kann nur angenommen werden, wenn die Verbindung hergestellt wird, nicht aber bei jedem Aufruf.<br />-   Delegate. Der Serverprozess kann einen Identitätswechsel für den Sicherheitskontext des Clients durchführen, während er im Auftrag des Clients handelt. Der Serverprozess kann auch ausgehende Aufrufe zu anderen Servern durchführen, während er im Auftrag des Clients handelt.|  
|**Integrierte Sicherheit**|Die Windows-Identität des Aufrufers wird verwendet, um eine Verbindung mit Analysis Services herzustellen. Gültige Werte sind ein leerer Wert, SSPI und BASIC.<br /><br /> **Integrated Security**=**SSPI** ist der Standardwert für TCP-Verbindungen und ermöglicht die NTLM-, Kerberos- oder anonyme Authentifizierung. Ein leerer Wert ist der Standardwert für HTTP-Verbindungen.<br /><br /> Bei Verwendung von **SSPI**muss **ProtectionLevel** auf einen der folgenden Werte festgelegt werden: **Connect**, **PktIntegrity**, **PktPrivacy**.|  
|**Persist Encrypted**|Legen Sie diese Eigenschaft fest, wenn das Datenquellenobjekt vertrauliche Authentifizierungsinformationen, wie ein Kennwort, für die Clientanwendung in verschlüsselter Form persistent speichern muss. Standardmäßig werden Authentifizierungsinformationen nicht persistent gespeichert.|  
|**Persist Security Info**|Gültige Werte sind True und False. Wenn diese Eigenschaft auf True festgelegt ist, können Sicherheitsinformationen, wie die Benutzeridentität oder das Kennwort, die zuvor in der Verbindungszeichenfolge angegeben wurden, von der Verbindung abgerufen werden, nachdem sie hergestellt wurde. Der Standardwert ist False.|  
|**Schutzebene**|Bestimmt die für die Verbindung verwendete Sicherheitsstufe. Gültige Werte sind:<br /><br /> -   **None**. Nicht authentifizierte oder anonyme Verbindungen. Führt keine Authentifizierung für die an den Server gesendeten Daten aus.<br />-   **Connect**. Authentifizierte Verbindungen. Führt nur eine Authentifizierung aus, wenn der Client eine Beziehung zu einem Server herstellt.<br />-   **Pkt Integrity**. Verschlüsselte Verbindungen. Stellt sicher, dass alle Daten vom Client empfangen und während der Übertragung nicht geändert wurden.<br />-   **Pkt Privacy**. Signierte Verschlüsselung, wird nur für XMLA unterstützt. Stellt sicher, dass alle Daten vom Client empfangen und während der Übertragung nicht geändert wurden und schützt die Daten, indem sie verschlüsselt werden.<br /><br /> Weitere Informationen finden Sie unter [Establishing Secure Connections in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections.md).|  
|**Roles**|Geben Sie eine durch Trennzeichen getrennte Liste vordefinierter Rollen an, um eine Verbindung mit einem Server oder einer Datenbank unter Verwendung der von der jeweiligen Rolle vermittelten Berechtigungen herzustellen. Wenn diese Eigenschaft weggelassen wird, werden alle Rollen verwendet, sodass die effektiven Berechtigungen einer Kombination aus allen Rollen entsprechen. Wird die Eigenschaft auf einen leeren Wert festgelegt (beispielsweise Roles=' '), weist die Clientverbindung keine Rollenmitgliedschaft auf.<br /><br /> Ein Administrator, der diese Eigenschaft verwendet, stellt eine Verbindung mit den Berechtigungen dieser Rolle her. Falls die Rolle keine ausreichenden Berechtigungen gewährt, können einige Befehle einen Fehler verursachen.|  
|**SSPI**|Gibt explizit an, welches Sicherheitspaket für die Clientauthentifizierung verwendet werden soll, wenn **Integrated Security** auf **SSPI**festgelegt ist. SSPI unterstützt mehrere Pakete, Sie können mithilfe dieser Eigenschaft jedoch auch ein bestimmtes Paket angeben. Gültige Werte sind Negotiate, Kerberos, NTLM und Anonymous User. Wenn diese Eigenschaft nicht festgelegt wird, sind alle Pakete für die Verbindung verfügbar.|  
|**Use Encryption for Data**|Verschlüsselt Datenübertragungen. Gültige Werte sind True und False.|  
|**User ID**=…; **Password**=|**User ID** und **Password** werden zusammen verwendet. Von Analysis Services wird die durch diese Anmeldeinformationen angegebene Benutzeridentität angenommen. Bei einer Analysis Services-Verbindung werden Anmeldeinformationen nur in der Befehlszeile angegeben, wenn der Server für den HTTP-Zugriff konfiguriert ist und Sie die Standardauthentifizierung anstelle der integrierten Sicherheit für das virtuelle IIS-Verzeichnis angegeben haben. Bei direkter Verbindung mit dem Server werden die Parameter **UserID** und **Password** der Verbindungszeichenfolge ignoriert, und die Verbindung wird über den Kontext des angemeldeten Benutzers hergestellt. <br /><br />Der Benutzername und das Kennwort müssen Anmeldeinformationen einer Windows-Identität, entweder eines lokalen oder Domänenbenutzerkontos, darstellen. Beachten Sie, dass **User ID** ein eingebettetes Leerzeichen enthält. Andere Aliase für diese Eigenschaft sind **UserName** (ohne Leerzeichen) und **UID**. Der Alias für **Password** ist **PWD**.|  
  
##  <a name="bkmk_special"></a> Spezielle Parameter  
 In diesem Abschnitt werden die übrigen Parameter für Verbindungszeichenfolgen beschrieben. Sie werden verwendet, um ein spezifisches, für eine Anwendung erforderliches Verbindungsverhalten zu gewährleisten.  
  
 Die Eigenschaften sind in alphabetischer Reihenfolge aufgeführt.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**Application Name**|Legt den Namen der Anwendung fest, die der Verbindung zugeordnet ist. Dieser Wert kann bei der Überwachung von Ablaufverfolgungsereignissen hilfreich sein, insbesondere wenn mehrere Anwendungen auf dieselben Datenbanken zugreifen. Wenn Sie einer Verbindungszeichenfolge beispielsweise Application Name='test' hinzufügen, wird 'test' in einer SQL Server Profiler-Ablaufverfolgung angezeigt, wie aus folgendem Bildschirmfoto ersichtlich:<br /><br /> ![SSAS_AppNameExcample](../../analysis-services/instances/media/ssas-appnameexcample.gif "SSAS_AppNameExcample")<br /><br /> Zu den Aliasen dieser Eigenschaft gehören **sspropinitAppName**und **AppName**. Weitere Informationen finden Sie unter [Verwenden des Application Name-Parameters beim Herstellen einer Verbindung mit SQL Server](http://go.microsoft.com/fwlink/?LinkId=301699).|  
|**AutoSyncPeriod**|Legt fest, wie häufig der Client- und Servercache synchronisiert werden (in Millisekunden). ADOMD.NET unterstützt das Clientcaching für häufig verwendete Objekte, die sich minimal auf die Arbeitsspeicherauslastung auswirken. Auf diese Weise wird die Anzahl von Roundtrips zum Server reduziert. Der Standardwert beträgt 10000 Millisekunden (oder zehn Sekunden). Beim Wert NULL oder 0 ist die automatische Synchronisierung deaktiviert.|  
|**Character Encoding**|Definiert, wie Zeichen in der Anforderung codiert werden. Gültige Werte sind Default oder UTF-8 (diese sind gleichwertig) sowie UTF-16.| 
|**CommitTimeout**|Eine XMLA-Eigenschaft. Bestimmt, wie lange in Milliskunden die Commitphase eines derzeit laufenden Befehls wartet, bevor ein Rollback eintritt. Wenn größer als 0, wird der Wert der entsprechenden CommitTimeout-Eigenschaft in der Serverkonfiguration überschrieben. |   
|**CompareCaseSensitiveStringFlags**|Passt Zeichenfolgenvergleiche für ein angegebenes Gebietsschema an, bei denen die Groß-/Kleinschreibung beachtet wird. Weitere Informationen zum Festlegen dieser Eigenschaft finden Sie unter [CompareCaseSensitiveStringFlags-Eigenschaft](http://msdn.microsoft.com/library/aa237459\(v=sql.80\).aspx).|  
|**Compression Level**|Wenn **TransportCompression** XPRESS lautet, können Sie den Komprimierungsgrad festlegen. Gültige Werte sind 0 bis 9, wobei mit 0 die geringste und 9 die höchste Komprimierung erzielt wird. Ein höherer Komprimierungsgrad wirkt sich negativ auf die Leistung aus. Der Standardwert ist 0.|  
|**Connect Timeout**|Bestimmt die maximale Zeitspanne (in Sekunden), in der der Client versucht, eine Verbindung herzustellen, bevor ein Timeout eintritt. Wenn innerhalb dieses Zeitraums keine Verbindung hergestellt wird, stellt der Client die Verbindungsversuche ein und generiert einen Fehler.|  
|**MDX Compatibility**|Diese Eigenschaft soll ein einheitliches MDX-Verhalten für Anwendungen gewährleisten, die MDX-Abfragen ausgeben. Da Excel MDX-Abfragen zum Auffüllen und Berechnen einer mit Analysis Services verbundenen PivotTable verwendet, wird diese Eigenschaft auf 1 festgelegt, um sicherzustellen, dass Platzhalterelemente in unregelmäßigen Hierarchien in einer PivotTable sichtbar sind. Gültige Werte sind 0, 1 und 2.<br /><br /> Bei 0 und 1 werden Platzhalterelemente verfügbar gemacht, bei 2 nicht. Bei einem leeren Wert wird 0 angenommen.|  
|**MDX Missing Member Mode=Error**|Gibt an, ob fehlende Elemente in MDX-Anweisungen ignoriert werden. Gültige Werte sind Default, Error und Ignore. Bei Default wird ein vom Server definierter Wert verwendet. Error generiert einen Fehler, wenn ein Element nicht vorhanden ist. „Ignore“ gibt an, dass fehlende Werte ignoriert werden sollen.|  
|**Optimize Response**|Eine Bitmaske, die angibt, welche der folgenden Optimierungen für Abfrageantworten aktiviert sind.<br /><br /> – 0x01: NormalTupleSet wird verwendet (Standardeinstellung).<br />– 0x02: wird bei leeren Slicern verwendet.|  
|**Packet Size**|Eine Netzwerkpaketgröße (in Bytes) zwischen 512 und 32.767. Die standardmäßige Netzwerkpaketgröße beträgt 4.096 Bytes.|  
|**Protocol Format**|Legt das Format der an den Server gesendeten XML fest. Gültige Werte sind Default, XML oder Binary. Als Protokoll wird XMLA verwendet. Sie können angeben, dass die XML komprimiert (Standardeinstellung), im unformatierten XML-Format oder in einem Binärformat gesendet wird. Bei Verwendung des Binärformats werden XML-Elemente und -Attribute codiert und verkleinert. Die Komprimierung stellt ein proprietäres Format dar, bei dem die Größe von Anforderungen und Antworten weiter reduziert wird. Die Komprimierung und Binärformate werden verwendet, um Datenübertragungsanforderungen und -antworten zu beschleunigen.<br /><br /> Bei Verwendung eines binären oder komprimierten Formats muss eine Clientbibliothek für die Verbindung verwendet werden. Der OLE DB-Anbieter kann Anforderungen und Antworten im Binär- oder komprimierten Format formatieren. AMO und ADOMD.NET formatieren Anforderungen als Text, akzeptieren jedoch Antworten im binären oder komprimierten Format.<br /><br /> Diese Verbindungszeichenfolgen-Eigenschaft entspricht den Serverkonfigurationseinstellungen **EnableBinaryXML** und **EnableCompression** .|  
|**Real Time Olap**|Legen Sie diese Eigenschaft so fest, dass das Caching umgangen wird, wodurch alle Partitionen aktiv auf Abfragebenachrichtigungen lauschen. Diese Eigenschaft wird standardmäßig nicht festgelegt.|  
|**Safety Options**|Legt die Sicherheitsstufe für benutzerdefinierte Funktionen und Aktionen fest. Gültige Werte sind 0, 1, 2. In einer Excel-Verbindung lautet diese Eigenschaft Safety Options=2. Ausführliche Informationen zu dieser Option finden Sie unter <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>.|  
|**SQLQueryMode**|Gibt an, ob SQL-Abfragen Berechnungen enthalten. Gültige Werte sind Data, Calculated und IncludeEmpty. Data bedeutet, dass keine Berechnungen zulässig sind. Bei Calculated sind Berechnungen zulässig. IncludeEmpty lässt Berechnungen zu und ermöglicht die Rückgabe leerer Zeilen in den Abfrageergebnissen.|  
|**Timeout**|Gibt an, wie viele Sekunden die Clientbibliothek auf die Ausführung eines Befehls wartet, bevor ein Fehler generiert wird.|  
|**Transport Compression**|Definiert, wie die Kommunikation zwischen Client und Server komprimiert wird, wenn die Komprimierung über die **Protocol Format** -Eigenschaft festgelegt wird. Gültige Werte sind Default, None, Compressed und **gzip**. Für TCP wird standardmäßig keine Komprimierung und für HTTP **gzip** verwendet. None gibt an, dass keine Komprimierung verwendet wird. Bei Compressed wird die XPRESS-Komprimierung (SQL Server 2008 und höher) verwendet. **gzip** ist nur für HTTP-Verbindungen gültig, in denen die HTTP-Anforderung „Accept-Encoding=gzip“ enthält.|  
|**UseExistingFile**|Wird beim Herstellen einer Verbindung mit einem lokalen Cube verwendet. Diese Eigenschaft gibt an, ob der lokale Cube überschrieben wird. Gültige Werte sind True oder False. Bei True muss die Cubedatei vorhanden sein. Die vorhandene Datei ist das Ziel der Verbindung. Bei False wird die Cubedatei überschrieben.|  
|**VisualMode**|Legen Sie diese Eigenschaft fest, um zu steuern, wie Elemente aggregiert werden, wenn Dimensionssicherheit angewendet wird.<br /><br /> Für Cubedaten, die jeder Benutzer einsehen darf, ist die Aggregation aller Elemente sinnvoll, da alle am Gesamtergebnis beteiligten Werte sichtbar sind. Wenn Sie jedoch Dimensionen anhand von Benutzeridentitäten filtern oder einschränken, kann die Anzeige eines auf allen Elementen basierenden Ergebnisses (das sowohl eingeschränkte als auch zulässige Werte in einem einzigen Gesamtergebnis kombiniert) verwirrend sein oder mehr Informationen offen legen, als gewünscht.<br /><br /> Um anzugeben, auf welche Weise Elemente bei Verwendung von Dimensionssicherheit aggregiert werden, können Sie diese Eigenschaft auf True festlegen, um nur zulässige Werte in die Aggregation aufzunehmen, oder auf False, um eingeschränkte Werte aus dem Gesamtwert auszuschließen.<br /><br /> Wird die Eigenschaft für die Verbindungszeichenfolge festgelegt, gilt dieser Wert auf Cube- oder Perspektivenebene. Innerhalb eines Modells können Sie sichtbare Gesamtwerte auf einer präziseren Ebene steuern.<br /><br /> Gültige Werte sind 0, 1 und 2.<br /><br /> – Der Standardwert ist 0. Das Standardverhalten entspricht derzeit dem Wert 2. Dabei enthalten Aggregationen Werte, die für den Benutzer ausgeblendet sind.<br />– Bei 1 werden ausgeblendete Werte vom Gesamtwert ausgeschlossen. Dies ist das Standardverhalten für Excel.<br />– 2 schließt ausgeblendete Werte in den Gesamtwert ein. Dies ist der Standardwert für den Server.<br /><br /> Zu den Aliasen dieser Eigenschaft gehören **Visual Total** oder **Default MDX Visual Mode**.|  
  
##  <a name="bkmk_reserved"></a> Für künftige Verwendung vorbehalten  
 Die folgenden Eigenschaften sind für Verbindungszeichenfolgen zulässig, in den aktuellen Versionen von Analysis Services jedoch nicht funktionsfähig.  
  
-   Authenticated User  
  
-   Cache Authentication  
  
-   Cache Mode (Die Verwendung dieser Eigenschaft wurde bereits in früheren Versionen untersucht, und obwohl deren Verwendung in manchen Blogbeiträgen möglicherweise empfohlen wird, sollten Sie die Eigenschaft nur festlegen, wenn Sie ausdrücklich vom Microsoft Support dazu aufgefordert werden.)  
  
-   Cache Policy  
  
-   Cache Ratio  
  
-   Cache Ratio2  
  
-   Dynamic Debug Limit  
  
-   Debug Mode  
  
-   Modus  
  
-   SQLCompatibility  
  
-   Use Formula Cache  
  
##  <a name="bkmk_examples"></a> Exemplarische Verbindungszeichenfolgen  
 In diesem Abschnitt wird die Verbindungszeichenfolge veranschaulicht, die Sie wahrscheinlich zur Einrichtung einer Analysis Services-Verbindung in häufig genutzten Anwendungen verwenden.  
  
 **Allgemeine Verbindungszeichenfolge**  
  
 Sie können eine mit der folgenden vergleichbare Verbindungszeichenfolge verwenden, wenn Sie eine Verbindung von Reporting Services konfigurieren.  
  
 `Data source=<servername>; initial catalog=<databasename>`  
  
 **Verbindungszeichenfolge in Excel**  
  
 In der standardmäßigen ADOMD.NET-Verbindungszeichenfolge in Excel werden der Datenanbieter, der Server, der Datenbankname und die integrierte Sicherheit von Windows angegeben. Der MDX-Kompatibilitätsgrad ist immer auf 1 festgelegt. Obwohl der Wert für die aktuelle Sitzung geändert werden kann, setzt Excel den Wert für den MDX-Kompatibilitätsgrad beim nächsten Öffnen der Datei auf 1 zurück.  
  
 `Provider=MSOLAP.5;Integrated Security=SSPI;Persist Security Info=True;Initial Catalog=Adventure Works DW 2008R2;Data Source=AW-SRV01;MDX Compatibility=1;Safety Options=2;MDX Missing Member Mode=Error`  
  
 Weitere Informationen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) und [Datenauthentifizierung für Excel Services in SharePoint Server 2013](http://go.microsoft.com/fwlink/?LinkId=296350).  
  
##  <a name="bkmk_supportedstrings"></a> In Analysis Services verwendete Formate für Verbindungszeichenfolgen  
 In diesem Abschnitt werden alle von Analysis Services unterstützten Verbindungszeichenfolgenformate aufgeführt. Mit Ausnahme von Verbindungen mit [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenbanken können Sie diese Verbindungszeichenfolgen in Anwendungen angeben, die eine Verbindung mit Analysis Services herstellen.  
  
 **Native (oder direkte) Verbindungen mit dem Server**  
  
 `Data Source=server[:port][\instance]` , wobei "port" und "\instance" optional sind. "Data Source=server1" öffnet z. B. eine Verbindung mit der Standardinstanz (und dem Standardport 2383) auf einem Server mit dem Namen "server1".  
  
 "Data Source=server1:port1" öffnet eine Verbindung mit einer Analysis Services-Instanz, die an Port "port1" auf "server1" ausgeführt wird.  
  
 "Data Source=server1\instance1" öffnet eine Verbindung mit SQL Browser (am Standardport 2382), löst den Port für die benannte Instanz "instance1" auf und öffnet dann die Verbindung mit diesem Analysis Services-Port.  
  
 "Data Source=server1:port1\instance1" öffnet eine Verbindung mit SQL Browser an "port1", löst den Port für die benannte Instanz "instance1" auf und öffnet dann die Verbindung mit diesem Analysis Services-Port.  
  
 **Lokale Cubeverbindungen (CUB-Dateien)**  
  
 `Data Source=<path>`, z.B. „Data Source=c:\temp\a.cub“  
  
 **HTTP(S)-Verbindungen mit „msmdpump.dll“**  
  
 `Data Source=<URL>`, wobei die URL die HTTP- oder HTTPS-Adresse des virtuellen IIS-Ordners ist, der „msmdpump.dll“ enthält. Weitere Informationen finden Sie unter [Configure HTTP Access to Analysis Services on Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
 **HTTP(S)-Verbindungen mit [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Arbeitsmappen (XLSX-, XLSB- oder XLSM-Dateien)**  
  
 `Data Source=<URL>`, wobei die URL der SharePoint-Pfad zu einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe ist, die in einer SharePoint-Bibliothek veröffentlicht wurde, Beispiel: `Data Source=http://localhost/Shared Documents/Sales.xlsx`.  
  
 **HTTP(S)-Verbindungen mit BI-Semantikmodell-Verbindungsdateien**  
  
 `Data Source=<URL>` , wobei die URL der SharePoint-Pfad zur BISM-Datei ist, Beispiel: `Data Source=http://localhost/Shared Documents/Sales.bism`.  
  
 **Eingebettete [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Verbindungen**  
  
 `Data Source=$Embedded$`, wobei $embedded$ ein Moniker ist, der auf ein eingebettetes [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Datenmodell in der Arbeitsmappe verweist. Diese Verbindungszeichenfolge wird intern erstellt und verwaltet. Ändern Sie sie nicht. Eingebettete Verbindungszeichenfolgen werden von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für Excel-Add-Ins auf Clientarbeitsstationen oder von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Instanzen in einer SharePoint-Farm aufgelöst.  
  
 **Lokaler Serverkontext in gespeicherten Analysis Services-Prozeduren**  
  
 `Data Source=*`, wobei * in die lokale Instanz aufgelöst wird.  
  
##  <a name="bkmk_encrypt"></a> Verschlüsseln von Verbindungszeichenfolgen  
 Analysis Services verwendet eigene Verschlüsselungsschlüssel für die Verschlüsselung von Verbindungszeichenfolgen. Ein selbstsigniertes Zertifikat wird nicht generiert.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verschlüsselt und speichert die Verbindungszeichenfolgen, die zum Herstellen einer Verbindung mit den zugehörigen Datenquellen verwendet werden. Wenn für die Verbindung zu einer Datenquelle ein Benutzername und ein Kennwort benötigt werden, können Sie [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] den Namen und das Kennwort gemeinsam mit der Verbindungszeichenfolge speichern oder den Namen und das Kennwort jedes Mal abfragen lassen, wenn das Herstellen einer Verbindung zur Datenquelle erforderlich ist. Wenn [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die Benutzerinformationen von Ihnen abfragt, müssen diese Informationen nicht gespeichert und verschlüsselt werden. Wenn Sie diese Informationen jedoch in der Verbindungszeichenfolge speichern, müssen diese Informationen verschlüsselt und gesichert werden.  
  
 Um die Verbindungszeichenfolgeninformationen zu verschlüsseln und zu schützen, verwendet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die Datenschutz-API.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwendet einen separaten Verschlüsselungsschlüssel zum Verschlüsseln der Verbindungszeichenfolgen-Informationen für jede [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erstellt diesen Schlüssel, wenn Sie eine Datenbank erstellen, und verschlüsselt die Informationen zur Verbindungszeichenfolge auf Grundlage des [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Startkontos. Beim Start von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] wird der verschlüsselte Schlüssel für jede Datenbank gelesen, entschlüsselt und gespeichert. Anschließend verwendet[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] den entsprechenden entschlüsselten Schlüssel zum Entschlüsseln der Verbindungszeichenfolgen-Informationen für die Datenquelle, wenn [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eine Verbindung mit einer Datenquelle herstellen muss.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren von HTTP-Zugriff auf Analysis Services unter Internetinformationsdienste &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)   
 [Konfigurieren von Analysis Services für die eingeschränkte Kerberos-Delegierung](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [Für Analysis Services-Verbindungen verwendete Datenanbieter](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md)   
 [Verbindung mit Analysis Services herstellen](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
