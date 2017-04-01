---
title: "Voraussetzungen f&#252;r die exemplarischen Vorgehensweisen f&#252;r Data Science (SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 0b0582b8-8843-4787-94a8-2e28bdc04fb2
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# Voraussetzungen f&#252;r die exemplarischen Vorgehensweisen f&#252;r Data Science (SQL Server R Services)
Es wird empfohlen, die exemplarischen Vorgehensweisen auf einer R-Arbeitsstation durchzuführen, die eine Verbindung mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer im demselben Netzwerk herstellen kann. Sie können die exemplarische Vorgehensweise auch auf einem Computer ausführen, der sowohl über [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als auch die über eine Entwicklungsumgebung verfügt. 
  
  
## <a name="install-sql-server-2016-r-services-in-database"></a>Installieren von SQL Server 2016 R Services (datenbankintern)  
Sie benötigen Zugriff auf eine Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  , auf der [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] installiert ist. Weitere Informationen zum Einrichten von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]finden Sie unter [Einrichten von SQL Server R Services (datenbankintern)](https://msdn.microsoft.com/library/mt696069.aspx).  
  
  
> [!IMPORTANT]  
> Verwenden Sie [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder höher. Frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützen keine Integration mit R, obwohl Sie ältere SQL-Datenbanken als ODBC-Datenquelle verwenden können.  
  
## <a name="install-an-r-development-environment"></a>Installieren einer R-Entwicklungsumgebung  
Sie benötigen eine R-Entwicklungsumgebung oder ein beliebiges anderes Befehlszeilentool, das R-Befehle ausführen kann, um diese exemplarische Vorgehensweise auf Ihrem Computer abschließen zu können.    
  
- **R Tools for Visual Studio** (R-Tools für Visual Studio) ist ein kostenloses Plug-In, das IntelliSense, Debugging sowie Unterstützung für Microsoft R Server und SQL Server R Services bietet. Gehen Sie unter [R Tools for Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx)(R-Tools für Visual Studio), um es herunterzuladen.  
    
- **Microsoft R Client** ist ein schlankes Entwicklungstool, das die Entwicklung in R mit den ScaleR-Paketen unterstützt. Unter [Erste Schritte mit Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-get-started) können Sie es herunterladen.
  
- **RStudio** ist eine der beliebtesten Umgebungen für die Entwicklung von R. Weitere Informationen finden Sie unter [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/).  
  
    Sie können jedoch dieses Tutorial nicht mit einer generischen Installation von RStudio oder einer anderen Umgebung abschließen. Sie müssen auch die R-Pakete und Verbindungsbibliotheken für Microsoft R Open installieren. Weitere Informationen finden Sie unter [Einrichten eines Data Science-Clients](https://msdn.microsoft.com/library/mt696067.aspx).  

- R-Tools (R.exe, RTerm.exe, RScripts.exe) werden standardmäßig bei der Installation von [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] installiert. Wenn Sie keine IDE installieren möchten, können Sie diese Tools verwenden.  
  
  
## <a name="get-permissions-to-connect-to-sql-server"></a>Berichtigungen zum Herstellen einer Verbindung zu SQL Server erhalten  
In dieser exemplarischen Vorgehensweise stellen Sie eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her, um Skripts auszuführen und Daten hochzuladen. Zu diesem Zweck müssen Sie über einen gültigen Login auf dem Datenbankserver verfügen.  Sie können entweder einen SQL-Anmeldenamen oder die integrierte Windows-Authentifizierung verwenden. Bitten Sie den Datenbankadministrator, Ihnen auf dem Server für die Datenbank, in der Sie R verwenden möchten, ein Konto mit den folgenden Berechtigungen zu erstellen:  
  
-   Erstellen von Datenbanken, Tabellen, Funktionen und gespeicherten Prozeduren    
-   Einfügen von Daten in eine Tabelle  
  
  
## <a name="start-the-walkthrough"></a>Starten der exemplarischen Vorgehensweise  
[Lektion 1: Vorbereiten der Daten &#40;Lückenlose exemplarische Data Science-Vorgehensweise&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
