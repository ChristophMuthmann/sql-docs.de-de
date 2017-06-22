---
title: Die Datenerfassung im ReportViewer-Steuerelement 2016 | Microsoft Docs
ms.custom: 
ms.date: 09/06/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
caps.latest.revision: 2
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4e8b0226c27380bd2089acf8d2d6c8d7b27c7c5b
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>Integrieren von Reporting Services mithilfe von ReportViewer-Steuerelementen - Datensammlung
Standardmäßig erfasst das ReportViewer-Steuerelement Nutzungsinformationen damit Microsoft besser nachvollziehen, wie Kunden werden mithilfe des Steuerelements. Erstellen Sie ein besseres Verständnis der wie Kunden bereitstellen und die Viewer-Steuerelement verwenden, kann künftige Entwicklungen auf Verbesserungen konzentrieren, die den größten Nutzen für Kunden bereitstellen.

Eine Erklärung der Datensammlungs- und Datennutzungsverfahren der Microsoft SQL Server 2016-Releases sowie anderer Produkte und Dienste finden Sie in diesen [Datenschutzbestimmungen von Microsoft](https://www.microsoft.com/EN-US/privacystatement/SQLServer/Default.aspx).

## <a name="opting-out-of-telemetry"></a>Wenn Sie keine Telemetrie

Telemetrie kann programmgesteuert über die "EnableTelemetry" deaktiviert werden. Dies kann erfolgen durch Bearbeiten der ASPX-Seite, die das Steuerelement hostet

```
\<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
\</rsweb:ReportViewer>
```

Oder pragmatically, bevor das Steuerelement etwa wie in der Hostseite Page_Load Aufruf gerendert wird.
    
```
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>Siehe auch

[Verwenden das WebForms-ReportViewer-Steuerelement](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[Integrieren von Reporting Services, die mit den ReportViewer-Steuerelementen](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 




