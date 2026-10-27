# 每段视频提示词：首帧与参考附件绑定

此文件定义本 Skill 的交付约定，不声称“附件 1”是 MiniMax H3 的官方特殊语法。编写任何带图像参考的最终视频提示词、或整理最终 HTML 时必须执行。

## 素材与编号

- 每段建立独立附件清单，记录上传顺序、提示词标识、实际文件名/路径、版本、用途及对应角色。只列实际存在且该段需要的图像；未提供的参考不占号、不虚构。
- 默认每段单独生成、编号从 1 开始：该段已验收首帧 → 角色参考（多角色按稳定角色 ID）→ 环境参考 → 道具参考。各类别多张时逐张编号。跳过缺失类别，编号连续；不是始终把环境固定为附件 3。
- 中英文使用相同数字和文件对应，中文称“附件 1”，英文称“Attachment 1”。每段都给完整清单，不用“同上”。同一文件兼多种用途时只上传一次，并写清各用途。
- 首帧不存在的纯提示词任务，不声称已提供首帧；使用现有参考连续编号，或输出无附件的纯文本版本。完整工作流生图前的文本属于待绑定草稿，首帧验收后必须更新为真实图片与当前版本。
- 清单是待用户上传的计划，不代表生成端已收到图片。若实际界面提供图片标签或独立首帧槽位，以实际标签及槽位为准，逐一映射并同步修改双语提示词与清单；不得凭空编造平台标签或保证多参考兼容。入口无法同时承载这些参考时，明确说明并提供兼容该入口的版本，不能指示上传不存在的槽位。
- 一次提交多个镜头时，为整次提交建立唯一的全局编号，逐镜头指明各自首帧；不可把多份从 1 开始的单段清单直接合并提交。

## 必须写进最终可复制提示词的内容

每段均在提示词正文中明确各附件用途，不仅写在 HTML 图片标题或块外说明。基础模式可放入 `integrated_multimodal_description` 开头；多参考模式在 `subject_definitions` 绑定，并在动作正文写清起始锚点。

1. **首帧**：明确使用本段首帧作为准确开场画面，保持初始姿态、构图、角色位置、场景、道具和光照；从此姿态自然开始后续动作，不能停留为静态画面或误用其他段首帧。
2. **角色图（如有）**：逐图绑定角色 ID，控制身份、外观、身体结构、材质、配色与比例；不照搬参考图的姿势、背景、排版或三视图，不引入额外角色。
3. **环境图（如有）**：明确控制哪些布局、建筑、材质或环境特征；具体机位、开场构图和角色位置以本段首帧为准，避免被环境参考中的人物替换主角。
4. **道具图（如有）**：明确绑定对应物品及外观、材质、尺度等范围，不迁移无关内容。
5. 紧接参考绑定写完整的时序动作与镜头变化。参考图不能代替动作描述；不要求模型自行猜测参考作用。

正式角色/环境参考与首帧若冲突，先修正首帧或明确采用的版本，并重新获得受影响批次验收，再交付最终提示词。不可同时命令严格保持互相冲突的图像。

以下只是三图示例；实际输出必须替换为本段真实编号、角色、参考控制范围和完整动作，不能把示例空缺当成最终提示词：

中文参考绑定示例：
> 以附件 1 作为本段视频的准确首帧，保持其初始构图、角色位置、姿态、道具与光照，从图中姿态自然开始下述动作。附件 2 是角色 A 的外观参考，保持其身份、身体结构、比例、材质和配色，不复制参考图的姿势或背景。附件 3 是环境参考，用于保持场景建筑与材质特征；开场机位、构图及角色位置以附件 1 为准。

English reference-binding example:
> Use Attachment 1 as the exact opening frame of this segment. Preserve its initial composition, character placement, pose, props, and lighting, and begin the following action naturally from that pose. Attachment 2 defines Character A’s identity, anatomy, proportions, materials, and colors; do not copy its pose or background. Attachment 3 defines the setting’s architecture and materials; use Attachment 1 for the opening camera viewpoint, composition, and character placement.

## 上传清单、HTML 与交付提醒

每段提示词旁提供附件表：上传顺序｜提示词编号｜实际文件名与原图链接｜用途。中英文版本对应相同素材。HTML 提供首帧和实际使用参考图的原图入口；打包时保留原图字节及可用相对路径，避免仅链接开发机器上的文件。未经允许分享的角色素材仅纳入用户本地交付，不上传公开 Skill 仓库。

提示词输出后必须明确告诉用户：

> 在 MiniMax H3 生成本段视频时，请按本段附件清单逐张添加图片，顺序必须与提示词中的附件编号一致，不能打乱。上传后核对缩略图和实际标签；若平台重新排序，请恢复顺序，或同步修改提示词中的全部编号。HTML 中显示图片不等于已上传到 MiniMax H3。每段单独提交，不要将全部段落的首帧一起上传到单段任务。

> When generating this segment in MiniMax H3, add the images in the exact order listed for this segment. Their order must match the attachment numbers in the prompt. Check the thumbnails and actual labels after upload. If the platform reorders them, restore the order or update every affected reference in the prompt. Images displayed in the HTML are not automatically uploaded to MiniMax H3. Submit segments separately; do not upload all segments’ first frames into a single-segment task.

实际有独立首帧槽位时，把提醒中的操作调整为“首帧放入首帧槽位，其余图片按所列顺序上传”，同时展示准确的槽位/标签映射。不要把本 Skill 的默认上传顺序宣传为平台硬性规定。

交付检查：每个引用均有真实文件；编号无遗漏、重复或串段；双语绑定与清单完全一致；首帧为当前已验收版本；复制按钮包含完整参考绑定；动作正文与首帧及参考不冲突；上传提醒明确可见。
