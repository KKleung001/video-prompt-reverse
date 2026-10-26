# Video Prompt Reverse · 视频反推与首帧工作流

**中文**：把视频文件或可访问的视频链接拆解成分镜，反推完整的中英文视频提示词；按用户选择保留或替换主角，生成每段首帧原图，最后整理成可离线查看的 HTML 文档。

**English**: Turn a video file or an accessible video link into a shot breakdown and complete Chinese and English video prompts. Keep or replace the subject, generate an original-resolution first-frame image for each segment, and assemble the results into an offline HTML document.

[中文说明](#中文说明) · [English guide](#english-guide) · [下载 ZIP / Download ZIP](https://github.com/KKleung001/video-prompt-reverse/archive/refs/heads/main.zip) · [Skill 规则 / Instructions](SKILL.md)

## 中文说明

### 这是什么

这是供支持 `SKILL.md` 的 AI 助手使用的工作流 Skill，首先面向 Codex。它是指令与参考文档，不是独立运行的视频分析网站，也不自带视频下载服务或生图模型。

视频读取、生图、文件保存和浏览器预览取决于执行环境提供的工具。视频链接受到登录、地区或访问限制时，需要提供可访问的链接或本地视频。没有实际看到的内容不会被当作已分析事实。

### 完整工作流

1. **拆解前确认主角**：保留原视频主角，或替换为用户提供的角色。支持人类、动物、外星生物和多角色互动。
2. **分析视频**：检查可访问范围，拆解动作、角色关系、镜头、环境、光影及可核验声音，保留真实剪辑顺序。
3. **反推双语提示词**：中文版和英文版分别集中呈现，角色、时间、动作与镜头要求保持一致。
4. **生图前确认参考图**：询问是否有背景、场景或物品参考图，并明确每份素材的作用。
5. **确认生成批次**：一次完成全部首帧，或分批生成；分批未指定数量时默认每批 3 张，每批完成后展示并等待用户明确确认“无需修改”才继续；要求修改时，修改后重新验收。全量模式也需整批验收。
6. **生成每段首帧**：使用适合后续视频动作的起始姿态，保持角色、场景、光向和道具连续，保存生成原图。
7. **自动整理 HTML**：全部计划首帧完成，且每批（含最后一批）均获用户确认无需修改后，生成含对应原图、分镜及中英文提示词的 HTML，附复制、原图查看和下载入口；默认将 HTML 与图片文件夹打包为 ZIP。

用户已经明确回答的选项不会重复询问。也可只执行提示词分析、指定首帧或 HTML 整理阶段。此 Skill 不生成或发布视频，不自动公开用户素材。

### 下载与安装

- **查看**：直接阅读本仓库的 [SKILL.md](SKILL.md) 与 `references/`。
- **下载**：点击上方 ZIP 链接，或使用 GitHub 的 **Code → Download ZIP**。
- **Codex 安装**：解压后，将包含 `SKILL.md`、`agents/` 和 `references/` 的整个目录命名为 `video-prompt-reverse`，放入你的 Codex 技能目录。默认位置为 `~/.codex/skills/`；如果配置了 `CODEX_HOME`，使用其下的 `skills/`。在能够识别新技能的对话中使用它。

也可以将本仓库克隆到技能目录；如果目标文件夹已经存在，先查看已有内容，不直接覆盖。

### 使用示例

```text
使用 $video-prompt-reverse 完整工作流处理这个视频：[视频链接或附件]
```

```text
主角替换为我上传的角色。背景沿用原视频，没有其他物品参考图。
每批生成 3 张首帧，每批先由我确认无需修改再继续，最后一批确认后自动整理 HTML。
```

```text
本批无需修改，继续生成下一批首帧。
```

### 输出与质量边界

每次任务可保存 `workflow.json`，记录角色、素材、分镜、提示词、首帧状态及下一批起点，便于继续执行。分镜数量取决于源视频，画幅不固定，不限定题材。

首帧原图保持生成文件的原始分辨率和字节，HTML 只按显示尺寸缩放。角色替换同步应用于图片和目标提示词。抽帧分析会说明采样限制；未核验音轨时不编造音乐、对白或静音。反推结果是复现可见效果的制作描述，不是原作者提示词的恢复，也不保证逐帧一致。

### MiniMax H3 写作参考

本 Skill 参考用户指定的两个第三方指南，采用具体动作、清晰运镜、素材分工及声画关系的写法。第三方结构字段不被宣称为官方强制 API 语法；目标生成入口有明确要求时，需按实际文档适配。来源和边界见 [H3 编写说明](references/h3-writing.md)。

### 自定义角色适配

仓库包含通用的角色替换与动作适配规则。用户提供角色参考，助手按目标身体结构调整动作、接触位置和构图。角色图、个人项目资料和生成示例图片不随本仓库分发；请自行提供有权使用的参考。仓库文字许可不授予任何独立角色或素材的使用权。

## English guide

### What this is

A workflow skill for AI assistants that support `SKILL.md`, designed primarily for Codex. This repository contains instructions and references, not a standalone video-analysis application, a hosted downloader, or an image-generation model.

Video inspection, image generation, file creation, and browser previews depend on tools available in the execution environment. If a video URL requires login or is otherwise inaccessible, provide an accessible link or a local file. Unseen content must not be presented as observed evidence.

### End-to-end workflow

1. **Confirm the subject before analysis**: retain the original subject or replace it with a user-supplied character. Humans, animals, alien creatures, and multiple interacting subjects are supported.
2. **Inspect and break down the video**: record the accessible scope, actions, subject relationships, camera behavior, setting, lighting, and verifiable audio. Preserve the observed edit order.
3. **Write bilingual prompts**: present complete Chinese prompts and complete English prompts in separate groups, with matching subjects, timing, actions, and camera instructions.
4. **Ask about references before generating images**: check for background, setting, or prop reference images and define the role of each asset.
5. **Confirm the generation schedule**: generate all planned frames or work in batches. A batch defaults to three images if no size is specified; show each batch and wait for explicit confirmation that no changes are needed before proceeding. Requested revisions must be shown and approved again. All-at-once generation is also reviewed as one batch.
6. **Generate each first frame**: use a practical starting pose for the segment, maintain identity and visual continuity, and preserve the original generated image files.
7. **Automatically assemble HTML**: after all planned frames are complete and every batch, including the final batch, has been explicitly approved with no further changes needed, create an offline document with matched images, shot analysis, bilingual prompts, copy controls, and original-image view/download links. By default, package the HTML and images together in a ZIP archive.

Do not ask again when a choice has already been explicitly provided for the current task. Prompt-only analysis, selected frames, and HTML-only work are also supported. The skill does not generate or publish videos or automatically publish user assets.

### Download and install

- **Read** [SKILL.md](SKILL.md) and the `references/` directory directly on GitHub.
- **Download** the ZIP linked above, or choose **Code → Download ZIP**.
- **Install in Codex**: extract the archive, name the directory containing `SKILL.md`, `agents/`, and `references/` as `video-prompt-reverse`, and place it in your Codex skills directory. The default is `~/.codex/skills/`; if `CODEX_HOME` is configured, use its `skills/` directory. Invoke it in a conversation where the new skill is available.

You may also clone this repository into your skills directory. If the target directory already exists, inspect it before replacing anything.

### Example requests

```text
Use $video-prompt-reverse to process this video through the complete workflow: [link or attachment].
```

```text
Replace the main subject with my uploaded character. Keep the source setting;
there are no additional prop references. Generate first frames in batches of three,
Ask me to approve each batch with no further changes needed before proceeding.
Automatically assemble the HTML after I approve the final batch.
```

```text
No changes are needed for this batch. Continue with the next batch of first frames.
```

The operational instructions are currently written in Chinese. Bilingual output is explicitly required, but an assistant's instruction-reading ability determines how well it follows the workflow.

### Outputs and limitations

A task can preserve its source, choices, shot list, prompts, frame status, and batch cursor in `workflow.json` to support continuation. The workflow does not assume twelve shots, a portrait aspect ratio, or any particular subject matter.

Original image resolution and bytes are preserved; HTML scales their display size only. Subject replacements must match the target video prompts as well as the images. Frame sampling limitations are disclosed. Unverified audio is not invented or treated as silence. Reverse prompts describe a way to reproduce visible effects; they do not recover the creator's original prompt or guarantee frame-for-frame reproduction.

### H3 writing references and custom characters

The workflow draws on two user-selected third-party H3 prompt guides. Their field names and formatting conventions are not represented as mandatory official API syntax. Adapt to the actual generation interface when verified documentation requires it. See [writing references](references/h3-writing.md).

Generic character-adaptation rules explain how to transfer actions while respecting the target body structure, contact positions, and framing. Character art, private project documents, and generated example images are not distributed here. Supply references that you are entitled to use. The license for repository text does not grant rights to independently owned characters or assets.

## 文件结构 / Repository contents

```text
video-prompt-reverse/
├── README.md
├── SKILL.md
├── LICENSE
├── agents/
│   └── openai.yaml
└── references/
    ├── first-frame-workflow.md
    ├── h3-writing.md
    └── character-adaptation.md
```

## 参考来源 / Sources

- [MiniMax official H3 overview / MiniMax 官方 H3 介绍](https://www.minimax.io/blog/minimax-h3)
- [Independent prompt guide / 独立提示词指南](https://minimaxh3.co/prompt-guide)
- [Independent practical guide / 独立实用指南](https://minimax-h3.app/prompt-guide)

This repository is independently maintained and is not affiliated with MiniMax. 本仓库为独立维护内容，与 MiniMax 无隶属关系。

## 许可与权利 / License and rights

**中文**：本仓库公开供任何人查看，以及下载、保存未修改副本以供查看。其他权利保留；修改、改编、再分发、再发布、商业使用或其他用途，除法律另有规定外，需事先取得版权所有者书面授权。它采用有限公开许可，不是 MIT 等开源许可证。完整条款见 [LICENSE](LICENSE)。独立角色及素材不在授权范围内。

**English**: Anyone may view this public repository and download and retain unmodified copies for viewing. All other rights are reserved. Modification, adaptation, redistribution, republication, commercial use, and other uses require prior written authorization unless permitted by applicable law. This is a limited public license, not an MIT or other open-source license. See [LICENSE](LICENSE) for the complete terms. Independently owned characters and assets are excluded.
