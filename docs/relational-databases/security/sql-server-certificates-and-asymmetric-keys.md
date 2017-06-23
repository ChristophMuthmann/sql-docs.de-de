---
title: "SQL Server-Zertifikate und asymmetrische Schlüssel | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [SQL Server], certificates and asymmetric keys
ms.assetid: 8519aa2f-f09c-4c1c-96b5-abc24811e60c
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: b742bd3be2754628c05349cd55315afd44eb3b8d
ms.contentlocale: de-de
ms.lasthandoff: 06/23/2017

---
# <a name="sql-server-certificates-and-asymmetric-keys"></a>SQL Server-Zertifikate und asymmetrische Schlüssel
  Die Verschlüsselung mit öffentlichen Schlüsseln (Public Key Cryptography, PKI) ist eine Form der Nachrichtenverschlüsselung, bei der ein Benutzer einen *öffentlichen* Schlüssel und einen *privaten* Schlüssel erstellt. Der private Schlüssel wird geheim gehalten, der öffentliche Schlüssel kann an andere verteilt werden. Zwar sind die Schlüssel mathematisch miteinander verknüpft, jedoch kann der private Schlüssel nicht einfach aus dem öffentlichen Schlüssel abgeleitet werden. Der öffentliche Schlüssel wird verwendet, um Daten zu verschlüsseln und der private Schlüssel wird verwendet, um Daten zu entschlüsseln. Eine mit dem öffentlichen Schlüssel verschlüsselte Nachricht kann nur mit dem korrekten privaten Schlüssel wieder entschlüsselt werden. Da es sich um zwei verschiedene Schlüssel handelt, werden diese Schlüssel als *asymmetrisch*bezeichnet.  
  
 Zertifikate und asymmetrische Schlüssel sind beides Möglichkeiten, asymmetrische Verschlüsselung zu verwenden. Zertifikate werden oft als Container für asymmetrische Schlüssel verwendet, da sie weitere Informationen enthalten können, beispielsweise Ablaufdaten und Zertifikatsaussteller. In Bezug auf den kryptografischen Algorithmus gibt es zwischen den beiden Mechanismen keinen Unterschied, und bei gegebener Schlüssellänge auch keinen Unterschied in der Verschlüsselungsstärke. Im Allgemeinen verwenden Sie ein Zertifikat, um andere Typen von Verschlüsselungsschlüsseln in einer Datenbank zu verschlüsseln oder um Codemodule zu signieren.  
  
 Zertifikate und asymmetrische Schlüssel können Daten entschlüsseln, die mit dem jeweils anderen Schlüssel verschlüsselt wurden. Im Allgemeinen verwenden Sie eine asymmetrische Verschlüsselung, um einen symmetrischen Schlüssel für die Speicherung in einer Datenbank zu verschlüsseln.  
  
 Ein öffentlicher Schlüssel hat kein einem Zertifikat vergleichbares bestimmtes Format, und Sie können ihn nicht in eine Datei exportieren.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält Funktionen, mit denen Sie Zertifikate und Schlüssel zur Verwendung mit dem Server und der Datenbank erstellen und verwalten können. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann nicht zum Erstellen und Verwalten von Zertifikaten und Schlüsseln mit anderen Anwendungen oder im Betriebssystem verwendet werden.  
  
## <a name="certificates"></a>Zertifikate  
 Ein Zertifikat ist ein digital signiertes Sicherheitsobjekt, das einen öffentlichen (und optional einen privaten) Schlüssel für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]enthält. Sie können extern generierte Zertifikate verwenden, aber auch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann Zertifikate generieren.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Zertifikate entsprechen dem Zertifizierungsstandard IETF X.509v3.  
  
 Zertifikate sind nützlich, weil sie die Möglichkeit bieten, Schlüssel in X.509-Zertifikatsdateien zu exportieren und aus ihnen zu importieren. Die Syntax der Zertifikatserstellung lässt die Angabe von Optionen für Zertifikate zu, z.&#160;B. die Angabe eines Ablaufdatums.  
  
### <a name="using-a-certificate-in-sql-server"></a>Verwenden eines Zertifikats in SQL Server  
 Zertifikate können verwendet werden, um Verbindungen und Datenbankspiegelungen zu sichern, um Pakete und andere Objekte zu signieren oder um Daten und Verbindungen zu verschlüsseln. In der folgenden Tabelle werden zusätzliche Ressourcen für Zertifikate in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]aufgeführt.  
  
|Thema|Beschreibung|  
|-----------|-----------------|  
|[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)|Erklärt den Befehl zum Erstellen von Zertifikaten.|  
|[Identifizieren der Quelle von Paketen mit digitalen Signaturen](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md)|Zeigt Informationen über das Verwenden von Zertifikaten zur Signierung von Softwarepaketen an.|  
|[Verwenden von Zertifikaten für einen Datenbankspiegelungs-Endpunkt &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)|Bietet Informationen über das Verwenden von Zertifikaten bei Datenbankspiegelungen.|  
  
## <a name="asymmetric-keys"></a>Asymmetrische Schlüssel  
 Asymmetrische Schlüssel werden zum Sichern von symmetrischen Schlüsseln verwendet. Sie können auch für eine eingeschränkte Datenverschlüsselung und die digitale Signierung von Datenbankobjekten verwendet werden. Ein asymmetrischer Schlüssel besteht aus einem privaten Schlüssel und einem entsprechenden öffentlichen Schlüssel. Weitere Informationen zu asymmetrischen Schlüsseln finden Sie unter [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)bezeichnet.  
  
 Asymmetrische Schlüssel können aus Schlüsseldateien mit starkem Namen importiert, jedoch nicht exportiert werden. Sie verfügen auch nicht über Ablaufoptionen. Asymmetrische Schlüssel können keine Verbindungen verschlüsseln.  
  
### <a name="using-an-asymmetric-key-in-sql-server"></a>Verwenden eines asymmetrischen Schlüssels in SQL Server  
 Asymmetrische Schlüssel können verwendet werden, um Daten zu sichern oder Nur-Text zu signieren. In der folgenden Tabelle werden zusätzliche Ressourcen für asymmetrischen Schlüssel in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]aufgeführt.  
  
|Thema|Beschreibung|  
|-----------|-----------------|  
|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)|Erklärt den Befehl zum Erstellen von asymmetrischen Schlüsseln.|  
|[SIGNBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)|Erläutert die Optionen zum Signieren von Objekten.|  
  
## <a name="tools"></a>Tools  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] stellt Tools und Hilfsprogramme bereit, die Zertifikate und Schlüsseldateien mit starkem Namen generieren. Mithilfe dieser Tools können Schlüssel wesentlich flexibler generiert werden, als dies mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Syntax möglich ist. Sie können mit diesen Tools RSA-Schlüssel mit komplexerer Schlüssellänge erstellen und diese dann in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]importieren. Die folgende Tabelle erklärt, wo diese Tools zu finden sind.  
  
|||  
|-|-|  
|Tool|Zweck|  
|[makecert](http://msdn2.microsoft.com/library/bfsktky3\(VS.80\).aspx)|Erstellt Zertifikate.|  
|[sn](http://msdn2.microsoft.com/library/k5b5tt23\(VS.80\).aspx)|Erstellt starke Namen für symmetrische Schlüssel.|  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 [Auswählen eines Verschlüsselungsalgorithmus](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
  
## <a name="see-also"></a>Siehe auch  
 [sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)   
 [Transparente Datenverschlüsselung &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption-tde.md)  
  
  
