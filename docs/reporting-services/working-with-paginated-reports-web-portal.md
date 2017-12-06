---
title: Arbeiten mit paginierten Berichten (Webportal) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb0bc38f-dc56-4350-8457-cd135c0346e1
caps.latest.revision: "6"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 68a7523b0c044a90c9c71d53ffbb00c6e680b5a1
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="working-with-paginated-reports-web-portal"></a>Arbeiten mit paginierten Berichten (Webportal)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Sie können die Eigenschaften eines paginierten Berichts innerhalb des Webportals anzeigen und verwalten. Über das Webportal erhalten Sie Zugriff auf den Berichts-Generator, um paginierte Berichte zu erstellen oder zu bearbeiten.  
   
## <a name="create-a-paginated-report"></a>Erstellen eines paginierten Berichts  
  
Sie können Folgendes tun, um ein neues freigegebenes Dataset zu erstellen.  
  
1.  Wählen Sie in der Menüleiste „Neu“ aus.  
  
2.  Wählen Sie **Paginierter Bericht**aus.  
  
    ![ssRSWebPortal-new-report](../reporting-services/media/ssrswebportal-new-report.png)  
  
3.  Entweder wird jetzt der Berichts-Generator gestartet, oder Sie werden aufgefordert, ihn herunterzuladen.  
  
4.  Erstellen Sie Ihren Bericht, und wählen Sie dann das **Speichern** -Symbol in der oberen linken Ecke aus, um den paginierten Bericht wieder auf dem Berichtsserver zu speichern.  
  
## <a name="manage-an-existing-paginated-report"></a>Verwalten eines vorhandenen paginierten Berichts  
  
Beim Verwalten eines vorhandenen paginierten Berichts haben Sie verschiedene Möglichkeiten.  
  
> [!NOTE]
> Wenn im jeweiligen Ordner keine paginierten Berichte angezeigt werden, sollten Sie sich vergewissern, dass Sie paginierte Berichte anzeigen. Sie können **Ansicht** aus der Menüleiste in der oberen rechten Ecke des Webportals auswählen. Stellen Sie sicher, dass das Kontrollkästchen **Paginierte Berichte** aktiviert ist.  
  
1.  Klicken Sie auf die **Auslassungspunkte (...)** für das Dataset aus, das Sie verwalten möchten.  
      
    ![ssRSWebPortal-manage-report1](../reporting-services/media/ssrswebportal-manage-report1.png)  
  
2.  Wählen Sie **Verwalten** aus, womit Sie auf den Bearbeitungsbildschirm gelangen.  
    
    ![ssRSWebPortal-manage-report2](../reporting-services/media/ssrswebportal-manage-report2.png)  
  
## <a name="properties"></a>Eigenschaften  
  
Im Eigenschaftenbildschirm können Sie den **Namen** und die **Beschreibung** des paginierten Berichts ändern. Außerdem stehen Ihnen folgende Optionen zur Verfügung: **Löschen**, **Verschieben**, **Verknüpften Bericht erstellen**, **Im Berichts-Generator bearbeiten**, **Herunterladen** oder **Ersetzen**.  
    
![ssRSWebPortal-report-properties](../reporting-services/media/ssrswebportal-report-properties.png)  
   
## <a name="parameters"></a>Parameter  
  
Sie können vorhandene Parameter eines paginierten Berichts ändern. Um einen neuen Parameter hinzuzufügen, müssen Sie den Bericht im Berichts-Generator oder in SQL Server Data Tools bearbeiten.  
  
![ssRSWebPortal-report-parameters](../reporting-services/media/ssrswebportal-report-parameters.png)  
   
## <a name="data-source"></a>Datenquelle  
Sie können auf eine freigegebene Datenquelle verweisen oder Verbindungsinformationen für eine benutzerdefinierte Datenquelle eingeben.  
  
![ssRSWebPortal-report-datasource](../reporting-services/media/ssrswebportal-report-datasource.png)  
  
Die folgenden Optionen können beim Angeben einer benutzerdefinierten Datenquelle verwendet werden.  
  
**Typ**  
  
Geben Sie eine Datenverarbeitungserweiterung an, die zum Verarbeiten von Daten aus der Datenquelle verwendet wird. Eine Liste der integrierten Datenerweiterungen finden Sie unter [Von Reporting Services unterstützte Datenquellen (SSRS)]. Weitere Datenverarbeitungserweiterungen können von Drittanbietern zur Verfügung stehen.  
  
**Verbindungszeichenfolge**  
  
Geben Sie die Verbindungszeichenfolge an, die vom Berichtsserver zum Herstellen der Verbindung mit der Datenquelle verwendet wird. Der Verbindungstyp bestimmt die Syntax, die Sie verwenden sollten. So ist z.B. eine Verbindungszeichenfolge für die XML-Datenverarbeitungserweiterung eine URL zu einem XML-Dokument. In den meisten Fällen gibt eine typische Verbindungszeichenfolge den Datenbankserver und die Datendatei an. Im folgenden Beispiel wird eine Verbindungszeichenfolge gezeigt, die für die Verbindung mit einer SQL Server-Datenbank mit dem Namen „MyData“ verwendet wird:  
  
    data source=(a SQL Server instance);initial catalog=MyData  
  
Eine Verbindungszeichenfolge kann als ein Ausdruck konfiguriert werden, sodass Sie die Datenquelle zur Laufzeit angeben können. Datenquellenausdrücke für den Bericht werden im Berichts-Designer definiert. Datenquellenausdrücke können im Webportal nicht definiert, angezeigt oder geändert werden. Sie können einen Datenquellenausdruck jedoch ersetzen, indem Sie auf **Standardwert überschreiben** klicken, um eine statische Verbindungszeichenfolge einzugeben. Wenn Sie zurück zum Ausdruck wechseln möchten, klicken Sie auf **Standardwert wiederherstellen**. Der Berichtsserver speichert die ursprüngliche Verbindungszeichenfolge für den Fall, dass Sie sie wiederherstellen müssen. Um Datenquellenausdrücke verwenden zu können, müssen Sie die ursprünglich im Bericht veröffentlichten Informationen zur Datenquellenverbindung verwenden. Freigegebene Datenquellen unterstützen die Verwendung von Ausdrücken in der Verbindungszeichenfolge nicht.  
  
**Anmeldeinformationen**  
  
Sie können eine Option angeben, die bestimmt, wie Anmeldeinformationen abgerufen werden.  
  
> [!IMPORTANT]
> Falls die Verbindungszeichenfolge Anmeldeinformationen enthält, werden die in diesem Abschnitt festgelegten Optionen und Werte ignoriert. Beachten Sie, dass bei Angabe der Anmeldeinformationen in der Verbindungszeichenfolge die Werte für alle Benutzer, die diese Seite anzeigen, in Klartext angezeigt werden.  
  
**Als Benutzer, der den Bericht anzeigt**  
  
Verwenden Sie die Windows-Anmeldeinformationen des aktuellen Benutzers für den Zugriff auf die Datenquelle. Wählen Sie diese Option aus, wenn die für den Zugriff auf die Datenquelle verwendeten Anmeldeinformationen mit denen übereinstimmen, die zum Anmelden an der Netzwerkdomäne verwendet werden. Diese Option kann am besten verwendet werden, wenn die Kerberos-Authentifizierung für die Domäne aktiviert ist oder wenn sich die Datenquelle auf demselben Computer wie der Berichtsserver befindet. Wenn Kerberos nicht aktiviert ist, können keine Windows-Anmeldeinformationen an einen anderen Dienst oder einen Remotecomputer übergeben werden. Falls weitere Computerverbindungen erforderlich sind, wird eine Fehlermeldung statt der erwarteten Daten zurückgegeben.  
  
Ein Berichtsserveradministrator kann die Verwendung der integrierten Sicherheit von Windows deaktivieren, um auf Berichtsdatenquellen zugreifen zu können. Wenn dieser Wert ausgegraut ist, ist die Funktion nicht verfügbar.  
  
Verwenden Sie diese Option nicht, wenn Sie vorhaben, diesen Bericht zu planen oder zu abonnieren. Die geplante oder unbeaufsichtigte Berichtsverarbeitung benötigt Anmeldeinformationen, die ohne Benutzereingaben oder den Sicherheitskontext des aktuellen Benutzers abgerufen werden können. Diese Möglichkeit bieten nur gespeicherte Anmeldeinformationen. Aus diesem Grund hindert Sie der Berichtsserver daran, die Ausführung eines Berichts oder eines Abonnements zu planen, wenn der Bericht für den Anmeldeinformationstyp der integrierten Windows-Sicherheit konfiguriert ist. Wenn Sie diese Option für einen Bericht wählen, der bereits abonniert ist oder geplante Vorgänge aufweist, werden das Abonnement und die geplanten Vorgänge beendet.  
  
**Diese Anmeldeinformationen verwenden**  
  
Speichern Sie einen verschlüsselten Benutzernamen und ein Kennwort in der Berichtsserver-Datenbank. Wählen Sie diese Option aus, um einen Bericht unbeaufsichtigt auszuführen (z.B. Berichte, die durch Zeitpläne oder durch Ereignisse anstelle einer Benutzeraktion initiiert werden).   
  
Sie können auch den Typ der Anmeldeinformationen auswählen, der hier infrage kommt. Das ist entweder die Windows-Authentifizierung (Windows-Benutzername und -Kennwort) oder spezielle Datenbank-Anmeldeinformationen (Benutzername und Kennwort für eine Datenbank), wie z.B. bei der SQL-Authentifizierung.  
  
Wenn es sich um ein Konto mit Windows-Anmeldeinformationen handelt, muss das angegebene Konto über die Berechtigung zum lokalen Anmelden auf dem Computer verfügen, der die von dem Bericht verwendete Datenquelle hostet.  
  
Wählen Sie **Mit diesen Anmeldeinformationen anmelden, aber dann versuchen, die Identität des Benutzers anzunehmen, der den Bericht anzeigt** , um eine Delegierung von Anmeldeinformationen zuzulassen. Dies ist jedoch nur möglich, wenn die jeweilige Datenquelle den Identitätswechsel unterstützt. In SQL Server-Datenbanken wird durch diese Option die SETUSER-Funktion festgelegt. Bei Analysis Services wird hierfür „EffectiveUserName“ verwendet.  
  
**Benutzer, der den Bericht anzeigt, zur Eingabe von Anmeldeinformationen auffordern**  
  
Jeder Benutzer muss einen Benutzernamen und ein Kennwort für den Zugriff auf die Datenquelle eingeben. Sie können den Text der Eingabeaufforderung definieren, in der die Benutzeranmeldeinformationen angefordert werden. Beispiel: „Geben Sie einen Benutzernamen und ein Kennwort für den Zugriff auf die Datenquelle ein.“  
  
Sie können auch den Typ der Anmeldeinformationen auswählen, der hier infrage kommt. Das ist entweder die Windows-Authentifizierung (Windows-Benutzername und -Kennwort) oder spezielle Datenbank-Anmeldeinformationen (Benutzername und Kennwort für eine Datenbank), wie z.B. bei der SQL-Authentifizierung.  
  
**Ohne Anmeldeinformationen**  
  
Durch Auswahl dieser Option haben Sie die Möglichkeit, keinerlei Anmeldeinformationen für die Datenquelle bereitzustellen. Wenn für die Datenquelle eine Benutzeranmeldung erforderlich ist, hat die Auswahl dieser Option keine Auswirkungen. Sie sollten diese Option nur auswählen, wenn für die Datenquellenverbindung keine Benutzeranmeldeinformationen erforderlich sind.  
  
Bevor Sie diese Option verwenden können, müssen Sie für den Berichtsserver das Konto für die unbeaufsichtigte Ausführung konfigurieren. Das Konto für die unbeaufsichtigte Ausführung wird zum Herstellen der Verbindung mit externen Datenquellen verwendet, wenn auf anderen Wegen keine Anmeldeinformationen verfügbar sind. Wenn Sie diese Option angeben und das Konto nicht konfiguriert ist, schlägt die Verbindung mit der Berichtsdatenquelle fehl, und der Bericht wird nicht verarbeitet. Weitere Informationen zu diesem Konto finden Sie unter [Konfigurieren des Kontos für die unbeaufsichtigte Ausführung (SSRS-Konfigurations-Manager)](../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
## <a name="subscriptions"></a>Abonnements  
Ein Reporting Services-Abonnement ist eine Konfiguration zur Übermittlung eines Berichts zu einem bestimmten Zeitpunkt oder als Reaktion auf ein Ereignis, und zwar in einem von Ihnen angegebenen Dateiformat. Speichern Sie beispielsweise jeden Donnerstag den Bericht MonthlySales.rdl als Microsoft Word-Dokument in eine Dateifreigabe. Sie können Abonnements verwenden, um die Übermittlung eines Berichts mit einem spezifischen Satz an Berichtsparameterwerten zeitlich festzulegen und zu automatisieren. Weitere Informationen finden Sie unter [Arbeiten mit Abonnements](working-with-subscriptions-web-portal.md).
  
![ssRSWebPortal-report-subscription1](../reporting-services/media/ssrswebportal-report-subscription1.png)
   
## <a name="dependent-items"></a>Abhängige Elemente  
Verwenden Sie die Seite „Abhängige Elemente“, um eine Liste der Elemente anzuzeigen, die auf diesen Bericht verweisen. Das Symbol für den jeweiligen Elementtyp gibt an, worum es sich dabei handelt. Sie können für jedes Element auf die **Auslassungspunkte (…)** klicken, um das entsprechende Element zu verwalten.  
  
## <a name="caching"></a>Caching  
Zum Zwischenspeichern von Daten für einen paginierten Bericht stehen Ihnen mehrere Optionen zur Verfügung. Sie beginnen mit einer einfachen Auswahl.  
  
1.  **Diesen Bericht immer mit den neuesten Daten ausführen** : Wenn Sie diese Option auswählen, wird bei jeder Ausführung des Berichts eine Abfrage an die Datenquelle ausgegeben. Dadurch entsteht ein bedarfsgesteuerter Bericht, der immer die neuesten Daten enthält. Bei jedem Öffnen des Berichts wird eine neue Instanz des Berichts erstellt, die die Ergebnisse einer neuen Abfrage enthält. Wenn bei dieser Vorgehensweise zehn Benutzer gleichzeitig den Bericht öffnen, werden zehn Abfragen zur Verarbeitung an die Datenquelle gesendet.  
  
2.  **Kopien von diesem Bericht zwischenspeichern und bei Verfügbarkeit verwenden** : Wenn Sie diese Option auswählen, wird eine temporäre Kopie der Daten zur späteren Verwendung in einem Cache abgelegt. Die Zwischenspeicherung erhöht in der Regel die Leistung, da die Daten aus dem Cache zurückgegeben werden und die Datasetabfrage nicht erneut ausgeführt werden muss. Wenn bei dieser Vorgehensweise zehn Benutzer den Bericht öffnen, führt nur die erste Anforderung zu einer Abfrage an die Datenquelle. Der Bericht wird dann zwischengespeichert, und für die restlichen neun Benutzer wird der aus dem Cache abgerufene Bericht angezeigt.  
  
3.  **Diesen Bericht immer für vorher generierte Momentaufnahmen ausführen** : Wenn Sie diese Option auswählen, werden das Layout und die Daten eines Berichts für einen angegebenen Zeitraum zwischengespeichert. Sie können einen Bericht als Berichtsmomentaufnahme ausführen, um zu verhindern, dass der Bericht zu willkürlichen Zeiten ausgeführt wird (z.B. während einer geplanten Sicherung). Die Momentaufnahme kann nach einem festgelegten Zeitplan aktualisiert werden. [Weitere Informationen]  
  
![ssRSWebPortal-report-caching1](../reporting-services/media/ssrswebportal-report-caching1.png)  
   
Wenn Sie **Kopien von diesem Bericht zwischenspeichern und bei Verfügbarkeit verwenden** auswählen, können Sie einige zusätzliche Optionen festlegen.  
  
![ssRSWebPortal-report-caching2](../reporting-services/media/ssrswebportal-report-caching2.png)  

Weitere Informationen finden Sie unter [Arbeiten mit Momentaufnahmen](working-with-snapshots-web-portal.md).
  
### <a name="cache-expiration"></a>Cacheablauf  
  
Sie können steuern, ob der Cache für den paginierten Bericht nach einer bestimmten Zeitspanne oder nach einem festgelegten Zeitplan ablaufen soll. Sie können einen freigegebenen Zeitplan verwenden  
  
> [!NOTE]
> Dadurch wird der Cache nicht aktualisiert.  
  
### <a name="cache-refresh-plans"></a>Cacheaktualisierungspläne  
  
Mithilfe der Option „Cacheaktualisierungspläne“ können Sie Zeitpläne erstellen, nach denen temporäre Kopien der Daten für einen paginierten Bericht vorab in den Cache geladen werden. Ein Aktualisierungsplan enthält einen Zeitplan und bietet die Möglichkeit, Werte für Parameter anzugeben oder zu überschreiben. Sie können keine Werte für Parameter überschreiben, die als schreibgeschützt gekennzeichnet sind. Sie können mehr als einen Aktualisierungsplan erstellen und verwenden.  
   
Die folgenden Standardrollenzuweisungen ermöglichen es Ihnen, paginierte Berichte für Cacheaktualisierungspläne hinzuzufügen, zu löschen und zu ändern: „Inhalts-Manager“, „Meine Berichte“ und „Verleger“.  
  
Nachdem Sie die obenstehende Option zum Zwischenspeichern angewendet haben, können Sie einen Cacheaktualisierungsplan definieren. Wählen Sie den Link **Manage Refresh Plans** (Aktualisierungspläne verwalten), der angezeigt wird, nachdem Sie die Cacheeinstellungen anwenden. Dadurch gelangen Sie auf die Seite „Cacheaktualisierungsplan“.   
  
Wählen Sie **Neuer Cacheaktualisierungsplan**, um einen neuen Cacheplan zu erstellen. Sie können einen Namen für den Plan eingeben und einen Zeitplan angeben. Falls das Dataset über definierte Parameter verfügt, werden Ihnen diese aufgelistet angezeigt, und es wird Ihnen möglich sein, Werte bereitzustellen, sofern sie nicht als schreibgeschützt gekennzeichnet sind.  
  
Sobald Sie fertig sind, können Sie **Cacheaktualisierungsplan erstellen**auswählen.  
  
![ssRSWebPortal-report-caching3](../reporting-services/media/ssrswebportal-report-caching3.png)  
  
> [!NOTE]
> SQL Server-Agent muss ausgeführt werden, um einen Cacheaktualisierungsplan zu erstellen.  
  
Sie können gelistete Pläne **Bearbeiten** oder **Löschen** . Die Option **Neu aus vorhandenem** wird nur aktiviert, wenn genau ein Cacheaktualisierungsplan ausgewählt ist. Durch diese Option wird ein neuer Aktualisierungsplan erstellt, der vom ursprünglichen Plan kopiert wird. Die Seite Cacheaktualisierungsplan wird geöffnet und enthält bereits die Details des ausgewählten Plans. Anschließend können Sie die Optionen für den Aktualisierungsplan ändern und den Plan mit einer neuen Beschreibung speichern.  
  
## <a name="history-snapshots"></a>Verlaufsmomentaufnahmen  
  
Mithilfe der Seite „Verlaufsmomentaufnahmen“ können Sie die im Laufe der Zeit generierten und gespeicherten Berichtsmomentaufnahmen anzeigen. Abhängig von den festgelegten Optionen enthält der Berichtsverlauf möglicherweise nur die neueren Momentaufnahmen.  
  
Der Berichtsverlauf wird immer im Kontext des Berichts angezeigt, aus dem er stammt. Es ist nicht möglich, den Verlauf aller Berichte auf einem Berichtsserver zentral anzuzeigen.  
  
Wenn Sie eine Momentaufnahme generieren möchten, muss der Bericht unbeaufsichtigt ausgeführt werden können. Das heißt, er muss gespeicherte Anmeldeinformationen verwenden, und parametrisierte Berichte müssen Standardparameterwerte für alle Parameter enthalten. Der Momentaufnahmen können manuell oder mithilfe eines geplanten Vorgangs generiert werden.   
  
Klicken Sie auf eine Momentaufnahme zum Berichtsverlauf, um diese anzuzeigen. Die im Berichtsverlauf angezeigten Momentaufnahmen unterscheiden sich nur durch das Datum und die Uhrzeit ihrer Erstellung. Es gibt keinen grafischen Hinweis, ob eine Momentaufnahme als Folge eines Zeitplans oder durch einen manuellen Vorgang generiert wurde.  
  
## <a name="security"></a>Sicherheit  
Mithilfe der Eigenschaftenseite „Sicherheit“ können Sie die Sicherheitseinstellungen für den Zugriff auf den Bericht anzeigen und ändern. Diese Seite steht für Elemente zur Verfügung, für die Sie die Berechtigung zur Änderung der Sicherheitseinstellungen besitzen.  
  
Der Zugriff auf Elemente wird durch Rollenzuweisungen definiert, in denen die Aufgaben angegeben sind, die eine Gruppe oder ein Benutzer ausführen kann. Eine Rollenzuweisung besteht aus einem Benutzer- oder Gruppennamen und einer oder mehreren Rollendefinitionen, die eine Sammlung von Aufgaben angeben.  
  
**Elementsicherheit bearbeiten**  
  
Wählen Sie diese Option aus, um die Definition der Sicherheit für das aktuelle Element zu ändern.

## <a name="next-steps"></a>Nächste Schritte

[Web portal (Webportal)](../reporting-services/web-portal-ssrs-native-mode.md)  
[Work with shared datasets (Arbeiten mit freigegebenen Datasets)](../reporting-services/work-with-shared-datasets-web-portal.md)

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
