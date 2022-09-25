# Easy-Typing Plugin For Obsidian
This plugin is designed for better typing experience in [Obsidian](https://obsidian.md). The plugin's features includes automatic formatting of text and symbol editing enhancement during editing. Auto format text standardizes the format of the document and beautifies the appearance of the document. Editing enhancement optimizes the user's editing experience.

**Automatic text formatting** provides the feature of capitalizing the first letter. In addition, automatic text formatting can automatically add spaces to specific parts of each line during the input process according to the rules set by the user, such as spaces between Chinese and English, spaces between text and English punctuation, spaces between text and inline formula/inline code/wiki link, spaces between text blocks and user-defined regular matching blocks, etc. So as to standardize the format of the document and beautify the appearance of the document.

**Automatic text formatting takes effect immediately during editing by default**. You can also turn off the option of automatic text formatting during editing in settings. You can also use the plug-in command to format the full text of the current article, the current line, or the currently selected area.

**Edit Enhance**. For example, entering two '￥' consecutively will become `$$`, and positioning the cursor in the middle, entering two `【` will become `[[|]]`. In many cases, Chinese users do not need to switch input methods to get a smooth writing experience in OBSIDIAN! The symbol input enhancements, Edit Enhance features including 1. Automatic pairing/deletion of symbols; 2. Symbol editing enhancement of selected text; 3. Continuous full width symbol to half width symbol; 4. Obsidian syntax related editing enhancements. This plug-in also supports user-defined conversion rules, which is highly playable.

This plug-in also supports customizable conversion rules, which is highly playable.

Note: This plug-in is designed for the mixed input of Chinese and English in OBSIDIAN, and may not be effective for other languages.

# Core Features
## 1. Text Autoformatting
Automatic text formatting provides the ability to capitalize the first letter. In addition, automatic text formatting can automatically add spaces to specific parts of each line during the input process according to the rules set by the user, such as spaces between Chinese and English, spaces between text and English punctuation, spaces between text and inline formula/inline code/wiki link, spaces between text blocks and user-defined regular matching blocks, etc.

![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926001743.png)

The master switch of automatic text formatting is as above. After closing, the text will not be automatically formatted during the input process. However, it will not affect the enhanced functions of symbol editing, nor will it affect the plug-in's built-in commands: format full-text, format the current line/currently selected area.
### 1.1 Auto Capitalize
![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926002011.png)

This plug-in provides the feature of automatically capitalizing the first letter when the input method is in English input mode, that is, the letter at the beginning of each sentence is automatically capitalized. In setting tab, you can select whether auto capitalize works only when typing or work globally. **When the Only When Typing mode is choosen, auto capitalize operation can be undone, and the letter will not be capitalized after being undone.**

### 1.2 AutoSpace between text and punctuation
![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926002044.png)

Automatic space between text and punctuation will intelligently add space between other text and English punctuation.
### 1.3 Space Policy of different inline Block
This plug-in divides each text line into several blocks: text block, inline formula block, inline code block, link block, and user-defined regular matching block. The space policy between blocks can be set in settings tab.

![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926002125.png)

There are three space strategies to choose from: 1. No requirements; 2. Soft Space; 3. Strict Space. The default setting is soft space.

|Space Policy|illustration|
|:-----|:---:|
|No Require|There is no space requirement between this block and other blocks|
|Soft Space|This block can be separated from other blocks by soft spaces, that is, punctuation can also be used as a soft space.|
|Strict Space|This block must be separated from other blocks by a space.|

For instance
```markdown
some text,[[markdown link|双向链接]]还有`inline code`。其他文本。
```
This plugin devide the markdown above into 5 blocks:
1. text block：some text,
2. link block：\[\[markdown link\|双向链接\]\]
3. text block：还有
4. inline code block：\`inline code\`
5. text block：。其他文本

According to the default settings, there must be a soft space between the link block and other blocks, and the adjacent content between the link block and the left text block is a comma in English, which does not meet the requirements of soft space, so add a space between the text block 1 and the link block 2 (if it is a Chinese comma, it meets the requirements of soft space).

The adjacent content between link block 2 and text block 3 is `还`, which does not meet the soft space requirements. However, because smart space mode is selected in the space policy setting of the link text, the plug-in will make smart space with the text on the right according to the display content of the link block (here is the alias of the link: `双向链接`). Then the two adjacent content of the block and text block 3 are `接还`, and no space is need between the two Chinese characters, Therefore, no space is added between the  wiki link block 2 and the text block 3.

The adjacent characters between text block 3 and inline code block 4 is `有`, which not meet the requirements of the space policy for inline code blocks, so a space is added between text block 3 and inline code block 4.

The adjacent characters between the inline code block 4 and the text block 5 is `。`, which meet the requirements of the space policy for inline code blocks, so no space is added between inline code block 4 and text block 5.

So the final formatted text is below
```markdown
some text, [[markdown link|双向链接]]还有 `inline code`。其他文本。
```
### 1.4 User-defined Regular expression match block
In some cases, users do not want to format a specific form of content, such as `{}` internal content or `<>` internal content. **This plug-in can enable the plug-in to not format specific forms of content by user-defined regular expressions**.

In addition, each custom regular matching block can set its left and right space policies.

![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926002222.png)

Three space strategies are represented by three symbols, No require（-）, Soft Space（=）, Strict Space（+）。

More Detail about regular expression, see [《阮一峰：正则表达式简明教程》](https://javascript.ruanyifeng.com/stdlib/regexp.html#)

#### 1.4.1 自定义正则表达式语法
在自定义正则表达式的文本编辑区域，每一行字符串都为一个正则规则，其格式如下：
```
<正则表达式>|<左空格策略><右空格策略>
```
#### 1.4.2 自定义正则表达式规则示例
举例说明，如默认正则表达式区块的第二行内容如下：
```
#[\u4e00-\u9fa5\w\/]+|++
```
首先最后的两个字符串为该正则区块的左右空格策略，这里为++代表左右空格策略都为严格空格。
倒数第三个字符必须为 | ，其用于将正则表达式部分和左右空格策略部分分开，使其视觉上更容易辨认。

剩下的字符串为正则表达式本身，`#[\u4e00-\u9fa5\w\/]+`，该正则表达式可以匹配以 `#` 键开头的后续有一个或者多个符合 `[\u4e00-\u9fa5\w\/]` 范围的字符，该字符包含汉字、字母、数字、下划线以及 / 符号。

这样说起来比较复杂，简单点就是用来识别 Obsidian 中的标签（即 tag）的。
Obsidian 的标签需要在标签左右都添加空格（中文标点符号也不行，必须是空格），否则不会识别为标签。

![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/input-tag-plugin-off.gif)

![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/input-tag-plugin-on.gif)

上面两张 Gif 演示了使用该自定义正则表达式前后，在 Obsidian 输入标签时的不同。

#### 1.4.3 更多自定义正则的应用
比如默认设置中的如下自定义正则规则是用来识别网络链接的
```
(https?:\/\/|ftp:\/\/|obsidian:\/\/|zotero:\/\/|www.)[^\s（）《》。,，！？;；：“”‘’\)\(\[\]\{\}']+|++
```
下面的规则是用来识别 Obsidian 的 callout 语法块的。

```
\[\!.*?\][-+]{0,1}|-+
```

`<.*?>|--` 是用来识别双尖括号块的，保证其内部文本不被自动格式化影响。如在使用 Templater 插件创建模板时，需要使用<% tp.file.cursor() %>这样的语法。启用该自定义规则可以防止其内容被错误添加空格（因为内部的点号会被认为句子的结束，从而本插件会自动在点号与后面的文本间添加空格）。

我期待该自定义正则表达式规则可以满足不同用户的个性化需求，它的更多用法也有待大家发掘~~

## 2 增强编辑
编辑增强包含了 4 个部分的功能，包括 1. 符号自动配对/删除；2. 选中文本的符号编辑增强；3. 连续全角符号转半角符号；4. Obsidian 语法相关的编辑增强。可以在插件设置中分别设置 4 个功能的打开和关闭。

![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926003124.png)
### 2.1 基础编辑增强
基础编辑增强功能提供了一些考虑 Obsidian 及 Markdown 语法的编辑增强。

以下为软件内部所有基础编辑增强的规则
```python
[['··|', '`|`'], ["`·|`", "```|\n```"],
		["【【|】", "[[|]]"], ['【【|', "[[|]]"], ['￥￥|', '$|$'], ['$￥|$', "$$\n|\n$$"], ["$$|$", "$$\n|\n$$"], ['$$|', "$|$"],
		[">》|", ">>|"], ['\n》|', "\n>|"], [" 》|", " >|"], ["\n、|", "\n/|"], [' 、|', " /|"]]
```
- 第一条规则表示 \·\·| 转化为 \`|\`
- 第二条规则表示 \`·|\` 转化为 \`\`\`\\n|\`\`\`
- 第三和第四条规则为两次【 输入会变成 \[\[|\]\]
- 最后第二条规则表示句首输入、会转化为斜杠符号/。 (为了适配 Obsidian 核心插件 Slash commands)
- 最后一条规则表示空格后面输入、会转化成斜杠符号 /。(为了适配 Obsidian 核心插件 Slash commands)
- 以此类推
### 2.2 符号配对/删除
#### 2.2.1 符号自动配对
符号自动配对即输入成对符号的左半边，插件会自动补全其右半边的内容。

比如：输入《|，会得到《|》（竖线|代表光标位置）。

本插件支持的配对符号如下：
```python
["【】", "（）", "<>", "《》", "“”", "‘’", "「」", "『』"]
```
由于英文小括号、中括号、花括号等符号 Obsidian 本体已经提供了自动配对的选项，本插件不重复提供该功能，需要的话只要打开设置选项 `Editor→Auto pair brackets`。
#### 2.2.2 配对符号删除
当光标左右为配对符号时，使用退格键删除时，会自动把整个配对符号删除。

比如：【|】 按退格键，会变成 |。（竖线|代表光标位置）

本插件支持所有上述自动配对的符号的配对删除。此外，插件还提供了公式块、代码块、高亮块符号的快捷配对删除，其规则如下：
```python
[["$|$", "|"], ['```|\n```', '|'], ['==|==', '|'], ['$$\n|\n$$', "|"]]
```

### 2.3 选中文本时的编辑增强
有时我们会想对文中的某些部分转化为双向链接或者是代码块、公式块。在选中文本情况下，我们想输入英文 `$` 符号将选中部分转化为公式块，如果此时是中文输入法，选中的文本将被替换成￥符号。本插件会识别这些场景，并且实现用户心中所想。

|选中的文本|按键输入|最终结果| 
|:-----|:----|:-----|
|文本|【|[文本]|
|x+y|￥|\$x+y\$| 
|some code|·|\`some code\`|

此外，选中文本的情况下输入一些中文配对符号也会对选中的文本左右加上配对符号

|选中的文本|按键输入|最终结果|
|:-----|:-----|:-----|
|文本|《|《文本》| 
|文本|“ 或者 ”|“文本”| 
|文本|‘ 或者 ’|‘文本’|
|文本|<|<文本>|
|文本|（|（文本）| 

### 2.4 连续全角符号转半角
功能如其名称所示，连续输入两个全角符号会转化成半角符号。

插件内置实现的转换规则如下
```python
[["。。|", ".|"], ["！！|", "!|"], ["；；|", ";|"], ["，，|", ",|"],
		["：：|", ":|"], ['？？|', '?|'], ['、、|', '/|'], ['（（|）', "(|)"], ['（（|', '(|)'],
		["》》|", ">|"], ["《《|》", "<|"], ['《《|', "<|"]]
```
如上面第一个规则代表两个连续的中文句号会变成英文的点。第二条规则表示输入两个连续的中文感叹号会变成一个英文叹号，以此类推。

### 2.5 用户自定义编辑转化规则
![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926003149.png)

这里参考了 [aptend/typing-transformer-obsidian](https://github.com/aptend/typing-transformer-obsidian) 的转换规则的想法，可以让用户自定义转换规则，从而使插件更通用。感谢 [aptend/typing-transformer-obsidian](https://github.com/aptend/typing-transformer-obsidian)！
#### 2.5.1 选中文本情况下的自定义转换规则
![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926003230.png)

在设置栏分别输入触发符号、转换后的左右的字符串，再点击右边的添加规则按钮，即可生成一条用户自定义规则。设置好规则后，在选中文本的情况下，输入设置的触发符号，就会在选中的文本的左右分别添加 `转换后左边字符串` 和 `转换后右边字符串`。

如我分别输入 `-`、`~~`、`~~`，然后添加规则，即可得到如上图中的第一条规则。该规则设置完成后，选中文本，再输入 `-`，则会得到 `~~选中的文本~~`。

已经添加的规则可以点击编辑按钮进行改动，或者删除按钮删除规则。

选中文本自定义转换规则的优先级高于插件内置转换。
#### 2.5.2 删除时的自定义转换规则
![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926003212.png)

删除规则需要输入删除前的文本状态和按删除键后的文本状态，用|来表示光标的位置，前后的文本状态都必须有 | 以表明光标位置。光标左右都可以任意添加文本。

如内置的符号配对删除功能其实是添加了一系列删除规则，比如《》的配对删除规则如下

![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926003249.png)

点击右边加号按钮即可添加规则。同样的每条自定义删除规则也可以进行编辑和删除。

**删除规则只在使用退格键删除光标前文本时生效**，在选中文本或者使用 delete 键向后删除时不会生效。

用户自定义删除规则优先级高于插件内置删除规则。
#### 2.5.3 输入时的自定义转换规则
![](https://yaozhuwa-cloud.oss-cn-hangzhou.aliyuncs.com/Pictures/20220926003300.png)

输入时的自定义转换规则类似删除时的自定义转换规则，差别在于其在输入字符的过程中生效。
如上图中我添加了一条自定义转换规则，在我输入 `:)` 时，插件会将其转化为😀。这种转化操作是可以撤销的。

输入时的自定义转换规则优先级比插件内置的转换规则（如符号自动配对、连续全角符号转半角）低。
## Change log
FULL changelog see `./changelog.md`

### EasyTyping 5.0.0 Release!
EasyTyping 5.0.0 reconstructs the code framework, re implements all previous functions with new interfaces, greatly improves the performance and scalability of the plug-in, and introduce a lot of new features.
- Improvement and new things
	- **Now support for mobile device!**
	- **The line mode has been canceled.** Now the plug-in can better identify the end of Chinese input. There is no need for line mode and there will be no previous bug with incorrect input. Now, the plug-in formats the text at the end of each Chinese input and at the end of each English character input.
	- **Improve automatic pairing of symbols, add feature of quick deletion of paired symbols.** When the cursor is between paired symbols, pressing the Delete key will delete all the paired symbols. For example, pressing the Delete key when "《|》" will directly delete all the 《》. More symbol pairs are supported, such as ` "`, ` $$`, ` () `, etc.
	- The feature classification of symbol input enhancement is refined and the switches are set respectively: 1. Automatic pairing/deletion of symbols; 2. Symbol editing enhancement of selected text; 3. Continuous full width symbol to half width symbol; 4. Obsidian syntax related editing enhancements. See the readme document for details.
	- **A user-defined editing and conversion rule** has been added, which supports user-defined text conversion rules for selected text, backspace deletion, and typing situations. (Thanks to aptend's idea [aptend/typing-transformer-obsidian](https://github.com/aptend/typing-transformer-obsidian))
	- **Added the setting of different block space strategies, including three space strategies: 1. No requirements; 2. Soft space; 3. Strictly space.** Soft space means that the current block can be separated from other blocks by punctuation {for example, `$formula-block$, txet-block`, formula block (`$formula-block$`) and text block (`, txet-block`) are separated by commas (`,`), and this comma is a soft space}. Strict space means that there must be a space between this block and other blocks.
	- **The feature of custom regular expression block adds the space policy settings on the both left and right sides of the custom block**, greatly enhancing the practicality and playability of the regular block. See the readme document for details.
	- Add a new command "insert code block w/wo selection", code block syntax can be inserted adaptively with and without text selected (for myself convenience).
	- **Improved performance**.
- Changes
	- **Legacy Editor is no longer supported** because CodeMirror 6 API is used.
- Acknowledge
	- Thanks to [aptend/typing-transformer-obsidian](https://github.com/aptend/typing-transformer-obsidian), I learned how to use related APIs of CodeMirror 6. 