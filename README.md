# 恶魔城X 月下夜想曲 简体中文包（SymphonyRecomp）

[SymphonyRecomp](https://github.com/BlackLabelHQ/SymphonyRecomp)（PS1 美版《恶魔城X 月下夜想曲》重编译版）
配套简体中文包：在美版基础上，把说明、图鉴、系统提示和过场对白换成中文，并附带一个高清菜单字体。

这是第三方制作的中文包，与 BlackLabelHQ 无关；使用中遇到中文包的问题，请在本仓库提 issue。

## 内容

| 目录                 | 作用                                                                                                                                                             |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `translations/zh-cn` | **中文语言包**：道具、饰品、魔导器、魔法的说明，魔导器名和魔法名，魔物图鉴，存档、文件选择、设置菜单的提示，门上的提示，拾取提示「得到」，以及全部 19 段过场对白；另带开场字幕卡「重返 1792 年」和序章关卡标题「最终关：『血脉』」的替换贴图（`textures/`，选中文时自动加载） |
| `mods/zh-cn`         | **中文 mod**：进入新区域时的区域名（中文 + 英文对照）、标题画面的「请按开始键」、各区域的拾取提示「得到」，以及使魔列表里美版遗留的日文（改为英文） |
| `packs/hd-menu-font` | **高清菜单字体**（贴图包）：菜单、道具名等用的 8×8 小字体换成 4 倍分辨率的英文字体，保留原来的各种颜色（包括不可用时的暗色）；与语言无关，英文模式下也有效 |

保持英文的部分（有意为之）：菜单、道具 / 敌人 / 饰品的名字（游戏用 8×8 小字体显示，配合高清菜单字体）、人名标签、
序章滚动字幕、片尾字幕和其余图片文字。配音是美版英文原声。

## 安装

1. 准备好 SymphonyRecomp（[官方发布页](https://github.com/BlackLabelHQ/SymphonyRecomp/releases)，或自行编译）和合法拥有的北美版 PS1 光盘。
2. 把本仓库的 `translations/zh-cn` 复制到游戏目录的 `translations/` 下，`mods/zh-cn` 复制到 `mods/` 下，
   `packs/hd-menu-font` 复制到 `packs/` 下。游戏目录就是 `sotn.exe` 所在的目录；这几个文件夹没有的话手动建一个
   （`translations/`、`packs/` 游戏首次启动也会自动创建）。高清菜单字体是可选的，不想要就不复制。
3. 启动游戏，在 设置 → 语言 → 游戏语言 里选「简体中文」。mod 和贴图包都默认启用，mod 可在「模组」菜单里查看和开关。

适用版本：SymphonyRecomp pre-release 1.2.0（提交 `fb0520e`）。语言包按游戏数据的位置制作，SymphonyRecomp 更新后
如有部分文字对不上，请提 issue。

## 已知问题：pre-release 1.2.0 下语言包无法加载

城堡主塔里希特获救后的那段对白（`translations/zh-cn/scripts/top_cutscene_data.yaml`）碰上了 SymphonyRecomp 1.2.0
自身的一个错误：程序内置的这段脚本的定位数据，把两个数字写成了字符串，只要语言包里有这段脚本，整个语言包就会被拒绝，
游戏里选不到中文。已向上游报告，修复后这一节会删掉。在那之前，二选一：

**A. 直接用官方 1.2.0：去掉这段对白的翻译**

把 `translations/zh-cn/scripts/top_cutscene_data.yaml` 删掉，或改个扩展名（例如改成 `top_cutscene_data.off`）。
只有这一段对白会显示英文，其余不受影响。

**B. 自己编译 SymphonyRecomp：修正那条定位数据**

打开 `patches/translation/TranslationBindings.cs`，找到 `"top:cutscene_data"` 这一条（文件里只有一处），
把它末尾的

```
"base":"2149056512","loadOffset":"0"
```

改成（去掉引号，和其他各条一致）

```
"base":2149056512,"loadOffset":0
```

然后重新编译。这一行非常长，建议用编辑器的查找替换；也可以在 SymphonyRecomp 目录下用 Git Bash 执行：

```sh
sed -i 's/"top:cutscene_data":{\([^}]*\)"base":"2149056512","loadOffset":"0"/"top:cutscene_data":{\1"base":2149056512,"loadOffset":0/' patches/translation/TranslationBindings.cs
```

## 关于译文

这是基于美版制作的中文版，译文以美版英文为准：

- **过场对白**按美版英文剧本完整重新翻译，并按英文配音的节奏调整了字幕出现的速度，使字幕与配音同步。
- **说明、图鉴、魔导器与魔法名、系统提示**逐条对照美版英文校订：美版改过内容的、和英文意思不符的，都按英文重新翻译；
  人名、怪物名采用现在通行的译法（阿鲁卡多、里希特、玛丽亚、德古拉、贝尔蒙特等）。

说明和图鉴的部分译文沿用了民间流传的 PS1 中文版（与美版英文意思一致的条目）。这个中文版可以追溯到约 20 多年前论坛上
流传的《月下夜想曲》半汉化（配合中文 BIOS 使用的日版镜像），原作者已不可考。

**中文字形**：游戏内文字全部用开源的 [GNU Unifont](https://unifoundry.com/unifont/)（16×16 点阵，压成游戏使用的 16×15），
图片文字也都用开源字体绘制，不含民间中文版或其他来源不明的字库。

## 致谢

- [BlackLabelHQ](https://github.com/BlackLabelHQ) 的 SymphonyRecomp 与 RecompOne，以及其中的翻译框架和 mod 支持。
- 当年论坛里汉化《月下夜想曲》的前辈们，以及之后所有做过勘误、整理的朋友。原作者已不可考，谨此致谢。
- 字体：
  - 中文字形：[GNU Unifont](https://unifoundry.com/unifont/) 16.0.04（SIL OFL 1.1，见 `translations/zh-cn/LICENSE-unifont.txt`）。
  - 对白里的省略号、标题画面的「请按开始键」：[Fusion Pixel Font](https://github.com/TakWolf/fusion-pixel-font)（SIL OFL 1.1，见 `translations/zh-cn/LICENSE-font.txt`）。
  - 开场字幕卡、序章关卡标题：[霞鹜文楷 LXGW WenKai](https://github.com/lxgw/LxgwWenKai)（SIL OFL 1.1）。
  - 高清菜单字体：[JetBrains Mono](https://github.com/JetBrains/JetBrainsMono) Bold，横向拉宽（SIL OFL 1.1，见 `packs/hd-menu-font/LICENSE-JetBrainsMono.txt`）。
  - 区域名下方的英文：[EB Garamond](https://github.com/octaviopardo/EBGaramond12)（SIL OFL 1.1）。
  - `translations/zh-cn/fonts/bios-font`：RecompOne 自带的公有领域日文字库（由东云 16 点阵字体生成，见其中的
    `FONT_LICENSE.md`），原样复制，用于设定对白行距和显示英文、标点。

中文游戏汉化的成果长期以来多在论坛和网盘间口口相传，很少有人整理成可追溯的公开仓库。这个仓库也算是做一点整理工作，希望这些前人的心血能留存下来。

## 声明

本仓库不包含任何游戏数据，需自备合法拥有的北美版 PS1 光盘。中文内容仅供学习交流，请勿用于商业用途。
相关作者或团队如认为不妥，请通过 issue 联系，我会及时处理或删除。
