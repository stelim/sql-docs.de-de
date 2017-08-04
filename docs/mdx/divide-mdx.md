---
title: Dividieren (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 9fe4a47b-d5e8-4dc7-ad4a-3e47ab463f03
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2f05c20a10b72b3c919672fd528a4222c6d204d7
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="divide-mdx"></a>Dividieren (MDX)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Führt eine Division aus und gibt ein alternatives Ergebnis oder BLANK() bei Division durch 0 zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Divide (<numerator>, <denominator> [,<alternateresult>])  
```  
  
## <a name="arguments"></a>Argumente  
 *Zähler*  
 Der Dividend oder Zahl dividiert werden soll.  
  
 *Nenner*  
 Der Divisor oder Zahl, durch die dividiert werden soll.  
  
 *alternateresult*  
 (Optional) Der Rückgabewert, wenn die Division durch null zu einem Fehler führt. Der Standardwert ist BLANK(), wenn nichts angegeben ist.  
  
## <a name="remarks"></a>Hinweise  
 Das alternative Ergebnis für eine Division durch 0 muss eine Konstante sein.  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
