---
title: "Anpassen des Verhaltens der Wörtertrennung mit einem Benutzerwörterbuch | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f4b984764897fd59b09a5a0eb5b17f76b573fd5b
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="customize-the-behavior-of-word-breakers-with-a-custom-dictionary"></a>Anpassen des Verhaltens der Wörtertrennung mit einem Benutzerwörterbuch
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Sie können das Verhalten der Wörtertrennung für eine bestimmte Sprache anpassen, indem Sie eine sprachspezifische Benutzerwörterbuchdatei erstellen. Sie können z. B. verhindern, dass die Wörtertrennung bestimmte Begriffe oder Muster trennt.  
  
 Weitere Informationen finden Sie im folgenden SharePoint-Artikel:  
  
 [Erstellen eines Benutzerwörterbuchs (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=215011)  
  
 Speichern Sie Benutzerwörterbuchdateien für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]in dem folgenden Ordner:  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 Starten Sie nach dem Erstellen oder Ändern von Benutzerwörterbuchdateien das Startprogramm für den SQL-Volltextfilterdaemon mit dem folgenden Befehl neu:  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
  
