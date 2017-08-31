---
title: Verwalten von Berichtsteilen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 41947b4c-8ecf-4e4f-b30e-66e1d6692b74
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 310cad57050dba44c5303b78ea33e5b3f42d309c
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="managing-report-parts"></a>Verwalten von Berichtsteilen
  Berichtsteile können in paginierten Berichten von mehreren Benutzern und in mehreren Berichten wiederverwendet werden. Benutzer können nach Berichtsteilen auf dem Server suchen und sie einem Bericht hinzufügen.  Benutzer können auch über Updates am Berichtsteil auf dem Server informiert werden und neue Versionen eines Berichtsteils erneut veröffentlichen. Diese Berichterstellungsaktionen können durch Sicherheitsberechtigungen der Reporting Services beeinflusst und gesteuert werden.  In diesem Thema werden Eigenschaften und Verhaltensweisen von Berichtsteilen erörtert, nachdem diese auf dem Server gespeichert wurden.  
  
## <a name="managing-report-parts"></a>Verwalten von Berichtsteilen  
 Für einen Berichtsserver im einheitlichen Modus können Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Webportal und für einen Berichtsserver im integrierten SharePoint-Modus Anwendungsseiten verwenden, um Berichtsteile zu verwalten.  
  
### <a name="server-side-interaction-and-search"></a>Serverseitige Interaktion und Suche  
 Berichtsteile können entweder im einheitlichen Modus oder im integrierten SharePoint-Modus auf einem Berichtsserver veröffentlicht werden. Benutzer können die Berichtsteilkatalog-Funktion in einer Berichterstellungsanwendung wie [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Berichts-Generator verwenden, um Berichtsteile zu suchen und ihren Berichten hinzuzufügen. Wenn ein Benutzer einen Berichtsteil sucht, durchsucht die Suchfunktion unabhängig vom Modus, für den der Server installiert wurde, den Berichtsserverkatalog.  
  
 Wenn Berichtsteile von einer Berichterstellungsanwendung wie Berichts-Generator auf einem Berichtsserver im integrierten SharePoint-Modus veröffentlicht werden, wird auch der Berichtsserverkatalog aktualisiert, und die Suchergebnisse aus dem Berichtsteilkatalog entsprechen exakt dem neuen oder aktualisierten Berichtsteil.  
  
#### <a name="directly-uploading-report-parts-to-a-sharepoint-folder"></a>Direktes Hochladen von Berichtsteilen in einen SharePoint-Ordner  
 Wenn ein Berichtsteil direkt in einen SharePoint-Dokumentordner hochgeladen (und nicht von einer Berichterstellungsanwendung veröffentlicht) wird, wird der Berichtsserverkatalog nicht zusätzlich aktualisiert. Daher wird der hochgeladene Berichtsteil bei Suchen im Berichtsteilkatalog nicht gefunden. Um besser zu gewährleisten, dass die SharePoint-Ordner und der Berichtsserverkatalog synchronisiert bleiben, können Sie die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktion zum Synchronisieren von Dateien auf dem SharePoint-Server aktivieren. Weitere Informationen finden Sie unter [Aktivieren der Funktion zur Synchronisierung der Berichtsserverdateien in der SharePoint-Zentraladministration](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md).  
  
 Die Dateien können auch durch das Aufrufen einiger Reporting Services-Verwaltung-APIs wie GetProperties und SetProperties synchronisiert werden.  
  
### <a name="organizing-and-moving-report-parts"></a>Organisieren und Verschieben von Berichtsteilen  
 Sie sollten im Voraus planen, wie Ihr Team Berichtsteile, gemeinsam genutzte Datasets und Datenquellen nutzen und organisieren wird. Obwohl Sie sie zu einem späteren Zeitpunkt verschieben können, kann es Probleme geben.  
  
#### <a name="native-mode-report-server"></a>Berichtsserver im einheitlichen Modus  
 Wenn Sie einen Berichtsteil auf einem Berichtsserver im einheitlichen Modus in einen anderen Ordner auf dem gleichen Server verschieben, können Berichterstellungsanwendungen weiterhin Updates des Berichtsteils suchen oder herunterladen. Dies liegt daran, dass der Server die eindeutigen ComponentID verwendet. Wenn der Berichtsteil jedoch in einen Ordner verschoben wird, für den ein Benutzer keine Berechtigungen besitzt, wird der Berichtsteil bei der Benutzersuche nicht gefunden, und für Berichte des Benutzers wird keine Updatebenachrichtigung gesendet, wenn der Berichtsteil aktualisiert wird.  
  
#### <a name="report-server-in-sharepoint-integrated-mode"></a>Berichtsserver im integrierten SharePoint-Modus  
 Die Verschiebung von Berichtsteilen in eine andere Dokumentbibliothek oder einen anderen Ordner hat die gleichen Auswirkungen wie das direkte Hochladen auf einen SharePoint-Serve: Der Berichtsserverkatalog wird nicht synchronisiert. Um dieses zu vermeiden, aktivieren Sie die Funktion Report Server File Sync auf dem SharePoint-Server.  
  
 Unterordner bilden eine Ausnahme. Wenn Sie einen Berichtsteil manuell in einen Unterordner verschieben, wird er bei einer Suche im Berichtsteilkatalog weiterhin gefunden, da Unterordner bei der Suche immer berücksichtigt werden.  
  
### <a name="report-server-catalog-properties"></a>Eigenschaften von Berichtsserverkatalogen  
 In der folgenden Tabelle wird erläutert, in welcher Weise sich vorhandenen Felder im Berichtsserverkatalog auf einen Berichtsteil und auf neue Felder beziehen, die dem Katalog für Berichtsteile hinzugefügt wurden. Diese Felder stehen im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Webportal und in SharePoint-Bibliotheken sowie in Berichterstellungsanwendungen wie dem Berichts-Generator zur Verfügung.  
  
 (*) Neu in dieser Version.  
  
|Eigenschaft|Description|Berichtsteil<br /><br /> Katalogsuchkriterien|  
|--------------|-----------------|---------------------------------------------|  
|Name|Dies ist eines der Kriterien, nach denen ein Benutzer im Berichtsteilkatalog suchen kann.|Ja|  
|Description|Möglicherweise möchten Sie Berichtsteilnamen auf eine Weise organisieren, die es für Benutzer einfacher macht, sie im Katalog zu finden. Beispielweise können Sie nach einer Beschreibung suchen, die mit "Vertrieb>>" beginnt, um alle Berichtsteile zu finden, die sich auf Vertriebsdaten und -präsentationen beziehen.|Ja|  
|CreatedBy|Die ID des Benutzers, der den Berichtsteil zur Berichtsserver-Datenbank hinzugefügt hat. Das genaue Format hängt von der Authentifizierungsmethode ab. Einige Authentifizierungsmethoden führen z. B. dazu, dass der vollständige Domänen-\Benutzername im CreatedBy-Feld und dem ModifiedBy-Feld angezeigt wird.|Ja|  
|CreationDate|Das Datum, an dem der Berichtsteil ursprünglich erstellt wurde.<br /><br /> Dies ist eines der Kriterien, nach denen ein Benutzer im Berichtsteilkatalog suchen kann.|Ja|  
|ModifiedBy|ModifiedBy ist der Name des Benutzers, der den Berichtsteil zuletzt geändert hat.|Ja|  
|ModifiedDate|Das Datum, an dem der Berichtsteil zuletzt auf dem Server geändert wurde.<br /><br /> Dieses Feld wird als Teil der Logik verwendet, mit der serverseitige Updates an einem Berichtsteil ermittelt werden. Weitere Informationen finden Sie in der Beschreibung der ComponentID weiter unten in dieser Tabelle.|Ja|  
|SubType (*)|SubType ist eine Zeichenfolge, die die Art des Berichtsteil angibt, nach dem gesucht werden soll, z.B. "Tablix" oder "Chart".|Ja|  
|ComponentID (*)|ComponentID ist ein eindeutiger Bezeichner für den Berichtsteil. Dieses Feld wurde dem Katalog neu hinzugefügt und ist sowohl auf dem Server als auch in Berichterstellungsanwendungen wie Berichts-Generator sichtbar.<br /><br /> Dieses Feld wird von Clientanwendungen bei der Suche nach Berichtsteilupdates auf dem Server verwendet. Die Clientanwendung durchsucht den Server nach ComponentIDs, die sich im aktuellen clientseitigen Bericht befinden. Wenn eine ComponentID-Übereinstimmung gefunden wird, wird das ModifiedDate dann mit dem clientseitigen SyncDate des Berichtselements verglichen.|N0|  
  
## <a name="controlling-access-to-report-parts"></a>Steuern des Zugriffs auf Berichtsteile  
 In den folgenden Tabellen werden die Standardrollenzuweisungen und die verschiedenen Aktionen beschrieben. Die Namen der Rollenzuweisungen unterscheiden sich abhängig vom verwendeten Berichtsserver.  
  
### <a name="server-in-native-mode"></a>Server im einheitlichen Modus  
  
|Aktionen|Rollen|  
|-------------|-----------|  
|Hinzufügen, Löschen, Bearbeiten von Elementeigenschaften, Verwalten der Sicherheit und Herunterladen von Berichtsteilen|Inhalts-Manager<br /><br /> Meine Berichte|  
|Hinzufügen, Löschen und Herunterladen von Berichtsteilen|Verleger|  
|Suchen und Wiederverwenden|Browser<br /><br /> Berichts-Generator|  
  
### <a name="server-in-sharepoint-integrated-mode"></a>Server im integrierten SharePoint-Modus  
  
|Aktionen|Rolle|  
|-------------|----------|  
|Hinzufügen, Löschen, Bearbeiten von Elementeigenschaften, Verwalten der Sicherheit und Herunterladen von Berichtsteilen|Vollzugriff|  
|Hinzufügen, Löschen, Bearbeiten von Elementeigenschaften und Herunterladen von Berichtsteilen|Entwerfen<br /><br /> Mitwirken|  
|Suchen und Wiederverwenden|Lesen<br /><br /> Nur anzeigen|  
  
### <a name="security-considerations"></a>Überlegungen zur Sicherheit  
  
-   Wenn Berichtsteildefinitionen in einem Bericht wiederverwendet werden, werden sie zusammen mit der identifizierenden Komponenten-ID vollständig in die Berichtsdefinition kopiert. Wenn ein Berichtsteil auf dem Server aktualisiert wird, können Benutzer wählen, die aktualisierten Berichtsteile zu ihrem Bericht herunterzuladen. Die heruntergeladenen Updates sind ebenfalls vollständige Kopien des Berichtsteils in der Berichtsdefinition und ersetzen die vorhandene Version des Berichtsteils, die im Bericht enthalten war.  
  
    > [!IMPORTANT]  
    >  In jedem dieser Schritte sollte sichergestellt werden, dass die in Berichten wiederverwendeten Berichtsteile von vertrauenswürdigen Speicherorten bzw. Benutzern stammen.  
  
-   Für Berichtsteile werden die gleichen Berechtigungsrichtlinien wie für den vorhandenen Elementtyp für Ressourcen verwendet. Hinsichtlich der Vererbung von Sicherheitsberechtigungen wird innerhalb eines Ordners nicht zwischen herkömmlichen Ressourcenelementen und Berichtsteilen unterschieden. Beispielsweise erbt der Berichtsteil die gleiche Berechtigungsrichtlinie wie die Bilder im selben Ordner. Wenn diese Unterscheidung erforderlich ist, kann die Sicherheit auf Elementebene für die gewünschten Berichtsteile konfiguriert werden. Andernfalls können Sie Berichtsteile in separaten Ordnern speichern, für die die benötigten Berechtigungen konfiguriert wurden.  
  
## <a name="see-also"></a>Siehe auch  
 [Berichtsteile und Datasets in Berichts-Generator](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [Berichtsinhaltsverwaltung für Server &#40; SSRS im einheitlichen Modus &#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Problembehandlung bei Berichtsteilen (Berichts-Generator und SSRS)](http://msdn.microsoft.com/en-us/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [Berichtsteile im Berichts-Designer &#40; SSRS &#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md)  
  
  
