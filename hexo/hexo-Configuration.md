# 配置

>参考：https://hexo.io/zh-cn/docs/configuration

您可以在 _config.yml 中修改大部分的配置。

## 网站 site

|参数|描述|自定义值|
|:-|:-|:-|
|title      |网站标题       |haona_li's Blog|
|subtitle   |网站副标题     |书山有路勤为径，学海无涯苦作舟|
|description|网站描述       |百川东到海，何时复西归|
|keywords	|网站的关键词。使用半角逗号,分隔多个关键词。|
|author	    |您的名字       |haona_li|
|language	|网站使用的语言。详见 `themes\next\languages` 文件夹中 .yml 文件名 |zh-CN|
|timezone	|网站时区。Hexo 默认使用您电脑的时区。<br>请参考 时区列表 进行设置，如 America/New_York、 Japan 和 UTC。<br>一般的，对于中国大陆地区可以使用 Asia/Shanghai。|Asia/Shanghai|

其中，description主要用于SEO，告诉搜索引擎一个关于您站点的简单描述，通常建议在其中包含您网站的关键词。author参数用于主题显示文章的作者。

## 网址 url

|参数	|描述	|默认值     |自定义值|
|:-|:-|:-|:-|
|url	|网址	|           |https://blog.ilxy.tech|
|root	|网站根目录	|/||
|permalink	|文章的 *永久链接* 格式	|:year/:month/:day/:title/||
|permalink_defaults	|永久链接中各部分的默认值	|||
|pretty_urls	|改写 *permalink* 的值来美化 URL	|||
|pretty_urls.trailing_index	|是否在永久链接中保留尾部的 index.html，设置为 false 时去除	|true||
|pretty_urls.trailing_html	|是否在永久链接中保留尾部的 .html, 设置为 false 时去除 (对尾部的 index.html无效)	|true||

## 目录 Directory

|参数	|描述	|默认值|
|:-|:-|:-|
|source_dir	    |资源文件夹，这个文件夹用来存放内容。	        |source|
|public_dir	    |公共文件夹，这个文件夹用于存放生成的站点文件。	 |public|
|tag_dir	    |标签文件夹	                                  |tags|
|archive_dir	|归档文件夹	                                  |archives|
|category_dir	|分类文件夹	                                  |categories|
|code_dir	    |Include code 文件夹，source_dir 下的子目录	   |downloads/code|
|i18n_dir	    |国际化（i18n）文件夹	                       |:lang|
|skip_render	|跳过指定文件的渲染。<br>匹配到的文件将会被不做改动地复制到 public 目录中。<br>您可使用 glob 表达式来匹配路径。||

## 文章 Writing

|参数	|描述	|默认值|
|:-|:-|:-|
|new_post_name	        |新文章的文件名称                               |:title.md|
|default_layout	        |预设布局                                       |post|
|auto_spacing	        |在中文和英文之间加入空格                       |false|
|titlecase	            |把标题转换为 title case                        |false|
|external_link	        |在新标签中打开链接                             |true|
|external_link.enable	|在新标签中打开链接                             |true|
|external_link.field	|对整个网站（site）生效或仅对文章（post）生效   |site|
|external_link.exclude	|需要排除的域名。主域名和子域名如 www 需分别配置    |[]|
|filename_case	        |把文件名称转换为 (1) 小写或 (2) 大写           |0|
|render_drafts	        |显示草稿                                       |false|
|post_asset_folder	    |启动 Asset 文件夹                              |false|
|relative_link	        |把链接改为与根目录的相对位址                   |false|
|future	                |显示未来的文章                                 |true|
|highlight	            |代码块的设置||
|highlight.enable	    |开启代码块高亮                                 |true|
|highlight.auto_detect	|如果未指定语言，则启用自动检测                 |false|
|highlight.line_number	|显示行数<br>Enabling this option will also enable wrap option  |true|
|highlight.tab_replace	|用 n 个空格替换 tabs；如果值为空，则不会替换 tabs                  |''|
|highlight.wrap	        |Wrap the code block in \<table>	            |true|
|highlight.hljs	        |Use the hljs-* prefix for CSS classes          |false|

## 主页设置 Home page setting

|参数	|描述	|默认值|
|:-|:-|:-|
|index_generator|||
|path |Root path for your blogs index page. |''|
|per_page |Posts displayed per page. (0 = disable pagination)|10|
|order_by |Posts order. (Order by date descending by default)|-date|

## 分类 & 标签 Category & Tag

|参数	|描述	|默认值|
|:-|:-|:-|
|default_category	|默认分类	|uncategorized|
|category_map	|分类别名	||
|tag_map	|标签别名	||

## Metadata elements

https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta

|参数	|描述	|默认值|
|:-|:-|:-|
|meta_generator |Meta generator 标签。值为 false 时 Hexo 不会在头部插入该标签|true|

## 日期 / 时间格式 Date / Time format

Hexo 使用 Moment.js 来解析和显示时间。

|参数	|描述	|默认值|
|:-|:-|:-|
|date_format	|日期格式	|YYYY-MM-DD|
|time_format	|时间格式	|HH:mm:ss|
|use_date_for_updated	|启用以后，如果 Front Matter 中没有指定 updated，post.updated 将会使用 date 的值而不是文件的创建时间。<br>在 Git 工作流中这个选项会很有用	|true|

## 分页 Pagination

|参数	|描述	|默认值|
|:-|:-|:-|
|per_page	|每页显示的文章量 (0 = 关闭分页功能)	|10|
|pagination_dir	|分页目录	|page|

## 包括或不包括目录和文件 Include / Exclude file(s)

在 Hexo 配置文件中，通过设置 include/exclude 可以让 Hexo 进行处理或忽略某些目录和文件夹。你可以使用 glob 表达式 对目录和文件进行匹配。

include and exclude options only apply to the source/ folder, whereas ignore option applies to all folders.

|参数	|描述|
|:-|:-|
|include	|Hexo 默认会忽略隐藏文件和文件夹（包括名称以下划线和 . 开头的文件和文件夹，Hexo 的 _posts 和 _data 等目录除外）。<br>通过设置此字段将使 Hexo 处理他们并将它们复制到 source 目录下。|
|exclude	|Hexo 会忽略这些文件和目录|
|ignore	|Ignore files/folders|

## 扩展 Extensions

|参数	|描述|
|:-|:-|
|theme	|当前主题名称。值为false时禁用主题|
|theme_config	|主题的配置文件。在这里放置的配置会覆盖主题目录下的 _config.yml 中的配置|

## 部署 Deployment

|参数	|描述   |自定义值|
|:-|:-|:-|
|deploy	|部署部分的设置|
|deploy.type||git|
|deploy.repo||https://github.com/909986101/909986101.github.io|
|deploy.branch||master|