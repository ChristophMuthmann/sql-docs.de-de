---
title: "Unterstützen von mehreren Zielversionen in benutzerdefinierten Komponenten | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server (starting with 2016)
ms.assetid: ec611374-16bf-4a56-8fd9-45d3ddd7befc
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fea00f80ddaa43ee5bcd5d26ddcc515d2f6e849a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="support-multi-targeting-in-your-custom-components"></a>Unterstützen von mehreren Zielversionen in benutzerdefinierten Komponenten
 Sie können nun den SSIS-Designer in SQL Server Data Tools (SSDT) verwenden, um Pakete zu erstellen, zu verwalten und auszuführen, die auf SQL Server 2016, SQL Server 2014 oder SQL Server 2012 ausgerichtet sind. SSDT für Visual Studio 2015 können Sie unter [Download Latest SQL Server Data Tools (Herunterladen der aktuellen Version von SQL Server Data Tools)](../../ssdt/download-sql-server-data-tools-ssdt.md) herunterladen. 

 Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf ein Integration Services-Projekt, und wählen Sie **Eigenschaften** aus, um die Eigenschaftsseiten für das Projekt zu öffnen. Klicken Sie in der Registerkarte **Allgemein** in den **Konfigurationseigenschaften**auf die Eigenschaft **TargetServerVersion** , und wählen Sie dann SQL Server 2016, 2014 oder 2012 aus.  
   
 ![TargetServerVersion-Eigenschaft im Dialogfeld „Projekteigenschaften“](../../integration-services/media/targetserverversion2.png "TargetServerVersion property in project properties dialog box")  
 
 ## <a name="multiple-version-support-and-multi-targeting-for-custom-components"></a>Unterstützen von Versionen und Festlegen von Zielversionen für benutzerdefinierte Komponenten
 
Die fünf benutzerdefinierten SSIS-Erweiterungen unterstützen alle die Festlegung von Zielversionen.
-   Verbindungs-Manager
-   Aufgaben
-   Enumeratoren
-   Protokollanbieter
-   Datenflusskomponenten

Für verwaltete Erweiterungen lädt der SSIS-Designer die Erweiterungsversion für die angegebene Zielversion herunter. Beispiel:
-   Wenn die Zielversion SQL Server 2012 ist, lädt der Designer die SQL Server 2012-Version der Erweiterung herunter.
-   Wenn die Zielversion SQL Server 2016 ist, lädt der Designer die SQL Server 2016-Version der Erweiterung herunter.

COM-Erweiterungen unterstützen die Festlegung von Zielversionen nicht. Der SSIS-Designer lädt unabhängig von der angegebenen Zielversion immer die COM-Erweiterung für die aktuelle Version von SQL Server herunter.

## <a name="add-basic-support-for-multiple-versions-and-multi-targeting"></a>Hinzufügen grundlegender Unterstützung für mehrere Versionen und für die Festlegung von Zielversionen

Allgemeine Hinweise finden Sie unter [Getting your SSIS custom extensions to be supported by the multi-version support of SSDT 2015 for SQL Server 2016 (Unterstützen benutzerdefinierter SSIS-Erweiterungen durch die Zielversionsunterstützung von SSDT 2015 für SQL Server 2016)](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/). In diesem Blogbeitrag werden die folgenden Schritte bzw. Anforderungen beschrieben:

-   Bereitstellen von Assemblys in den entsprechenden Ordnern

-   Erstellen einer Erweiterungszuordnungsdatei für SQL Server 2014 und höhere Versionen

## <a name="add-code-to-switch-versions"></a>Hinzufügen von Code für Versionswechsel

### <a name="switch-versions-in-a-custom-connection-manager-task-enumerator-or-log-provider"></a>Wechseln zwischen Versionen in einem benutzerdefinierten Verbindungs-Manager, Enumerator, Protokollanbieter oder in einer benutzerdefinierten Aufgabe

Fügen Sie einem benutzerdefinierten Verbindungs-Manager, Enumerator, Protokollanbieter oder einer benutzerdefinierten Aufgabe eine Herabstufungslogik in der **SaveToXML**-Methode hinzu.

```csharp
public void SaveToXML(XmlDocument doc, IDTSInfoEvents events)
{
    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
    }

    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2012)
    {
         // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
    }
}
```

### <a name="switch-versions-in-a-custom-data-flow-component"></a>Wechseln zwischen Versionen in einer benutzerdefinierten Datenflusskomponente

Fügen Sie einem benutzerdefinierten Verbindungs-Manager, Enumerator, Protokollanbieter oder einer benutzerdefinierten Aufgabe eine Herabstufungslogik in der neuen **PerformDowngrade**-Methode hinzu.

```csharp
public override void PerformDowngrade(int pipelineVersion, DTSTargetServerVersion targetServerVersion)
{
    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
        ComponentMetaData.Version = 8;
    }

    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2012)
    {
          // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
        ComponentMetaData.Version = 6;
    }
}
```

## <a name="common-errors"></a>Häufige Fehler

### <a name="invalidcastexception"></a>InvalidCastException

**Fehlermeldung:** Das COM-Objekt des Typs „System.__ComObject“ kann nicht in den Schnittstellentyp „Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100“ umgewandelt werden. Dieser Vorgang konnte nicht durchgeführt werden, da der QueryInterface-Aufruf an die COM-Komponente für die Schnittstelle mit der IID „{BE8C48A3-155B-4810-BA5C-BDF68A659E9E}“ aufgrund des folgenden Fehlers nicht durchgeführt werden konnte: Schnittstelle nicht unterstützt (Ausnahme von HRESULT: 0x80004002 (E_NOINTERFACE)). (Microsoft.SqlServer.DTSPipelineWrap).

**Lösung:** Wenn Ihre benutzerdefinierte Erweiterung auf SSIS-Interop-Assemblys wie Microsoft.SqlServer.DTSPipelineWrap oder Microsoft.SqlServer.DTSRuntimeWrap verweist, legen Sie den Wert der Eigenschaft **Interop-Typen einbetten** auf FALSE fest.

![Interop-Typen einbetten](../../integration-services/extending-packages-custom-objects/media/embed-interop-types.png)

### <a name="unable-to-load-some-types-when-target-version-is-sql-server-2012"></a>Mehrere Typen können bei SQL Server 2012 als festgelegter Zielversion nicht geladen werden

Dieses Problem betrifft bestimmte Typen wie IErrorReportingService oder IUserPromptService.

**Fehlermeldung (Beispiel):** Der Typ „Microsoft.DataWarehouse.Design.IErrorReportingService“ in der Assembly „Microsoft.DataWarehouse, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91“ konnte nicht geladen werden.

**Problemumgehung:** Verwenden Sie anstelle der Schnittstellen ein Meldungsfenster (MessageBox), wenn als Zielversion SQL Server 2012 verwendet wird.

