---
title: "Unterstützung der Festlegung von Zielversionen in Ihre benutzerdefinierten Komponenten | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016)
ms.assetid: ec611374-16bf-4a56-8fd9-45d3ddd7befc
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 57ac95d7883ce47e1a39d4d50d3f60b968bccf21
ms.contentlocale: de-de
ms.lasthandoff: 09/21/2017

---
# <a name="support-multi-targeting-in-your-custom-components"></a>Festlegung von Zielversionen in Ihre benutzerdefinierten Komponenten zu unterstützen
 Sie können nun SSIS-Designer in SQL Server Data Tools (SSDT) erstellen, verwalten und Ausführen von Paketen, für SQL Server 2016, SQL Server 2014 oder SQL Server 2012. SSDT für Visual Studio 2015 finden Sie unter [herunterladen neueste SQL Server Data Tools](/sql-docs/docs/ssdt/download-sql-server-data-tools-ssdt). 

 Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf ein Integration Services-Projekt, und wählen Sie **Eigenschaften** aus, um die Eigenschaftsseiten für das Projekt zu öffnen. Klicken Sie in der Registerkarte **Allgemein** in den **Konfigurationseigenschaften**auf die Eigenschaft **TargetServerVersion** , und wählen Sie dann SQL Server 2016, 2014 oder 2012 aus.  
   
 ![TargetServerVersion-Eigenschaft im Dialogfeld Projekt](../../integration-services/media/targetserverversion2.png "TargetServerVersion-Eigenschaft in den Projekteigenschaften (Dialogfeld)")  
 
 ## <a name="multiple-version-support-and-multi-targeting-for-custom-components"></a>Mehrere Unterstützung von Berichtsversionen und Festlegung von Zielversionen für benutzerdefinierte Komponenten
 
Alle fünf Typen von benutzerdefinierten SSIS-Erweiterungen unterstützen die Festlegung von Zielversionen.
-   Verbindungs-Manager
-   Aufgaben
-   Enumeratoren
-   Protokollanbieter
-   Datenflusskomponenten

Für managed Extensions lädt SSIS-Designer die Version der Erweiterung für die Version des angegebenen Zielservers. Beispiel:
-   Wenn die Zielversion SQL Server 2012 ist, lädt den Designer die 2012-Version der Erweiterung an.
-   Wenn die Zielversion SQL Server 2016 ist, lädt den Designer 2016-Version der Erweiterung an.

Com-Erweiterungen unterstützen die Festlegung von Zielversionen nicht. SSIS-Designer lädt immer die COM-Erweiterung für die aktuelle Version von SQL Server, unabhängig von der Version des angegebenen Zielservers.

## <a name="add-basic-support-for-multiple-versions-and-multi-targeting"></a>Fügen Sie grundlegende Unterstützung für mehrere Versionen und Festlegung von Zielversionen

Grundlegende Anleitung finden Sie unter [erste Ihre benutzerdefinierten SSIS-Erweiterungen, die von der Unterstützung mehrerer Versionen von SSDT 2015 für SQL Server 2016 unterstützt werden](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/). In diesem Blogbeitrag wird beschrieben, die folgenden Schritte oder Anforderungen.

-   Bereitstellen von Assemblys in die entsprechenden Ordner.

-   Erstellen Sie eine Erweiterung Zuordnungsdatei für SQL Server 2014 und hohe Versionen.

## <a name="add-code-to-switch-versions"></a>Fügen Sie Code zum Wechseln von Versionen

### <a name="switch-versions-in-a-custom-connection-manager-task-enumerator-or-log-provider"></a>Wechseln Sie in einem benutzerdefinierten Verbindungs-Manager, der Aufgabe, Enumerator oder Protokollanbieter Versionen

Fügen Sie für einen benutzerdefinierten Verbindungs-Manager, der Task, der Enumerator oder Protokollanbieter, Downgrade für die Logik in der **SaveToXML** Methode.

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

### <a name="switch-versions-in-a-custom-data-flow-component"></a>Wechseln Sie in einer benutzerdefinierten Datenflusskomponente Versionen

Fügen Sie für einen benutzerdefinierten Verbindungs-Manager, der Task, der Enumerator oder Protokollanbieter, Downgrade für die Logik in der neuen **PerformDowngrade** Methode.

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

### <a name="invalidcastexception"></a>InvalidCastException-Ausnahme

**Fehlermeldung.** "__ComObject" Schnittstelle Typ kann nicht Umwandlung COM-Objekt des Typs "Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100". Dieser Vorgang ist fehlgeschlagen, da der Aufruf von QueryInterface auf die COM-Komponente für die Schnittstelle mit IID "{BE8C48A3-155B-4810-BA5C-BDF68A659E9E}" aufgrund des folgenden Fehlers: keine Schnittstelle unterstützt (Ausnahme von HRESULT: 0 x 80004002 (E_NOINTERFACE)). (Microsoft.SqlServer.DTSPipelineWrap).

**Die Lösung.** Wenn die benutzerdefinierte Erweiterung SSIS-Interop-Assemblys wie Microsoft.SqlServer.DTSPipelineWrap oder Microsoft.SqlServer.sqltask verweist, legen Sie den Wert von der **Interoptypen** Eigenschaft ** "false" ".

![Einbetten von Interop-Typen](../../integration-services/extending-packages-custom-objects/media/embed-interop-types.png)

### <a name="unable-to-load-some-types-when-target-version-is-sql-server-2012"></a>Kann nicht einige Typen geladen, wenn die Zielversion SQL Server 2012 ist

Dieses Problem wirkt sich auf bestimmte Typen, z. B. IErrorReportingService oder IUserPromptService.

**Fehlermeldung (Beispiel).** Typ "Microsoft.DataWarehouse.Design.IErrorReportingService" konnte nicht aus der Assembly geladen "Microsoft.DataWarehouse, Version = 13.0.0.0, Culture = Neutral, PublicKeyToken = 89845dcd8080cc91".

**Dieses Problem zu umgehen.** Verwenden Sie eine MessageBox anstelle dieser Schnittstellen an, wenn die Zielversion SQL Server 2012 ist.


