---
title: "Erstellen oder Löschen eines Serveralias für die Verwendung durch einen Client | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- server alias
helpviewer_keywords:
- aliases [SQL Server], deleting
- aliases [SQL Server], creating
ms.assetid: b687e376-ee33-470d-b65a-87246bfefe6f
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 559cf56887726ec4410165de70ec380b44773e97
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="create-or-delete-a-server-alias-for-use-by-a-client"></a>Erstellen oder Löschen eines Serveralias für die Verwendung durch einen Client
  In diesem Thema wird beschrieben, wie Sie einen Serveralias in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe des SQL Server-Konfigurations-Managers erstellen oder löschen können. Bei einem Alias handelt es sich um einen alternativen Namen, der zum Herstellen einer Verbindung verwendet werden kann. In dem Alias eingeschlossen werden erforderliche Elemente einer Verbindungszeichenfolge. Diese Elemente werden mit einem vom Benutzer ausgewählten Namen offen gelegt. Aliase können mit jeder Clientanwendung verwendet werden. Mithilfe von Serveraliasnamen kann der Clientcomputer eine Verbindung mit mehreren Servern über verschiedene Netzwerkprotokolle herstellen, ohne jeweils das Protokoll und die Verbindungsdetails angeben zu müssen. Des Weiteren können mehrere Netzwerkprotokolle gleichzeitig aktiviert sein, auch wenn Sie diese Protokolle nur sporadisch nutzen. Wenn Sie den Server so konfiguriert haben, dass dieser an einer nicht standardmäßigen Portnummer oder Named Pipe lauscht und dabei der SQL Server-Browserdienst deaktiviert ist, erstellen Sie einen Alias, mit dem die neue Portnummer oder Named Pipe angegeben wird.  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
  
#### <a name="to-create-an-alias"></a>So erstellen Sie einen Alias  
  
1.  Erweitern Sie im SQL Server-Konfigurations-Manager den Eintrag **SQL Server Native Client-Konfiguration**, klicken Sie mit der rechten Maustaste auf **Aliase**, und klicken Sie auf **Neuer Alias**.  
  
2.  Geben Sie im Feld **Aliasname** den Namen des Alias ein. Die Clientanwendungen verwenden diesen Namen, wenn eine Verbindung aufgebaut werden soll.  
  
3.  Geben Sie in das Feld **Server** den Namen oder die IP-Adresse eines Servers ein. Bei einer benannten Instanz hängen Sie den Namen der Instanz an.  
  
4.  Wählen Sie im Feld **Protokoll** das zu verwendende Protokoll für diesen Alias aus. Sobald Sie ein Protokoll angegeben haben, erhält das optionale Eigenschaftsfeld die Bezeichnung "Portnummer", "Pipename" oder "Verbindungszeichenfolge".  
  
 Die in der Hilfe zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager beschriebenen Verbindungszeichenfolgen können für Programmierer hilfreich sein, die ihre eigenen Verbindungszeichenfolgen erstellen. Drücken Sie F1, oder rufen Sie die Hilfe auf **** , um auf diese Informationen, im Dialogfeld **Neuer Alias**, zuzugreifen.  
  
> [!NOTE]  
>  Wenn ein konfigurierter Alias eine Verbindung mit dem falschen Server oder zur falschen Instanz herstellt, deaktivieren Sie das zugeordnete Netzwerkprotokoll, und aktivieren Sie es erneut. Dadurch werden alle zwischengespeicherten Verbindungsinformationen gelöscht, und der Client kann die Verbindung ordnungsgemäß herstellen.  
  
#### <a name="to-delete-an-alias"></a>So löschen Sie einen Alias  
  
1.  Erweitern Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager **SQL Server Native Client-Konfiguration**, und klicken Sie dann auf **Aliase**.  
  
2.  Klicken Sie im Detailbereich mit der rechten Maustaste auf den Alias, den Sie löschen möchten, und klicken Sie dann auf **Löschen**.  
  
  
