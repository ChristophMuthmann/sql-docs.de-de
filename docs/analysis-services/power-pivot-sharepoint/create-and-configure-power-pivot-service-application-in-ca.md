---
title: Erstellen und Konfigurieren von PowerPivot-Dienstanwendung in der Zertifizierungsstelle | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b2e5693e-4af3-453f-83f3-07481ab1ac6a
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 27d009450f9bdfac7eeff0f1bc9e1909d8968f01
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-and-configure-power-pivot-service-application-in-ca"></a>Erstellen und Konfigurieren von PowerPivot-Dienstanwendung in der Zertifizierungsstelle
  Eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung ist eine freigegebene Dienstinstanz des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdiensts. Jede Dienstanwendung verfügt über eine eigene Anwendungsidentität, Konfigurationseinstellungen, Eigenschaften und einen internen Datenspeicher.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Bestimmen, ob eine neue PowerPivot-Dienstanwendung erstellt werden muss](#determine)  
  
 [Erstellen einer PowerPivot-Dienstanwendung](#CreateApp)  
  
 [Konfigurieren der PowerPivot-Dienstanwendung](#ConfigApp)  
  
 [Zuweisen einer PowerPivot-Dienstanwendung zu einer Webanwendung](#AssignGSA)  
  
 [Bearbeiten von Eigenschaften für Dienstanwendungen](#EditGSA)  
  
##  <a name="determine"></a> Bestimmen, ob eine neue PowerPivot-Dienstanwendung erstellt werden muss  
 Eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Installation muss mindestens eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung in der Farm enthalten. Eine Dienstanwendung wird automatisch erstellt, wenn Sie das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Konfigurationstool zum Konfigurieren des Servers verwendet haben. Andernfalls müssen Sie in der Zentraladministration manuell eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung erstellen.  
  
 Beim Erstellen einer Dienstanwendung wird der Dienst verfügbar gemacht und die Datenbank der Dienstanwendung generiert. Abhängig von den beim Erstellen der Dienstanwendung ausgewählten Optionen wird der Standard-Dienstverbindungsgruppe eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstverbindung hinzugefügt. Alle SharePoint-Webanwendungen, die die Standard-Dienstverbindungsgruppe abonnieren, erhalten automatisch direkten Zugriff auf die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung.  
  
 Sie können mehrere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen erstellen. Obwohl eine Dienstanwendung für die meisten Bereitstellungsszenarien ausreichend ist, kann die Erstellung einer zusätzlichen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung in Betracht gezogen werden, falls folgende Geschäftsanforderungen bestehen:  
  
-   Verwenden unterschiedlicher Konten für unbeaufsichtigte [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenaktualisierungen für jede Anwendung.  
  
-   Verwenden unterschiedlicher Timeouts, Verwendungsverläufe und Schwellenwerte für Abfrageantwortberichte.  
  
-   Delegieren der Dienstverwaltung an unterschiedliche Personen. Ein Administrator sieht den Datenaktualisierungsverlauf, die Verwendungsdaten und andere Eigenschaften nur für die Anwendung, die er verwaltet. Es kann erforderlich sein, SharePoint-Webanwendungen zu isolieren, z.B. wenn Ihr Unternehmen ein Hostingdienst ist, der Datenisolation für die SharePoint-Webanwendungen garantieren muss, die unterschiedlichen Kunden gehören. In diesem Fall können Sie diese Isolationsanforderungen durch Erstellen separater [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen erfüllen. Stellen Sie dabei sicher, dass jeder Dienstadministrator nur die Konfigurationseinstellungen und die Eigenschaften für die Anwendung sieht, die er verwaltet.  
  
 Die Erstellung zusätzlicher Dienstanwendungen führt zu neuen Anforderungen beim Verwalten von Dienstzuordnungen. Sie müssen dann nämlich benutzerdefinierte Dienstzuordnungslisten für jede zusätzliche erstellte Dienstanwendung erstellen und verwenden.  
  
 Wenn kein bestimmter Grund für die Erstellung einer zusätzlichen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung vorliegt, sollten Sie eine einzige Dienstanwendung für alle Webanwendungen in der Farm verwenden.  
  
##  <a name="CreateApp"></a> Erstellen einer PowerPivot-Dienstanwendung  
  
1.  Klicken Sie in der Zentraladministration unter Anwendungsverwaltung auf **Dienstanwendungen verwalten**.  
  
2.  Klicken Sie im Menüband **Dienstanwendungen** auf **Neu**.  
  
3.  Wählen Sie **SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung** aus. Wenn dies nicht in der Liste angezeigt wird, wurde [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint nicht installiert oder nicht ordnungsgemäß konfiguriert.  
  
4.  Geben Sie auf der Seite **Neue [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung erstellen** einen Namen für die Anwendung ein. Der Standardwert ist PowerPivotServiceApplication\<Anzahl >. Wenn Sie mehrere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen erstellen, hilft ein aussagekräftiger Name anderen Administratoren, die Verwendung der Anwendung zu verstehen.  
  
5.  Erstellen Sie in Anwendungspool einen neuen Anwendungspool für die Anwendung (empfohlen). Wählen Sie ein verwaltetes Konto für den Anwendungspool aus, oder erstellen Sie es. Sie müssen ein Domänenbenutzerkonto angeben. Ein Domänenbenutzerkonto ermöglicht die Verwendung der in SharePoint verfügbaren Funktion Verwaltetes Konto, mit der Sie Kennwörter und Kontoinformationen zentral aktualisieren können. Domänenkonten sind auch erforderlich, wenn Sie beabsichtigen, die Bereitstellung auf zusätzlichen Dienstinstanzen, die unter der gleichen Identität ausgeführt werden, zu skalieren.  
  
6.  Der Standardwert unter **Datenbankserver**entspricht der SQL Server-Datenbankmodul-Instanz, die die Konfigurationsdatenbanken der Farm hostet. Sie können diesen Server verwenden oder einen anderen SQL Server auswählen.  
  
7.  In **Datenbankname**, der Standardwert ist PowerPivotServiceApplication1_\<Guid >. Sie müssen eine eindeutige Datenbank für jede [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung erstellen. Der Standardname für die Datenbank entspricht dem Standardnamen der Dienstanwendung. Wenn Sie einen eindeutigen Dienstanwendungsnamen eingegeben haben, verwenden Sie eine ähnliche Benennungskonvention für den Datenbanknamen, damit Sie sie zusammen verwalten können.  
  
8.  Der Standardwert unter **Datenbankauthentifizierung**lautet Windows-Authentifizierung. Wenn Sie **SQL-Authentifizierung**auswählen, finden Sie im SharePoint-Administratorhandbuch bewährte Methoden zur Verwendung dieses Authentifizierungstyps in einer SharePoint-Bereitstellung.  
  
9. Aktivieren Sie optional das Kontrollkästchen für **Proxy für diese [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung zur Standardproxygruppe der Farm hinzufügen**. . Dadurch wird der Standard-Dienstverbindungsgruppe die Dienstanwendungsverbindung hinzugefügt.  
  
     Sie müssen dieses Kontrollkästchen aktivieren, wenn Sie Ihre erste [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung erstellen. Es muss eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung in der Standardverbindungsgruppe vorhanden sein, um sicherzustellen, dass das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard ordnungsgemäß funktioniert.  
  
     Fügen Sie die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung nicht der Standardverbindungsgruppe hinzu, wenn bereits eine vorhanden ist. Das Hinzufügen mehrerer Einträge des gleichen Dienstanwendungstyps ist keine unterstützte Konfiguration und könnte Fehler verursachen. Wenn Sie zusätzliche Dienstanwendungen erstellen, nehmen Sie sie nicht in die Standardverbindungsgruppe auf. Fügen Sie sie stattdessen benutzerdefinierten Listen hinzu.  
  
     Weitere Informationen zu Dienstzuordnungen finden Sie unter [Verbinden einer PowerPivot-Dienstanwendung mit einer SharePoint-Webanwendung in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md).  
  
10. Klicken Sie auf **OK.** Der Dienst wird zusammen mit anderen verwalteten Diensten in der Dienstanwendungsliste der Farm angezeigt.  
  
##  <a name="ConfigApp"></a> Konfigurieren der PowerPivot-Dienstanwendung  
 Eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung wird unter Verwendung einer Standardkonfiguration erstellt. Für die meisten Szenarien werden die Standardeinstellungen empfohlen. Diese sollten nur geändert werden, falls Antwortzeiten zu lang sind oder Verbindungen getrennt werden, oder wenn Sie unterschiedliche [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstkonfigurationen für bestimmte SharePoint-Webanwendungen verwenden.  
  
1.  Klicken Sie in der Zentraladministration unter Anwendungsverwaltung auf **Dienstanwendungen verwalten**.  
  
     In der Liste der Dienstanwendungen sollte die gerade erstellte und benannte Dienstanwendung angezeigt werden. Der Standardname ist **PowerPivotServiceApplication1**.  
  
2.  Klicken Sie auf die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung. Dadurch wird das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard geöffnet.  
  
3.  Klicken Sie in der Liste **Aktionen** oben rechts im Dashboard auf **Einstellungen für Dienstanwendung konfigurieren**.  
  
4.  Erhöhen oder verringern Sie den Wert unter **Timeout für das Laden der Datenbank**, um die Dauer zu ändern, die der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienst auf eine Antwort von der SQL Server Analysis Services-Instanz ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) wartet, an die der Dienst eine Anforderung zum Laden von Daten weitergeleitet hat. Da die Übertragung sehr großer Datasets einige Zeit dauern kann, müssen Sie genügend Zeit vorsehen, damit die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstinstanz die Excel-Arbeitsmappe abrufen und die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten zur Abfrageverarbeitung in eine Analysis Services-Instanz verschieben kann. Da [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten ungewöhnlich umfangreich sein können, ist der Standardwert 30 Minuten.  
  
5.  Erhöhen oder verringern Sie den Wert unter **Timeout für Verbindungspool**, um die Dauer in Minuten zu ändern, die eine Datenverbindung im Leerlauf geöffnet gehalten wird. Der Standardwert ist 30 Minuten. Während dieses Zeitraums wird die Datenverbindung im Leerlauf für schreibgeschützte Anforderungen vom gleichen SharePoint-Benutzer für die gleichen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten vom [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienst wiederverwendet. Wenn im angegebenen Zeitraum keine weiteren Anforderungen für diese Daten empfangen werden, wird die Verbindung aus dem Pool entfernt. Gültige Werte reichen von 1 bis 3600 Sekunden. Weitere Informationen zu Verbindungspools finden Sie unter [Konfigurationseinstellungsverweis &#40;PowerPivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md).  
  
6.  Erhöhen oder verringern Sie den Wert unter **Maximale benutzerdefinierte Größe für den Datenverbindungspool**, um die maximale Anzahl von Verbindungen im Leerlauf zu ändern, die der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienst in einzelnen Verbindungspools für die einzelnen SharePoint-Benutzer, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datasets und Versionskombinationen erstellt.  
  
     Der Standardwert ist 1.000 Verbindungen im Leerlauf. Gültige Werte sind -1 (unbegrenzt), 0 (deaktiviert das Pooling von Benutzerverbindungen) oder 1 bis 10.000.  
  
     Durch diese Verbindungspools kann der Dienst fortlaufende Verbindungen mit den gleichen schreibgeschützten Daten, die vom selben Benutzer hergestellt werden, effizienter unterstützen. Wenn Sie das Verbindungspooling deaktivieren, wird jede Verbindung erneut erstellt.  
  
     Beachten Sie, dass Änderungen am Grenzwert der Verbindungspoolgröße (auch die Festlegung auf 0) nicht dazu führen, dass Verbindungen getrennt werden. Verbindungspools sind vorhanden, um Wartezeiten beim Herstellen einer Datenverbindung zu reduzieren. Der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienst wird nie eine Verbindung aufgrund von Verbindungspooleinstellungen ablehnen.  
  
7.  Erhöhen oder verringern Sie den Wert unter **Maximale administrative Größe des Serververbindungspools**, um die Anzahl von geöffneten Verbindungen in einem Verbindungspool zu ändern, der für eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstverbindung mit Analysis Services erstellt wurde. Jede [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstinstanz öffnet eine separate Administratorverbindung zur Analysis Services-Instanz auf demselben Computer. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienst erstellt einen separaten Pool, damit Administratorverbindungen wiederverwendet werden können, um Verbindungen im Leerlauf zu suchen und den Serverstatus zu überwachen. Der Standardwert ist 200 Verbindungen. Gültige Werte sind -1 (unbegrenzt), 0 (deaktiviert die Verwendung des Verwaltungsverbindungspools) oder 1 bis 10000. Wenn Sie 0 auswählen, wird jede Verbindung neu erstellt.  
  
8.  Unter **Belegungsmethode**können Sie das Lastenausgleichsschema angeben, das der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst verwendet, um eine bestimmte [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung für den Lastenausgleich einer ersten Anforderung auszuwählen. Die Standardeinstellung ist **Zustandsbasiert**, mit der Anforderungen auf Grundlage des Serverzustands zugeordnet werden, wie anhand des verfügbaren Arbeitsspeichers und der Prozessorauslastung ermittelt. Alternativ können Sie **Roundrobin** auswählen, um Anforderungen den Servern in der gleichen wiederholten Reihenfolge zuzuordnen, unabhängig davon, ob ein Server ausgelastet oder im Leerlauf ist.  
  
9. Unter Datenaktualisierung in **Geschäftszeiten**können Sie den Zeitraum angeben, der einen Geschäftstag definiert. Zeitpläne zur Datenaktualisierung können am Ende eines Geschäftstags ausgeführt werden, um die während der regulären Geschäftszeiten generierten Transaktionsdaten zu sammeln.  
  
10. Unter **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenaktualisierungskonto**können Sie eine vordefinierte Secure Store Service-Zielanwendung angeben, die ein vordefiniertes Konto zum Ausführen von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenaktualisierungsaufträgen speichert. Stellen Sie sicher, dass Sie den Namen der Zielanwendung und nicht die ID angeben. Die Zielanwendung für die unbeaufsichtigte Datenaktualisierung wird automatisch erstellt, wenn Sie die Option „Neuer Server“ im SQL Server-Setup verwendet haben, um [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint zu installieren. Andernfalls müssen Sie die Zielanwendung manuell erstellen. Eine Anleitung zum Konfigurieren des Kontos finden Sie unter [Konfigurieren des PowerPivot-Kontos für die unbeaufsichtigte Datenaktualisierung (PowerPivot für SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493).  
  
11. Unter **Benutzer dürfen benutzerdefinierte Windows-Anmeldeinformationen eingeben**können Sie das Kontrollkästchen aktivieren oder deaktivieren, um anzugeben, ob Zeitplanbesitzer beliebige Windows-Anmeldeinformationen für die Ausführung eines Datenaktualisierungszeitplans eingeben können. Wenn Sie dieses Kontrollkästchen aktivieren, erstellt und verwaltet die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung eine Zielanwendung für jeden Satz gespeicherter Anmeldeinformationen. Weitere Informationen finden Sie unter [Konfigurieren gespeicherter Anmeldeinformationen für die PowerPivot-Datenaktualisierung (PowerPivot für SharePoint)](http://msdn.microsoft.com/en-us/987eff0f-bcfe-4bbd-81e0-9aca993a2a75).  
  
12. Unter **Maximale Verarbeitungsverlaufslänge**können Sie angeben, wie lange ein Verlaufsdatensatz der Datenaktualisierungsverarbeitung beibehalten wird. Diese Informationen werden auf den Seiten für den Datenaktualisierungsverlauf angezeigt, die für jede Arbeitsmappe angelegt werden, die die Datenaktualisierung nutzt. Sie werden auch im [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard angezeigt.  
  
13. Geben Sie unter Sammlung von Verwendungsdaten in **Berichtsintervall für Abfragen**ein Zeitintervall an, in dem Abfragestatistiken gemeldet werden. Abfragestatistiken werden als einzelnes Ereignis gemeldet, um die Kommunikation zwischen den Servern zu minimieren.  
  
14. Geben Sie unter Verwendungsdatenverlauf an, wie lange ein Verlaufsdatensatz der Verwendungsdaten beibehalten wird. Die Nutzungsinformationen werden im [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard angezeigt. Die Berichte sind weniger effektiv, wenn Sie für den Verwendungsdatenverlauf einen zu niedrigen Wert angeben.  
  
15. Geben Sie unter Sammlung von Verwendungsdaten für jeden Abfrageantwort-Schwellenwert eine Obergrenze an, die bestimmt, wo eine Kategorie aufhört und die nächste beginnt. Durch diese Kategorien wird eine Basislinie festgelegt, auf deren Grundlage das Abfrageverhalten gemessen wird. Sie können diese Kategorien verwenden, um Trends in den Abfrageantwortzeiten Ihres Systems zu überwachen. Diese Informationen werden im [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard angezeigt.  
  
16. Klicken Sie auf **OK** , um die Änderungen zu speichern.  
  
     Änderungen am Timeout für Ladevorgänge oder an der Zuordnungsmethode werden nur auf neu eingehende Anforderungen angewendet. Für Anforderungen, die bereits ausgeführt werden, gelten die Werte, die beim Empfang der Anforderung gültig waren.  
  
##  <a name="AssignGSA"></a> Zuweisen einer PowerPivot-Dienstanwendung zu einer Webanwendung  
 Nachdem Sie eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung konfiguriert haben, können Sie sie einer Webanwendung zuweisen, indem Sie sie der Liste der Dienstanwendungsverbindungen der jeweiligen Webanwendung hinzufügen. Hierfür gibt es zwei Möglichkeiten:  
  
-   Fügen Sie die Anwendung der **Standardverbindungsgruppe** hinzu. Die *Standardverbindungsgruppe* ist eine Sammlung von Dienstanwendungsverbindungen, die jeder Webanwendung zur Verfügung stehen, die darauf verweist. Sie müssen dieser Liste eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung hinzufügen.  
  
-   Erstellen Sie für eine bestimmte Webanwendung eine **benutzerdefinierte** Verbindungsliste. Wenn Sie mehrere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen erstellt haben, können Sie die zu verwendende Anwendung aus einer benutzerdefinierten Liste auswählen.  
  
 Die Standardverbindungsgruppe kann mehr als eine Dienstanwendung des gleichen Typs enthalten. Beachten Sie jedoch, dass das Hinzufügen von mehr als einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung zu dieser Liste keine unterstützte Konfiguration ist.  
  
1.  Klicken Sie in der Zentraladministration unter **Anwendungsverwaltung**auf **Webanwendungen verwalten**.  
  
2.  Wählen Sie die Anwendung aus, für die Sie eine Verbindung zuweisen möchten (z. B. SharePoint -80).  
  
3.  Klicken Sie auf **Dienstverbindungen**.  
  
4.  Wählen Sie unter **Folgende Zuordnungsgruppe bearbeiten**entweder **default** oder **[custom]**aus.  
  
5.  Aktivieren Sie für **[custom]**das Kontrollkästchen neben jeder Dienstanwendungsverbindung, die Sie verwenden möchten. Falls Sie über mehrere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen verfügen (am Typ **Proxy der PowerPivot-Dienstanwendung**erkennbar), achten Sie darauf, nur eine auszuwählen.  
  
6.  Klicken Sie auf **OK**.  
  
##  <a name="EditGSA"></a> Bearbeiten von Eigenschaften für Dienstanwendungen  
 Verwenden Sie die folgenden Anweisungen, um die Eigenschaftenseite erneut zu öffnen, die den Dienstanwendungsnamen, den Anwendungspool sowie die Datenbankeinstellungen und Dienstzuordnungen enthält.  
  
1.  Klicken Sie in der Zentraladministration unter Anwendungsverwaltung auf **Dienstanwendungen verwalten**.  
  
2.  Wählen Sie die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung aus, aber klicken Sie nicht darauf. Sie können auf den Typnamen klicken, um die gesamte Zeile auszuwählen.  
  
3.  Klicken Sie im Menüband auf **Eigenschaften** .  
  
## <a name="see-also"></a>Siehe auch  
 [PowerPivot-Serververwaltung und -konfiguration in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
