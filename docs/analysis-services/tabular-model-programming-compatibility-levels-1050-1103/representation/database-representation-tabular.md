---
title: Datenbankdarstellung | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 16a233fb-f83b-4ca1-acb5-6186eca0a62c
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4c64a2963cf4011e8bb98cb23b6530fc2e3a4c81
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="database-representationtabular"></a>Datenbankdarstellung (tabellarisch)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Im tabellarischen Modus ist die Datenbank der Container für alle Objekte im tabellarischen Modell.  
  
## <a name="database-representation"></a>Datenbankdarstellung  
 Die Datenbank ist die Stelle, an der sich alle Objekte befinden, die ein tabellarisches Modell bilden. In der Datenbank findet der Entwickler Objekte wie Verbindungen, Tabellen, Rollen u.v.m. vor.  
  
### <a name="database-in-amo"></a>Datenbank in AMO  
 Wenn eine tabellarische Modelldatenbank mithilfe von AMO verwaltet wird, entspricht das <xref:Microsoft.AnalysisServices.Database>-Objekt in AMO 1:1 dem logischen Datenbankobjekt in einem tabellarischen Modell.  
  
> [!NOTE]  
>  Um Zugriff auf ein Datenbankobjekt in AMO zu erhalten, benötigt der Benutzer Zugriff auf ein Serverobjekt und muss eine Verbindung damit herstellen.  
  
### <a name="database-in-adomdnet"></a>Datenbank in ADOMD.Net  
 Wenn ADOMD verwendet wird, um eine tabellarische Modelldatenbank abzufragen, wird die Verbindung mit einer bestimmten Datenbank durch das <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekt erreicht.  
  
 Mit dem folgenden Codeabschnitt können Sie direkt eine Verbindung zu einer bestimmten Datenbank herstellen:  
  
```csharp  
using ADOMD = Microsoft.AnalysisServices.AdomdClient;  
…  
   ADOMD.AdomdConnection currrentCnx = new ADOMD.AdomdConnection("Data Source=<<server\instance>>;Catalog=<<database>>");  
   currrentCnx.Open();  
…  
  
```  
  
 Über ein vorhandenes Verbindungsobjekt (das nicht geschlossen wurde) können Sie auch von der aktuellen Datenbank zu einer anderen Datenbank wechseln, wie im folgenden Codeausschnitt gezeigt:  
  
```csharp  
currentCnx.ChangeDatabase("myOtherDatabase");  
  
```  
  
## <a name="database-in-amo"></a>Datenbank in AMO  
 Wenn Sie AMO verwenden, um ein Datenbankobjekt zu verwalten, beginnen Sie mit einem <xref:Microsoft.AnalysisServices.Server>-Objekt. Suchen Sie dann Ihre Datenbank in der Datenbankauflistung, oder erstellen Sie eine neue Datenbank, indem Sie sie der Auflistung hinzufügen.  
  
 Der folgende Codeausschnitt veranschaulicht die Schritte, mit denen eine Verbindung mit einem Server hergestellt und eine leere Datenbank erstellt wird, nachdem überprüft wurde, dass die Datenbank noch nicht vorhanden ist:  
  
```  
  
AMO.Server CurrentServer = new AMO.Server();  
try  
{  
    CurrentServer.Connect(currentServerName);  
}  
catch (Exception cnxException)  
{  
    MessageBox.Show(string.Format("Error while trying to connect to server: [{0}]\nError message: {1}", currentServerName, cnxException.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
    return;  
}  
newDatabaseName = DatabaseName.Text;  
if (CurrentServer.Databases.Contains(newDatabaseName))  
{  
    return;  
}  
try  
{  
    AMO.Database newDatabase = CurrentServer.Databases.Add(newDatabaseName);  
  
    CurrentServer.Update();  
}  
catch (Exception createDBxc)  
{  
    MessageBox.Show(String.Format("Database [{0}] couldn't be created.\n{1}", newDatabaseName, createDBxc.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
    newDatabaseAvailable = false;  
}  
  
```  
  
 Ein praktisches Verständnis für die Verwendung von AMO zur Erstellung und Bearbeitung von datenbankdarstellungen, finden Sie in der Quellcode in der Stichprobe Tabular AMO 2012; Prüfen Sie insbesondere die Quelldatei: Database.cs. Das Beispiel ist auf Codeplex verfügbar. Beispielcode wird nur zur Verdeutlichung der hier erläuterten logischen Konzepte bereitgestellt und sollte nicht in einer Produktionsumgebung verwendet werden.  
  
  
