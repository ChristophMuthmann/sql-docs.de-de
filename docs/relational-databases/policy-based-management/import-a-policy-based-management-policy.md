---
title: So importieren Sie eine richtlinienbasierte Verwaltungsrichtlinie | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b2afe5a00c5a9c8f24fdf9d9dd86681c0909bfd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="import-a-policy-based-management-policy"></a>Importieren einer Richtlinie der richtlinienbasierten Verwaltung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Sie eine Instanz einer Richtlinie der richtlinienbasierten Verwaltung mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] importieren.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **Importieren einer Richtlinieninstanz mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält Richtlinien, die verwendet werden können, um eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu überwachen. Diese Richtlinien sind standardmäßig nicht im [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] installiert, können aber aus dem Standardspeicherort C:\Programme\Microsoft SQL Server\###\Tools\Policies\DatabaseEngine\1033 oder C:\Programme (x86)\Microsoft SQL Server\###\Tools\Policies\DatabaseEngine\1033 auf 64-Bit-Versionen importiert werden.
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der PolicyAdministratorRole-Rolle in der msdb-Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-import-a-policy-instance"></a>So importieren Sie eine Richtlinieninstanz  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen, um den Server zu erweitern, in dem sich die neu importierte Richtlinieninstanz befinden wird.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Verwaltung** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um **Richtlinienverwaltung**zu erweitern.  
  
4.  Klicken Sie mit der rechten Maustaste auf den Ordner **Richtlinien** , und wählen Sie **Richtlinie importieren**aus.  
  
5.  Geben Sie im Dialogfeld **Importieren** den Pfad und den Namen der Datei ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen (**…**), um die XML-Datei zu suchen, die die Richtlinie enthält, und wählen Sie dann die Datei aus. Weitere Informationen zu den Optionen im Dialogfeld **Importieren** finden Sie unter [Import Policies Dialog Box](../../relational-databases/policy-based-management/import-policies-dialog-box.md).  
  
6.  Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
  
