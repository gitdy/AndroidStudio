
# 《AndroidStudio实用指南》

[《AndroidStudio实用指南》](http://yuedu.baidu.com/ebook/31beb61a9b6648d7c1c746e8)是老毕的新书,从2015年5月初开始在百度阅读上陆续更新.

# 问题反馈

AndroidStudio实用指南中所有的建议和问题请大家在这里提BUG给我,我会及时修正. 多谢各位支持.

# 出版计划

- 5月14号: 完成第12章更新及校对  **√ DONE**
- 5月16号: 完成第13章更新及校对  **√ DONE**
- 5月18号: 完成第14章更新及校对 **√ DONE**
- 5月20号: 完成第16章更新及校对 **√ DONE**
- 5月22号: 完成第11章更新及校对 **√ DONE**
- 5月24号: 完成第09章更新及校对 **√ DONE**
- 5月26号: 完成第02章更新及校对 **√ DONE**
- 5月28号: 完成第10章更新及校对 **√ DONE**
- 6月01号: 完成所有重要章节更新及校对 **√ DONE**
- 6月15号: 完成第二次校对和代码Review **√ DONE**
- 6月20号: 完成附录
- 6月25号: 完成前言、序、推荐语 **√ 80%**
- 6月30号: 交稿 **√ DONE**
- 10月1号之前出版.


# 更新日志

本书针对最新版本的Review的时间表和进度表.

## **Android Studio 2.2**
在7月之前已经全部更新完。

| 章节   | 进度   | 时间         |
| ---- | ---- | ---------- |
| 第1章  | 100% | 2016.06.23 |
| 第2章  | 100% | 2016.05.23 |
| 第3章  |  100% | 2016.05.23 |
| 第4章  | 100% | 2016.05.23 |
| 第5章  |    100% | 2016.05.23 |
| 第6章  |  100% | 2016.05.23 |
| 第7章  |   100% | 2016.05.23 |
| 第8章  |   100% | 2016.05.23 |
| 第9章  |  100% | 2016.05.23 |
| 第10章 |  100% | 2016.05.23 |
| 第11章 | 100% | 2016.05.23 |
| 第12章 |  100% | 2016.05.23 |
| 第13章 | 100% | 2016.05.27 |
| 第14章 | 100% | 2016.05.27 |
| 第15章 | 100% | 2016.05.27 |
| 第16章 | 100% | 2016.05.27 |

## **Android Studio 2.1.1**

已全部更新完毕..



## 更新日期: 2016年4月10日

之前有很多很多的更新,但没在这里记录下来. 一些更新内容大家可以在issues列表里看到.

目前本书已经成型,细节和缺失的部分会陆续完善和补充.多谢支持我的朋友们.

BUG有很多,请大家多多指出. 提BUG给我哈. (现在都是我自己给自己提BUG)

--------------------------------------------------- 我是分割线 --------------------------------------------------- 

## 更新日期: 2016年3月5日

第14章新增了20个设置技巧,并重新编排了目录,看起来更加清晰,一眼就能找到你想要的设置.

这里漏了很多更新日志......

--------------------------------------------------- 我是分割线 --------------------------------------------------- 

## 更新日期: 2015年8月16日

新增 11章第1节 配置JIRA、Github、Gitlab任务(task)

## 更新日期: 2015年8月15日

新增10.8节 恢复程序运行、暂停程序运行、停止进程、查看断点等

新增 10.8节 禁用断点、 获取线程堆栈、恢复布局、设置、固定标签等

新增 10.9 单步调试工具栏

新增 10.10 计算表达式
```
import android.graphics.Paint
import androidx.compose.foundation.Canvas
import androidx.compose.foundation.layout.*
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.geometry.CornerRadius
import androidx.compose.ui.geometry.Offset
import androidx.compose.ui.geometry.Size
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.graphics.Path
import androidx.compose.ui.graphics.drawscope.drawIntoCanvas
import androidx.compose.ui.graphics.nativeCanvas
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp

@Composable
fun RiskLevelIndicator(
    productRiskLevel: Int = 3,
    userRiskTolerance: Int = 4
) {
    val boxWidth = 60f
    val boxHeight = 60f
    val boxGap = 8f

    Column(horizontalAlignment = Alignment.CenterHorizontally) {
        Text("Product risk level", fontSize = 14.sp)
        Canvas(
            modifier = Modifier
                .fillMaxWidth()
                .height(120.dp)
                .padding(horizontal = 16.dp)
        ) {
            val totalBoxes = 6
            val startX = (size.width - (boxWidth * totalBoxes + boxGap * (totalBoxes - 1))) / 2f
            val centerY = size.height / 2f

            for (i in 0 until totalBoxes) {
                val x = startX + i * (boxWidth + boxGap)
                val color = when (i) {
                    productRiskLevel -> Color(0xFF2B4A78) // 深蓝色
                    userRiskTolerance -> Color(0xFF4CAF50) // 绿色
                    else -> Color(0xFFD3D3D3) // 浅灰色
                }

                drawRoundRect(
                    color = color,
                    topLeft = Offset(x, centerY - boxHeight / 2),
                    size = Size(boxWidth, boxHeight),
                    cornerRadius = CornerRadius(8f, 8f)
                )

                // 绘制数字
                drawIntoCanvas {
                    it.nativeCanvas.apply {
                        val textPaint = Paint().apply {
                            color = android.graphics.Color.BLACK
                            textAlign = Paint.Align.CENTER
                            textSize = 36f
                            isAntiAlias = true
                        }
                        drawText(
                            "$i",
                            x + boxWidth / 2,
                            centerY + 12f,
                            textPaint
                        )
                    }
                }
            }

            // 绘制上方箭头（产品风险）
            val px = startX + productRiskLevel * (boxWidth + boxGap) + boxWidth / 2
            drawPath(
                path = Path().apply {
                    moveTo(px, centerY - boxHeight / 2 - 10)
                    lineTo(px - 10, centerY - boxHeight / 2 - 30)
                    lineTo(px + 10, centerY - boxHeight / 2 - 30)
                    close()
                },
                color = Color.Black
            )

            // 绘制下方箭头（用户容忍度）
            val ux = startX + userRiskTolerance * (boxWidth + boxGap) + boxWidth / 2
            drawPath(
                path = Path().apply {
                    moveTo(ux, centerY + boxHeight / 2 + 10)
                    lineTo(ux - 10, centerY + boxHeight / 2 + 30)
                    lineTo(ux + 10, centerY + boxHeight / 2 + 30)
                    close()
                },
                color = Color.Black
            )
        }
        Text("Your risk tolerance", fontSize = 14.sp)
    }
}

```
