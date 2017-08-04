---
title: Anzeigen der Liste der Pakete auf dem Integration Services-Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 67a992d1-7524-4f4b-b3d8-ebd9e5ea82a8
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7686512a05d243f1802d1dd5b0d27bd777210161
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="view-the-list-of-packages-on-the-integration-services-server"></a>Anzeigen der Liste der auf dem Integration Services-Server gespeicherten Pakete
  Sie können die Liste der Pakete mit einer von zwei Methoden anzeigen, die in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf dem Server gespeichert sind.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]-Zugriff  
 Fragen Sie die Sicht [catalog.packages &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-packages-ssisdb-database.md) ab, um die Liste der auf dem Server gespeicherten Pakete anzuzeigen.  
  
 In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 Folgen Sie der unten angegebenen Prozedur, um mit dem Objekt-Explorer in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]auf dem Server gespeicherten Pakete anzuzeigen.  
  
### <a name="to-view-packages-using-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>So zeigen Sie Pakete mithilfe von[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung zum [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server her. Dies bedeutet, dass eine Verbindung mit der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Instanz hergestellt werden muss, die als Host für die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Datenbank fungiert.  
  
2.  Erweitern Sie im Objekt-Explorer die Struktur, um den Knoten **Integration Services-Kataloge** anzuzeigen.  
  
3.  Erweitern Sie den Knoten **Integration Services-Kataloge** , um den Knoten **SSISDB** anzuzeigen.  
  
4.  Erweitern Sie den Knoten **SSISDB** , um eine Liste mit mindestens einem Ordner anzuzeigen. Jeder Ordner enthält mindestens ein Projekt im Ordner **Projekte** , und jedes Projekt enthält mindestens ein Paket im Ordner **Pakete** .  
  
  
