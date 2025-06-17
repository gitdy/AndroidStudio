
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
import subprocess
import time

def get_android_clipboard():
    try:
        output = subprocess.run(
            ["adb", "shell", "service", "call", "clipboard", "1"],
            capture_output=True, text=True
        )

        if "Parcel" not in output.stdout:
            return ""

        lines = output.stdout.split("\n")
        hex_str = ""
        for line in lines:
            if "'" in line:
                hex_part = line.split("'")[1].replace("\\x", "").replace(".", "").strip()
                hex_str += hex_part

        if not hex_str:
            return ""

        # 解码 UTF-16
        bytes_data = bytes.fromhex(hex_str)
        text = bytes_data.decode("utf-16", errors="ignore")
        return text.strip()

    except Exception as e:
        print(f"ADB错误：{e}")
        return ""

def copy_to_mac_clipboard(text):
    try:
        process = subprocess.Popen(['pbcopy'], stdin=subprocess.PIPE)
        process.communicate(text.encode('utf-8'))
        print(f"[已同步到 Mac 剪贴板]: {text}\n")
    except Exception as e:
        print(f"粘贴板同步失败：{e}")

def start_sync(interval=2):
    print("开始同步手机剪贴板内容到 Mac 剪贴板（按 Ctrl+C 停止）...")
    last_content = ""
    while True:
        content = get_android_clipboard()
        if content and content != last_content:
            copy_to_mac_clipboard(content)
            last_content = content
        time.sleep(interval)

if __name__ == "__main__":
    start_sync()
```
