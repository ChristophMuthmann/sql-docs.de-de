---
title: Erste Schritte mit das Steuerelement ReportViewer 2016 | Microsoft Docs
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
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a6a0bbee9141df565966df3e90f396e33c9b96a7
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
<a id="integrating-reporting-services-using-reportviewer-controls---get-started" class="xliff"></a>
# Integrieren von Reporting Services mithilfe von ReportViewer-Steuerelemente – erste Schritte

Erfahren Sie, wie Entwickler paginierte Berichte in ASP.NET-Websites und Windows Forms-apps über das Reporting Services 2016 ReportViewer-Steuerelement einbetten können. Sie können das Steuerelement ein neues Projekt hinzufügen oder aktualisieren ein vorhandenes Projekts.

<a id="adding-the-reportviewer-control-to-a-new-web-project" class="xliff"></a>
## Das ReportViewer-Steuerelement hinzufügen, um ein neues Webprojekt

1. Erstellen Sie ein neues **leere ASP.NET-Website** oder ein vorhandenes ASP.NET-Projekt öffnen.

    ![SsRS--neues-ASPNET-Projekt erstellen](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. Installieren Sie das ReportViewer-2016 Steuerelement NuGet-Paket über die **NuGet-Paket-Manager-Konsole**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. Fügen Sie eine neue ASPX-Seite auf das Projekt, und registrieren Sie das ReportViewer-Steuerelement-Assembly für die Verwendung auf der Seite.

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. Hinzufügen einer **ScriptManagerControl** auf der Seite.

5. Fügen Sie das ReportViewer-Steuerelement auf der Seite hinzu. Der Codeausschnitt unten kann aktualisiert werden, um einen Bericht auf einem Remoteberichtsserver gehostet zu verweisen.

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
Die letzte Seite sollte wie folgt aussehen.

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

<a id="updating-an-existing-project-to-use-the-reportviewer-control" class="xliff"></a>
## Aktualisiert ein vorhandenes Projekt aus, um das ReportViewer-Steuerelement zu verwenden.

Verwenden des 2016 ReportViewer-Steuerelements in einem vorhandenen Projekt, fügen Sie das Steuerelement über Nuget und aktualisieren die Verweise auf Version der Assembly vornehmen *14.0.0.0*. Dies umfasst das Aktualisieren des Projekts "Web.config" und alle ASPX-Seiten, die das ReportViewer-Steuerelement verweisen.

<a id="sample-webconfig-changes" class="xliff"></a>
### Beispiel "Web.config" geändert

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

<a id="sample-aspx" class="xliff"></a>
### Aspx-Beispiel

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 14.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

<a id="adding-the-reportviewer-control-to-a-new-windows-forms-project" class="xliff"></a>
## Das ReportViewer-Steuerelement hinzufügen, um ein neues Windows Forms-Projekt

1. Erstellen Sie ein neues **Windows Forms-Anwendung** oder ein vorhandenes Projekt öffnen.

    ![SsRS--neues-Winforms-Projekt erstellen](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. Installieren Sie das ReportViewer-2016 Steuerelement NuGet-Paket über die **NuGet-Paket-Manager-Konsole**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. Fügen Sie ein neues Steuerelement aus dem Code oder [fügen Sie das Steuerelement zur Toolbox](##adding-control-to-visual-studio-toolbar).

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

<a id="how-to-set-100-height-on-the-report-viewer-2016-control" class="xliff"></a>
## Zum Festlegen von 100 % Höhe im Berichts-Viewer 2016-Steuerelement

Das neue Steuerelement des Berichts-Viewer 2016 für HTML5-Standards-Modus Seiten optimiert ist und funktioniert in allen modernen Browsern. In der Vergangenheit mit dem alten RVC-Steuerelement beim Festlegen der Höheneigenschaft von 100 % arbeitet er auch wenn keine Vorgänger Höhe angegeben hatten. Dieses Verhalten wurde in HTML5 geändert. Wenn Sie diese Eigenschaft auf dem neuen RVC Steuerelement festlegen, sie ordnungsgemäß funktioniert nur, wenn das übergeordnete Element eine definierte Höhe verfügt, d. h. kein Wert von "Auto" oder alle Vorfahren RVC haben Höhe von 100 % zu.

Im folgenden sind die beiden Beispiele dazu.

<a id="by-setting-the-height-of-all-the-parent-elements-to-100" class="xliff"></a>
### Durch Festlegen der Höhe aller übergeordneten Elemente auf 100 %

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

<a id="by-setting-the-style-height-attribute-on-the-parent-of-the-reportviewer-control" class="xliff"></a>
### Durch Festlegen der Formatvorlage Height-Attribut für das übergeordnete Element des Reportviewer-Steuerelements

Weitere Informationen, Viewports Prozentsatz Längen, finden Sie unter [Viewport Prozentsatz Längen](https://www.w3.org/TR/css3-values/#viewport-relative-lengths).

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

<a id="adding-control-to-visual-studio-toolbar" class="xliff"></a>
## Hinzufügen des Steuerelements auf der Symbolleiste von Visual Studio

Das ReportViewer-Steuerelement ist jetzt als ein NuGet-Paket zur Verfügung gestellt. Aus diesem Grund sehen Sie nicht das ReportViewer-Steuerelement in der Standardeinstellung in der Visual Studio-Toolbox angezeigt. Sie können das Steuerelement zur Toolbox hinzufügen, indem Sie wie folgt.

1. Installieren Sie das NuGet-Paket für die Windows Forms- oder der WebForms wie oben erwähnt.

2. Entfernen Sie das ReportViewer-Steuerelement, das aufgeführt ist, in der Toolbox. Dies ist das Steuerelement mit einer Version von 12.x.

    ![SsRS-Remove-alte-Rvcontrol-toolbox](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. Mit der rechten Maustaste an einer beliebigen Stelle in der Toolbox in, und wählen Sie dann **Elemente auswählen...** .

    ![SsRS-Toolbox-wählen-Element](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. Auf der **.NET Framework-Komponenten**Option **Durchsuchen**.

    ![SsRS-Toolbox-durchsuchen](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. Wählen Sie die **Microsoft.ReportViewer.WinForms.dll** oder **Microsoft.ReportViewer.WebForms.dll** aus dem NuGet-Paket, das Sie installiert haben.

    > [!NOTE] 
    > Das NuGet-Paket wird in dem Projektmappenverzeichnis des Projekts installiert werden. Der Pfad zur Dll wird ähnlich der folgenden sein: `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40` oder `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`.

6. Das neue Steuerelement sollte in der Toolbox angezeigt werden. Anschließend können Sie es in eine andere Registerkarte in der Toolbox verschieben, wenn Sie möchten.

    ![SsRS-Toolbox-rvcontrol](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

<a id="things-to-be-aware-of" class="xliff"></a>
### Aspekte zu berücksichtigen

- Dadurch wird einen Verweis auf die installierten NuGet-Paket innerhalb des aktuellen Projekts hinzugefügt. Das Element in der Toolbox wird auf andere Projekte beibehalten werden. Wenn Sie in einem neuen Projektmappe/Projekt das NuGet-Paket installieren, kann das Toolboxelement eine ältere Version verweisen. 

- Das Steuerelement wird in der Toolbox verbleiben, selbst wenn die Assembly nicht mehr verfügbar ist. Wenn dieses Projekt gelöscht wurde, wird Visual Studio ein Fehler ausgelöst, wenn Sie versuchen, und fügen Sie das Steuerelement aus der Toolbox. Um diesen Fehler zu beheben, entfernen Sie das Steuerelement aus der Toolbox, und mit den oben beschriebenen Schritten erneut hinzufügen.


<a id="common-issues" class="xliff"></a>
## Häufige Probleme
    
- Das Steuerelement ReportViewer 2016 dient mit modernen Browsern verwendet werden soll. Das Steuerelement möglicherweise nicht ausgeführt werden, wenn der Browser die Webseite in einem Internet Explorer-Kompatibilitätsmodus rendern. Intranetsites möglicherweise ein Meta-Tag, um die Einstellung zu überschreiben, das Rendern von Intranetseiten im Kompatibilitätsmodus empfehlen.

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
<a id="providing-feedback" class="xliff"></a>
## Bereitstellen von feedback

Lassen Sie das Team Probleme erfahren Sie mit dem Steuerelement auftreten, auf die [Reporting Services MSDN-Foren](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices) oder per e-Mail an [ RVCFeedback@microsoft.com ](mailto:RVCFeedback@microsoft.com).

<a id="see-also" class="xliff"></a>
## Siehe auch

[Die Datensammlung im Steuerelement ReportingViewer 2016](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
Weiteren Fragen wenden? [Wiederholen Sie den Reporting Services-forum](http://go.microsoft.com/fwlink/?LinkId=620231)


