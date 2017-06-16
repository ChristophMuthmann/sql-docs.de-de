---
title: Mithilfe des RSClientPrint-Steuerelements in benutzerdefinierten Anwendungen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- RSPrintClient control
- print controls [Reporting Services]
- custom printing [Reporting Services]
- client-side printing
ms.assetid: 8c0bdd18-8905-4e22-9774-a240fc81a8a7
caps.latest.revision: 31
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8afee187160da9d35efd0c7079b649bac7e73740
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="using-the-rsclientprint-control-in-custom-applications"></a>Verwenden des RSClientPrint-Steuerelements in benutzerdefinierten Anwendungen
  Die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ActiveX-Steuerelement **RSPrintClient**, bietet die clientseitige Drucks für Berichte in HTML-Viewer angezeigt. Er bietet eine **Drucken** Dialogfeld, damit ein Benutzer Druckaufträge initiieren, Vorschau eines Berichts anzuzeigen, geben Sie die zu druckenden Seiten aus und Ränder ändern. Während eines clientseitigen Druckvorgangs rendert der Berichtsserver den Bericht mithilfe der Bildrenderingerweiterung (EMF) und verwendet die Druckfunktionen des Betriebssystems zum Erstellen des Druckauftrags und zum Senden des Auftrags an einen Drucker.  
  
 Mithilfe der clientseitigen Druckfunktion kann die Qualität eines Druckes für einen HTML-Bericht gesteuert und verbessert werden, indem die Druckereinstellungen des Browsers auf dem Computer des Benutzers übergangen und stattdessen die Seitengrößen, Ränder sowie der Kopf- und Fußzeilentext des Berichts zum Erstellen der Druckausgabe verwendet werden. Vom Drucksteuerelement werden Eigenschaftswerte des Berichts gelesen, um die Seitengröße und Ränder festzulegen.  
  
 Entwickler, die die clientseitige Druckfunktion im Drittanbieter-Symbolleisten oder Viewer aktivieren möchten erreichen das ActiveX-Steuerelement über die **RSClientPrint** COM-Objekt. Das Steuerelement kann frei verteilt werden. In der folgenden Liste sind Empfehlungen für die Verwendung des Steuerelements enthalten:  
  
-   Verwenden Sie das Steuerelement zum Verbessern des Druckes von webbasierten Berichten. Geben Sie das Objekt in einem von der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]--kompatiblen Programmiersprache oder per Skript. In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Forms-Anwendungen kann das Steuerelement nicht verwendet werden.  
  
-   Kopieren Sie die CAB-Datei aus den [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Programmdateien, und fügen Sie sie zur Codebasis Ihrer benutzerdefinierten Anwendung hinzu.  
  
-   Verwenden einer \<Objekt >-Tag zum Angeben des Steuerelements.  
  
-   Geben Sie eine relative oder vollqualifizierte URL zur CAB-Datei im OBJECT CODEBASE-Attribut an.  
  
-   Geben Sie eigene Informationen zur Anwendungsversion der CAB-Datei an, damit Sie nachverfolgen können, welche Version in der Anwendung verwendet wird.  
  
-   Lesen Sie sich die Themen in der Onlinedokumentation zur Bildrenderingerweiterung (EMF) durch, um Grundlegendes zum Rendern von Seiten für die Druckvorschau und -ausgabe zu erfahren.  
  
## <a name="rsprintclient-overview"></a>Übersicht über RSPrintClient  
 Vom Steuerelement wird ein benutzerdefiniertes Dialogfeld zum Drucken angezeigt, das die in Dialogfeldern zum Drucken üblichen Funktionen enthält. Dazu zählen Druckvorschau, Seitenauswahl zum Angeben bestimmter Seiten und Bereiche, Seitenränder und Ausrichtung. Das Steuerelement ist in eine CAB-Datei verpackt. Der Text in der **Drucken** Dialogfeld ist in allen in unterstützten Sprachen lokalisiert [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **RSPrintClient** ActiveX-Steuerelement die bildrenderingerweiterung (EMF) verwendet, um den Bericht zu drucken. Die folgenden EMF-Geräteinformationen werden verwendet: StartPage, EndPage, MarginBottom, MarginLeft, MarginTop, MarginRight, PageHeight und PageWidth. Andere Einstellungen für Geräteinformationen werden für Bildrendering nicht unterstützt.  
  
### <a name="language-support"></a>Sprachunterstützung  
 Das Drucksteuerelement stellt Text in der Benutzeroberfläche in unterschiedlichen Sprachen bereit und akzeptiert Eingabewerte mit einer Kalibrierung für unterschiedliche Maßsysteme. Die Sprach- und Maßsystem System verwendet werden bestimmt, indem die **Kultur** und **UICulture** Eigenschaften. Beide Eigenschaften akzeptieren LCID-Werte. Wenn Sie einen LCID-Wert für eine Sprache angeben, die eine Variante einer unterstützten Sprache ist, wird die Sprache verwendet, die am nächsten zu Ihrer Angabe liegt. Falls Sie einen LCID-Wert angeben, der nicht unterstützt wird und auch keine enge Übereinstimmung mit einem anderen LCID-Wert aufweist, wird Englisch (Vereinigte Staaten) verwendet.  
  
## <a name="using-rsclientprint-in-code"></a>Verwenden von "RSClientPrint" im Code  
 Die **RSClientPrint** Objekt wird verwendet, um programmgesteuert auf das ActiveX-Steuerelement und seine Methoden und Eigenschaften zugreifen. Das Steuerelement stellt einen modalen Dialog für die Druckvorschau bereit.  
  
### <a name="specifying-default-values"></a>Angeben von Standardwerten  
 Sie können Initialisieren der **Drucken** Dialogfeld mit den Rand- und Seitenwerten des Berichts. Wird standardmäßig die **Drucken** im Dialogfeld mit Werten aus der Berichtsdefinition initialisiert wird. Sie können die Standardwerte verwenden oder andere Werte angeben, indem Sie die Eigenschaften des Objekts festlegen.  
  
 Alle Dimensionen werden in Millimetern festgelegt. Maßkonvertierung findet zur Laufzeit auf, wenn die **Kultur** und **UICulture** auf denen keine metrischen Maße Gebietsschemas festgelegt sind.  
  
 Um zu verstehen, welche Werte für Seitengrößen und Ränder verwendet werden, können Sie die **GetProperties** Methode, um die Standardwerte abrufen:  
  
-   **PageHeight** und **PageWidth** die standardseitenhöhe und Breite angeben. Beim Starten des Drucksteuerelements werden diese Eigenschaftswerte zur Auswahl der nächsten verfügbaren Papiergröße für den aktuell ausgewählten Drucker verwendet. Wenn **PageWidth** ist größer als die **PageHeight**, der die Ausrichtung auf Querformat festgelegt. Andernfalls ist sie auf Hochformat festgelegt.  
  
-   **LeftMargin**, **RightMargin**, **TopMargin**, und **BottomMargin** 12,2 standardmäßig festgelegt sind.  
  
 Diese Eigenschaften werden gespeichert, der **Element** Properties-Auflistung, auf dem Berichtsserver. Die Werte werden bei jedem Update der Berichtsdefinition überschrieben.  
  
### <a name="rsclientprint-properties"></a>RSClientPrint-Eigenschaften  
  
|Eigenschaft|Typ|RW|Standardwert|Description|  
|--------------|----------|--------|-------------|-----------------|  
|MarginLeft|Double|RW|Berichteinstellung|Ruft den linken Rand ab bzw. legt ihn fest. Wird kein Wert vom Entwickler festgelegt oder im Bericht angegeben, wird 12,2 Millimeter als Standardwert verwendet.|  
|MarginRight|Double|RW|Berichteinstellung|Ruft den rechten Rand ab bzw. legt ihn fest. Wird kein Wert vom Entwickler festgelegt oder im Bericht angegeben, wird 12,2 Millimeter als Standardwert verwendet.|  
|MarginTop|Double|RW|Berichteinstellung|Ruft den oberen Rand ab bzw. legt ihn fest. Wird kein Wert vom Entwickler festgelegt oder im Bericht angegeben, wird 12,2 Millimeter als Standardwert verwendet.|  
|MarginBottom|Double|RW|Berichteinstellung|Ruft den unteren Rand ab bzw. legt ihn fest. Wird kein Wert vom Entwickler festgelegt oder im Bericht angegeben, wird 12,2 Millimeter als Standardwert verwendet.|  
|PageWidth|Double|RW|Berichteinstellung|Ruft die Seitenbreite ab bzw. legt sie fest. Der Standardwert, wenn keine Gruppe vom Entwickler oder in der Berichtsdefinition 215,9 Millimeter.|  
|PageHeight|Double|RW|Berichteinstellung|Ruft die Seitenhöhe ab bzw. legt sie fest. Wird kein Wert vom Entwickler oder in der Berichtsdefinition festgelegt, wird 279,4 Millimeter als Standardwert verwendet.|  
|Culture|Int32|RW|Browsergebietsschema|Gibt den Gebietsschemabezeichner (LCID) an. Mit diesem Wert wird die Maßeinheit für die Benutzereingaben bestimmt. Angenommen, eine Benutzertypen **3**, der Wert in Millimetern gemessen, wenn die Sprache Französisch oder Zoll, falls die Sprache Englisch (Vereinigte Staaten) ist. Zu den gültigen Werten zählen folgende: 1028, 1031, 1033, 1036, 1040, 1041, 1042, 2052, 3082.|  
|UICulture|String|RW|Clientkultur|Gibt die Zeichenfolgenlokalisierung des Dialogfelds an. Der Text im Dialogfeld Drucken ist in folgende Sprachen lokalisiert: Vereinfachtes Chinesisch, Traditionelles Chinesisch, Englisch, Französisch, Deutsch, Italienisch, Japanisch, Koreanisch und Spanisch. Zu den gültigen Werten zählen folgende: 1028, 1031, 1033, 1036, 1040, 1041, 1042, 2052, 3082.|  
|Authenticate|Boolean|RW|Falsch|Gibt an, ob das Steuerelement einen GET-Befehl für den Berichtsserver ausgibt, um eine Verbindung für das Drucken außerhalb der Sitzung zu initiieren.|  
  
### <a name="when-to-set-the-authenticate-property"></a>Festlegen der Authenticate-Eigenschaft  
 Wenn Sie von einer Browsersitzung heraus drucken, müssen Sie nicht Festlegen der **authentifizieren** Eigenschaft. Im Kontext einer aktiven Sitzung werden alle Anforderungen vom Drucksteuerelement an den Berichtsserver über den Browser verarbeitet. Der Browser legt die für die Kommunikation mit dem Berichtsserver erforderlichen Sitzungsvariablen fest.  
  
 Wenn Sie außerhalb der Sitzung (z. B. einen Bericht direkt an einen Drucker senden, ohne ihn zuvor zu öffnen) drucken, muss das Drucksteuerelement eine HTTP ausgeben **abrufen** Anforderung zum Einrichten der Sitzungs mit dem Berichtsserver her. Um die Umgehung der **abrufen** -Anforderung legen Sie **authentifizieren** auf **"true"**.  
  
 Nur müssen Sie die **abrufen** Anforderung bei Verwendung von Windows integrierte Sicherheit oder grundlegende Authentifizierung. Bei Verwendung der Formularauthentifizierung den **authentifizieren** Eigenschaft wird ignoriert. Der Anwendungscode muss die Sitzung festlegen und den Benutzer mithilfe der von Ihnen angegebenen benutzerdefinierten Sicherheitserweiterung authentifizieren. Wenn Sie die Formularauthentifizierung verwenden, müssen Sie den Ablaufwert im Authentifizierungscookie so festlegen, dass Sitzungen eine angemessene Zeit lang beibehalten werden. Ist der Wert zu niedrig, werden die Benutzer jedes Mal, wenn das Cookie abläuft, zur Eingabe ihrer Anmeldeinformationen aufgefordert.  
  
### <a name="clsids"></a>CLSIDs  
 Wenn Sie den Bericht lokal ausführen, verwenden Sie die folgenden CLSID-Werte.  
  
-   41861299-EAB2-4DCC-986C-802AE12AC499  
  
-   5554DCB0-700B-498D-9B58-4E40E5814405  
  
-   60677965-AB8B-464f-9B04-4BA871A2F17F  
  
 Wenn Sie den Bericht in Windows Azure SQL Reporting ausführen, verwenden Sie die folgenden CLSID-Werte.  
  
-   3DD32426-554D-48C0-A200-65D3BF880E38  
  
-   05662494-ACF9-446A-BE4C-7D3F7EA7F62F  
  
### <a name="rsprintclient-support-for-the-print-method"></a>RSPrintClient-Unterstützung für die Print-Methode  
 Die **RSClientPrint** -Objekt unterstützt die **Drucken** Methode verwendet, um das Dialogfeld Drucken zu starten. Die **Drucken** Methode hat die folgenden Argumente.  
  
|Argument|E/A|Typ|Description|  
|--------------|----------|----------|-----------------|  
|ServerPath|In|String|Gibt das virtuelle Verzeichnis des Berichtsservers an (z. B. `https://adventure-works/reportserver`).|  
|ReportPathParameters|In|String|Gibt den vollständigen Namen zum Bericht im Ordnernamespace des Berichtsservers einschließlich Parameter an. Berichte werden über den URL-Zugriff abgerufen. Beispiel: "/AdventureWorks Sample Reports/Employee Sales Summary&EmpID=1234"|  
|ReportName|In|String|Der kurze Name des Berichts (im Beispiel oben lautet der kurze Name Employee Sales Summary). Dieser Name wird im Dialogfeld Drucken und in der Druckerwarteschlange angezeigt.|  
  
### <a name="example"></a>Beispiel  
 Im folgende HTML-Beispiel wird gezeigt, wie die CAB-Datei an **Drucken** -Methode und Eigenschaften in JavaScript:  
  
 `<BODY onload="Print()">`  
  
 `<OBJECT ID="RSClientPrint" CLASSID="CLSID: 5554DCB0-700B-498D-9B58-4E40E5814405D3" CODEBASE="<URL to the .CAB file>#Version=<your application version information>" VIEWASTEXT></OBJECT>`  
  
 `<script language="javascript">`  
  
 `function Print()`  
  
 `{`  
  
 `RSClientPrint.MarginLeft = 12.7;`  
  
 `RSClientPrint.MarginTop = 12.7;`  
  
 `RSClientPrint.MarginRight = 12.7;`  
  
 `RSClientPrint.MarginBottom = 12.7;`  
  
 `RSClientPrint.Culture = 1033;`  
  
 `RSClientPrint.UICulture = 9;`  
  
 `RSClientPrint.Print('http://localhost/rtm', '%2fEmployee_Sales_Summary&ReportMonth=6&ReportYear=2004&EmpID=20', 'Employee_Sales_Summary')`  
  
 `}`  
  
 `</script>`  
  
 `</BODY>`  
  
## <a name="see-also"></a>Siehe auch  
 [Drucken von Berichten in einem Browser mit dem Drucksteuerelement &#40; Berichts-Generator und SSRS &#41;](../../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)   
 [Drucken von Berichten &#40; Berichts-Generator und SSRS &#41;](../../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [Geräteinformationseinstellungen für Bilder](../../../reporting-services/image-device-information-settings.md)  
  
  
