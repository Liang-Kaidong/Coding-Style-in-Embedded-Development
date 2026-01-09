# 《嵌入式开发中混合注释风格详解》

## 一、文件头部注释（带边框）
```
/*******************************************************
 * Copyright (C) 2025 XXXX
 * FileName: main.c
 * Author: KD
 * Date: 2025-06-01
 * Description: 主程序文件，实现系统初始化与任务调度
 * Version: V1.0
 ******************************************************/
```

## 二、函数注释（星号顶格，后接空格）
```
/*
 * 功能: 初始化GPIO引脚
 * 参数: 
 *     port - GPIO端口号(如GPIOA/GPIOB)
 *     pin - 引脚号(0-15)
 *     mode - 引脚模式(INPUT/OUTPUT/AF)
 * 返回值: 0-成功，-1-失败
 */

int gpio_init(uint32_t port, uint8_t pin, uint8_t mode) {
    /* 函数实现 */ 
    
    return 0;
}
```

## 三、复杂逻辑注释（星号顶格，后接空格）
```
/*
 * 算法说明:
 * 1. 采用二分查找法在有序数组中查找目标值
 * 2. 时间复杂度O(log n)
 * 3. 要求数组必须按升序排列
 */

int binary_search(int arr[], int left, int right, int target) {
    while (left <= right) {
        int mid = left + (right - left) / 2;  /* 防止整数溢出 */
        if (arr[mid] == target) {
            return mid;  /* 找到目标值 */
        } if (arr[mid] < target) {
            left = mid + 1;  /* 搜索右半部分 */
        } else {
            right = mid - 1;  /* 搜索左半部分 */
        }
    }
    
    return -1;  /* 未找到目标值 */
}
```

## 四、条件编译注释（星号顶格，后接空格）
```
/*
 * 平台说明:
 * - __ARM__: ARM架构平台
 * - __x86_64__: x86_64架构平台
 */

#if def __ARM__
    #include "arm_arch.h"
#else
    #include "x86_arch.h"

#endif
```

## 五、宏定义注释（星号顶格，后接空格）
```
/*
 * 宏定义: LIMIT(x, min, max)
 * 功能: 将值限制在指定范围内
 * 参数:
 *     x - 待限制的值
 *     min - 最小值
 *     max - 最大值
 * 返回: 若x在[min,max]内则返回x，否则返回边界值
 */

#define LIMIT(x, min, max) (((x) < (min)) ? (min) : (((x) > (max)) ? (max) : (x)))
```

## 六、风格对比表
| 场景 | 头部注释 | 其他注释 |
| --- | --- | --- |
| 首行格式 | /********... | /* |
| 内容行 | *内容（无空格） | * 内容（有空格） |
| 末行格式 | *********/ | */ |
| 适用场景 | 文件头部、版权声明 | 函数、算法、逻辑块说明 |

## 七、自动化生成方案
**1.VS Code 配置：在 settings.json 中添加：**
```
"fileheader.customMade": {
    "Description": "",
    "Version": "V1.0",
    "Author": "KD",
    "Date": "Do not edit",
    "LastEditTime": "Do not edit"
},

"fileheader.cursorMode": {
    "name": "",
    "description": "",
    "param": "",
    "return": ""
},

"fileheader.configObj": {
    "autoAdd": false,
    "prohibitAutoAdd": ["json", "md"],
    "specialOptions": {
        "c": {
            "head": "/*******************************************************",
            "middle": " * @",
            "end": " *******************************************************/"
        }
    }
}
```

## 八、注意事项
> **1.严格区分场景：**
* 仅文件头部使用带边框注释，其他地方一律使用星号顶格加空格的格式。
* 避免混用两种风格，保持一致性。

> **2.工具辅助：**
* 使用 IDE 插件或脚本自动生成注释模板，减少手动输入错误。
* 对于多人协作项目，建议在.editorconfig中明确注释风格。

> **3.可读性优先：**
* 长注释可适当分行，但需保持星号对齐和内容紧凑。

* 避免注释过长导致屏幕滚动，复杂说明可参考外部文档。

这种混合风格既能突出文件头部的重要性，又能保持代码其他部分的简洁性，是嵌入式开发中常见的规范模式。其他的书写规范亦可参考[【正点原子】嵌入式LinuxC代码规范化V1.0.pdf](https://github.com/user-attachments/files/20538185/16.LinuxC.V1.0.pdf)
