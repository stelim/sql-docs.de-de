---
title: MSSQL_ENG020574 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG02574 error
ms.assetid: 4e98f8de-287c-4090-81ee-dc8f80dfa6a1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6e448c4f63e0b64984623fff07238ee977cfa0dd
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356388"
---
# <a name="mssqleng020574"></a>MSSQL_ENG020574
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|20574|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Fehler bei der Datenüberprüfung für das Abonnement des Abonnenten '%s' für den '%s'-Artikel in der '%s'-Veröffentlichung.|  
  
## <a name="explanation"></a>Erklärung  
 Die Daten des Abonnenten wurden gegen die Daten des Verlegers abgeglichen, und es wurde keine Übereinstimmung der Daten festgestellt. Daher konnte die Überprüfung nicht erfolgreich abgeschlossen werden. Weitere Informationen zur Überprüfung finden Sie unter [Validate Replicated Data](../../relational-databases/replication/validate-replicated-data.md).  
  
## <a name="user-action"></a>Benutzeraktion  
 Es wird empfohlen, folgendermaßen vorzugehen:  
  
-   Ermitteln Sie den Grund für den Fehler bei der Überprüfung.  
  
-   Beheben Sie das zugrunde liegende Problem, das zu dem Fehler geführt hat.  
  
-   Stellen Sie die Konvergenz der Daten her, indem Sie das Abonnement erneut initialisieren oder eine andere geeignete Methode verwenden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
