---
title: Перечисление CorSetENC
ms.date: 03/30/2017
api_name:
- CorSetENC
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorSetENC
helpviewer_keywords:
- CorSetENC enumeration [.NET Framework metadata]
ms.assetid: fe4150e8-071d-43fb-8e06-c3c616dbeed2
topic_type:
- apiref
ms.openlocfilehash: 39f72e670ddc700c257f50f6bad6fab702ec21b6
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/23/2019
ms.locfileid: "74432777"
---
# <a name="corsetenc-enumeration"></a>Перечисление CorSetENC
Содержит значения, используемые для оказания влияния на поведение во время создания метаданных.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
typedef enum CorSetENC {  
  
    MDSetENCOn                  = 0x00000001,  
    MDSetENCOff                 = 0x00000002,  
  
    MDUpdateENC                 = 0x00000001,  
    MDUpdateFull                = 0x00000002,  
    MDUpdateExtension           = 0x00000003,  
    MDUpdateIncremental         = 0x00000004,  
    MDUpdateDelta               = 0x00000005,  
    MDUpdateMask                = 0x00000007  
  
} CorSetENC;  
```  
  
## <a name="members"></a>Члены  
  
|Член|Описание|  
|------------|-----------------|  
|`MDSetENCOn`|Устарело.|  
|`MDSetENCOff`|Устарело.|  
|`MDUpdateENC`|Указывает, что в то время как метаданные могут быть обновлены, токены перемещаться нельзя.|  
|`MDUpdateFull`|Указывает, что токены можно перемещать во время обновлений.|  
|`MDUpdateExtension`|Указывает, что обновления могут состоять только из добавлений. Маркеры не могут быть перемещены.|  
|`MDUpdateIncremental`|Указывает, что компиляция является добавочной.|  
|`MDUpdateDelta`|Указывает, что должны быть сохранены только измененные метаданные.|  
|`MDUpdateMask`|Включает `MDUpdateENC`, `MDUpdateFull` и `MDUpdateIncremental`.|  
  
## <a name="requirements"></a>Требования  
 **Платформы:** см. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** Корхдр. h  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также:

- [Перечисления метаданных](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
