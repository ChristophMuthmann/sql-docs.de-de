---
title: Erste Schritte mit dem ReportViewer 2016-Steuerelement | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 01a821c4-2920-400c-be03-93d26c749bb1
caps.latest.revision: "12"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.openlocfilehash: dff598efce33f778359c2b6fb4c3a0184f2b88f6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="integrating-reporting-services-using-reportviewer-controls---get-started"></a>Integrieren von Reporting Services mit den ReportViewer-Steuerelementen: Erste Schritte

Erfahren Sie, wie Entwickler über das Reporting Services 2016 ReportViewer-Steuerelement paginierte Berichte in ASP.NET-Websites und Windows Forms-Apps einbetten können. Sie können das Steuerelement zu einem neuen Projekt hinzufügen oder ein vorhandenes Projekt aktualisieren.

## <a name="adding-the-reportviewer-control-to-a-new-web-project"></a>Hinzufügen des ReportViewer-Steuerelement zu einem neuen Webprojekt

1. Erstellen Sie eine **leere ASP.NET-Website**, oder öffnen Sie ein vorhandenes ASP.NET-Projekt.

    ![ssRS-Erstellen-Neues-ASPNET-Projekt](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. Installieren Sie das Steuerelemente-NuGet-Paket für ReportViewer 2016 über die **Manager-Konsole für NuGet-Pakete**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. Fügen Sie dem Projekt eine neue ASPX-Seite hinzu, und registrieren Sie die ReportViewer-Steuerelementassembly zur Verwendung auf der Seite.

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. Fügen Sie **ScriptManagerControl** zu der Seite hinzu.

5. Fügen Sie das ReportViewer-Steuerelement zu der Seite hinzu. Der untenstehende Ausschnitt kann aktualisiert werden, um auf einen gehosteten Bericht auf einem Remoteberichtsserver zu verweisen.

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
Die letzte Seite sollte wie folgt aussehen:

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="Sample" %>

<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <meta http-equiv="X-UA-Compatible" content="IE=edge" /> 
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
    <asp:ScriptManager runat="server"></asp:ScriptManager>        
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
            <ServerReport ReportServerUrl="http://AContosoDepartment/ReportServer" ReportPath="/LatestSales" />
        </rsweb:ReportViewer>
    </form>
</body>
</html>

```

## <a name="updating-an-existing-project-to-use-the-reportviewer-control"></a>Aktualisieren eines vorhandenen Projekts zur Verwendung des ReportViewer-Steuerelements

Fügen Sie das Steuerelement über NuGet hinzu, und aktualisieren Sie die Verweise der Assembly auf Version *14.0.0.0*, um das ReportViewer 2016-Steuerelement zu einem vorhandenen Projekt hinzuzufügen. Dafür müssen Sie außerdem die Datei „web.config“ des Projekts und alle ASPX-Projekte aktualisieren, die auf das ReportViewer-Steuerelement verweisen.

### <a name="sample-webconfig-changes"></a>Beispiel für web.config-Änderungen

```
<?xml version="1.0"?>
<!--
  For more information on how to configure your ASP.NET application, please visit
  http://go.microsoft.com/fwlink/?LinkId=169433
  -->
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.5.2">
      <assemblies>
        <!-- All assemblies updated to version 14.0.0.0. -->
        <add assembly="Microsoft.ReportViewer.Common, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.DataVisualization, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.Design, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.ProcessingObjectModel, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebDesign, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WinForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </assemblies>
      <buildProviders>
        <!-- Version updated to 14.0.0.0. -->
        <add extension=".rdlc"
          type="Microsoft.Reporting.RdlBuildProvider, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </buildProviders>
    </compilation>
    <httpRuntime targetFramework="4.5.2"/>
    <httpHandlers>
      <!-- Version updated to 14.0.0.0 -->
      <add path="Reserved.ReportViewerWebControl.axd" verb="*"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"
        validate="false"/>
    </httpHandlers>
  </system.web>
  <system.webServer>
    <validation validateIntegratedModeConfiguration="false"/>
    <modules runAllManagedModulesForAllRequests="true"/>
    <handlers>
      <!-- Version updated to 14.0.0.0 -->
      <add name="ReportViewerWebControlHandler" verb="*" path="Reserved.ReportViewerWebControl.axd" preCondition="integratedMode"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
    </handlers>
  </system.webServer>
</configuration>
```

### <a name="sample-aspx"></a>Beispiel für eine ASPX-Datei

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 14.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="adding-the-reportviewer-control-to-a-new-windows-forms-project"></a>Hinzufügen des ReportViewer-Steuerelements zu einem neuen Windows Forms-Projekt

1. Erstellen Sie eine neue **Windows Forms-Anwendung**, oder öffnen Sie ein vorhandenes Projekt.

    ![ssRS-Erstellen-Neues-Winforms-Projekt](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. Installieren Sie das Steuerelemente-NuGet-Paket für ReportViewer 2016 über die **Manager-Konsole für NuGet-Pakete**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. Fügen Sie entweder ein neues Steuerelement aus Code hinzu oder [fügen Sie der Toolbox das Steuerelement hinzu](##adding-control-to-visual-studio-toolbar).

    ```
    private Microsoft.Reporting.WinForms.ReportViewer reportViewer1;
    
    private void InitializeComponent()
    {
        this.reportViewer1 = new Microsoft.Reporting.WinForms.ReportViewer();
        this.SuspendLayout();
        // 
        // reportViewer1
        // 
        this.reportViewer1.Location = new System.Drawing.Point(168, 132);
        this.reportViewer1.Name = "reportViewer1";
        this.reportViewer1.ServerReport.BearerToken = null;
        this.reportViewer1.Size = new System.Drawing.Size(396, 246);
        this.reportViewer1.TabIndex = 0;
        // 
        // Form1
        // 
        this.Controls.Add(this.reportViewer1);
    }
    ```

## <a name="how-to-set-100-height-on-the-report-viewer-2016-control"></a>Festlegen einer Höhe von 100 Prozent für das ReportViewer 2016-Steuerelement

Das neue ReportViewer 2016-Steuerelement wurde für HTML5-Seiten im Standardmodus optimiert und funktioniert in allen modernen Browsern. In der Vergangenheit hat die 100 Prozent-Höheneigenschaft für das RVC-Steuerelement funktioniert, auch wenn für die Vorgängerelemente keine Höhe angegeben war. Dieses Verhalten wurde in HTML5 geändert. Wenn Sie diese Eigenschaft für das neue RVC-Steuerelement festlegen, wird sie nur korrekt ausgeführt, wenn für das übergeordnete Element eine Höhe festgelegt ist, d.h., es darf kein automatischer Wert festgelegt sein, oder wenn für alle Vorgängerelemente von RVC eine Höhe von 100 Prozent festgelegt ist.

Im Folgenden sind zwei Beispiele aufgeführt, in denen erklärt wird, wie Sie dies festlegen.

### <a name="by-setting-the-height-of-all-the-parent-elements-to-100"></a>Festlegen der Höhe für alle übergeordneten Elemente auf 100 Prozent

```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <style>
        html,body,form,#div1 {
            height: 100%; 
        }
    </style>
   </head>
<body>
    <form id="form1" runat="server">
    <div id="div1" >
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="http://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

### <a name="by-setting-the-style-height-attribute-on-the-parent-of-the-reportviewer-control"></a>Festlegen des Formathöhenattributs auf das übergeordnete Steuerelement des ReportViewer-Steuerelements

Weitere Informationen zu den Längen der Viewports in Prozent finden Sie unter [Viewport-percentage lengths (Längen der Viewports in Prozent)](https://www.w3.org/TR/css3-values/#viewport-relative-lengths).

```
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
</head>
<body>
    <form id="form1" runat="server">
    <div style="height:100vh;">
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="http://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>

```

## <a name="adding-control-to-visual-studio-toolbar"></a>Hinzufügen eines Steuerelements zur Visual Studio-Symbolleiste

Das ReportViewer-Steuerelement wird jetzt als NuGet-Paket versendet. Aus diesem Grund wird Ihnen standardmäßig nicht das ReportViewer-Steuerelement in der Visual Studio-Toolbox angezeigt. Sie können das Steuerelement wie folgt zur Toolbox hinzufügen:

1. Installieren Sie wie zuvor erwähnt das NuGet-Paket entweder für WinForms oder für WebForms.

2. Entfernen Sie das ReportViewer-Steuerelement aus der Toolbox. Dabei handelt es sich um das Steuerelement mit einer Version von 12.x.

    ![ssRS-remove-old-rvcontrol-toolbox](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. Klicken Sie mit der rechten Maustaste zunächst auf eine beliebige Stelle in der Toolbox und anschließend auf **Elemente auswählen**.

    ![ssRS-toolbox-choose-item](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. Klicken Sie unter den **.NET Framework-Komponenten** auf **Durchsuchen**.

    ![ssRS-toolbox-browse](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. Klicken Sie in dem von Ihnen installierten NuGet-Paket auf **Microsoft.ReportViewer.WinForms.dll** oder **Microsoft.ReportViewer.WebForms.dll**.

    > [!NOTE] 
    > Das NuGet-Paket wird im Projektmappenverzeichnis Ihres Projekts installiert. Der Pfad zur DLL ähnelt einem der folgenden Pfade: `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40` oder `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`.

6. Das neue Steuerelement sollte jetzt in der Toolbox angezeigt werden. Sie können es nun in eine andere Registerkarte in der Toolbox verschieben, wenn Sie möchten.

    ![ssRS-toolbox-rvcontrol](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

### <a name="things-to-be-aware-of"></a>Worauf Sie achten sollten

- Dadurch fügen Sie einen Verweis auf das installierte NuGet-Paket zu Ihrem aktuellen Projekt hinzu. Das Element in der Toolbox bleibt für andere Projekte erhalten. Wenn Sie das NuGet-Paket in einer neuen Projektmappe oder einem neuen Projekt speichern, verweist das Toolboxelement unter Umständen auf eine ältere Version. 

- Das Steuerelement bleibt in der Toolbox, auch wenn die Assembly nicht mehr verfügbar ist. Wenn dieses Projekt gelöscht wurde, wird von Visual Studio ein Fehler ausgelöst, wenn Sie versuchen, das Steuerelement aus der Toolbox hinzuzufügen. Um diesen Fehler zu beheben, müssen Sie das Steuerelement aus der Toolbox entfernen und es über die vorstehend beschriebenen Schritte erneut hinzufügen.


## <a name="common-issues"></a>Häufige Probleme
    
- Das ReportViewer 2016-Steuerelement ist für die Verwendung mit modernen Browsern bestimmt. Das Steuerelement funktioniert möglicherweise nicht, wenn Browser die Webseite in einem mit Internet Explorer kompatiblen Modus rendern. Für Intranet-Websites ist möglicherweise ein META-Tag erforderlich, um Einstellungen außer Kraft zu setzen, mit denen Intranetseiten im Kompatibilitätsmodus gerendert werden können.

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
## <a name="providing-feedback"></a>Senden von Feedback

Informieren Sie das Team über mögliche Probleme mit dem Steuerelement über die [MSDN Reporting Services-Foren](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices) oder per E-Mail unter [RVCFeedback@microsoft.com](mailto:RVCFeedback@microsoft.com).

## <a name="see-also"></a>Siehe auch

[Datensammlung im ReportingViewer 2016-Steuerelement](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
Haben Sie dazu Fragen? [Besuchen Sie das Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)

