---
title: Sichere Berichte und Ressourcen | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [Reporting Services], reports
- security [Reporting Services], resources
- reports [Reporting Services], security
- confidential reports [Reporting Services]
- resources [Reporting Services], security
ms.assetid: 63cd55c7-fd2a-49e3-a3f8-59eb1a1c6e83
caps.latest.revision: 47
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 66e32b412558ec3c06fcbfcb3b4dbd1b7b2e06e0
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="secure-reports-and-resources"></a>Sichere Berichte und Ressourcen
  Die Sicherheit kann für einzelne Berichte und Ressourcen festgelegt werden, um die Zugriffsebene der Benutzer für diese Objekte zu steuern. In der Standardeinstellung können nur Benutzer, die Mitglieder der integrierten Gruppe **Administratoren** sind, Berichte ausführen, Ressourcen anzeigen, Eigenschaften ändern und die Elemente löschen. Für alle anderen Benutzer müssen Rollenzuweisungen erstellt werden, die den Zugriff auf einen Bericht oder eine Ressource zulassen.  
  
## <a name="role-based-access-to-reports-and-resources"></a>Rollenbasierter Zugriff auf Berichte und Ressourcen  
 Wenn Sie den Zugriff auf Berichte und Ressourcen gewähren möchten, können Sie es den Benutzern ermöglichen, vorhandene Rollenzuweisungen von einem übergeordneten Ordner zu erben oder selbst eine neue Rollenzuweisung für das Element zu erstellen.  
  
 In den meisten Fällen möchten Sie wahrscheinlich die Berechtigungen verwenden, die von einem übergeordneten Ordner geerbt werden. Das Festlegen der Sicherheit für einzelne Berichte und Ressourcen ist normalerweise nur dann erforderlich, wenn Sie den Bericht oder die Ressource für die Benutzer ausblenden möchten, die nicht über das Vorhandensein des Berichts oder der Ressource informiert sein müssen, oder wenn Sie die Zugriffsstufe für einen Bericht oder ein Element erhöhen möchten. Diese Zielsetzungen schließen sich nicht gegenseitig aus. Sie können den Zugriff auf einen Bericht auf eine kleinere Benutzergruppe beschränken und allen oder einigen Benutzern zusätzliche Privilegien zur Verwaltung des Berichts gewähren.  
  
 Möglicherweise müssen Sie zu diesem Zweck mehrere Rollenzuweisungen erstellen. Angenommen, Sie möchten den Benutzern Anna und Fernando sowie der Gruppe der leitenden Mitarbeiter der Personalabteilung einen Bericht zur Verfügung stellen. Anna und Fernando müssen den Bericht verwalten können; die leitenden Mitarbeiter der Personalabteilung müssen ihn jedoch nur ausführen können. Um alle diese Benutzer zu berücksichtigen, müssen Sie drei separate Rollenzuweisungen erstellen: je eine Rollenzuweisung, um Anna bzw. Fernando als Inhalts-Manager des Berichts festzulegen, sowie eine Rollenzuweisung, die ausschließlich Anzeigeaufgaben für die Gruppe der leitenden Mitarbeiter der Personalabteilung unterstützt.  
  
 Die Sicherheitseinstellungen eines Berichts oder einer Ressource bleiben dem Element zugeordnet, selbst wenn Sie es an einen neuen Speicherort verschieben. Wenn Sie z. B. einen Bericht verschieben, auf den nur ein paar wenige Personen Zugriff haben, ist dieser Bericht auch weiterhin nur für diese Benutzer verfügbar, auch wenn Sie ihn in einen Ordner mit einer relativ offenen Sicherheitsrichtlinie verschieben.  
  
## <a name="mitigating-html-injection-attacks-in-a-published-report-or-document"></a>Verhindern von HTML-Injection-Angriffen in einem veröffentlichten Bericht oder Dokument  
 In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]werden Berichte und Ressourcen unter der Sicherheitsidentität des Benutzers verarbeitet, der den Bericht aktuell ausführt. Wenn der Bericht Ausdrücke, Skripts, benutzerdefinierte Berichtselemente oder benutzerdefinierte Assemblys enthält, wird der Code mit den Anmeldeinformationen des Benutzers ausgeführt. Wenn eine Ressource ein HTML-Dokument darstellt, das Skript enthält, wird das Skript ausgeführt, wenn der Benutzer das Dokument auf dem Berichtsserver öffnet. Die Möglichkeit, Skript oder Code in einem Bericht auszuführen, ist eine leistungsstarke Funktion, die ein gewisses Risiko mit sich bringt. Wenn der Code bösartig ist, sind der Berichtsserver und der den Bericht ausführende Benutzer potenziellen Angriffen ausgesetzt.  
  
 Wenn der Zugriff auf Berichte und Ressourcen gewährt wird, die als HTML verarbeitet werden, sollte unbedingt bedacht werden, dass die Berichte mit voller Vertrauenswürdigkeit verarbeitet werden und dass potenziell bösartige Skripts möglicherweise an den Client gesendet werden. In Abhängigkeit von den Browsereinstellungen führt der Client den HTML-Code auf der Vertrauensebene aus, die im Browser angegeben ist.  
  
 Sie können das Risiko, bösartige Skripts auszuführen, reduzieren. Treffen Sie dazu die folgenden Vorkehrungen:  
  
-   Überlegen Sie sich genau, wem Sie die Möglichkeit geben, Inhalte auf einem Berichtsserver zu veröffentlichen. Da das Potenzial der Veröffentlichung von bösartigen Inhalten besteht, sollten Sie die Gruppe der Personen, die Inhalte veröffentlichen können, auf eine kleine Anzahl vertrauenswürdiger Benutzer begrenzen.  
  
-   Alle Verleger sollten es vermeiden, Berichte und Ressourcen zu veröffentlichen, die aus unbekannten oder nicht vertrauenswürdigen Quellen stammen. Öffnen Sie die Datei gegebenenfalls in einem Text-Editor, und prüfen Sie sie auf verdächtige Skripts und URLs.  
  
## <a name="report-parameters-and-script-injection"></a>Berichtsparameter und Script-Injection  
 Berichtsparameter stellen Flexibilität zum Gesamtberichtsentwurf und der Ausführung bereit. Dieselbe Flexibilität kann jedoch in einigen Fällen von einem Angreifer in Lockangriffen verwendet werden. Um das Risiko der versehentlichen Ausführung schädlicher Skripts zu minimieren, sollten gerenderte Berichte nur aus vertrauenswürdigen Quellen geöffnet werden. Sie sollten das folgende Szenario, das ein potenzieller HTML-Renderer-Script-Injection-Angriff ist, berücksichtigen:  
  
1.  Ein Bericht enthält ein Textfeld, bei dem die Linkaktion auf den Wert eines Parameters festgelegt wurde, der böswilligen Text enthalten könnte.  
  
2.  Der Bericht wird auf einem Berichtsserver veröffentlicht oder auf eine andere Weise verfügbar gemacht, sodass der Berichtsparameterwert von der URL einer Webseite gesteuert werden kann.  
  
3.  Ein Angreifer erstellt einen Link zu der Webseite oder der Berichtsserver den Wert des Parameters angeben, in der Form "Javascript:\<bösartiges Skript hier >" und sendet diesen Link an jemanden in einem Lockangriff.  
  
## <a name="mitigating-script-injection-attacks-in-a-hyperlink-in-a-published-report-or-document"></a>Abwehren von Script-Injection-Angriffen in einem Link in einem veröffentlichten Bericht oder Dokument  
 Berichte können eingebettete Links im Wert der Action-Eigenschaft in einem Berichtselement oder einem Teil eines Berichtselements enthalten. Links können an Daten gebunden werden, die aus einer externen Datenquelle abgerufen werden, wenn der Bericht verarbeitet wird. Wenn ein böswilliger Benutzer die zugrunde liegenden Daten ändert, könnte der Link für Skriptexploits eingesetzt werden. Wenn ein Benutzer im veröffentlichten oder exportierten Bericht auf den Link klickt, könnte bösartiges Skript ausgeführt werden.  
  
 Um das Risiko des Einschließen von Links in einem Bericht, der versehentlich bösartige Skripts ausführt, zu verringern, binden Sie Links nur an Daten von vertrauenswürdigen Quellen. Stellen Sie sicher, dass Daten von den Abfrageergebnissen und den Ausdrücken, die Daten an Links binden, keine Links erstellen, die missbraucht werden können. Verwenden Sie z. B. keinen Link als Grundlage für einen Ausdruck, der Daten aus mehreren Datasetfeldern verkettet. Wechseln Sie ggf. zum Bericht, und suchen Sie nach verdächtigen Skripts und URLs mithilfe von "Quelle anzeigen".  
  
## <a name="mitigating-sql-injection-attacks-in-a-parameterized-report"></a>Verhindern von SQL-Injection-Angriffen in einem parametrisierten Bericht  
 Verwenden Sie in einem Bericht, der einen Parameter vom Typ **String**enthält, eine Liste der verfügbaren Werte (wird auch als Liste der gültigen Werte bezeichnet), und stellen Sie sicher, dass Benutzer, die den Bericht ausführen, nur über die Berechtigungen verfügen, die zum Anzeigen der Daten im Bericht erforderlich sind. Wenn Sie einen Parameter vom Typ **String**definieren, wird für den Benutzer ein Textfeld bereitgestellt, das jeden beliebigen Wert annehmen kann. Mit einer Liste der verfügbaren Werte werden die Werte eingeschränkt, die eingegeben werden können. Wenn der Berichtsparameter an einen Abfrageparameter gebunden ist und Sie keine Liste mit verfügbaren Werten verwenden, kann ein Benutzer des Berichts SQL-Syntax in das Textfeld eingeben. Damit öffnet er den Bericht und Ihren Server potenziell für einen SQL-Injection-Angriff. Wenn der Benutzer über Berechtigungen zum Ausführen der neuen SQL-Anweisung verfügt, können daraus unerwünschte Ergebnisse auf dem Server resultieren.  
  
 Wenn ein Berichtsparameter nicht an einen Abfrageparameter gebunden ist und die Parameterwerte im Bericht enthalten sind, können die Benutzer des Berichts Ausdruckssyntax oder eine URL in den Parameterwert eingeben und den Bericht für Excel oder HTML rendern. Wenn anschließend ein anderer Benutzer den Bericht anzeigt und auf die gerenderten Parameterinhalte klickt, führt der Benutzer möglicherweise unbeabsichtigt das bösartige Skript bzw. den bösartigen Link aus.  
  
 Um das Risiko der versehentlichen Ausführung schädlicher Skripts zu minimieren, sollten gerenderte Berichte nur aus vertrauenswürdigen Quellen geöffnet werden.  
  
> [!NOTE]  
>  In früheren Versionen der Dokumentation war ein Beispiel zum Erstellen einer dynamischen Abfrage als Ausdruck enthalten. Durch diese Art der Abfrage entsteht eine Angriffsfläche für SQL-Injection-Angriffe; daher wird dies nicht empfohlen.  
  
## <a name="securing-confidential-reports"></a>Sichern vertraulicher Berichte  
 Berichte mit vertraulichen Informationen sollten auf der Datenzugriffsebene geschützt werden. Benutzer müssen in diesem Fall Anmeldeinformationen angeben, um auf die vertraulichen Daten zugreifen zu können. Weitere Informationen finden Sie unter [Specify Credential and Connection Information for Report Data Sources](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md). Darüber hinaus können Sie einen Ordner für unbefugte Benutzer sperren. Weitere Informationen finden Sie unter [Sichere Ordner](../../reporting-services/security/secure-folders.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Verwalten von Rollenzuweisungen](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [Konfigurieren des Berichts-Generator-Zugriffs](../../reporting-services/report-server/configure-report-builder-access.md)   
 [Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Sichern freigegebener Datenquellenelemente](../../reporting-services/security/secure-shared-data-source-items.md)   
 [Speichern von Anmeldeinformationen in einer Reporting Services-Datenquelle](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
