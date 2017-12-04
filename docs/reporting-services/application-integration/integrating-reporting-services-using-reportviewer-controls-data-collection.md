---
title: Datensammlung im ReportViewer-Steuerelement 2016 | Microsoft-Dokumentation
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
caps.latest.revision: "2"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b2f5f4743b838598aeb5f74271fa063af9bb60f3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>Integrieren von Reporting Services mit den ReportViewer-Steuerelementen: Datensammlung
Standardmäßig erfasst das ReportViewer-Steuerelement anonyme Nutzungsinformationen, damit Microsoft besser nachvollziehen kann, wie die Steuerelemente von den Kunden verwendet werden. Durch ein besseres Verständnis darüber, wie die Kunden Bereitstellungen durchführen und das Viewer-Steuerelement verwenden, können zukünftige Entwicklungen so verbessert werden, dass für den Kunden der größtmögliche Nutzen erzielt wird.

Eine Erklärung der Datensammlungs- und Datennutzungsverfahren der Microsoft SQL Server 2016-Releases sowie anderer Produkte und Dienste finden Sie in diesen [Datenschutzbestimmungen von Microsoft](https://www.microsoft.com/EN-US/privacystatement/SQLServer/Default.aspx).

## <a name="opting-out-of-telemetry"></a>Deaktivieren der Telemetrie

Die Telemetrie kann programmgesteuert über „EnableTelemetry“ deaktiviert werden. Dies kann durch Bearbeiten der ASPX-Seite erfolgen, die das Steuerelement hostet,

```
\<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
\</rsweb:ReportViewer>
```

oder bevor das Steuerelement gerendert wird, z.B. durch einen Aufruf der Page_Load-Methode der Hostingseite.
    
```
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>Siehe auch

[Verwenden des ReportViewer-Steuerelements in WebForms](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[Integrieren von Reporting Services mithilfe der ReportViewer-Steuerelemente](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 



