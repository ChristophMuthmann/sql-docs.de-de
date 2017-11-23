---
title: "Ändern der SQL Server-Dienst erweiterten Eigenschaften mithilfe von VBScript | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
dev_langs: VB
helpviewer_keywords:
- VBScript [WMI]
- modifying SQL Server Service properties
- WMI Provider for Configuration Management, VBScript
ms.assetid: f3c5d981-eaa3-4d34-9b91-37e42636aa81
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 51810d0a14e7a0a20bacc7276febf95da17fa09e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="access-wmi-provider-for-configuration-management-using-vbscript"></a>WMI-Anbieter für den Zugriff für die Konfigurationsverwaltung mit VBScript
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]In diesem Abschnitt wird beschrieben, wie ein VBScript-Programm zu erstellen, die die Version der installierten Instanzen von listet [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die auf einem Computer ausgeführt werden.  
  
 Mit dem Codebeispiel werden die Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die auf dem Computer ausgeführt werden, und deren Version aufgeführt.  
  
### <a name="listing-name-and-version-of-installed-instances-of-sql-server"></a>Auflisten der Namen und der Version von installierten Instanzen von SQL Server  
  
1.  Öffnen Sie ein neues Dokument in einem Texteditor wie [!INCLUDE[msCoName](../../includes/msconame-md.md)] Editor. Kopieren Sie den Code, den Sie im Anschluss an diese Prozedur finden, und speichern Sie die Datei mit der Erweiterung .vbs. Dieses Beispiel hat den Namen test.vbs.  
  
2.  Stellen Sie eine Verbindung zu einer Instanz des WMI-Anbieters für die Computerverwaltung mit der VBScript `GetObject`-Funktion her. In diesem Beispiel wird eine Verbindung zu einem Remotecomputer mit dem Namen mpc hergestellt, allerdings wird der Computername zur Verbindung zum lokalen Computer ausgelassen: winmgmts:root\Microsoft\SqlServer\ComputerManagement. Weitere Informationen zur `GetObject`-Funktion finden Sie in der VBScript-Referenz.  
  
3.  Verwenden Sie die `InstancesOf`-Methode, um eine Liste der Dienste aufzuzählen. Die Dienste können auch mit einer einfachen WQL-Abfrage und einer `ExecQuery`-Methode anstelle der `InstancesOf`-Methode aufgezählt werden.  
  
4.  Verwenden Sie die `ExecQuery`-Methode und eine WQL-Abfrage, um den Namen und die Version der installierten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abzurufen.  
  
5.  Speichern Sie die Datei.  
  
6.  Führen Sie das Skript durch Eingabe **Cscript test.vbs** an der Eingabeaufforderung.  
  
## <a name="example"></a>Beispiel  
  
```  
set wmi = GetObject("WINMGMTS:\\.\root\Microsoft\SqlServer\ComputerManagement12")  
for each prop in wmi.ExecQuery("select * from SqlServiceAdvancedProperty where SQLServiceType = 1 AND PropertyName = 'VERSION'")  
WScript.Echo prop.ServiceName & " " & prop.PropertyName & ": " & prop.PropertyStrValue  
next  
```  
  
  
